# MyCVPlanner Grafana

This repository contains the Grafana deployment used for `grafana.mycvplanner.com`.

## Run on Debian host (192.168.1.126)

```bash
cp .env.example .env
vi .env
docker compose pull
docker compose up -d
```

Grafana is exposed on `0.0.0.0:3300` and is intended to be accessed through the GNOME edge proxy over HTTPS.

## Edge nginx snapshot

The GNOME edge vhost snapshot for this service is stored in:

- `deploy/nginx/grafana.mycvplanner.com.conf`

## Initial login

- URL: `https://grafana.mycvplanner.com`
- Username: value of `GF_SECURITY_ADMIN_USER`
- Password: value of `GF_SECURITY_ADMIN_PASSWORD`

## Update admin password

Edit `.env`, then restart:

```bash
docker compose up -d
```

## Stop

```bash
docker compose down
```
