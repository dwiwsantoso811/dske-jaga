# dske-jaga

Penjaga Supabase DSKE.

Supabase free mem-pause project setelah 7 hari tanpa aktivitas. Repo ini
menjalankan satu request HTTP tiap hari lewat GitHub Actions sehingga timer
7 hari selalu ter-reset — tidak bergantung pada PC menyala.

## Isi

- `.github/workflows/jaga.yml` — cron harian 08:00 WIB, memanggil RPC `dske_tema`
  (fungsi publik yang aman, tanpa data sensitif).

## Rahasia yang diperlukan

Setelan repo → Secrets and variables → Actions → New repository secret:

| Nama | Nilai |
|---|---|
| `SUPABASE_URL` | `https://sjjhmtcnrniyrpldcgdf.supabase.co` |
| `SUPABASE_KEY` | publishable / anon key (bukan secret key) |

Publishable key memang aman di tempat publik: tabel mentah ditolak RLS,
hanya RPC `security definer` yang bisa dipanggil.

## Uji manual

Actions → `jaga-supabase` → Run workflow. Berhasil bila langkah terakhir
mencetak `HTTP 200` beserta JSON tema.

## Kalau terlanjur pause

Dashboard Supabase → project → Restore project. Data tidak hilang.
