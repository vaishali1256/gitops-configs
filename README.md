# GitOps Configs

This repository contains Kubernetes manifests for a simple 3-tier web application deployed with Argo CD.

## What is in this repo

- `argocd-application.yaml` defines an Argo CD Application that points to this repository and syncs it into the cluster.
- `kustomization.yaml` centralizes shared settings such as the target namespace, image tags, and replica counts.
- `namespace.yaml` creates the application namespace.
- `frontend.yaml` deploys the frontend service and exposes it.
- `backend.yaml` deploys the backend API and configures its environment from ConfigMaps and secrets.
- `postgres.yaml` deploys PostgreSQL with persistent storage.
- `external-secrets-placeholder.yaml` documents that secrets are expected to be provided by External Secrets Operator and Azure Key Vault.

## Deployment flow

1. Argo CD reads the Application manifest.
2. Argo CD syncs the manifests from this repository into the Kubernetes cluster.
3. Kubernetes creates or updates the namespace, frontend, backend, and PostgreSQL resources.
4. The application becomes available with the configured images and settings.

## Notes

- The repo uses Kustomize for manifest composition.
- Images are versioned centrally in `kustomization.yaml`.
- Database credentials and other sensitive values are intended to be managed externally rather than stored directly in Git.
