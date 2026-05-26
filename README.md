# nomad-client-grafana

Grafana dashboard for **external Nomad clients** — agents that run outside the Nomad server cluster (GPU hosts, CI executors, bare-metal workers, etc.).

Works with any Prometheus that scrapes Nomad’s built-in metrics endpoint (`/v1/metrics?format=prometheus` on port 4646). The **Client** variable lists every scraped `instance`; one client or many.

## Dashboard

| File | UID | Description |
|------|-----|-------------|
| `grafana/nomad-clients.json` | `nomad-clients` | Allocations, tasks, host resources, TLS cert expiry, agent runtime |

## Prometheus

Example scrape (static clients):

```yaml
# Prometheus Operator ScrapeConfig (illustrative)
spec:
  jobName: nomad-client
  metricsPath: /v1/metrics
  params:
    format: [prometheus]
  staticConfigs:
    - targets: ["10.0.0.30:4646"]
      labels:
        nomad_client: my-executor-1
  relabelings:
    - sourceLabels: [nomad_client]
      targetLabel: instance
```

Nomad must expose Prometheus metrics (`telemetry { prometheus_metrics = true }` and client node/allocation metrics as needed). See [HashiCorp: Monitor Nomad](https://developer.hashicorp.com/nomad/docs/monitor).

## Grafana Git Sync

Point [Grafana Git Sync](https://grafana.com/docs/grafana/latest/as-code/observability-as-code/git-sync/) at this repo with path `grafana/`. Read-only sync is enough if you only consume the dashboard from Git.

## Contributing

Edit JSON under `grafana/` and merge to `main`.
