# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a Helm charts repository for the `secflow-collector` application - a GitHub repository scanner that fetches repositories and publishes metadata to NATS messaging system. The application runs as a scheduled job in Kubernetes.

## Chart Structure

The main chart is located in `secflow-collector/` and follows standard Helm conventions:
- `Chart.yaml` - Chart metadata and dependencies
- `values.yaml` - Default configuration values
- `templates/` - Kubernetes manifest templates
- `templates/_helpers.tpl` - Template helper functions

## Key Configuration Areas

The application requires these key configurations in `values.yaml`:
- `github.organization` - Target GitHub organization to scan
- `github.tokenSecretName` - Kubernetes secret containing GitHub token
- `nats.url` - NATS server connection URL
- `nats.subject` - NATS subject for publishing repository data
- `cron.schedule` - Cron expression for scanning frequency
- `cron.runOnStartup` - Boolean to run scan immediately on deployment

## Development Commands

Validate chart syntax:
```bash
helm lint secflow-collector/
```

Render templates locally:
```bash
helm template secflow-collector secflow-collector/
```

Install/upgrade chart:
```bash
helm upgrade --install secflow-collector secflow-collector/ --set github.organization=YOUR_ORG
```

## Application Architecture

The deployment creates a single pod that:
1. Connects to GitHub API using provided organization and token
2. Scans repositories in the organization
3. Publishes repository metadata to NATS subject
4. Runs on a cron schedule with optional startup execution

Environment variables are injected from values and secrets, with the GitHub token stored securely in a Kubernetes secret referenced by `github.tokenSecretName`.