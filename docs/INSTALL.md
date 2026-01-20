# Gandalf Observability – Install / Restore

This repo contains:
- scripts/gandalf-backup
- scripts/gandalf-healthcheck
- systemd/* units (and optional timers)
- systemd/dropins/* (service overrides)

## Important
Do NOT commit secrets. Configure locally:
- /etc/gandalf/backup.env (ignored by git)

## Install steps (on target host)
1) Copy scripts:
   sudo install -m 0755 scripts/gandalf-backup /usr/local/sbin/gandalf-backup
   sudo install -m 0755 scripts/gandalf-healthcheck /usr/local/sbin/gandalf-healthcheck

2) Copy systemd units:
   sudo install -m 0644 systemd/gandalf-backup.service /etc/systemd/system/gandalf-backup.service
   sudo install -m 0644 systemd/gandalf-healthcheck.service /etc/systemd/system/gandalf-healthcheck.service

   (If timers exist in repo)
   sudo install -m 0644 systemd/gandalf-backup.timer /etc/systemd/system/gandalf-backup.timer
   sudo install -m 0644 systemd/gandalf-healthcheck.timer /etc/systemd/system/gandalf-healthcheck.timer

3) Copy drop-ins (if present):
   sudo install -d -m 0755 /etc/systemd/system/gandalf-backup.service.d
   sudo cp -a systemd/dropins/gandalf-backup.service.d/. /etc/systemd/system/gandalf-backup.service.d/ 2>/dev/null || true

   sudo install -d -m 0755 /etc/systemd/system/gandalf-healthcheck.service.d
   sudo cp -a systemd/dropins/gandalf-healthcheck.service.d/. /etc/systemd/system/gandalf-healthcheck.service.d/ 2>/dev/null || true

4) Reload + enable:
   sudo systemctl daemon-reload
   sudo systemctl enable --now gandalf-backup.timer gandalf-healthcheck.timer

5) Validate:
   systemctl list-timers | egrep "gandalf-backup|gandalf-healthcheck"
   sudo systemctl start gandalf-backup.service
   sudo /usr/local/sbin/gandalf-healthcheck; echo "rc=$?"
