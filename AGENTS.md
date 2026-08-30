# Base44 dev notes

Run: `docker compose -f docker-compose.base44.yml up -d`
- customer app → host port 3000 (Vite 5173), admin app → 3001 (Vite 5174), Go API → 8080.
- Postgres 18 volume must be mounted at `/var/lib/postgresql` (not `/data`) or the container exits.
- Do NOT mount `apps/api/migrations` into `/docker-entrypoint-initdb.d`: the SQL files conflict with the
  API's GORM auto-migration (fails on `uni_admin_users_email`). The API migrates the schema itself on boot.
- API first boot takes ~2 min (Go module download); it logs `api listening on :8080` when ready.
- Vite configs got `server.host: true` + `allowedHosts: true` so the preview proxy host is accepted.
- Customer UI shows "please open via LINE" until `VITE_LIFF_ID` is set (LINE LIFF is required for booking).
- Default admin login: admin@example.com / admin1234 (set via compose env).
