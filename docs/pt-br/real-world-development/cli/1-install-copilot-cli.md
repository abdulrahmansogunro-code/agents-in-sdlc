---
title: "Lição 1 - Instalar o GitHub Copilot CLI"
description: "Instale e autentique o Copilot CLI no Codespace, conheça o ambiente e localize a issue de filtragem criada para o workshop."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

O [GitHub Copilot CLI][about-copilot-cli] é um assistente de programação baseado em agentes executado no terminal. Ele explora bases de código, gera código, executa comandos e interage com ferramentas externas pela linha de comando. Você pode delegar tarefas, solicitar alterações e manter o foco. Primeiro, instale a ferramenta usando recursos que já conhece.

Nesta lição, você vai:

- instalar o GitHub Copilot CLI com npm.
- autenticar com sua conta do GitHub.
- confiar no repositório do workshop e iniciar uma conversa de teste.
- localizar a issue de filtragem com o servidor do Model Context Protocol (MCP) integrado do GitHub.

## Cenário

Sua equipe está começando a usar agentes de inteligência artificial para trabalhar em um backlog crescente. O Copilot CLI oferece esses recursos no terminal, onde muitos desenvolvedores já trabalham. Nesta lição, você instalará e autenticará a ferramenta para usá-la no restante do workshop.

## Instale o Copilot CLI

Você pode instalar o Copilot CLI com [npm][install-cli], WinGet ou Homebrew. Como o GitHub Codespaces já inclui o Node.js, use npm.

1. Volte ao Codespace e abra um terminal.
2. Confirme se o Node.js está instalado e atende ao requisito de versão:

   ```bash
   node --version
   ```

   A versão deve ser 24 ou posterior.

3. Instale o Copilot CLI globalmente:

   ```bash
   npm install -g @github/copilot
   ```

4. Confirme a instalação:

   ```bash
   copilot --version
   ```

   O comando deve exibir o número da versão instalada.

## Autentique-se com o GitHub

Na primeira inicialização, o Copilot CLI solicita a autenticação com sua conta do GitHub.

1. Inicie o Copilot CLI:

   ```bash
   copilot
   ```

2. Se solicitado, siga as instruções do código de dispositivo para autenticar e autorizar o Copilot CLI.
3. O Copilot CLI exibirá esta solicitação:

   ```plaintext
   Copilot can read files in this folder and, with your permission, edit them or run code and shell commands. It will remember your permissions for the rest of this session.

   Do you trust the files in this folder?
   ```

4. Confirme que o caminho corresponde ao repositório Tailspin Toys e responda selecionando **Yes, and remember this folder for future sessions**.

> [!NOTE]
> Em um Codespace, talvez você já esteja autenticado pela sessão do GitHub. Se o Copilot CLI iniciar sem pedir autenticação, está tudo certo.

## Conheça o ambiente

Os comandos digitados no prompt normal do shell são executados diretamente no Codespace. Depois que o Copilot CLI é iniciado, linguagem natural é enviada ao agente e os comandos de barra controlam a conversa.

1. Digite `/model`, use as setas para selecionar **Auto**, pressione <kbd>Enter</kbd> e pressione <kbd>Enter</kbd> novamente para confirmar.
2. Digite `/help` para ver os comandos disponíveis na versão instalada e pressione <kbd>Esc</kbd> para fechar a tela de ajuda.
3. Faça uma pergunta simples para confirmar que tudo está funcionando:

   ```plaintext
   Quais são os principais arquivos deste projeto?
   ```

4. Leia a resposta e observe como o Copilot explora o repositório antes de responder.
5. Digite `/mcp list` e confirme que o servidor MCP integrado do GitHub está disponível.
6. Peça ao Copilot que encontre a issue de filtragem:

   ```plaintext
   Usando o GitHub MCP, encontre neste repositório a issue intitulada "Allow users to filter games by category and publisher". Informe a URL e um resumo breve. Não altere nada.
   ```

7. Abra a URL e leia a issue. Você trabalhará nela depois de concluir uma primeira alteração rápida.

> [!TIP]
> Uma sessão normal do Copilot CLI usa a branch atualmente selecionada no terminal; ela não cria uma worktree automaticamente. Você criará uma branch de funcionalidade antes de cada alteração.

## Use o atalho do workshop

Normalmente, o Copilot CLI pede autorização antes de usar ferramentas fora das permissões já concedidas. Neste workshop, você reiniciará o CLI com `--yolo`, um atalho autorizado por você que remove essas solicitações no Codespace para que possa se concentrar nos exercícios.

> [!CAUTION]
> `--yolo` habilita permissões automáticas completas (`--allow-all-tools`, `--allow-all-paths` e `--allow-all-urls`). Use-o somente em um ambiente isolado, como um Codespace ou uma máquina virtual (VM), e nunca crie um alias padrão para o desenvolvimento diário. Consulte [Permitir e negar o uso de ferramentas][allow-all-warning] para saber mais.

Neste workshop, `--enable-all-github-mcp-tools` habilita as ferramentas MCP de leitura e gravação do GitHub usadas nas lições seguintes para trabalhar com issues e pull requests. O Codespace limita o acesso ao computador local, mas os recursos autenticados do GitHub continuam sendo reais. Revise as alterações antes de publicá-las ou mesclá-las.

1. Saia do Copilot CLI com `/exit`.
2. Reinicie-o na raiz do repositório:

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. Faça outra pergunta simples sobre o projeto para confirmar que a conversa funciona e saia com `/exit`.

O Copilot salva as conversas automaticamente. Mais adiante, depois de alterar as instruções ou adicionar um agente, você usará `copilot --resume` para voltar à mesma conversa e branch da funcionalidade.

## Resumo e próximos passos

Parabéns! Nesta lição, você:

- instalou o GitHub Copilot CLI com npm.
- autenticou com sua conta do GitHub.
- confiou no repositório do workshop e iniciou uma conversa de teste.
- localizou a issue de filtragem com o servidor MCP integrado do GitHub.

Em seguida, você [fará sua primeira alteração pontual][next-lesson] e usará o Copilot CLI para exibir avaliações por estrelas nos cartões de jogos.

## Recursos

- [Instalar o GitHub Copilot CLI][install-cli]
- [Sobre o GitHub Copilot CLI][about-copilot-cli]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
