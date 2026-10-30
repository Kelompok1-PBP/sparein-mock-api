# Sparein Mock API

Mock API untuk [Sparein](https://github.com/Kelompok1-PBP/sparein). Isinya data suku cadang dan toko, karena belum ada Public API untuk harga suku cadang di Indonesia. Repo ini sengaja tidak digabung dengan Sparein supaya Sparein berinteraksi dengannya lewat HTTP seperti API pihak ketiga.

**Semua data di sini buatan.** Nama toko, harga, dan nomor kontak dibuat untuk keperluan tugas kelompok. Link toko hanya mengarah ke halaman pencarian marketplace.

## Endpoint

```
GET https://kelompok1-pbp.github.io/sparein-mock-api/v1/parts.json
```

Tidak perlu API key. File disajikan GitHub Pages, jadi hanya mendukung `GET`.

## Skema

| Kunci | Tipe | Keterangan |
|---|---|---|
| `version` | string | Versi skema |
| `generated_at` | string | Waktu data dibuat, ISO 8601 |
| `parts` | array | Daftar suku cadang |

Tiap isi `parts`:

| Kunci | Tipe | Keterangan |
|---|---|---|
| `id` | string | ID tetap, jangan diubah. Sparein memakainya supaya sync ulang tidak dobel |
| `name` | string | Nama suku cadang, maksimal 200 karakter |
| `part_number` | string | Boleh kosong |
| `category` | string | `battery`, `screen`, `charger`, `cable`, `motor`, atau `other` |
| `description` | string | Boleh kosong |
| `image_url` | string | Boleh kosong |
| `compatible_devices` | array | `{slug, note}`, `slug` mengikuti slug perangkat Sparein |
| `sources` | array | Daftar toko, boleh kosong |

Tiap isi `sources`:

| Kunci | Tipe | Keterangan |
|---|---|---|
| `id` | string | ID tetap, jangan diubah |
| `vendor_name` | string | Nama toko |
| `city` | string | Kota toko |
| `price` | integer | Harga dalam rupiah, minimal 1 |
| `currency` | string | Kode mata uang, `IDR` |
| `url` | string | Wajib `https://` |
| `contact` | string | Boleh kosong |
| `last_checked` | string | Tanggal terakhir dicek, `YYYY-MM-DD` |

## Mengubah data

Edit `v1/parts.json`, commit, lalu push ke `main`. GitHub Pages memperbarui file dalam beberapa menit.

Kalau data di sini berubah, salin juga ke `parts/data/parts_snapshot.json` di repo Sparein. Salinan itu akan dipakai saat API tidak bisa diakses.
