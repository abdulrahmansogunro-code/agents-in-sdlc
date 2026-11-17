---
title: "Exercício 4 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## O que são agentes personalizados?

Os [agentes personalizados][custom-agents-concept] do GitHub Copilot permitem criar assistentes de inteligência artificial especializados para tarefas ou domínios específicos do fluxo de desenvolvimento. Ao definir agentes em arquivos Markdown na pasta `.github/agents` do repositório, você fornece instruções específicas, práticas recomendadas, padrões de código e conhecimentos de domínio para orientar o agente. As equipes podem registrar sua experiência em agentes reutilizáveis, como um agente de acessibilidade que aplica as [Diretrizes de Acessibilidade para Conteúdo Web (WCAG)][wcag], um agente de segurança que segue práticas de programação segura ou um agente de testes que mantém padrões consistentes.

Os agentes personalizados são definidos em arquivos Markdown na pasta `.github/agents` do projeto ou globalmente em `~/.copilot/agents`. Cada arquivo tem frontmatter YAML com pelo menos `name` e `description`, seguido de um prompt Markdown que define o comportamento, a especialização e as instruções do agente.

### Agentes personalizados e skills de agente

Agentes personalizados e [skills de agente][agent-skills-concept] têm algumas semelhanças: ambos são definidos principalmente em arquivos Markdown e orientam uma inteligência artificial sobre como executar tarefas. Uma distinção útil é que o **agente personalizado** é quem executa o trabalho e as **skills** são as ferramentas.

Os agentes personalizados têm uma janela de contexto própria e podem coordenar skills e até outros agentes. Neste exercício, o agente personalizado de acessibilidade revisará e atualizará o site conforme as diretrizes de acessibilidade. Durante o trabalho, ele poderá usar skills, como uma skill para o fluxo de pull requests ou para executar e gerenciar testes.

> [!NOTE]
> Não há uma única maneira correta de criar um agente personalizado. Teste e itere para encontrar o que funciona em cada ambiente e cenário.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Cenário

A Tailspin Toys quer tornar sua plataforma de financiamento coletivo acessível a pessoas com diferentes habilidades e preferências visuais. Comentários de usuários indicaram que algumas pessoas têm dificuldade para ler o tema escuro atual por causa do contraste insuficiente entre o texto e o fundo. Para resolver esse problema, a equipe de design solicitou um modo de alto contraste que as pessoas possam ativar e desativar.

Neste exercício, você vai:

- revisar um agente personalizado de acessibilidade existente.
- usar o agente de acessibilidade no Copilot Chat para implementar o modo de alto contraste.

## Revise o agente personalizado de acessibilidade

O projeto já inclui um agente personalizado de acessibilidade. Revise o conteúdo para entender como ele orientará o Copilot.

1. Volte ao Codespace e abra um terminal. Selecione uma branch nova a partir de `main` para manter o PR de filtragem do Exercício 3 separado:

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

2. Abra `.github/agents/accessibility.md`.
3. Observe o frontmatter YAML com os campos `name` e `description`.

> [!CAUTION]
> O frontmatter com `name` e `description` é obrigatório para agentes personalizados.

4. Leia as seções seguintes, que descrevem:
   - responsabilidades principais ao gerar código para um site acessível.
   - práticas recomendadas de acessibilidade.
   - exemplos de código HyperText Markup Language (HTML), folhas de estilo em cascata (CSS) e JavaScript.
   - erros comuns e como evitá-los.

## Use o agente personalizado no Copilot Chat

O VS Code exibe os agentes personalizados definidos em `.github/agents` na lista de agentes na parte inferior da visualização Copilot Chat. Você pode selecionar um agente para aplicar suas instruções e ferramentas à conversa.

> [!TIP]
> **Abra o Copilot Chat**
>
> Volte ao Codespace, abra o painel Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. O modo e o modelo variam conforme o exercício; as etapas indicam as opções necessárias.

1. Na lista de agentes da visualização Chat, selecione **Agent**, se ainda não estiver selecionado.

   ![Seletor de agente na visualização Chat](../../../_images/shared-chat-mode-selector.png)

2. Abra a lista de agentes na parte inferior da visualização Chat. Por padrão, o agente ativo é **default**.
3. Selecione **Accessibility agent** na lista.
4. Envie este prompt ao agente de acessibilidade:

   ```plaintext
   Adicione um modo de alto contraste ao site. Deve haver um controle para ativar o alto contraste, e a configuração deve continuar aplicada após recarregar a página, usando o local storage do navegador.
   ```

5. O Copilot explorará a base de código, proporá alterações e editará os arquivos do projeto. Cada edição aparecerá na conversa com o caminho do arquivo e um diff para revisão.
6. Observe o indicador **Files changed**, que mostra os arquivos alterados pelo agente.

> [!NOTE]
> Esse processo pode levar alguns minutos. O Copilot está fazendo alterações reais no repositório: pode editar componentes Astro, CSS e testes relacionados.

Você revisará e orientará esse trabalho em andamento no próximo exercício.

## Resumo e próximos passos

Neste exercício, você explorou os [agentes personalizados][custom-agents] do GitHub Copilot, assistentes especializados para tarefas e domínios específicos. Eles permitem registrar a experiência e os padrões da equipe em agentes reutilizáveis.

Você explorou:

- como os agentes personalizados são definidos.
- como usar um agente personalizado no modo de agente do Copilot Chat.

Em seguida, você [acompanhará e orientará o trabalho do agente][next-lesson], revisando as alterações à medida que são feitas e adicionando um controle de modo claro à mesma sessão.

## Recursos

- [Sobre agentes personalizados][custom-agents]
- [Criar agentes personalizados no IDE][creating-custom-agents-ide]
- [Agentes personalizados no VS Code][custom-agents-vscode]
- [Configuração de agentes personalizados][custom-agents-config]
- [Agentes personalizados no awesome-copilot][awesome-copilot-agents]

---

| [← Lição anterior: Testar a funcionalidade com o servidor MCP do Playwright][previous-lesson] | [Próxima lição: Monitorar e gerenciar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
