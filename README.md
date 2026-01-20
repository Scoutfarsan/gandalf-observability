# Gandalf Observability

This repo contains operational scripts for the Gandalf node.

## Contents
- `scripts/gandalf-backup` – backup pipeline (tar -> pigz -> rclone rcat)
- `scripts/gandalf-healthcheck` – silent OK, ntfy on failure
- `systemd/` – units/timers
- `systemd/dropins/` – overrides used on Gandalf
## Notes
Secrets/config must NOT be committed. Use env files locally (e.g. `/etc/gandalf/backup.env`).

