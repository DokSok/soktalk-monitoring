# soktalk-monitoring

Git-backed source of truth for the Prometheus monitoring stack on the doksok cluster.

## Structure

```
monitoring/
├── service-monitors/     # ServiceMonitor CRDs for scrape targets
├── scrape-configs/       # additionalScrapeConfigs source files (rendered into Secrets)
├── prometheus-rules/     # PrometheusRule CRDs (alerting rules)
└── alerting/             # Alertmanager configuration (alertmanager.yml)
```

## Sync

The cluster uses a git-sync sidecar (or apply job) to pull these files in
and apply them. Pushing to `main` triggers a sync within 60 s.

## Local extraction

To pull current live cluster state into this repo for comparison:

```bash
python3 deploy/extract-configs.py
```

## Relation to other repos

- Dashboards: sibling repo `doksok/soktalk-grafana-dashboards`.
- Promtail config: sibling repo `doksok/soktalk-logging`.
