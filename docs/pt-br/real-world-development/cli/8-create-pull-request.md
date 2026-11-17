---
title: "Lição 8 - Criar e mesclar o pull request (PR) da funcionalidade"
description: "Revise a filtragem, as instruções, a atualização da skill, o perfil de QA e os testes; depois, crie um PR e use o Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

A implementação da filtragem, as atualizações de instruções, a atualização da skill, o perfil de garantia de qualidade (QA) e os testes estão salvos em uma única branch. Agora, revise todos esses itens e abra um pull request (PR). Você mesclou o PR das avaliações por estrelas manualmente; desta vez, usará o **Agent Merge** para gerenciar o processo.

> [!NOTE]
> Em geral, separaríamos a funcionalidade, as atualizações de instruções, a atualização da skill e o agente de QA em alguns PRs. Para simplificar o workshop, mantivemos todo o fluxo de filtragem e qualidade em uma conversa e branch e incluiremos o trabalho em um único PR.

Nesta lição, você vai:

- aprender o que é o Agent Merge e como ele automatiza o ciclo de vida da mesclagem.
- inspecionar a alteração completa da funcionalidade e as evidências de verificação.
- criar o PR da filtragem.
- habilitar o Agent Merge somente depois da revisão e confirmar que o PR foi mesclado.

## Cenário

Durante o fluxo de filtragem, você usou o Copilot para planejar, implementar e verificar uma funcionalidade. Agora, a Tailspin Toys quer automatizar o trabalho restante do PR, mantendo a autorização da mesclagem sob o controle do desenvolvedor.

## Conheça o Agent Merge

O **Agent Merge** automatiza o trabalho restante para concluir um pull request. Quando habilitado, o Copilot resolve os impedimentos do PR — corrige verificações de integração contínua (CI) com falha, responde aos comentários de revisão e faz rebase quando necessário — e depois habilita a mesclagem automática do GitHub se o repositório permitir.

Até agora, você selecionou **Merge pull request** manualmente. O Agent Merge pode assumir essa responsabilidade. Revise o trabalho e confirme que ele está pronto antes de habilitar o Agent Merge.

## Use o Agent Merge para gerenciar o PR

Com todo o código pronto, revise-o, crie o PR e deixe que o Agent Merge gerencie o restante do processo.

1. Volte ao Codespace.
2. Abra a caixa de diálogo do agente digitando `/agent`.
3. Selecione **Default** na lista de opções e pressione <kbd>Enter</kbd>.
4. Crie um novo PR com o comando `/pr create`.
5. Ative o Agent Merge com `/pr agentmerge`.
6. O Copilot acompanhará o processo de integração contínua do PR. Quando tudo for aprovado, ele fará a mesclagem.
7. Confirme que o Copilot exibiu uma mensagem semelhante a “PR #14 was squash-merged successfully”.

> [!IMPORTANT]
> O Agent Merge não ignora aprovações obrigatórias, proteção de branch, filas de mesclagem, configurações do repositório nem permissões ausentes. Se houver um bloqueio, leia o motivo informado e conclua manualmente a mesclagem revisada quando o repositório permitir.

## Resumo e próximos passos

Você automatizou várias etapas do processo de desenvolvimento: geração de código, teste e validação e, agora, o processo do pull request. Nesta lição, você:

- aprendeu o que é o Agent Merge e como ele automatiza o ciclo de vida da mesclagem.
- inspecionou a alteração completa da funcionalidade e as evidências de verificação.
- criou o PR da filtragem.
- habilitou o Agent Merge somente depois da revisão e confirmou que o PR foi mesclado.

Em seguida, você [explorará outros comandos de barra úteis do Copilot CLI][next-lesson] para contexto, modelos, compartilhamento e delegação opcional para a nuvem.

## Recursos

- [Gerenciar pull requests com o Copilot CLI][manage-prs]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
