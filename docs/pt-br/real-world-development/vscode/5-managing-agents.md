---
title: "Exercício 5 - Monitorar e gerenciar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Agentes personalizados][previous-lesson] |
|:--|

No modo de agente, o GitHub Copilot trabalha de forma autônoma: explora a base de código, propõe alterações, edita arquivos e executa comandos. Como esse trabalho acontece em tempo real no computador, o Copilot Chat no VS Code mostra as chamadas de ferramentas e as edições de arquivos. Você pode revisar cada diff, aceitar ou rejeitar alterações e orientar a conversa com prompts complementares sem sair do editor.

Neste exercício, você vai:

- acompanhar em tempo real o trabalho do agente de acessibilidade.
- revisar e aceitar as edições propostas nos arquivos.
- orientar o agente durante a sessão para adicionar um controle de modo claro junto ao modo de alto contraste.

## Cenário

O agente personalizado de acessibilidade do [Exercício 4][previous-lesson] está implementando o modo de alto contraste. Enquanto o trabalho está em andamento, a equipe de design solicita também um controle de modo claro para pessoas que consideram o tema padrão escuro demais. Em vez de começar uma conversa nova, você orientará a sessão existente.

## Acompanhe o progresso do Copilot

A visualização Copilot Chat mostra cada etapa do agente: os arquivos explorados, os comandos executados e as edições propostas. Cada edição aparece na conversa com um diff e os controles **Keep** e **Undo**.

1. Volte à visualização Copilot Chat do Exercício 4.
2. Enquanto o agente trabalha, percorra a conversa e acompanhe as chamadas de ferramentas, leituras e edições de arquivos e os comandos de terminal solicitados.
3. Quando o agente propuser uma edição, revise o diff:
   - Selecione **Keep** para aceitar a alteração.
   - Selecione **Undo** para desfazê-la e permitir que o agente tente novamente.
4. Abra o indicador **Files changed** na parte superior do chat para revisar todos os arquivos alterados durante a sessão.

> [!NOTE]
> Se uma chamada de ferramenta exigir permissão, por exemplo, para executar um comando de terminal, o agente aguardará e exibirá uma solicitação **Allow**. Aprove somente os comandos que você considerar seguros.

5. Aguarde o agente concluir o modo de alto contraste. Ele deverá apresentar uma mensagem final que resume as alterações.

## Oriente o agente para adicionar o modo claro

Depois de implementar o modo de alto contraste, estenda a mesma conversa para adicionar um controle de modo claro. Como você continuará na mesma sessão, o agente manterá o contexto do trabalho, incluindo os componentes alterados, a abordagem de estilo e o uso de local storage.

1. No campo de entrada do Copilot Chat, envie este prompt complementar:

   ```plaintext
   Bom trabalho! Agora, adicione um controle de modo claro ao lado do controle de alto contraste. O modo claro deve seguir o mesmo padrão: salvar a configuração no local storage e ficar disponível na mesma área da interface. As pessoas devem poder ativar o alto contraste e o modo claro de forma independente.
   ```

2. O agente continuará o trabalho, explorando as alterações existentes e propondo novas alterações para o modo claro.
3. Revise cada nova edição e use **Keep** ou **Undo** no diff.
4. Se o agente seguir uma direção indesejada, como refatorar os controles de uma maneira que você não quer, interrompa-o com o botão **Stop** ao lado do campo de entrada e envie uma mensagem para esclarecer a solicitação.

> [!TIP]
> Orientar uma sessão em andamento é mais rápido do que começar de novo. Use prompts complementares para pedir ajustes, corrigir o rumo ou ampliar o escopo.

## Revise o conjunto de alterações

Antes de confirmar o trabalho, revise tudo que o agente alterou.

1. Abra a visualização **Source Control** no VS Code.
2. Revise a lista completa dos arquivos alterados. Ela deve incluir componentes Astro, estilos e testes relacionados.
3. Abra alguns arquivos alterados e percorra os diffs. Confirme se a implementação segue os padrões de acessibilidade indicados pelo agente personalizado: atributos Accessible Rich Internet Applications (ARIA), navegação por teclado, HyperText Markup Language (HTML) semântico e persistência no local storage.
4. Quando estiver satisfeito, prepare e confirme as alterações na visualização Source Control. Você as publicará na [próxima lição][next-lesson].

## Resumo e próximos passos

Você usou o modo de agente do Copilot Chat para acompanhar e orientar uma sessão em andamento: revisou cada edição, aceitou ou rejeitou alterações e enviou prompts complementares para ampliar o trabalho sem perder o contexto.

Nesta lição, você:

- acompanhou o trabalho do agente em tempo real.
- aceitou e rejeitou edições individuais.
- orientou uma sessão em andamento com prompts complementares.

Na [próxima lição][next-lesson], você publicará o trabalho de acessibilidade em um pull request e revisará as alterações produzidas pelo agente personalizado local durante o workshop.

## Recursos

- [Copilot Chat no VS Code][copilot-chat-vscode]
- [Usar o modo de agente][agent-mode]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar sobre o trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
