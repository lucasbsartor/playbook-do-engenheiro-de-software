# 🏔️ Pirâmide de Code Review: Priorizando o que Mais Importa

> **Revise o que humanos fazem melhor e deixe automação cuidar do resto**

**Autor:** Lucas de Bona Sartor  
**Data da última atualização:** Maio de 2025

---

## 📚 Índice

- [🤖 1. Base: Checagens Automatizadas (Baixo Esforço)](#-1-base-checagens-automatizadas-baixo-esforço)
  - [💅 Estilo de Código e Legibilidade](#-estilo-de-código-e-legibilidade)
  - [✅ Testes e Testabilidade](#-testes-e-testabilidade)
- [🧠 2. Topo: Foco da Revisão Humana (Alto Esforço)](#-2-topo-foco-da-revisão-humana-alto-esforço)
  - [📚 Documentação](#-documentação)
  - [💡 Lógica e Qualidade da Implementação](#-lógica-e-qualidade-da-implementação)
  - [🤝 Design e Semântica de APIs](#-design-e-semântica-de-apis)

---

## 🤖 1. Base: Checagens Automatizadas (Baixo Esforço)

Deixe as ferramentas fazerem o trabalho pesado das tarefas repetitivas e objetivas. Isso libera os revisores humanos para um trabalho mais profundo e valioso.

### 💅 Estilo de Código e Legibilidade

- **Automatize Com:** Linters (ESLint, Flake8), Formatadores (Prettier, Black), Análise Estática.
- **Checklist Automatizado:**
  - Formatação e indentação
  - Convenções de nomes (claros, descritivos, consistentes)
  - Sem duplicação desnecessária de código (DRY)
  - Funções/métodos com tamanho e complexidade razoáveis

**⚡ Ganhos Rápidos:**

- Configure e aplique linters e formatadores automáticos no seu pipeline CI/CD.
- Use análise estática para pegar problemas de estilo e duplicação antes da revisão.
- Mantenha funções e métodos concisos e bem nomeados para facilitar a revisão.

### ✅ Testes e Testabilidade

- **Automatize Com:** Pipelines CI/CD, ferramentas de cobertura, suítes de testes automatizados.
- **Checklist Automatizado:**
  - Todos os testes passam (unitários, integração, E2E)
  - Novos recursos/mudanças estão cobertos por testes
  - Casos de borda e caminhos de erro são testados
  - Tipos de teste apropriados (unitário vs. integração)
  - Requisitos não-funcionais (performance, segurança) são checados quando possível

**🔑 Principais Lições:**

- Todo código deve ser coberto por testes automatizados antes da revisão humana.
- Garanta que novos recursos e casos de borda estejam testados.
- Use CI/CD para pegar regressões cedo e com frequência.

---

## 🧠 2. Topo: Foco da Revisão Humana (Alto Esforço)

Aqui é onde sua expertise, julgamento e contexto agregam mais valor.

### 📚 Documentação

- **Checklist Humano:**
  - Novos recursos e lógicas complexas estão documentados (no código e externamente)?
  - Toda documentação relevante está atualizada (README, docs de API, guias de usuário)?
  - A documentação está clara, precisa e atualizada?

**⚡ Ganhos Rápidos:**

- Atualize a documentação em todo PR—nunca deixe para depois.
- Use comentários claros e concisos para lógicas complexas.
- Mantenha READMEs e docs de API sincronizados com o código.

### 💡 Lógica e Qualidade da Implementação

- **Checklist Humano:**
  - O código atende totalmente aos requisitos e critérios de aceitação?
  - A lógica está correta, robusta e tão simples quanto possível?
  - O tratamento de erros é abrangente? Concorrência e resiliência foram considerados?
  - Existem problemas óbvios de performance ou segurança?
  - O código é observável (logs, métricas, tracing)?
  - Novas dependências são justificadas e possuem licença adequada?

**🔑 Principais Lições:**

- Foque em correção, simplicidade e robustez.
- Sempre cheque tratamento de erros, performance e segurança.
- Justifique novas dependências e garanta observabilidade.

### 🤝 Design e Semântica de APIs

- **Checklist Humano:**
  - A API é minimalista, focada e consistente com padrões existentes?
  - Existe uma forma única e idiomática de realizar cada ação?
  - Encapsulamento é respeitado (sem vazamento de detalhes internos)?
  - Mudanças breaking são justificadas e comunicadas?
  - A API é útil e preparada para o futuro?

**⚡ Ganhos Rápidos:**

- Mantenha APIs minimalistas e consistentes com padrões existentes.
- Evite breaking changes a menos que seja absolutamente necessário—e documente-os.
- Garanta que interfaces públicas sejam limpas e encapsuladas.

---

> **Dica:** Use esta pirâmide como modelo mental e referência rápida. Deixe a automação cuidar do básico, assim você pode focar no que realmente exige insight humano.

---

**Este guia é um documento vivo. Contribua com melhorias e exemplos à medida que encontrar novos desafios!**

[Voltar ao Índice de Boas Práticas](./index.md)  
[Voltar à página inicial](../index.md)

_Criado e mantido por [Lucas de Bona Sartor](https://github.com/lucasbsartor). Publicado com [GitHub Pages](https://pages.github.com/)._
