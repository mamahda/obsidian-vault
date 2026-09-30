**Kategori:** Forensics / EXIF Steganography <br>
**File:** `DCIM_Camera.zip` (12 file JPG) <br>
**Flag:** `HCS{3x1f_3x1f_t3rus_di4nu_4nukan_k3lar_kan_yh}` <br>
**AI Chat:** https://chat.ragita.net/s/e55ec243-26a6-4344-bf5e-82739b17ba15

---

## 1. Deskripsi Challenge

Diberikan sebuah ZIP berisi foto-foto kamera. Rahasianya disembunyikan di **metadata EXIF**, dan berlapis: satu payload terenkripsi + satu kunci yang disembunyikan terpisah di tempat yang tidak biasa.

---

## 2. Recon: Extract & Metadata

Extract ZIP → dapat **12 file JPG** di `DCIM_Camera/`:

```
$ ls
IMG_2480.JPG  IMG_2486.JPG  IMG_2490.JPG  IMG_2496.JPG  IMG_2498.JPG  IMG_2503.JPG
IMG_2483.JPG  IMG_2489.JPG  IMG_2493.JPG  IMG_2497.JPG  IMG_2501.JPG  IMG_2506.JPG
```

Cek metadata seluruh file pakai **exiftool**. Cuma beberapa yang punya `User Comment`, dan yang menarik ada di **IMG_2501.JPG** — sebuah payload berlabel XOR-HEX:

```
Date/Time Original : 2026:08:19 20:28:00
User Comment       : PAYLOAD(XOR-HEX): 0f31670275495d03727e48535733116c3646056e070c192f003b051a5828095a6e05030a22072c1f510a26263a4e
GPS Latitude Ref   : North
```

Ciphertext (46 byte) — ini flag terenkripsi, tapi butuh **key** untuk XOR balik.

---

## 3. Menemukan Pasangan Key (Nested Thumbnail EXIF)

XOR butuh 2 parameter, jadi kita perlu payload pasangannya. Setelah cari-cari, kuncinya ada di tempat licik: **EXIF milik thumbnail yang di-embed di dalam IMG_2501.JPG** (nested IFD1) — bukan `User Comment` gambar utamanya.

```
Exif Byte Order : Big-endian (Motorola, MM)
Software        : Adobe Photoshop 25.0 (Macintosh)
User Comment    : <75 byte non-ASCII, tanpa charset marker>
Image Width     : 160
Image Height    : 120
```

`User Comment` si thumbnail ini 75 byte data mentah (tanpa marker ASCII) → terlihat seperti teks yang di-mask.

---

## 4. Brute Force Single-byte XOR Mask

Karena ini soal XOR dan key di-mask dengan satu byte, dan 1 byte cuma **256 kemungkinan**, brute force adalah cara paling gampang. Kriteria kandidat: hasil decode harus **100% printable ASCII**, lalu diranking berdasarkan seberapa "wordy" (banyak alnum/`_`/`-`/`=`).

```python
# ekstrak nested UserComment dari thumbnail, lalu coba 256 mask
thumb = subprocess.run(
    ["exiftool", "-b", "-ThumbnailImage", "DCIM_Camera/IMG_2501.JPG"],
    capture_output=True).stdout
open("_thumb.jpg", "wb").write(thumb)
data = subprocess.run(
    ["exiftool", "-b", "-UserComment", "_thumb.jpg"],
    capture_output=True).stdout

for key in range(256):
    hasil = bytes([b ^ key for b in data])
    teks = "".join(chr(c) if 32 <= c < 127 else "." for c in hasil)
    print(key, teks)
```

Mask terbaik: **158 (0x9E)**, menghasilkan recovery key:

```
recovery_key=Gr4yF1le-M0b1le_D3v1ce-Aud1t-Ch41n0fCust0dy_R3c0v3ry_K3y_2026!
```

---

## 5. Solver Lengkap (End-to-End)

Gabungkan semua: (1) ambil `PAYLOAD(XOR-HEX)` dari gambar utama, (2) ambil nested UserComment thumbnail, (3) brute mask 0x9E → recovery key, (4) XOR payload dengan key (repeating) → flag.

```python
#!/usr/bin/env python3
import re, subprocess, sys
from pathlib import Path

IMAGE_NAME = "IMG_2501.JPG"
ALLOWED_WORDY = set(b"abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789_-=!")

def exiftool_text(*args):
    return subprocess.run(["exiftool", *args], capture_output=True, check=True).stdout

def get_main_payload(image_path):
    out = exiftool_text("-UserComment", "-s3", str(image_path)).decode()
    m = re.search(r"PAYLOAD\(XOR-HEX\):\s*([0-9a-fA-F]+)", out)
    return bytes.fromhex(m.group(1))

def get_nested_thumb_comment(image_path):
    thumb = exiftool_text("-b", "-ThumbnailImage", str(image_path))
    tmp = image_path.parent / "_tmp_thumb_2501.jpg"
    tmp.write_bytes(thumb)
    try:
        raw = exiftool_text("-b", "-UserComment", str(tmp))
    finally:
        tmp.unlink(missing_ok=True)
    return raw

def brute_force_mask(blob):
    out = []
    for mask in range(256):
        dec = bytes(b ^ mask for b in blob)
        if all(32 <= b < 127 for b in dec):                 # 100% printable
            score = sum(1 for b in dec if b in ALLOWED_WORDY)
            out.append((score, mask, dec))
    out.sort(reverse=True)                                  # paling "wordy" dulu
    return out

def main():
    dcim = Path(sys.argv[1]) if len(sys.argv) > 1 else Path("DCIM_Camera")
    img = dcim / IMAGE_NAME

    payload = get_main_payload(img)
    blob = get_nested_thumb_comment(img)
    _, best_mask, best_text = brute_force_mask(blob)[0]      # mask = 0x9E

    m = re.search(r"=([^=]+)$", best_text.decode())
    key = (m.group(1) if m else best_text.decode()).encode()

    flag = bytes(payload[i] ^ key[i % len(key)] for i in range(len(payload)))
    print(f"[+] mask=0x{best_mask:02x}  key={key!r}")
    print(f"[+] FLAG: {flag.decode(errors='replace')}")

if __name__ == "__main__":
    main()
```

---

## 6. Verifikasi

```
$ python3 solve.py DCIM_Camera/IMG_2501.JPG
Dapatkan ciphertext (46 bytes): 0f31670275495d...26263a4e
Mask terbaik: 0x9E
Recovery key: b'Gr4yF1le-M0b1le_D3v1ce-Aud1t-Ch41n0fCust0dy_R3c0v3ry_K3y_2026!'
Flag: HCS{3x1f_3x1f_t3rus_di4nu_4nukan_k3lar_kan_yh}
```

Chain-nya: **EXIF UserComment utama (payload) + nested EXIF thumbnail (key ter-mask 0x9E) → repeating-XOR → flag**. Format `HCS{...}` cocok. 
_Solved!_
