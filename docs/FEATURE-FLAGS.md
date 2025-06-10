# 🧩 Feature Flags no Trunk Based Development

## 🎯 O que são Feature Flags?

Feature Flags (ou toggles de funcionalidade) são mecanismos que controlam dinamicamente se uma funcionalidade estará ativa ou inativa no código, mesmo após ser integrada ao `main`.

No Trunk Based Development (TBD), onde o código é integrado frequentemente na branch principal, as feature flags permitem que funcionalidades incompletas sejam entregues sem afetar os usuários finais.

---

## ✅ Por que usar Feature Flags no TBD?

| Benefício             | Descrição                                                                 |
|-----------------------|---------------------------------------------------------------------------|
| 🔄 Deploy contínuo     | Permite deployar código incompleto sem liberar a funcionalidade           |
| 🧪 Testes A/B          | Ativar funcionalidades para subconjuntos de usuários                      |
| 🔧 Rollback instantâneo| Desligue uma feature sem precisar fazer rollback de deploy                |
| 🤝 Integração segura   | Permite merges frequentes no `main` sem riscos para produção              |

---

## 🧪 Exemplo prático

### Sem Feature Flag:

```ts
renderNovoCheckout(); // Executa direto ao entrar no main
```

### Com Feature Flag:

```ts
if (isFeatureEnabled('NOVO_CHECKOUT')) {
  renderNovoCheckout();
} else {
  renderCheckoutAntigo();
}
```

---

## 🛠️ Implementações comuns

- **Simples**: uso de variáveis de ambiente ou arquivos de configuração
- **Dashboards completas**: serviços especializados com controle remoto de flags

### Exemplos de ferramentas:

- [LaunchDarkly](https://launchdarkly.com/)
- [Unleash](https://www.getunleash.io/)
- [Flagsmith](https://www.flagsmith.com/)
- [ConfigCat](https://configcat.com/)

---

## 🚨 Boas Práticas

| Prática                      | Recomendação                                                      |
|------------------------------|-------------------------------------------------------------------|
| 🏷️ Nome claro da flag        | Ex: `ENABLE_NOVO_CHECKOUT`, `USE_RECOMMENDATION_ENGINE`          |
| 🧼 Limpeza após liberação     | Remover código antigo após o rollout final                       |
| 🧪 Testar os dois caminhos    | Testar o comportamento com a flag `on` e `off`                   |
| 🔒 Escopo controlado          | Evite múltiplas flags interdependentes ou com escopo global      |

---

## 📌 Resumo

- Feature Flags são **essenciais para Trunk Based Development**
- Permitem merge contínuo no `main` sem impacto direto em produção
- Facilitam **CI/CD**, rollback seguro e entrega progressiva de funcionalidades

---

## 📚 Referências

- [Trunk Based Development - Feature Flags](https://trunkbaseddevelopment.com/feature-flags/)
- [Martin Fowler - Feature Toggles](https://martinfowler.com/articles/feature-toggles.html)
- [LaunchDarkly](https://launchdarkly.com/)
- [Unleash](https://www.getunleash.io/)

