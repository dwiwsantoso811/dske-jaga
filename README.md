# dske-jaga

Penjaga Supabase DSKE.

Supabase free mem-pause project setelah **7 hari** tanpa aktivitas. Repo ini
memanggil satu request HTTP tiap hari lewat GitHub Actions sehingga timer
selalu ter-reset — tidak bergantung pada PC menyala.

- Workflow: `.github/workflows/jaga.yml`
- Jadwal: `0 1 * * *` (08:00 WIB)
- Yang dipanggil: RPC `dske_tema` (publik, tanpa data sensitif)
- Uji manual: tab **Actions** -> `jaga-supabase` -> **Run workflow**

URL dan publishable key ditulis langsung di workflow, bukan Secrets, karena
keduanya memang publik (publishable key juga ada di HTML website). Tabel
mentah dilindungi RLS; hanya RPC `security definer` yang bisa dipanggil.

Kalau terlanjur pause: Dashboard Supabase -> project -> **Restore project**.
Data tidak hilang.
