# axios

HTTP client di Nusantara. JSON auto encode/decode, cookie jar, header default per instance.

## Pasang

```
nusa get github.com/NusaLang/axios
```

atau taruh manual di `nusantara_modules/axios/`.

## Pakai

```
buat axios = impor("axios");
buat a = axios.Axios("https://api.contoh.com");

a.atur_header("Authorization", "Bearer token123");

buat r = a.get("/api/user");
cetak(r.status, r.data);

buat r2 = a.post("/api/login", peta_baru());
cetak(r2.status, r2.data);
```

`get`/`post`/`put`/`hapus` balikin `{ok, status, header, data}` -- `data` otomatis di-`json_decode`, atau teks mentah kalau body-nya bukan JSON. Kalau request-nya sendiri gagal (DNS/koneksi/TLS), `{ok: salah, error}`.

Cookie ke-set otomatis dari respons (`Set-Cookie`) dan kepakai lagi di request berikutnya lewat instance yang sama -- gak perlu urus manual. **Catatan:** kalau server redirect abis set cookie, `Set-Cookie`-nya ada di respons redirect-nya, bukan yang final -- request-nya sendiri otomatis ngikutin redirect (maks 10), jadi header itu gak ke-lihat. Kalau butuh cookie dari alur redirect, matiin dulu ikutin manual pakai plugin `http` langsung.

Jalan tanpa plugin apa pun (GET/POST doang, lewat `http_get`/`http_post` bawaan) -- gak ada header custom/cookie jar/response header di mode ini, itu bukan bagian dari builtin inti. Kalau plugin native `http` ke-build (`make plugins`), semuanya otomatis kepake: PUT/DELETE, header custom, cookie jar.

## Lisensi

MIT
