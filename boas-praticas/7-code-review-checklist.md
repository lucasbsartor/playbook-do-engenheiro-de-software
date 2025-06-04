# 📋✅ Checklist de Code Review: Referência Prática

> **Checklist para não ficar apenas no LGTM!**

**Autor:** Lucas de Bona Sartor  
**Data da última atualização:** Maio de 2025

---

## 📚 Índice

- [🎯 1. Requisitos e Escopo](#-1-requisitos-e-escopo)
- [🧹 2. Limpeza e Legibilidade do Código](#-2-limpeza-e-legibilidade-do-código)
- [🧪 3. Testes e Validação](#-3-testes-e-validação)
- [🛡️ 4. Segurança e Robustez](#️-4-segurança-e-robustez)
- [⚡ 5. Performance e Escalabilidade](#-5-performance-e-escalabilidade)
- [📐 6. Arquitetura e Design](#-6-arquitetura-e-design)
- [📊 7. Observabilidade e Monitoramento](#-7-observabilidade-e-monitoramento)
- [📚 8. Documentação e Comunicação](#-8-documentação-e-comunicação)
- [🚀 9. Prontidão para Release e Deploy](#-9-prontidão-para-release-e-deploy)

---

## 🎯 1. Requisitos e Escopo

- [ ] **Funcionalidade Completa:** O código cobre todos os requisitos e critérios de aceitação?
- [ ] **Alinhamento com Stakeholders:** Stakeholders aprovaram mudanças relevantes?

**🔑 Principais Lições:**

- Garanta que o código atende totalmente aos requisitos e critérios de aceitação antes da revisão.
- Confirme alinhamento com stakeholders para mudanças importantes.

## 🧹 2. Limpeza e Legibilidade do Código

- [ ] **Estilo e Formatação:** Consistente com o guia de estilo do time (idealmente automatizado).
- [ ] **Sem Código Morto:** Remova variáveis, funções, arquivos ou assets não utilizados.
- [ ] **DRY:** Sem duplicação desnecessária de código.
- [ ] **Nomes Claros:** Nomes claros, concisos e descritivos.
- [ ] **Legibilidade e Simplicidade:** Código fácil de ler e entender; métodos/funções com tamanho razoável.
- [ ] **Comentários Significativos:** Comentários explicam o _porquê_ (não só o quê) e estão atualizados.

**⚡ Ganhos Rápidos:**

- Use linters/formatadores automáticos para garantir estilo.
- Remova código morto e duplicação antes de submeter para revisão.
- Priorize nomes claros e código conciso.

## 🧪 3. Testes e Validação

- [ ] **Todos os Testes Passam:** Testes unitários, integração e E2E estão passando.
- [ ] **Cobertura de Testes Adequada:** Novos recursos e correções estão testados.
- [ ] **Casos de Borda Cobertos:** Casos de borda e cenários de falha comuns estão testados.
- [ ] **Validação e Saneamento de Entradas:** Todas as entradas externas são validadas e saneadas.

**🔑 Principais Lições:**

- Todos os testes devem passar antes do merge.
- Cobertura de testes deve incluir novos recursos, correções e casos de borda.
- Valide e sanitize todas as entradas externas.

## 🛡️ 4. Segurança e Robustez

- [ ] **Seguro:** Sem vulnerabilidades óbvias (veja [Guia de Segurança de API](link-to-api-security)).
- [ ] **Tratamento de Erros:** Todos os erros são tratados de forma elegante.
- [ ] **Concorrência:** Sem race conditions ou bugs de concorrência.
- [ ] **Programação Defensiva:** Checagem de null/tipo, validação de entrada nas bordas.
- [ ] **Segurança e Licenciamento de Dependências:** Novas dependências são seguras e possuem licença adequada.

**⚡ Ganhos Rápidos:**

- Verifique vulnerabilidades óbvias e trate erros de forma elegante.
- Use programação defensiva e valide todas as bordas.
- Revise novas dependências quanto à segurança e licença.

## ⚡ 5. Performance e Escalabilidade

- [ ] **Sem Gargalos:** Sem problemas óbvios de performance (ex: queries N+1, loops ineficientes).
- [ ] **Eficiência de Recursos:** Uso eficiente de CPU, memória e I/O.
- [ ] **Escalabilidade:** Código suporta escala sob carga.
- [ ] **Cache:** Estratégias de cache apropriadas são usadas quando necessário.

**🔑 Principais Lições:**

- Evite gargalos de performance e padrões ineficientes.
- Garanta que o código escala e usa recursos de forma eficiente.
- Aplique cache onde for apropriado.

## 📐 6. Arquitetura e Design

- [ ] **Alinhamento de Design:** Código segue arquitetura e princípios de design do sistema.
- [ ] **Separação de Responsabilidades:** Responsabilidades bem separadas.
- [ ] **Configurabilidade:** Parâmetros relevantes são configuráveis, não hardcoded.
- [ ] **Feature Flags:** Usadas para recursos novos/experimentais quando necessário.
- [ ] **Sem Vazamento Interno:** APIs públicas não expõem detalhes internos.
- [ ] **Design de API/Interface:** Mínima, consistente e sem breaking changes.

**⚡ Ganhos Rápidos:**

- Alinhe o código à arquitetura e princípios do sistema.
- Separe responsabilidades e evite vazamento de detalhes internos em APIs.
- Use feature flags para recursos novos/experimentais.

## 📊 7. Observabilidade e Monitoramento

- [ ] **Logs Eficazes:** Eventos importantes são logados com contexto (sem dados sensíveis).
- [ ] **Métricas:** Métricas relevantes são expostas para monitoramento.
- [ ] **Tracing:** Contexto de tracing propagado em sistemas distribuídos.
- [ ] **Alertas:** Novos erros/métricas disparam alertas quando necessário.

**🔑 Principais Lições:**

- Logue eventos importantes com contexto, mas nunca dados sensíveis.
- Exponha métricas e tracing relevantes para sistemas distribuídos.
- Configure alertas para novos erros ou métricas críticas.

## 📚 8. Documentação e Comunicação

- [ ] **Documentação do Código:** Código é autoexplicativo e partes complexas estão comentadas.
- [ ] **README/API Docs Atualizados:** Docs refletem novos recursos, setup e mudanças de API.
- [ ] **Descrição Clara do PR:** PR inclui contexto, links e instruções de teste.
- [ ] **Sem Comentários Obsoletos:** Todos os comentários de revisão anteriores foram tratados.

**⚡ Ganhos Rápidos:**

- Mantenha código e documentação sincronizados.
- Escreva descrições claras de PR e trate todos os comentários de revisão.
- Atualize README/API docs para novos recursos ou mudanças.

## 🚀 9. Prontidão para Release e Deploy

- [ ] **Anotações de Release:** Tags de versão e changelogs atualizados se necessário.
- [ ] **Estratégia de Rollback:** Plano claro de rollback em caso de problemas.

**🔑 Principais Lições:**

- Anote releases e atualize changelogs quando necessário.
- Sempre tenha uma estratégia clara de rollback antes de deployar.

---

> **Dica:** Use este checklist junto com o Guia Completo de Code Review para contexto e melhores práticas. Adapte conforme a necessidade do seu time!

---

**Este guia é um documento vivo. Contribua com melhorias e exemplos à medida que encontrar novos desafios!**

[Voltar ao Índice de Boas Práticas](./index.md)  
[Voltar à página inicial](../index.md)

_Criado e mantido por [Lucas de Bona Sartor](https://github.com/lucasbsartor). Publicado com [GitHub Pages](https://pages.github.com/)._
