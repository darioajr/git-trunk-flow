# 🌳 Documentação: Trunk Based Development com GitHub

## 📌 Visão Geral

**Trunk Based Development (TBD)** é uma estratégia de branching onde todos os desenvolvedores colaboram em uma única branch principal — chamada de `trunk` (geralmente `main` ou `master`) — com integrações frequentes.

Essa abordagem foca em integração contínua, entregas rápidas e redução de conflitos de merge, sendo altamente eficaz quando combinada com GitHub e pipelines automatizados.

---

## ✅ Benefícios

- 🔁 Integração contínua e frequente
- 💥 Menor risco de conflitos de merge
- 🚀 Maior velocidade de entrega
- 🤝 Colaboração fluida em equipe
- 🔧 Estimula o uso de automação (CI/CD)

---

## 🛠️ Estrutura de Branches

Em Trunk Based, o foco é manter **apenas uma branch principal** e fazer **commits frequentes** nela.

| Branch        | Função                                                                 |
|---------------|------------------------------------------------------------------------|
| `main` (ou `trunk`) | Branch principal, sempre estável, sempre pronta para produção        |
| `feature/*`   | Opcional, para alterações pequenas e rápidas (idealmente < 1 dia)      |

> ⚠️ **Branches longas e paralelas são evitadas.**

---

## 🔄 Fluxo de Trabalho com GitHub

### 1. Clonar o repositório

```bash
git clone git@github.com:suaorg/seuprojeto.git
cd seuprojeto
```

### 2. Criar branch de feature (opcional)

```bash
git checkout -b feature/login-botao
```

### 3. Comitar pequenas alterações

```bash
git add .
git commit -m "feat: adiciona botão de login"
```

### 4. Criar Pull Request para `main`

- PRs pequenos e frequentes
- Revisão rápida
- Merge preferencialmente com **Squash and Merge**

### 5. Merge no `main`

- CI obrigatório
- Deploy automático via pipeline

---

## ⚙️ Integração Contínua com GitHub Actions

Exemplo de `.github/workflows/ci.yml`:

```yaml
name: CI
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - run: npm install
      - run: npm test
```

---

## 🧪 Feature Toggles (Flags de Funcionalidade)

Ao invés de branches longas, utilize **feature flags**:

```ts
if (isFeatureEnabled('NOVO_LOGIN')) {
  renderNovoLogin();
} else {
  renderLoginAntigo();
}
```

Isso permite:

- Deployar código incompleto sem expor ao usuário final
- Fazer rollback apenas desativando a flag
- Testar funcionalidades em produção com segurança

---

## 🛡️ Boas Práticas

| Prática                     | Descrição                                                             |
|-----------------------------|----------------------------------------------------------------------|
| 🔄 Merge diário             | Integre no `main` ao menos uma vez por dia                           |
| 🔍 Revisão rápida de PR     | Código deve ser revisado em minutos, não dias                        |
| ✅ CI obrigatório           | Nenhum código entra no `main` sem testes passando                    |
| 🔐 Proteção de branch       | Ative regras no GitHub (`main` protegido com revisão + CI obrigatório) |
| 🚫 Branches long-living     | Evite branches vivas por mais de 1 dia                               |

---

## 🔐 Configuração de Proteção no GitHub

**Settings → Branches → Add Rule**

- ✅ Require pull request reviews before merging
- ✅ Require status checks to pass before merging
- ✅ Require linear history
- ✅ Include administrators

---

## 📈 Métricas Importantes (DORA)

| Métrica                    | O que mede                                   |
|----------------------------|-----------------------------------------------|
| Lead Time for Changes      | Tempo entre commit e deploy                   |
| Deployment Frequency       | Quantidade de deploys em um período           |
| Change Failure Rate        | Percentual de deploys com erro                |
| Mean Time to Recovery (MTTR) | Tempo médio para restaurar após falha         |

---

## ❌ Quando NÃO usar TBD

- Equipes muito grandes e dispersas
- Projetos com **baixo nível de automação**
- Códigos legados com testes manuais
- Necessidade de múltiplas versões simultâneas

> ⚠️ Nesses casos, Git Flow ou modelos híbridos podem ser mais indicados.

---

## 📚 Referências

- [Trunk Based Development - Site Oficial](https://trunkbaseddevelopment.com/)
- [GitHub Docs - Protected Branches](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-a-branch-protection-rule)
- [DORA Metrics - DevOps Research](https://cloud.google.com/devops)
