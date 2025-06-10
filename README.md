# ⚖️ Comparativo: Git Flow vs Trunk Based Development

## 📌 Visão Geral

Comparação entre dois modelos de estratégia de branches utilizados em Git: **[Git Flow](GIT-FLOW.md)** e **[Trunk Based Development](GIT-TRUNK)**, com foco em:

- Equipes pequenas
- Processos bem definidos: `dev → QA → UAT → cert → prod`
- Planejamento de versões (ex: 1.0.0, 1.1.0...)

---

## 🌳 Git Flow

**Modelo tradicional com múltiplas branches para cada etapa do ciclo de vida do software.**

### Principais Branches

| Branch        | Função                                               |
|---------------|------------------------------------------------------|
| `main`        | Código em produção                                   |
| `develop`     | Código da próxima versão                             |
| `feature/*`   | Funcionalidades em desenvolvimento                   |
| `release/*`   | Preparação da release para QA/UAT                    |
| `hotfix/*`    | Correções emergenciais em produção                   |

### Vantagens

- Separação clara de ambientes e fases
- Ideal para versões agendadas
- Facilita rollback
- Histórico explícito por versão

### Desvantagens

- Overhead de branches e merges
- Fluxo mais lento e complexo
- CI/CD mais difícil de integrar

---

## 🌱 Trunk Based Development

**Modelo simplificado com foco em integração contínua e branch única principal (`main`).**

### Características

- Todos desenvolvem direto na `main` (ou com PRs de curta duração)
- Feature flags são essenciais
- CI/CD automático promove código entre ambientes
- Deploy contínuo possível a qualquer momento

### Vantagens

- Rápido, leve e direto
- Menos conflitos e branches
- Ideal para automação e equipes pequenas
- Facilita entregas frequentes

### Desvantagens

- Requer disciplina e automação
- Exige testes e validação automatizada
- Controle de versão e ambientes via tagging + CI

---

## 🧩 Comparativo Lado a Lado

| Critério                           | Git Flow                                                  | Trunk Based Development                                |
|-----------------------------------|------------------------------------------------------------|--------------------------------------------------------|
| 🔀 Modelo de branches              | Múltiplas (`main`, `develop`, `release/*`, etc.)          | Principalmente `main`, com `feature/*` opcionais       |
| 📅 Planejamento de versões         | Natural com `release/*`                                   | Necessita tagging disciplinado                        |
| 🚧 Suporte a múltiplos ambientes   | Sim, com branches específicas                              | Requer CI/CD e tagging para promover entre ambientes  |
| 👥 Tamanho da equipe               | Médio a grande                                             | Pequeno a médio                                        |
| 🔁 Frequência de deploy            | Baixa a média (por versão)                                | Alta (contínua)                                        |
| 🧪 Integração contínua             | Mais complexa com múltiplas branches                      | Natural e centralizada                                |
| 💥 Risco de conflitos              | Médio a alto (branches longas)                            | Baixo (merge frequente)                               |
| 🏷️ Controle de versões            | Via branches `release/*` e `hotfix/*`                      | Via tags na `main`                                     |
| 🧼 Histórico de commits            | Verboso, múltiplos merges                                 | Limpo (squash e merge curtos)                         |
| 🧪 Feature flags                   | Raramente usadas                                           | Essenciais                                             |
| 🚀 Complexidade geral              | Alta                                                       | Baixa                                                  |

---

## ✅ Quando Usar Cada Modelo

### 🟢 **Git Flow: melhor quando...**

- Você tem **releases programadas**
- Precisa de **controle manual sobre ambientes**
- Cada fase do ciclo (QA, UAT) exige validação antes do deploy
- Rollbacks e versões paralelas são comuns

### 🟢 **Trunk Based: melhor quando...**

- Equipe pequena, com alta comunicação
- Você já usa **CI/CD com múltiplos ambientes**
- Usa **feature flags** para ativar/desativar funcionalidades
- Busca entregas rápidas, sem overhead de branches

---

## 🎯 Recomendação para Times Pequenos com Ciclo dev → QA → UAT → cert → prod

> **Recomendado iniciar com Git Flow se:**

- Seus ambientes ainda dependem de deploy manual
- O versionamento precisa de rastreabilidade clara por branch
- Você precisa manter múltiplas versões simultaneamente

> **Evoluir para Trunk Based quando:**

- A automação estiver madura
- Os ambientes forem promovidos por CI
- Feature flags estiverem implementadas
- O time quiser mais agilidade e simplicidade

---

## 📚 Referências

- [Git Flow - nvie.com](https://nvie.com/posts/a-successful-git-branching-model/)
- [Trunk Based Development](https://trunkbaseddevelopment.com/)
- [GitHub Docs - Branch Protection](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-a-branch-protection-rule)
- [DORA Metrics](https://cloud.google.com/devops)

---

