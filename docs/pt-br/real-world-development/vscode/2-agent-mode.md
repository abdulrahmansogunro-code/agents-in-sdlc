---
title: "Exercício 2 - Adicionar funcionalidades com o modo de agente do Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Até mesmo uma alteração simples costuma exigir modificações em vários arquivos e a execução de testes. Um fluxo comum de desenvolvimento inclui localizar os arquivos relevantes, fazer alterações, executar testes, depurar e descobrir se algum arquivo foi esquecido. O modo de agente do Copilot pode explorar a estrutura do projeto, fazer alterações coordenadas, executar tarefas como testes e corrigir problemas encontrados.

> [!NOTE]
> Embora tenham nomes semelhantes, o modo de agente e o agente de nuvem oferecem experiências diferentes. O modo de agente executa tarefas no IDE e permite ciclos de feedback rápidos e interação. O agente de nuvem trabalha de forma assíncrona, como parte da equipe, e interage por meio de issues e pull requests.

Neste exercício, você vai aprender como:

- o modo de agente do Copilot explora o projeto, identifica arquivos relevantes e coordena alterações.
- o modo de agente do GitHub Copilot implementa funcionalidades na interface e na camada de dados.
- revisar alterações e testes gerados pelo modo de agente antes de mesclá-los à base de código.

## Cenário

À medida que a lista de jogos cresce, você quer permitir que as pessoas filtrem por categoria e editora. No exercício anterior, você adicionou um auxiliar de editoras. Agora, concluirá o trabalho restante na camada de dados, na interface e nos testes com o modo de agente do Copilot.

## Execute o site Tailspin Toys

Antes de fazer alterações, explore o site para entender as funcionalidades atuais.

O site é uma plataforma de financiamento coletivo para jogos de tabuleiro com um tema para desenvolvedores. Ele permite listar jogos e exibir detalhes. O site é um único aplicativo Astro, que gera HyperText Markup Language (HTML) estático durante a compilação. As páginas consultam um banco de dados SQLite local diretamente no frontmatter com o Drizzle Object-Relational Mapping (ORM). Não há uma Application Programming Interface (API) de back-end separada nem um framework de interface do lado do cliente. Os auxiliares reutilizáveis de acesso a dados ficam em `src/lib/`, e a interatividade usa um pequeno `<script>` do Astro com APIs padrão do Document Object Model (DOM).

### Inicie o site

O comando `npm run dev` inicia o servidor de desenvolvimento do Astro. Execute-o no Codespace:

1. Volte ao Codespace. Você deve estar na branch `main` depois do exercício anterior.
2. Abra um terminal no Codespace pressionando <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Crie e selecione uma branch para o trabalho de filtragem:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicie o site:

   ```bash
   npm run dev
   ```

   Quando o servidor Astro estiver pronto, será exibido um banner semelhante a este:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Se uma caixa de diálogo pedir para abrir `http://localhost:4321` em um navegador, feche-a selecionando **x**.

5. Abra o site mantendo <kbd>Command</kbd> (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) pressionada enquanto seleciona `http://localhost:4321` no terminal.

> [!NOTE]
> Em um Codespace, selecionar o link `localhost` no terminal redireciona automaticamente para `https://<your-codespace-name>-4321.app.github.dev/`, um túnel privado para o servidor em execução no Codespace.

### Explore o site

Com o site em execução, explore suas funcionalidades:

- **Página inicial**: exibe uma lista de jogos de tabuleiro com títulos, imagens e descrições.
- **Página de detalhes do jogo**: selecione um jogo para ver mais informações, incluindo título, descrição, editora e categoria.

## Explore o backlog com o Copilot

> [!TIP]
> **Abra o Copilot Chat**
>
> Volte ao Codespace, abra o painel Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. O modo e o modelo variam conforme o exercício; as etapas indicam as opções necessárias.

O site já funciona, mas você quer adicionar recursos. O modelo do projeto cria automaticamente um backlog de issues. Peça ao GitHub Copilot que mostre essas tarefas.

1. Na lista de agentes da visualização Chat, selecione **Agent**. O agente planeja e implementa alterações em vários arquivos, executa comandos no terminal e chama ferramentas.

   ![Seletor de agente na visualização Chat](../../../_images/shared-chat-mode-selector.png)

2. Selecione **Claude Sonnet 4.5** na lista de modelos disponíveis.

> [!CAUTION]
> A inclusão de um modelo nestas instruções não representa preferência dos autores. O workshop foi criado com Claude Sonnet 4.5 para que as sugestões fossem relativamente consistentes. Como os modelos de linguagem são probabilísticos, as sugestões podem ser diferentes; isso é normal.

> [!NOTE]
> Devido à natureza probabilística dos modelos de linguagem, o Copilot pode usar um comando do Model Context Protocol (MCP) diferente, mas ainda deve conseguir concluir a tarefa.

3. Peça ao Copilot que mostre o backlog:

   ```plaintext
   Mostre o backlog de itens do meu repositório do GitHub. Ajude-me a priorizá-los de acordo com o que será mais útil para as pessoas usuárias.
   ```

4. Selecione **Continue** para permitir que o comando liste todas as issues.
5. Revise a lista gerada.

Observe como o Copilot prioriza os itens de acordo com a utilidade que estima para as pessoas usuárias.

## Revise os arquivos de instruções

Antes de pedir ao agente que gere o código, revise o arquivo de instruções que fornecerá contexto. Você usará o arquivo [interface do usuário (UI)](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md), que descreve como adicionar funcionalidades ao site.

1. No Codespace, abra `.github/instructions/ui.instructions.md`.
2. Observe as orientações gerais para adicionar funcionalidades:
   - uma visão geral da arquitetura.
   - princípios de projeto de componentes, testabilidade e acessibilidade.
   - links para arquivos de instruções específicos, incluindo Astro, folhas de estilo em cascata (CSS) do Tailwind e Drizzle.

> [!TIP]
> Os arquivos de instruções podem fazer referência a outros arquivos de instruções e a arquivos do projeto. Os caminhos são relativos ao arquivo de instruções, o que permite reutilizar conteúdo, dividir instruções complexas e fornecer exemplos.

## Implemente a filtragem

Para concluir a filtragem, serão necessárias pelo menos três alterações:

- adicionar ou aprimorar a lógica de filtragem na camada de dados (`src/lib/`).
- adicionar ou atualizar testes do comportamento de filtragem.
- atualizar a página de listagem de jogos para incluir a interface de filtragem.

Os testes também precisam ser executados e aprovados antes da mesclagem. Peça ao modo de agente do Copilot que faça esse trabalho.

1. Continue na conversa atual ou selecione **New Chat** para iniciar outra conversa.
2. Selecione **Add Context**, **Instructions** e **ui** para adicionar o arquivo de instruções.

   ![Seleção do arquivo de instruções da interface do usuário](../../../_images/ex3-select-instructions-file.png)

3. Confirme que **Agent** continua selecionado na lista de agentes da visualização Chat.
4. Confirme que **Claude Sonnet 4.5** continua selecionado como modelo.
5. Envie este prompt para implementar os requisitos da issue relacionada no backlog:

   ```plaintext
   Atualize o site para incluir a filtragem por editora e categoria conforme os requisitos da issue relacionada no backlog do GitHub. O auxiliar de editoras da lição anterior já existe; preserve e aprimore esse trabalho conforme necessário ao concluir as alterações restantes na camada de dados, na interface e nos testes. Confirme que todos os testes foram aprovados. O servidor já está em execução, portanto não é necessário iniciá-lo.
   ```

6. Observe o Copilot explorar o projeto, localizar os arquivos da funcionalidade, alterar a camada de dados e a interface e executar os testes.

   ![Copilot explorando os arquivos do projeto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> O Copilot pode explorar o projeto, modificar arquivos e executar testes por vários minutos. Durante o trabalho, os botões **Keep** e **Undo** podem aparecer no editor. Aguarde a conclusão antes de aceitar ou desfazer as alterações.

7. Quando solicitado pelo Copilot, selecione **Continue** para executar os testes.

   ![Solicitação no painel Copilot Chat para confirmar a execução dos testes](../../../_images/ex3-agent-mode-run-tests.png)

8. Alguns testes podem falhar durante o processo. O Copilot alterna entre geração de código e testes até concluir o trabalho e não detectar erros.

   ![Sessão concluída do modo de agente do Copilot](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Examine o código gerado para identificar possíveis problemas.

> [!CAUTION]
> Revise sempre o código gerado pelo Copilot ou por qualquer outra ferramenta de inteligência artificial.

10. Volte ao navegador que está exibindo o site e explore a nova funcionalidade.
11. Depois de confirmar que tudo funciona e revisar o código, selecione **Keep** na janela do Copilot Chat.

## Resumo e próximos passos

Neste exercício, você usou o modo de agente do GitHub Copilot para adicionar recursos ao site Tailspin Toys. Você aprendeu como:

- o modo de agente do GitHub Copilot implementa funcionalidades na interface e na camada de dados.
- o modo de agente do Copilot explora o projeto, identifica arquivos relevantes e coordena alterações.
- revisar alterações e testes gerados pelo modo de agente antes de mesclá-los à base de código.

Em seguida, você [testará a funcionalidade com o servidor MCP do Playwright][next-lesson] e abrirá um pull request.

### Exercício extra: implemente paginação

À medida que a lista de jogos cresce, será necessário adicionar paginação. Use as habilidades deste exercício e peça ao Copilot que atualize o site. Considere:

- seguir as práticas existentes, incluindo o uso dos arquivos de instruções.
- decidir se a pessoa usuária poderá escolher o tamanho da página ou se ele será fixo.
- incluir no prompt as orientações necessárias para obter a implementação desejada.
- iterar com o GitHub Copilot, pedindo alterações e fornecendo contexto. Esse processo é normal ao trabalhar com o Copilot.

## Recursos

- [Modos ask, edit e agent do Copilot: o que fazem e quando usar cada um][choose-mode]
- [Modo de agente no VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
