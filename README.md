# MyCVPlanner Grafana

This repository contains the Grafana deployment used for `grafana.mycvplanner.com`.

## Run on Debian host (192.168.1.126)

```bash
cp .env.example .env
vi .env
docker compose pull
docker compose up -d
```

The stack provisions:

- Grafana itself
- Prometheus for time-series storage
- Node Exporter for Debian host metrics
- A read-only SQLite connection to the platform database for business dashboards

Grafana is exposed on `0.0.0.0:3300` and is intended to be accessed through the GNOME edge proxy over HTTPS.

## Platform connection

Set `MYCVPLANNER_PLATFORM_DB_PATH` in `.env` to the platform SQLite database on the Debian host. The default expected path is:

```bash
/home/rob/Python/mycvplanner-platform/db.sqlite3
```

Grafana mounts that database read-only and provisions a `Platform SQLite` datasource. The business dashboards query `auth_user` and `home_purchaserecord` directly, so historical user growth and booked revenue render immediately from existing platform data.

## Provisioned dashboards

- `Platform Business Metrics`
- `Debian Host Health`

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
