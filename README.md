# vps-watchdog

Watchdog **dari luar VPS** — jalan di infrastruktur GitHub Actions, bukan di server.

Alat alert lain (Healthchecks, Uptime Kuma, cron Hermes) semuanya ada DI DALAM VPS,
jadi kalau VPS mati total nggak ada yang bisa ngirim notifikasi. Repo ini nutup lubang itu:

- Cek `https://health.dipo.sh/` tiap 10 menit (3x percobaan, jeda 15 detik).
- Gagal → issue `incident` dibuka + Pushover **emergency** (nagih tiap 5 menit sampai di-ack).
- Pulih → issue ditutup + Pushover "VPS UP lagi".
- Status bersih → diam, nggak ada notifikasi.

Tes manual: Actions → *VPS Watchdog (eksternal)* → Run workflow → `force: fail`
(lalu `force: ok` buat lihat jalur recovery).
