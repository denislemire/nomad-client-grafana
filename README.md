# ehws-grafana-dashboards

Public Grafana dashboards for the [EhWS](https://github.com/denislemire/ehws-infra) home lab.

Dashboards in `grafana/` are synced into EhWS Grafana via **Git Sync** (Grafana provisioning app).

## Dashboards

| File | UID | Description |
|------|-----|-------------|
| `grafana/nomad-clients.json` | `ehws-nomad-clients` | External Nomad clients (CircleCI executors on Pascal, etc.) |

## Prometheus

Nomad client scrape config lives in [ehws-infra](https://github.com/denislemire/ehws-infra) (`clusters/ehws/monitoring/nomad-client-scrape-config.yaml`).

## Contributing

Edit JSON under `grafana/` and merge to `main`. EhWS Grafana polls this repo (default 60s) or receives GitHub webhooks when configured.
