---
id: 07_ecommerce
title: Sprint Planning - E-commerce
---

# 07 - **Sprint Planning: Aplicativo Web de E-commerce**

**Tema proposto:**
**Desenvolvimento de um aplicativo web para gestão de pedidos, estoque e atendimento ao cliente**

**Contexto:**
Uma empresa de e-commerce quer melhorar a operação de vendas e oferecer mais autonomia aos clientes. O produto será planejado para vendedores, gerentes e clientes, com foco em busca de clientes, consulta de estoque, acompanhamento de pedidos e relatórios.

**Tecnologias:** HTML, CSS e JavaScript ou React, conforme a definição da equipe e os conteúdos trabalhados em aula. Integrações externas podem ser simuladas durante o protótipo.

## Objetivo do Projeto

Planejar e desenvolver, de forma incremental, uma primeira versão do aplicativo que permita:

1. Buscar clientes e consultar a disponibilidade de produtos durante uma venda.
2. Registrar pedidos e aplicar descontos respeitando as permissões de cada perfil.
3. Manter as informações de estoque atualizadas e sinalizar itens críticos.
4. Consultar relatórios de vendas e acompanhar pedidos.
5. Oferecer um canal básico de suporte para clientes.

## Organização do Product Backlog

As histórias abaixo derivam da análise de tarefas e dos protótipos do aplicativo. A prioridade é uma referência inicial para a atividade e pode ser revista pelo Product Owner.

| ID | História de usuário | Critérios de aceitação | Prioridade |
|---|---|---|---|
| **US01** | Como vendedor, quero buscar clientes por nome ou CPF para agilizar o atendimento. | A busca apresenta sugestões enquanto o usuário digita e retorna resultados em até 2 segundos. | Must |
| **US02** | Como vendedor, quero aplicar descontos personalizados para atender às necessidades do cliente. | O desconto é validado conforme o limite permitido para o perfil do vendedor. | Should |
| **US03** | Como vendedor, quero consultar o estoque durante a venda para evitar oferecer produtos indisponíveis. | A disponibilidade é exibida junto ao produto e itens com quantidade igual a zero aparecem como **ESGOTADO**. | Must |
| **US04** | Como gerente, quero aprovar descontos acima de 10% para proteger a margem de lucro. | Solicitações acima de 10% ficam pendentes até uma decisão do gerente e exibem o vendedor, o pedido e o percentual solicitado. | Could |
| **US05** | Como gerente, quero exportar relatórios de vendas por período para analisar os resultados. | O gerente seleciona um período e exporta o relatório em PDF ou Excel. | Should |
| **US06** | Como gerente, quero receber alertas de estoque crítico para evitar a falta de produtos. | O sistema sinaliza produtos com menos de 5 unidades disponíveis. | Should |
| **US07** | Como cliente, quero acompanhar o status do meu pedido para saber quando ele será entregue. | O pedido exibe as etapas Preparação, Entrega e Entregue, com a previsão disponível quando informada. | Should |
| **US08** | Como cliente, quero solicitar uma troca pelo canal de suporte para resolver problemas sem precisar ligar. | O histórico do pedido oferece a ação **Abrir Chamado** e permite registrar a solicitação. | Could |
| **US09** | Como sistema, preciso sincronizar o estoque com o PDV a cada 5 minutos para reduzir vendas de itens indisponíveis. | A sincronização ocorre em intervalos de até 5 minutos e atualiza a disponibilidade exibida no aplicativo. | Must |
| **US10** | Como equipe de UX, queremos redesenhar o fluxo de relatórios para reduzir etapas desnecessárias. | Um teste A/B demonstra redução de 50% no tempo de geração dos relatórios. | Won't nesta versão |

### Priorização inicial (MoSCoW)

- **Must:** US01, US03 e US09. São essenciais para uma operação básica de venda com consulta confiável de disponibilidade.
- **Should:** US02, US05, US06 e US07. Agregam valor importante à operação e à experiência do cliente.
- **Could:** US04 e US08. Podem ser incluídas se houver capacidade após a entrega dos itens de maior prioridade.
- **Won't nesta versão:** US10. Fica para uma versão futura; a equipe poderá coletar dados de usabilidade sem assumir a implementação do teste A/B neste ciclo.

## Sprint Backlog

Planejamento de referência para **4 sprints de 2 semanas**. A equipe deve confirmar capacidade, dependências e estimativas durante cada Sprint Planning. As tarefas são exemplos e podem ser divididas pelo time.

### Sprint 1: Estrutura e consulta de produtos

**Meta da Sprint:** disponibilizar uma base navegável para vendedores localizarem clientes e verificarem a disponibilidade dos produtos.

**Histórias foco:** US01 e US03.

**Tarefas sugeridas:**

- Criar a estrutura das telas e a navegação inicial do aplicativo.
- Implementar busca de clientes por nome ou CPF com dados de exemplo.
- Exibir catálogo de produtos com quantidade e estado de disponibilidade.
- Destacar visualmente os produtos esgotados.
- Testar a busca e a consulta de estoque com cenários válidos e sem resultados.

### Sprint 2: Registro de pedido e sincronização de estoque

**Meta da Sprint:** permitir que o vendedor registre um pedido com disponibilidade atualizada e regras básicas de desconto.

**Histórias foco:** US09 e US02. A US04 pode entrar como item adicional se a equipe concluir os itens Must e Should planejados.

**Tarefas sugeridas:**

- Definir e implementar a estratégia de sincronização do estoque com o PDV ou sua simulação.
- Atualizar a disponibilidade apresentada no catálogo após a sincronização.
- Criar o fluxo de seleção de cliente e inclusão de produtos no pedido.
- Calcular subtotal, desconto e total do pedido.
- Validar o limite de desconto conforme o perfil do vendedor.
- Caso a US04 seja selecionada, criar o estado de aprovação pendente e as ações para o gerente aprovar ou rejeitar.

### Sprint 3: Gestão e acompanhamento

**Meta da Sprint:** apoiar o gerente na operação e permitir que o cliente acompanhe o andamento de um pedido.

**Histórias foco:** US05, US06 e US07.

**Tarefas sugeridas:**

- Criar filtros de período e opções de relatório de vendas.
- Implementar exportação em PDF ou Excel, ou simular a geração caso a tecnologia do protótipo não ofereça essa integração.
- Sinalizar produtos com menos de 5 unidades em estoque.
- Exibir os estados do pedido para o cliente e a previsão de entrega, quando disponível.
- Validar os fluxos com dados de diferentes períodos, níveis de estoque e status de pedido.

### Sprint 4: Suporte, validação e entrega

**Meta da Sprint:** concluir os itens selecionados para a versão, validar os principais fluxos e preparar a demonstração do produto.

**História foco:** US08, se houver capacidade. Se a US04 não tiver sido selecionada na Sprint 2, o Product Owner pode considerá-la nesta sprint antes da US08.

**Tarefas sugeridas:**

- Implementar a abertura de chamado a partir do histórico do pedido, se a US08 estiver dentro da capacidade.
- Corrigir problemas encontrados nos fluxos de venda, estoque, relatórios e acompanhamento.
- Realizar testes de usabilidade com representantes das personas ou colegas de turma.
- Verificar responsividade e acessibilidade básica das telas principais.
- Preparar uma demonstração e registrar funcionalidades concluídas e itens adiados.
- Publicar o protótipo em um servidor estático, se aplicável ao escopo da disciplina.

## Definição de Pronto

Uma história pode ser considerada pronta quando:

- Os critérios de aceitação foram atendidos e demonstrados.
- O fluxo foi testado com dados representativos, incluindo situações de erro ou ausência de resultados.
- A interface mantém consistência visual e funciona nos tamanhos de tela definidos pela equipe.
- O código foi integrado à versão compartilhada do projeto e não impede os fluxos já concluídos.
- A documentação ou as instruções necessárias para a demonstração foram atualizadas.

## Dinâmica da Atividade

1. **Formação dos papéis:** organizar cada grupo com Product Owner, Scrum Master e equipe de desenvolvimento.
2. **Refinamento:** revisar as histórias, esclarecer critérios de aceitação e identificar dependências entre pedido, estoque e permissões.
3. **Priorização:** ordenar o backlog por valor, risco e esforço, registrando qualquer mudança em relação ao MoSCoW inicial.
4. **Planejamento:** definir a meta da sprint, selecionar histórias compatíveis com a capacidade e decompor o trabalho em tarefas.
5. **Adaptação a mudanças:** apresentar uma nova necessidade, como permitir cancelamento de pedidos, e discutir seu impacto sem assumir trabalho acima da capacidade.
6. **Revisão e retrospectiva:** ao final de cada sprint, demonstrar o incremento, coletar feedback e registrar uma melhoria para a próxima sprint.

## Checklist do Sprint Planning

- [ ] A meta da sprint está clara e orientada a um resultado demonstrável.
- [ ] As histórias selecionadas têm critérios de aceitação compreendidos pela equipe.
- [ ] Dependências, riscos e integrações simuladas estão identificados.
- [ ] O trabalho cabe na capacidade acordada para a sprint.
- [ ] Cada integrante sabe como acompanhar o progresso e comunicar impedimentos.

## Resultado Esperado

Ao final do planejamento, cada grupo terá um Product Backlog priorizado e quatro propostas de Sprint Backlog, com metas, histórias, tarefas e critérios para validar os incrementos do aplicativo de e-commerce.
