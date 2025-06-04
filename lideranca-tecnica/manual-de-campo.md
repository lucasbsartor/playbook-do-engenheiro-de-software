# **🚀 Essencial do Tech Lead: Guia Rápido para Liderança Técnica**

**Autor:** Lucas de Bona Sartor  
**Data da última atualização:** Maio de 2025

---

Bem-vindo ao prático para liderar equipes de desenvolvimento. Este documento é um atalho para as práticas e a cultura que nos impulsionam. Pense nele como seu **manual de campo** para o dia a dia, focado em ações que geram impacto imediato.

## **✨ Sobre Liderança Técnica: Multiplicando o Potencial**

Como Tech Leads, nosso foco vai além do código. Somos **facilitadores, mentores e arquitetos do crescimento do time**. Lideramos pelo exemplo, cultivando um ambiente seguro para experimentação, aprendizado e feedback. Nosso objetivo é maximizar as habilidades coletivas e o desenvolvimento de cada membro.

---

## **📚 Índice**

- [✨ Sobre Liderança Técnica: Multiplicando o Potencial](#-sobre-liderança-técnica-multiplicando-o-potencial)
- [🎯 1. Planejamento e Visibilidade: Alinhando Entregas](#-1-planejamento-e-visibilidade-alinhando-entregas)
- [📏 2. Estimativas Rápidas: Fibonacci e T-Shirt Sizing](#-2-estimativas-rápidas-fibonacci-e-t-shirt-sizing)
- [🃏 3. Planning Poker: Alinhamento e Conhecimento Compartilhado](#-3-planning-poker-alinhamento-e-conhecimento-compartilhado)
- [🧩 4. Tipos de Tarefas: Linguagem Comum](#-4-tipos-de-tarefas-linguagem-comum)
- [✅ 5. Qualidade e Operabilidade: Não Shippe Sem Isso!](#-5-qualidade-e-operabilidade-não-shippe-sem-isso)
- [📝 6. Documentação: Conhecimento Compartilhado e Valor](#-6-documentação-conhecimento-compartilhado-e-valor)
- [🤝 7. Colaboração e Conhecimento Compartilhado: Time Forte](#-7-colaboração-e-conhecimento-compartilhado-time-forte)
- [🗣️ 8. Boas Práticas de Comunicação: Clareza e Respeito](#-8-boas-práticas-de-comunicação-clareza-e-respeito)
- [🗓️ 9. Nossos Ritos: Cadência e Colaboração Essencial](#-9-nossos-ritos-cadência-e-colaboração-essencial)
- [🌱 10. Feedback e Melhoria Contínua: Crescendo Juntos](#-10-feedback-e-melhoria-contínua-crescendo-juntos)

## **🎯 1. Planejamento e Visibilidade: Alinhando Entregas**

Planejar e estimar com precisão é chave. Garanta que todos saibam "o quê" e "porquê".

- **Time no Centro do Planejamento:**
  - **Prática:** Inclua _todos_ nas reuniões de planejamento. A experiência de quem constrói é insubstituível.
  - **Exemplo:** Ao estimar uma nova funcionalidade, pergunte diretamente aos desenvolvedores: "Quais são os maiores desafios técnicos que vocês veem aqui?"
- **Refinamento Contínuo:**
  - **Prática:** Histórias são revisadas e discutidas regularmente. O objetivo é clareza total antes de codificar.
  - **Exemplo:** Antes de uma sprint, realize sessões de 30-60 minutos para quebrar histórias grandes em tarefas menores e discutir dependências.
- **Transparência Proativa:**
  - **Prática:** Comunique o progresso, riscos e impedimentos _rapidamente_ para gestão e produto.
  - **Exemplo:** Se uma integração externa atrasar, envie um alerta no Slack para os _stakeholders_ com a previsão de impacto e possíveis soluções.
- **"Done" Definido:**
  - **Prática:** Tenha uma definição clara do que significa "done" (código, testes, documentação, monitoramento, aprovação).
  - **Exemplo:** Para uma _feature_, "done" significa: "Código em produção, testes automatizados passando, documentação atualizada, métricas no APM configuradas e validadas pelo QA."

## **📏 2. Estimativas Rápidas: Fibonacci e T-Shirt Sizing**

Usamos Fibonacci para esforço e _T-Shirt Sizing_ para uma compreensão rápida.

### **Pontos Fibonacci (Esforço/Complexidade)**

| Pontos | Significado                                             |
| :----- | :------------------------------------------------------ |
| 1      | Muito Pequena (1-2 horas)                               |
| 2      | Pequena (bug simples, novo campo)                       |
| 3      | Média (feature simples, integração existente)           |
| 5      | Grande (feature complexa, refatoração de componente)    |
| 8      | Muito Grande (múltiplas integrações, desafios)          |
| 13     | Épica (módulo novo, provavelmente precisa ser quebrado) |

### **T-Shirt Sizing (Visão Rápida)**

| Parâmetro            | P (1 pts)                  | M (2 pts)                                | G (3 pts)                                     | GG (4 pts)                                        |
| :------------------- | :------------------------- | :--------------------------------------- | :-------------------------------------------- | :------------------------------------------------ |
| **Dependências**     | Isolada                    | Algumas internas                         | Muitas (internas/externas)                    | Crítico, muitas complexas                         |
| **Testabilidade**    | Fácil                      | Moderada                                 | Difícil (mocks/ambiente específico)           | Muito Difícil (alto acoplamento)                  |
| **Incertezas**       | Nenhuma, requisitos claros | Alguns pontos incertos                   | Alta incerteza (validação de requisitos)      | Muita incerteza (pesquisa extensa, POCs)          |
| **Complex. Técnica** | Baixa, solução padrão      | Média (desafios de design/implementação) | Alta (design cuidadoso, algoritmos complexos) | Muito Alta (algoritmos novos, otimização crítica) |

**Regra de Ouro:** Se a soma dos pontos da _T-Shirt Sizing_ for **maior que 10**, já é um sinal de alerta para avaliar a quebra da tarefa. **Acima de 13 pontos, a divisão é obrigatória** para garantir previsibilidade e qualidade na entrega.

#### Relacionando a Soma de Pontuação do T-Shirt Sizing aos Pontos Fibonacci

A tabela abaixo ajuda a converter a soma dos pontos do T-Shirt Sizing para Pontos Fibonacci, facilitando o refinamento e a priorização das tarefas. Essa relação torna a transição entre estimativas de alto nível e detalhadas mais objetiva e reduz ambiguidades.

| Soma Total T-Shirt | Pontos Fibonacci | Significado                                                                                       |
| ------------------ | ---------------- | ------------------------------------------------------------------------------------------------- |
| 4-6                | 1                | Muito pequena/trivial. Tarefas rápidas, de baixo risco e sem incertezas.                          |
| 7-8                | 2                | Pequena. Alguma complexidade, mas ainda bem compreendida e de baixo risco.                        |
| 9-10               | 3                | Média. Exige atenção a detalhes, pode envolver pequenas dependências ou incertezas.               |
| 11-12              | 5                | Grande. Tarefa relevante, com desafios técnicos ou de integração, mas ainda gerenciável.          |
| 13-14              | 8                | Muito grande. Complexidade alta, múltiplas dependências ou incertezas significativas.             |
| 15                 | 13               | Épica. Muito complexa, extensa ou incerta – deve ser obrigatoriamente quebrada em subtarefas.     |
| >15                | Quebrar tarefa   | **A história é excessivamente complexa e precisa ser dividida em partes menores e gerenciáveis.** |

> **Dica:** Use esta tabela como referência para promover discussões no refinamento e alinhar expectativas entre o time e stakeholders. Ajuste os exemplos conforme o contexto e maturidade da equipe.

## **🃏 3. Planning Poker: Alinhamento e Conhecimento Compartilhado**

_Planning Poker_ evita viés e garante que todos entendam a história.

- **Por que funciona?** Evita que a primeira estimativa influencie as demais. Promove discussões aprofundadas e um entendimento compartilhado.
- **Como fazer:** Cada um escolhe secretamente seu _story point_. Revelam simultaneamente. As diferenças geram discussões valiosas, levando a um consenso.
- **Lembre-se:** O objetivo não é _acertar_, mas _aprender e alinhar_.

## **🧩 4. Tipos de Tarefas: Linguagem Comum**

Para falarmos a mesma língua e entendermos a hierarquia do trabalho:

- **Theme:** Objetivo estratégico de alto nível (ex: "Melhorar experiência de checkout").
- **Epic:** Grande corpo de trabalho, dividido em histórias (ex: "Implementar novo fluxo de pagamento com Pix").
- **Story:** Entrega de valor para o usuário, pequena o suficiente para uma sprint (ex: "Como cliente, quero pagar com Pix para finalizar minha compra rapidamente.").
- **Task:** Passo necessário para completar uma Story/Epic, sem efeito direto no usuário (ex: "Criar endpoint para processar pagamentos Pix.").
- **Bug:** Comportamento inesperado do sistema (ex: "Erro ao calcular frete para CEPs do Nordeste.").
- **Technical Debt:** Código não ideal a ser corrigido (ex: "Refatorar módulo de autenticação para usar Oauth2.").

## **✅ 5. Qualidade e Operabilidade: Não Shippe Sem Isso!**

Antes de ir para produção, **sempre** verifique estes pontos:

1. **Testes no CI/CD:** Todos os testes (unitários, integração, E2E) devem passar.
2. **Análise Estática de Código:** Ferramentas (SonarQube, etc.) sem falhas críticas.
3. **APM (Application Performance Monitoring):** Alterações monitoradas (New Relic, Datadog).
4. **Health Check:** Novas rotas/serviços com endpoints de health check.
5. **Alertas Ativos:** Métricas de negócio/sistema com alertas configurados para o time.
6. **Release Versionada:** Seguir a estratégia de versionamento (SemVer).
7. **Runbook Atualizado:** Para features complexas, o runbook de operação/troubleshooting deve estar em dia.

## **📝 6. Documentação: Conhecimento Compartilhado e Valor**

> **Atenção:** Documentar faz parte da tarefa!  
> Tarefa sem documentação = tarefa sem teste.  
> A documentação é a memória do time. Garante que o conhecimento não se perca e facilita a integração.

- **User Flow:**
  - **O que é:** Mapeia a jornada do usuário no sistema. Ajuda a entender como as partes se conectam.
  - **Prática:** Use ferramentas colaborativas (Miro, Excalidraw) para desenhar o fluxo de uma nova feature. Vincule ao card da história.
- **BPMN (Business Process Model and Notation):**
  - **O que é:** Linguagem gráfica para desenhar fluxos de trabalho padronizados.
  - **Elementos Chave:**
    - **Piscina (Pool):** Processo completo.
    - **Raias (Lanes):** Papéis/sistemas no processo.
    - **Atividades (Activities):** Tarefas/etapas (retângulos).
    - **Eventos (Events):** Início/fim/ocorrências (círculos).
    - **Gateways (Gateways):** Pontos de decisão (losangos).
    - **Conectores (Sequence Flows):** Ordem do fluxo (setas).
  - **Prática:** Para um fluxo de negócio complexo, desenhe um BPMN para que todos compreendam as etapas e responsabilidades.

## **🤝 7. Colaboração e Conhecimento Compartilhado: Time Forte**

Quebre silos e fomente a interdependência.

- **Visibilidade Transparente:**
  - **Prática:** Mantenha o quadro de tarefas (Kanban/Scrum) sempre atualizado e visível.
  - **Exemplo:** Garanta que a descrição de cada tarefa tenha contexto de negócio e critérios de aceitação claros.
- **Colaboração Proativa:**
  - **Prática:** Incentive **Pair Programming** e **Mob Programming** para troca de conhecimento e resolução de problemas.
  - **Exemplo:** Agende sessões de "mob" para atacar um bug complexo ou para iniciar uma nova feature.
  - **Code Reviews:** Fomente discussões construtivas, não apenas busca de erros.
  - **Exemplo:** Em um code review, comente: "Gostei da clareza dessa função. Que tal explorarmos uma abordagem com map aqui para simplificar ainda mais?"
- **Quebrando Silos:**
  - **Prática:** Incentive rotação de membros em diferentes partes do sistema ("Buddy System").
  - **Exemplo:** Para uma nova feature, designe dois devs para trabalharem juntos nas primeiras semanas.
  - **Comunidades de Prática (CoPs):** Crie grupos para compartilhar conhecimento (ex: Guilda de Front-end).
  - **Documentação Viva:** Mantenha wikis, runbooks e READMEs atualizados.

## **🗣️ 8. Boas Práticas de Comunicação: Clareza e Respeito**

A comunicação intencional é vital no ambiente remoto/híbrido.

- **Claro, Conciso, Objetivo:**
  - **Prática:** Comece com a informação mais importante.
  - **Exemplo:** Em vez de "Oi, você está ocupado?", diga "Oi, preciso de ajuda com X. Você tem 5 minutos?".
- **Escolha o Canal Certo:**
  - **Chat:** Dúvidas rápidas, status.
  - **Chamada de Vídeo:** Discussões complexas, brainstorming.
  - **Documentos Compartilhados:** Decisões importantes, especificações.
  - **E-mail:** Anúncios formais, comunicação ampla.
- **Documente Decisões:**
  - **Prática:** Registre todas as decisões importantes em um local acessível.
  - **Exemplo:** Após uma reunião de design, crie um documento com as decisões técnicas e os próximos passos, compartilhando com todos.
- **Empatia e Boa Intenção:**
  - **Prática:** Presuma sempre a melhor das intenções. Se houver dúvida, chame para uma conversa.
  - **Evite:** Conflitos por escrito.
- **Comunicação Proativa:**
  - **Prática:** Se houver um problema ou impedimento, comunique imediatamente, não espere a Daily.
  - **Exemplo:** "Temos um bloqueio na integração com o serviço X que pode atrasar a entrega em 2 dias. Já estamos explorando a alternativa Y."

## **🗓️ 9. Nossos Ritos: Cadência e Colaboração Essencial**

Os ritos são a espinha dorsal do nosso trabalho.

#### **Dia a Dia**

- **Daily Scrum (Stand-up):**
  - **Objetivo:** Alinhar progresso, identificar impedimentos, planejar o dia (15 min).
  - **Perguntas:** "O que fiz ontem?", "O que farei hoje?", "Tenho algum impedimento?".
- **Refinamento:**
  - **Objetivo:** Aprofundar histórias futuras, quebrar tarefas, discutir soluções técnicas.
  - **Prática:** Pode ser em pair/mob programming ou reuniões dedicadas.
- **1-on-1s (Semanais/Quinzenais):**
  - **Objetivo:** Conversas individuais sobre desenvolvimento de carreira, feedback, desafios e bem-estar.
  - **Prática:** Prepare 2-3 pontos para discutir e incentive o membro a trazer os dele.
    - _Exemplo de 1:1:_ "Como você se sentiu com o último projeto? Quais são seus objetivos para os próximos 3 meses? Há algo que eu possa fazer para te apoiar?"

#### **Sprint (Cadência de 2 Semanas)**

- **Sprint Planning:**
  - **Objetivo:** Definir o objetivo da sprint e selecionar histórias.
  - **Prática:** Discutir "o quê" e "como" serão feitos.
- **Sprint Review (Demo):**
  - **Objetivo:** Demonstrar trabalho concluído para stakeholders, obter feedback.
  - **Prática:** Celebre as conquistas e mostre o valor entregue.
- **Sprint Retrospective (Retro):**
  - **Objetivo:** Refletir sobre o que foi bom, o que pode ser melhorado e ações para a próxima sprint.
  - **Prática:** Um pilar da melhoria contínua.

## **🌱 10. Feedback e Melhoria Contínua: Crescendo Juntos**

Feedback construtivo é sobre crescimento, não crítica.

- **Feedback Regular e Construtivo:**
  - **Prática:** Dê feedback rápido após o evento, focando em comportamentos específicos e seus impactos.
  - **Exemplo:** Em vez de "Você é desorganizado", diga: "Notei que o PR X não tinha descrição e faltavam testes. Isso dificultou a revisão e atrasou a aprovação. Como podemos garantir que isso não aconteça na próxima vez?"
  - **Equilibrado:** Busque um balanço entre positivo e para desenvolvimento.
  - **Bidirecional:** Incentive o time a dar feedback a você e uns aos outros.
- **Retrospectivas Eficazes:**
  - **Prática:** Use a Retro para focar na melhoria dos processos.
  - **Exemplo:** "O que funcionou bem na última sprint? O que podemos melhorar no nosso processo de code review? Qual ação concreta podemos tomar para isso?"
  - **Ações Concretas:** Garanta que as retros resultem em ações acompanhadas.
- **Mente Aberta para Experimentação:**
  - **"Fail Fast, Learn Faster":** Incentive a experimentação. Nem tudo funcionará de primeira.
  - **Prática:** "Vamos tentar essa nova ferramenta por uma sprint e ver como funciona. Se não der certo, aprendemos e tentamos outra coisa."
  - **Adaptação Contínua:** Este documento é vivo; sua contribuição é vital.

---

[Voltar à página inicial](../index.md)

_Criado e mantido por [Lucas de Bona Sartor](https://github.com/lucasbsartor). Publicado com [GitHub Pages](https://pages.github.com/)._
