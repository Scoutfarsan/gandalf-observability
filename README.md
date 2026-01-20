# Gandalf Observability

This repo contains operational scripts for the Gandalf node.

## Contents
- `scripts/gandalf-backup` – backup pipeline (tar -> pigz -> rclone rcat)

## Notes
Secrets/config must NOT be committed. Use env files locally (e.g. `/etc/gandalf/backup.env`).
