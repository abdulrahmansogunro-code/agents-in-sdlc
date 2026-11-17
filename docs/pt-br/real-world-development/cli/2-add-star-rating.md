---
title: "Lição 2 - Adicionar avaliações por estrelas: uma melhoria rápida"
description: "Use o Copilot CLI para fazer uma pequena alteração nos cartões de jogos, revisá-la em um navegador encaminhado e mesclá-la como seu primeiro pull request."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Agora que você instalou o Copilot CLI e iniciou uma conversa, é hora de fazer sua primeira alteração no projeto. Ela será pequena: os dados dos jogos já incluem uma avaliação por estrelas, mas os cartões da página inicial ainda não a exibem. Você pedirá ao agente que mostre a avaliação, revisará a alteração e a mesclará como seu primeiro pull request.

Nesta lição, você vai:

- iniciar uma conversa focada do Copilot em uma branch de funcionalidade.
- pedir ao agente que faça uma pequena alteração no projeto.
- revisar a alteração com `/diff`.
- executar o aplicativo e confirmar a alteração em um navegador encaminhado.
- abrir e mesclar seu primeiro pull request.

## Cenário

Cada jogo do Tailspin Toys pode ter uma avaliação por estrelas, que já aparece na página de detalhes do jogo. Porém, os cartões de jogos na página inicial exibem apenas o título, a categoria, a editora e a descrição. Como primeiro exercício, você pedirá ao agente que mostre em cada cartão a avaliação existente — uma alteração pequena e independente, ideal para sua primeira sessão.

## Anatomia de uma conversa

Uma **conversa** é o espaço em que você trabalha com o Copilot CLI em uma tarefa. Diferentemente do aplicativo Copilot, uma conversa normal no CLI usa o repositório e a branch do Git atualmente selecionados no terminal, em vez de criar uma worktree dedicada. As conversas salvas permitem retomar a mesma discussão depois, enquanto os arquivos e a branch continuam sendo o estado normal do Git no disco.

Em uma conversa, você verá três elementos: seus prompts e as respostas do agente, a atividade das ferramentas que o agente usa para explorar e editar arquivos e as alterações que você pode inspecionar com `/diff`.

## Inicie uma conversa e solicite a alteração

Comece uma nova conversa para implementar a funcionalidade.

1. Retorne ao seu Codespace.
2. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Se o Copilot ainda não estiver em execução, inicie-o com este comando:

   ```bash
   copilot --yolo
   ```

4. Inicie uma nova sessão com o comando de barra `/new` e pressione <kbd>Enter</kbd>.
5. Use este prompt para solicitar a alteração:

   ```plaintext
   Mostre nos cartões de jogos da página de listagem a propriedade starRating de cada jogo em uma escala de 5 estrelas. Se a avaliação for null, mostre "No rating yet". Mantenha o layout dos cartões e adicione testes; depois, execute as verificações relevantes.
   ```

O Copilot explora o projeto, localiza os arquivos que exibem os detalhes dos jogos e cria o código necessário. Você acaba de adicionar uma funcionalidade com o Copilot CLI.

## Revise o diff

Todas as alterações geradas por inteligência artificial precisam ser revisadas antes da mesclagem, mesmo as pequenas. Revise as alterações diretamente no Copilot CLI.

1. Digite `/diff` e inspecione cada arquivo alterado.
2. Confirme que o cartão de jogo exibe a avaliação numérica quando ela está disponível e `No rating yet` quando `starRating` é `null`.
3. Confirme que os testes cobrem os dois casos.
4. Revise os resultados das verificações executadas pelo Copilot e peça que ele corrija as falhas.
5. Ao concluir a revisão, pressione <kbd>Esc</kbd> para sair da tela de diff.

> [!NOTE]
> Como todas as ferramentas de IA generativa, o Copilot é probabilístico, não determinístico. O código exato pode variar. Revise o comportamento em vez de esperar uma implementação idêntica.

## Verifique as alterações

Não basta ler o código e presumir que ele funciona. Peça ao Copilot que inicie o site para que você examine a interface do usuário (UI) atualizada no navegador encaminhado pelo Codespaces.

1. Peça ao Copilot que inicie o aplicativo:

   ```plaintext
   Inicie o aplicativo para que eu possa inspecionar no navegador a alteração das avaliações por estrelas. Informe a URL e mantenha o servidor em execução.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Confirme que os cartões de jogos exibem as avaliações em uma escala de cinco estrelas.
4. Volte ao Copilot e peça que pare o servidor iniciado:

   ```plaintext
   Pare o servidor de desenvolvimento que você iniciou.
   ```

## Abra e mescle seu primeiro pull request

Você criou a funcionalidade. Agora, crie um pull request para mesclar o novo código ao projeto.

1. Peça ao agente padrão que confirme a alteração:

   ```plaintext
   Confirme as alterações revisadas das avaliações por estrelas com uma mensagem de commit adequada.
   ```

2. Digite `/pr create`. O Copilot CLI enviará o commit existente ao criar o PR e exibirá a URL do pull request.
3. Abra o PR mantendo <kbd>Command</kbd> (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) pressionada enquanto seleciona a URL exibida pelo Copilot CLI.
4. Revise os arquivos alterados e as verificações.
5. Quando estiver tudo pronto, selecione **Merge pull request** e confirme a mesclagem.
6. Volte ao Codespace e saia do Copilot CLI com `/exit`.
7. Atualize sua `main` local:

   ```bash
   git checkout main
   git pull
   ```

## Resumo e próximos passos

Parabéns! Você entregou sua primeira alteração usando o GitHub Copilot CLI. Nesta lição, você:

- iniciou uma conversa focada do Copilot em uma branch de funcionalidade.
- orientou o agente a fazer uma pequena alteração nos cartões de jogos.
- revisou a alteração com `/diff`.
- executou o aplicativo e confirmou as avaliações por estrelas em um navegador encaminhado.
- abriu e mesclou seu primeiro pull request.

Em seguida, você [começará pela issue de filtragem e usará os modos Plan e Autopilot][next-lesson] para desenvolver uma funcionalidade maior.

## Recursos

- [Sobre o GitHub Copilot CLI][about-copilot-cli]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
