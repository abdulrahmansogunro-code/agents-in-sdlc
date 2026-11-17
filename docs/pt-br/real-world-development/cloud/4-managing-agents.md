---
title: "Exercício 4 - Monitorar e gerenciar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Nas últimas atividades, você atribuiu três tarefas diferentes ao agente de nuvem do Copilot para melhorar a experiência do usuário e adicionar funcionalidades. Embora o agente trabalhe de forma assíncrona e autônoma, é importante acompanhar o andamento dessas tarefas.

Há várias ferramentas para gerenciar as tarefas atribuídas ao agente de nuvem, incluindo a [página de agentes][agents-page] no GitHub.com. Nesse painel central, você pode ver as tarefas de agentes que têm pull requests abertos, explorar as operações realizadas e orientar uma sessão em andamento.

Neste exercício, você vai:

- explorar a página de agentes para acompanhar as tarefas do agente de nuvem.
- orientar uma sessão em andamento para solicitar uma funcionalidade adicional.

## Cenário

Depois de atribuir ao agente a implementação do modo de alto contraste, a equipe percebeu que seria útil adicionar também um modo claro. Como já há trabalho para atualizar o estilo do site e adicionar controles, você vai orientar o agente para incluir o modo claro junto com o alto contraste.

## Revise as tarefas do agente de nuvem

Confira o estado atual das tarefas atribuídas ao agente de nuvem do Copilot.

1. Acesse a [página de agentes do Copilot](https://github.com/copilot/agents).
2. Observe a lista de tarefas no painel principal e no painel à esquerda. Ela deve incluir as tarefas atribuídas ao Copilot:
   - atualizar a documentação da base de código.
   - gerar APIs para modificar jogos.
   - adicionar um modo de alto contraste ao site.
3. Selecione uma tarefa em andamento e revise as operações executadas pelo Copilot, que podem incluir:
   - obter o código do repositório.
   - criar o ambiente de trabalho do Copilot.
   - configurar servidores MCP.
   - executar várias etapas para concluir a tarefa atribuída.

> [!NOTE]
> As etapas exatas exibidas variam de acordo com o estado do trabalho e a abordagem do Copilot.

4. Observe o painel do pull request à direita, que mostra o PR e os arquivos alterados.

## Oriente o agente de nuvem

Agora que você conferiu as tarefas ativas, peça ao Copilot que inclua o modo claro enquanto trabalha no modo de alto contraste.

1. Selecione a sessão referente ao modo de alto contraste. O título exato varia de acordo com o nome escolhido pelo Copilot e o estado atual do trabalho.

   ![Sessão de acessibilidade no painel central de agentes](../../../_images/ex6-accessibility-session.png)

2. Acompanhe a sessão por alguns minutos, até que ela indique que a configuração foi concluída e o trabalho começou.
3. Na caixa de diálogo **Steer active session while Copilot is working**, digite este prompt:

   ```plaintext
   Enquanto trabalhamos no modo de alto contraste, vamos adicionar também um modo claro. Deve haver um controle para esse modo, para que as pessoas possam selecionar a aparência desejada.
   ```

   ![Caixa de diálogo para orientar uma sessão ativa do agente de nuvem](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pressione <kbd>Enter</kbd> para enviar o prompt.
5. Observe como o Copilot confirma o recebimento e inclui a solicitação no trabalho.

## Deixe o Copilot trabalhar

O Copilot incorporará a nova solicitação ao fluxo de trabalho depois de concluir a etapa em andamento quando você enviou a mensagem.

O trabalho pode levar alguns minutos. Aproveite esse tempo para refletir sobre o que você aprendeu e explorou.

## Resumo e próximos passos

Neste exercício, você explorou a página de agentes do Copilot, o painel central para acompanhar e orientar tarefas do agente de nuvem do GitHub Copilot. Você pode acompanhar tarefas ativas e concluídas, revisar o trabalho e redirecionar tarefas em andamento para ajustar o escopo ou fornecer outras orientações.

Você explorou como:

- usar o painel central e a página de agentes para acompanhar as tarefas do agente de nuvem.
- redirecionar uma sessão em andamento para solicitar funcionalidades adicionais.

Enquanto o Copilot conclui o trabalho nos recursos de acessibilidade, você pode [iterar sobre os pull requests criados por ele][next-lesson].

## Recursos

- [Página de agentes do Copilot][agents-page]
- [Sobre agentes personalizados][custom-agents]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar sobre o trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
