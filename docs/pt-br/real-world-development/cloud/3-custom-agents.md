---
title: "Exercício 3 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## O que são agentes personalizados?

Os [agentes personalizados][custom-agents-concept] do GitHub Copilot permitem criar assistentes de inteligência artificial especializados para tarefas ou domínios específicos do fluxo de desenvolvimento. Ao definir agentes em arquivos Markdown na pasta `.github/agents` do repositório, você fornece instruções específicas, práticas recomendadas, padrões de código e conhecimentos de domínio para orientar o agente. As equipes podem registrar seu conhecimento em agentes reutilizáveis, como um agente de acessibilidade que aplica as diretrizes [WCAG][wcag], um agente de segurança que segue práticas de programação segura ou um agente de testes que mantém padrões consistentes.

Os agentes personalizados são definidos em arquivos Markdown na pasta `.github/agents` do projeto ou globalmente em `~/.copilot/agents`. Cada arquivo tem frontmatter YAML com pelo menos `name` e `description`, seguido de um prompt Markdown que define o comportamento, a especialização e as instruções do agente.

### Agentes personalizados e skills de agente

Agentes personalizados e [skills de agente][agent-skills-concept] têm algumas semelhanças: ambos são definidos principalmente em arquivos Markdown e orientam uma inteligência artificial sobre como executar tarefas. Uma distinção útil é que o **agente personalizado** é quem executa o trabalho e as **skills** são as ferramentas.

Os agentes personalizados têm uma janela de contexto própria e podem coordenar skills e até outros agentes. Neste exercício, o agente personalizado de acessibilidade revisará e atualizará o site conforme as diretrizes de acessibilidade. Durante o trabalho, ele poderá usar skills, como uma skill para o fluxo de pull requests ou para executar e gerenciar testes.

> [!NOTE]
> Não há uma única maneira correta de criar um agente personalizado. Como em qualquer recurso de inteligência artificial, teste e itere para encontrar o que funciona em cada ambiente e cenário.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

Neste exercício, você vai explorar:

- como os agentes personalizados são definidos.
- como atribuir uma tarefa a um agente personalizado.

## Cenário

A Tailspin Toys quer tornar sua plataforma de financiamento coletivo acessível a pessoas com diferentes habilidades e preferências visuais. Comentários de usuários indicaram que algumas pessoas têm dificuldade para ler o tema escuro atual por causa do contraste insuficiente entre o texto e o fundo. Para resolver esse problema, a equipe de design solicitou um modo de alto contraste que as pessoas possam ativar e desativar.

Como a acessibilidade é importante, você usará um agente personalizado para implementar a funcionalidade rapidamente.

## Revise o agente personalizado de acessibilidade

O projeto já inclui um agente personalizado de acessibilidade. Revise o arquivo para entender como ele orientará o Copilot.

1. Volte ao Codespace e abra `.github/agents/accessibility.md`.
2. Observe o frontmatter YAML com os campos `name` e `description`.

> [!CAUTION]
> O frontmatter com `name` e `description` é obrigatório para agentes personalizados.

3. Leia as seções seguintes, que descrevem:
   - responsabilidades principais ao gerar código para um site acessível.
   - práticas recomendadas de acessibilidade.
   - exemplos de código HyperText Markup Language (HTML), folhas de estilo em cascata (CSS) e JavaScript.
   - erros comuns e como evitá-los.

## Crie e atribua uma issue

O painel de agentes do GitHub é o local central para trabalhar com agentes no ambiente. Você pode atribuir tarefas ao agente de nuvem do Copilot, acompanhar as tarefas e fornecer orientações adicionais. Atribua ao agente de acessibilidade uma tarefa para criar o modo de alto contraste.

1. Acesse o repositório.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de diálogo de nova issue.
4. Selecione **Blank issue**.
5. No campo **Title**, digite `Add high contrast mode to website`.
6. No campo **Description**, digite:

   ```plaintext
   Precisamos de um modo de alto contraste para o site. Deve haver um controle que permita ao usuário ativar o alto contraste. A configuração deve ser armazenada no local storage do navegador.
   ```

7. Selecione **Create** para criar a issue.
8. À direita, selecione **Assign to Copilot** para abrir a caixa de diálogo de atribuição.
9. Selecione **Accessibility agent** na lista de agentes personalizados.

   ![Agente de acessibilidade selecionado na caixa de atribuição do agente de nuvem](../../../_images/ex5-select-custom-agent.png)

10. Selecione **Assign**.
11. O Copilot começará a trabalhar na tarefa em segundo plano.

## Resumo e próximos passos

Neste exercício, você explorou os [agentes personalizados][custom-agents] do GitHub Copilot, assistentes especializados que atendem a tarefas e domínios específicos. Eles permitem registrar a experiência e os padrões da equipe em agentes reutilizáveis.

Você explorou:

- como os agentes personalizados são definidos.
- como atribuir uma tarefa a um agente personalizado.

Enquanto o Copilot trabalha no modo de alto contraste, você pode [acompanhar e orientar a sessão do agente][next-lesson] no painel de agentes.

## Recursos

- [Sobre agentes personalizados][custom-agents]
- [Preparar sua organização para usar agentes personalizados][org-custom-agents]
- [Preparar sua empresa para usar agentes personalizados][enterprise-custom-agents]

---

| [← Lição anterior: Agente de nuvem do GitHub Copilot][previous-lesson] | [Próxima lição: Monitorar e gerenciar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
