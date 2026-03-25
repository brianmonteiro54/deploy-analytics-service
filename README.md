# Deploy Analytics Service

Repositório GitOps contendo os manifestos Kubernetes do **Analytics Service** da plataforma ToggleMaster.

## Visão Geral

Este repositório é monitorado pelo **ArgoCD** e contém exclusivamente os manifestos declarativos de deploy do Analytics Service. Qualquer alteração nos manifests dispara uma sincronização automática no cluster EKS.

A tag da imagem Docker é atualizada automaticamente pelo pipeline de CI do repositório [`analytics-service`](https://github.com/brianmonteiro54/analytics-service) a cada push na branch `main`.

## Manifestos

| Arquivo | Descrição |
|---|---|
| `deployment.yaml` | Deployment com probes e variáveis para SQS e DynamoDB |
| `service.yaml` | Service ClusterIP na porta 8005 |
| `ingress.yaml` | Ingress para exposição externa |
| `secretstore.yaml` | SecretStore para integração com AWS Secrets Manager |
| `externalsecret.yaml` | ExternalSecret para injeção segura de credenciais AWS |

## Fluxo GitOps

```
analytics-service (CI) → push na main → pipeline builda imagem → atualiza tag aqui → ArgoCD sincroniza → EKS
```

## Estrutura

```
├── manifests/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   ├── secretstore.yaml
│   └── externalsecret.yaml
└── README.md
```

## Contexto

Este repositório faz parte do **Tech Challenge Fase 3 — POSTECH**, que implementa práticas de IaC (Terraform), CI/CD com DevSecOps e GitOps (ArgoCD) para os 5 microsserviços do ToggleMaster, rodando em AWS EKS via AWS Academy.
