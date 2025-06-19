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

For more configuration options, see the [chart values](charts/secflow-collector/values.yaml).

## Development

### Chart Development

Validate chart syntax:
```bash
helm lint charts/secflow-collector/
```

Render templates for testing:
```bash
helm template secflow-collector charts/secflow-collector/
```

### Releases

Chart releases are automatically generated via GitHub Actions when changes are pushed to the `main` branch. The workflow uses [chart-releaser-action](https://github.com/helm/chart-releaser-action) to:

1. Package any changed charts
2. Create GitHub releases with chart archives
3. Update the Helm repository index
4. Publish to GitHub Pages

No manual intervention is required for releases.