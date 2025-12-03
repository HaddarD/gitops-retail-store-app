# GitOps Retail Store Application

This repository contains Kubernetes manifests managed by ArgoCD for the Retail Store application.

## Repository Structure

```
gitops-retail-store-app/
├── apps/
│   ├── ui/              # UI Service Helm Chart
│   ├── catalog/         # Catalog Service
│   ├── cart/            # Cart Service  
│   ├── orders/          # Orders Service
│   ├── checkout/        # Checkout Service
│   └── dependencies/    # PostgreSQL, Redis, RabbitMQ
│
└── argocd/
    └── applications/    # ArgoCD Application Definitions
```

## How It Works

1. **GitHub Actions** builds Docker images → pushes to ECR
2. **GitHub Actions** updates image tags in this repo
3. **ArgoCD** watches this repo for changes
4. **ArgoCD** automatically syncs changes to Kubernetes cluster

## Important Notes

- Images pulled from ECR using **ECR Credential Helper**
- No imagePullSecrets needed - IAM role handles authentication
- All deployments target namespace: `retail-store`

## Deployment Values

Current deployment configuration:
- ECR Registry: `630019796862.dkr.ecr.us-east-1.amazonaws.com`
- DynamoDB Table: `haddar-retail-store-cart-table`
- AWS Region: `us-east-1`
