# 🔍 Code Review: Um Guia Prático para Engenheiros

> **Revisando com confiança, clareza e impacto**

**Autor:** Lucas de Bona Sartor  
**Data da última atualização:** Maio de 2025

---

## 📚 Índice

- [🧭 1. Princípios Fundamentais](#-1-princípios-fundamentais)
- [🤝 2. Práticas e Expectativas do Time](#-2-práticas-e-expectativas-do-time)
- [✍️ 3. Responsabilidades do Autor Durante o Desenvolvimento](#️-3-responsabilidades-do-autor-durante-o-desenvolvimento)
- [🧹 4. Preparação do Autor Pré-Review](#-4-preparação-do-autor-pré-review)
- [👀 5. Preparação do Revisor Pré-Review](#-5-preparação-do-revisor-pré-review)
- [📝 6. Revisor durante a Review](#-6-revisor-durante-a-review)
- [🔄 7. Resposta do Autor Pós-Review](#-7-resposta-do-autor-pós-review)
- [✅ 8. Acompanhamento do Revisor Pós-Review](#-8-acompanhamento-do-revisor-pós-review)
- [🚀 9. Etapas Finais Após Aprovação](#-9-etapas-finais-após-aprovação)
- [📖 10. Leituras e Recursos Adicionais](#-10-leituras-e-recursos-adicionais)

---

## 🧭 1. Princípios Fundamentais

- **Qualidade em Primeiro Lugar:** Identifique bugs, falhas de design e problemas de manutenção cedo.
- **Compartilhamento de Conhecimento:** Espalhe boas práticas e entendimento do sistema.
- **Consistência:** Garanta padrões de código e convenções do time.
- **Colaboração:** Promova feedback construtivo e de apoio.
- **Redução de Riscos:** Identifique problemas de segurança, performance e escalabilidade antes de chegar à produção.

**🔑 Principais Lições:**

- Code reviews servem para qualidade, aprendizado e redução de riscos—não para críticas pessoais.
- Consistência, colaboração e troca de conhecimento são tão importantes quanto encontrar bugs.

**Erros Comuns:**

- Tratar code review como crítica pessoal, não como processo colaborativo.
- Focar apenas em estilo, ignorando design ou arquitetura.
- Pular revisões para mudanças "pequenas".

**Boas Práticas:**

- Aborde cada revisão com curiosidade e respeito.
- Priorize aprendizado e melhoria para todos do time.
- Use code reviews para reforçar padrões e conhecimento compartilhado.

---

## 🤝 2. Práticas e Expectativas do Time

- **Documente o Processo:** Deixe o fluxo, responsabilidades e ferramentas claros e acessíveis.
- **Propósito Acima do Ego:** Revisões são para qualidade e aprendizado—não críticas pessoais.
- **Definição de Pronto:** Deixe claro o que faz um PR estar "pronto" (testes, docs, aprovações, etc.).
- **Consistência:** Todos seguem o mesmo processo e padrões.
- **Resolução de Conflitos:** Tenha um processo claro para resolver discordâncias (ex: escalar para o tech lead).
- **Adote um Guia de Estilo:** Use e aplique um guia (ex: PEP 8, Airbnb, Google Java). Automatize com linters e formatadores.
- **Aproveite Ferramentas:** Integre linters, análise estática e CI para pegar problemas cedo.
- **Defina SLAs:** Estabeleça prazos para revisão (ex: até 24h úteis).
- **Reserve Tempo para Revisões:** Faça da revisão uma atividade agendada e prioritária.
- **Mentoria:** Use revisões para mentoria sênior-júnior e aprendizado entre times.
- **Revise Fora da Sua Área:** Incentive revisões em códigos desconhecidos para resiliência do time.
- **Melhoria Contínua:** Discuta e refine o processo regularmente.
- **Reconheça Bons Feedbacks:** Valorize revisores construtivos.
- **Minimize Interrupções:** Permita foco durante sessões de revisão.
- **Sessões Regulares de Revisão:** Reúna o time para discutir tendências e reforçar boas práticas.
- **Feedback Precoce:** Incentive feedback informal antes dos PRs formais.

**⚡ Ganhos Rápidos:**

- Documente o processo e torne-o acessível a todos.
- Use ferramentas automáticas para estilo e análise estática.
- Agende sessões regulares e reconheça bons feedbacks.

**Erros Comuns:**

- Não documentar ou atualizar o processo conforme o time evolui.
- Permitir que revisões virem gargalos por SLAs pouco claros.
- Confiar só na automação e pular revisão humana.
- Deixar preferências pessoais sobreporem padrões do time.

**Boas Práticas:**

- Revise e refine o processo em conjunto regularmente.
- Equilibre automação com feedback humano de qualidade.
- Promova cultura de mentoria e reconhecimento.

---

## ✍️ 3. Responsabilidades do Autor Durante o Desenvolvimento

- **Siga os Padrões:** Respeite guias de código e design.
- **Escreva Testes:**
  - Unitários, integração e E2E conforme necessário.
  - Garanta que todos os testes passam antes de submeter.
- **Divida Mudanças Grandes:** Envie PRs pequenos e focados.
- **Considere Impacto no Sistema:** Pense em performance, segurança e escalabilidade.
- **Comunique Proativamente:** Antecipe dúvidas e documente decisões importantes no PR.
- **Atualize Documentação:** Mantenha docs e READMEs alinhados ao código.

**🔑 Principais Lições:**

- Escreva e rode testes antes de submeter código.
- Comunique-se proativamente e mantenha docs atualizadas.
- Divida grandes mudanças para revisões mais fáceis e rápidas.

**Erros Comuns:**

- Submeter PRs grandes e difusos, difíceis de revisar.
- Não escrever ou atualizar testes.
- Não comunicar decisões de design ou trade-offs conhecidos.

**Boas Práticas:**

- Mantenha PRs pequenos e focados.
- Escreva testes abrangentes e mantenha docs atualizadas.
- Documente decisões e premissas importantes.

---

## 🧹 4. Preparação do Autor Pré-Review

- **Auto-revisão:** Revise criticamente seu próprio código antes de submeter.
  - Remova código de debug, comentários desnecessários e "gambiarras" temporárias.
  - Verifique clareza, correção e casos de borda.
- **Verifique Completude:** Garanta que testes, docs e configs estejam atualizados.
- **Verificação Local:** Compile e teste localmente.
- **Destaque Pontos de Atenção:** Aponte áreas que precisam de atenção especial na descrição do PR.
- **Capriche na Descrição do PR:**
  - Título e resumo claros.
  - Links para tickets/docs de design.
  - Screenshots/vídeos para mudanças de UI.
  - Liste mudanças de config e instruções de teste.
- **Mantenha a Mente Aberta:** Esteja pronto para aprender e colaborar.

**⚡ Ganhos Rápidos:**

- Faça auto-revisão antes de pedir revisão.
- Garanta que todos os testes passam e docs estão atualizadas.
- Escreva uma descrição de PR clara e completa.

**Erros Comuns:**

- Esquecer de remover código de debug ou gambiarras.
- Submeter código sem rodar todos os testes localmente.
- Fornecer descrições vagas ou incompletas no PR.

**Boas Práticas:**

- Sempre auto-revise e limpe o código antes de submeter.
- Garanta que todos os testes passam e docs estão atualizadas.
- Escreva descrições detalhadas com contexto e instruções.

---

## 👀 5. Preparação do Revisor Pré-Review

- **Entenda o Contexto:** Leia a descrição do PR, tickets e docs de design.
- **Prepare um Checklist:** Liste mentalmente ou fisicamente o que checar (segurança, performance, estilo, testes).
- **Conheça o Código:** Se não souber, peça um walkthrough.
- **Revise Docs/Especificações:** Garanta alinhamento com requisitos.
- **Identifique Riscos:** Fique atento a performance, segurança ou breaking changes.
- **Mentalidade Construtiva:** Foque em melhorar, não criticar.
- **Ajuste a Profundidade:** Aprofunde em grandes mudanças, faça checagem rápida em pequenos fixes.
- **Comprometa-se com a Colaboração:** Esteja pronto para um diálogo.

**🔑 Principais Lições:**

- Entenda contexto e requisitos antes de revisar.
- Prepare um checklist e foque em código e documentação.
- Aborde revisões com mentalidade construtiva e colaborativa.

**Erros Comuns:**

- Pular descrição do PR ou docs relacionadas.
- Não preparar checklist, deixando passar problemas.
- Revisar sem entender o contexto geral.

**Boas Práticas:**

- Leia todo o contexto e requisitos antes de começar.
- Use checklist para garantir revisão completa.
- Pergunte se algo estiver confuso antes de mergulhar no código.

---

## 📝 6. Revisor durante a Review

- **Seja Respeitoso:** Feedback deve ser gentil, específico e acionável.
- **Seja Específico:**
  - "Considere renomear `xyz` para `customerId` para mais clareza."
- **Explique o Porquê:** Referencie guias de estilo ou boas práticas.
- **Sugira, Não Imponha:** Ofereça alternativas, mas deixe o autor escolher.
- **Destaque Pontos-Chave:** Chame atenção para performance, segurança ou manutenção.
- **Priorize Feedback:** Marque como "Crítico", "Maior" ou "Menor".
- **Cheque Testes:**
  - Cobertura, qualidade e casos de borda.
- **Cheque Padrões:** Garanta aderência ao estilo e docs atualizadas.
- **Referencie Guias:** Use padrões do time ou da indústria, não só preferências pessoais.
- **Equilibre Perfeição e Progresso:** Busque melhor, não perfeito.
- **Sugira Pair Programming:** Para mudanças complexas.
- **Dê Feedback Positivo:** Reforce boas práticas e melhorias.

**⚡ Ganhos Rápidos:**

- Seja específico, gentil e acionável no feedback.
- Priorize questões críticas e cheque cobertura de testes.
- Dê feedback positivo além de sugestões de melhoria.

**Erros Comuns:**

- Feedback vago ou excessivamente crítico.
- Focar só em estilo, não em lógica ou design.
- Ignorar cobertura de testes ou atualização de docs.
- Deixar preferências pessoais sobreporem padrões do time.

**Boas Práticas:**

- Seja específico, gentil e acionável.
- Priorize questões críticas e referencie padrões.
- Cheque cobertura de testes e docs atualizadas.
- Equilibre rigor com pragmatismo—busque melhor, não perfeito.

---

## 🔄 7. Resposta do Autor Pós-Review

- **Enderece Todo Feedback:** Implemente mudanças, explique decisões ou peça esclarecimentos.
- **Rode os Testes Novamente:** Garanta que todos passam após atualizações.
- **Atualize Docs/Comentários:** Mantenha tudo sincronizado.
- **Peça Mais Opiniões se Preciso:** Não hesite em pedir ajuda.
- **Solicite Nova Revisão:** Quando pronto, peça nova revisão.

**🔑 Principais Lições:**

- Enderece todo feedback e rode testes após mudanças.
- Mantenha docs e comentários sincronizados com o código.
- Não hesite em pedir esclarecimentos ou mais opiniões.

**Erros Comuns:**

- Ignorar ou tratar parcialmente o feedback.
- Esquecer de rodar testes após mudanças.
- Não atualizar docs ou comentários após revisões.

**Boas Práticas:**

- Enderece todo feedback e comunique decisões.
- Sempre rode testes após mudanças.
- Mantenha docs e comentários sincronizados.

---

## ✅ 8. Acompanhamento do Revisor Pós-Review

- **Resolva Conflitos:** Discuta e escale se necessário.
- **Verifique Mudanças:** Confirme que todo feedback foi tratado.
- **Re-revise se Preciso:** Foque nas seções atualizadas.
- **Rode Testes Novamente:** Se houver mudanças grandes, garanta que o CI passou.
- **Mantenha Flexibilidade:** Esteja aberto a novos insights ou restrições.
- **Documente Aprendizados:** Anote problemas recorrentes ou melhorias para revisões futuras.
- **Comunique-se Claramente:** Avise quando tudo foi resolvido ou se ainda há pendências.

**Erros Comuns:**

- Aprovar sem checar se todo feedback foi tratado.
- Focar só no código, não em docs ou testes atualizados.
- Não comunicar claramente sobre pendências.
- Ignorar novos problemas introduzidos durante reworks.

**Boas Práticas:**

- Use checklists para garantir cobertura de todos os pontos.
- Colabore com o autor para resolver pendências.
- Registre problemas recorrentes para melhoria do processo.

**⚡ Ganhos Rápidos:**

- Verifique se todo feedback foi tratado antes de aprovar.
- Re-revise só as seções atualizadas para eficiência.
- Mantenha flexibilidade e abertura para novos insights.

---

## 🚀 9. Etapas Finais Após Aprovação

- **Faça o Merge:** Autor ou responsável faz o merge após aprovação.
- **Monitore em Produção:** Fique atento a regressões ou problemas pós-deploy.
- **Celebre o Sucesso:** Reconheça o esforço e aprendizado do time!

**🔑 Principais Lições:**

- Monitore mudanças em produção e celebre conquistas do time.
- Use aprendizados pós-merge para melhorar revisões futuras.

**Erros Comuns:**

- Fazer merge sem checar mudanças de última hora ou conflitos.
- Não monitorar produção após deploy.
- Não documentar aprendizados ou problemas pós-merge.

**Boas Práticas:**

- Revise mudanças de última hora antes do merge.
- Monitore produção de perto para regressões.
- Compartilhe aprendizados pós-merge para evoluir o processo.

---

## 📖 10. Leituras e Recursos Adicionais

- Google Engineering Practices - Code Review
- The Art of Readable Code, de Dustin Boswell e Trevor Foucher

---

> **Dica:** Code review é um esporte coletivo. Seja gentil, curioso e sempre busque deixar o código melhor do que encontrou.

---

**Este guia é um documento vivo. Contribua com melhorias e exemplos à medida que encontrar novos desafios!**

[Voltar ao Índice de Boas Práticas](./index.md)  
[Voltar à página inicial](../index.md)

_Criado e mantido por [Lucas de Bona Sartor](https://github.com/lucasbsartor). Publicado com [GitHub Pages](https://pages.github.com/)._
