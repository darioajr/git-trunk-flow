---
marp: true
title: Git Trunk Based Development
description: Apresentação sobre Feature Flags no Trunk Based Development
theme: default
footer: '@ 2025 Dario Alves Junior'
paginate: true
transition: fade 0.3s
---

# 🌿 Documentação: Git Flow com GitHub

## 📌 Visão Geral

**Git Flow** é uma estratégia de branching criada por Vincent Driessen que define um processo rigoroso para gerenciar versões de software. Ela é especialmente útil para projetos com ciclos de lançamento bem definidos, como versões mensais, releases LTS ou software embarcado.

O fluxo é composto por várias branches com papéis específicos e bem definidos.

---

## 🌿 Branches Principais

| Branch        | Função                                               |
|---------------|------------------------------------------------------|
| `main`        | Código em produção                                   |
| `develop`     | Código da próxima versão                             |
| `feature/*`   | Funcionalidades em desenvolvimento                   |
| `release/*`   | Preparação da release para QA/UAT                    |
| `hotfix/*`    | Correções emergenciais em produção                   |
| `bugfix/*`    | Correções menores em `develop`                       |

---

## 🔄 Fluxo de Trabalho no GitHub

### 1. Clonar repositório e criar `develop`

```bash
git clone git@github.com:suaorg/seuprojeto.git
cd seuprojeto
git checkout -b develop
```

---
### 2. Criar nova feature
```bash
git checkout -b feature/login-novo develop
# ...faz as mudanças...
git commit -m "feat: nova tela de login"
git checkout develop
git merge --no-ff feature/login-novo
git branch -d feature/login-novo
```

---
### 3. Criar release
```bash
git checkout -b release/1.0.0 develop
# ...ajustes finais, versionamento...
git commit -m "chore: prepara release 1.0.0"
git checkout main
git merge --no-ff release/1.0.0
git tag -a v1.0.0 -m "Release 1.0.0"
git checkout develop
git merge --no-ff release/1.0.0
git branch -d release/1.0.0
```

---
### 4. Criar hotfix
```bash
git checkout -b hotfix/1.0.1 main
# ...corrigir bug urgente...
git commit -m "fix: corrige crash na produção"
git checkout main
git merge --no-ff hotfix/1.0.1
git tag -a v1.0.1 -m "Hotfix 1.0.1"
git checkout develop
git merge --no-ff hotfix/1.0.1
git branch -d hotfix/1.0.1
```

---
## 🧪 Integração com GitHub Actions

> **Exemplo de .github/workflows/ci.yml:**

```yaml
name: CI
on:
  push:
    branches: [ develop, release/**, hotfix/** ]
  pull_request:
    branches: [ develop, release/** ]
```

---
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm ci
      - run: npm test
```
---

## 🛡️ Proteções e PRs no GitHub

> **Recomenda-se usar:**

| Branch        | Proteção                                               |
|---------------|------------------------------------------------------|
| `main`        | CI obrigatório + revisão de PR                                 |
| `develop`     | CI obrigatório                             |
| `release/*`   | Revisão e testes antes do merge                   |
| `hotfix/*`    | CI + revisão rápida                   |

---
## 📈 Vantagens do Git Flow

- ✅ Separação clara entre produção, desenvolvimento e features
- ✅ Ideal para equipes com releases planejadas
- ✅ Facilita múltiplas versões paralelas
- ✅ Histórico de mudanças organizado

---
## ⚠️ Desvantagens

- ❌ Fluxo complexo para times pequenos
- ❌ Dificulta integração contínua se mal configurado
- ❌ Alto overhead de branches
- ❌ Risco de divergência entre branches

---
📚 Referências
[**Git Flow - nvie.com**](https://nvie.com/posts/a-successful-git-branching-model/)
[**Git Flow CLI Tool**](https://github.com/nvie/gitflow)
[**GitHub Docs - Branch Protection**](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-a-branch-protection-rule)


