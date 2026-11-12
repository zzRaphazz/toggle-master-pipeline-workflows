# Workflows reutilizáveis — ToggleMaster

Este repositório contém workflows reutilizáveis do GitHub Actions compartilhados pelos repositórios independentes de serviços e Terraform.

## Workflows

- `service-ci.yml`: testa, aplica lint e scans, constrói e publica no ECR via OIDC e atualiza o manifesto correspondente em `toggle-master-k8s-manifests`.
- `terraform-ci.yml`: formata e valida a composição de infraestrutura ou cada módulo Terraform, sem credenciais AWS nem backend remoto.

Cada repositório de serviço mantém somente um workflow chamador pequeno. Os consumidores devem usar uma tag de release revisada ou SHA de commit e conceder apenas as permissões necessárias. Configure `AWS_ROLE_ARN`, `SONAR_TOKEN` e `GITOPS_TOKEN` em cada repositório de serviço; nunca armazene os valores neste repositório.

`GITOPS_TOKEN` é uma credencial entre repositórios e deve ser um token de GitHub App com permissões granulares (preferencial) ou equivalente, limitado a escrita de conteúdo no repositório GitOps. A validação de Pull Requests não publica imagens nem atualiza o GitOps.
