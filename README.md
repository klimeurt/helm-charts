# Klimeurt Helm Charts

This repository contains Helm charts for Klimeurt organization applications.

## Usage

Add this Helm repository:

```bash
helm repo add klimeurt https://klimeurt.github.io/helm-charts
helm repo update
```

## Charts

### secflow-collector

A GitHub repository scanner that fetches repositories and publishes metadata to NATS messaging system.

```bash
helm install secflow-collector klimeurt/secflow-collector \
  --set github.organization=your-org \
  --set github.tokenSecretName=github-token \
  --set nats.url=nats://your-nats:4222
```

For more configuration options, see the [chart values](secflow-collector/values.yaml).

## Development

To package and update the repository index:

```bash
helm package secflow-collector/
helm repo index . --url https://klimeurt.github.io/helm-charts
```