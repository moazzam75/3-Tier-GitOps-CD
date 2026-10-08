# 3-Tier Application - CD Repository

This repository acts as the single source of truth for the Kubernetes deployment manifests managed via GitOps and Argo CD.

## Architecture & Sync Flow

1. The CI repository (`3-Tier-GitOps-CI`) builds new container images and automatically updates the deployment image tags in this repository.
2. **Argo CD** detects the updated manifests and automatically synchronizes the changes to the target Kubernetes cluster.
3. If an issue occurs, rolling back the deployment only requires reverting the relevant commit in this repository.

## Repository Contents

```text
├── k8s-prod/
│   ├── namespace.yaml       # Namespace definition
│   ├── database.yaml        # Database deployment and persistent volume
│   ├── backend.yaml         # Backend API deployment and service
│   ├── frontend.yaml        # Frontend web deployment and service
│   └── ingress.yaml         # Ingress rules / routing
├── argocd/
│   └── application.yaml     # Argo CD Application Custom Resource (CRD)
└── README.md
