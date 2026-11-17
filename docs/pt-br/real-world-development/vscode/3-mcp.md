---
title: "Exercício 3 - Testar a funcionalidade com o servidor MCP do Playwright"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Modo de agente][previous-lesson] · [Próxima lição: Agentes personalizados →][next-lesson]

Você acabou de criar a funcionalidade de filtragem com o modo de agente. Antes de abrir um pull request (PR), confirme que ela funciona no navegador. Em vez de testar o aplicativo manualmente, conecte o **servidor do Model Context Protocol (MCP) do Playwright** e peça ao Copilot que controle um navegador real. Depois, publique a branch e abra o PR.

Neste exercício, você vai:

- aprender o que é o Model Context Protocol (MCP) e como os servidores MCP ampliam as ferramentas do Copilot.
- adicionar o servidor MCP do Playwright ao espaço de trabalho.
- pedir ao Copilot que use o servidor para testar manualmente a filtragem em um navegador.
- publicar a branch e abrir um pull request para o trabalho de filtragem.

## O que é o Model Context Protocol (MCP)?

O modo de agente ganha mais recursos quando pode acessar ferramentas além do editor. O Model Context Protocol (MCP) é um padrão que permite ao Copilot se comunicar com ferramentas e serviços externos.

![Diagrama da interação do modo de agente com o contexto, o modelo de linguagem e as ferramentas, incluindo ferramentas fornecidas por servidores MCP e extensões do VS Code](../../../_images/ex1-mcp-diagram.png)

O [Model Context Protocol (MCP)][mcp-blog-post] permite que agentes de inteligência artificial se comuniquem com ferramentas e serviços externos em tempo real. Assim, eles podem acessar informações atualizadas usando recursos e executar ações em seu nome usando ferramentas.

Um servidor MCP atua como ponte entre o agente de inteligência artificial e as ferramentas e os serviços externos, como APIs existentes ou ferramentas locais em pacotes npm. Cada servidor oferece um conjunto diferente de ferramentas e recursos.

Alguns servidores MCP conhecidos:

- **[Servidor MCP do GitHub][github-mcp-server]**: dá acesso a interfaces de programação de aplicações (APIs) para gerenciar repositórios, issues e pull requests do GitHub.
- **[Servidor MCP do Playwright][playwright-mcp-server]**: oferece automação de navegador pelo Playwright, incluindo navegação por páginas, preenchimento de formulários e seleção de botões.

Há muitos outros servidores MCP disponíveis. O GitHub mantém um [registro de MCP][mcp-registry] para facilitar a descoberta e as contribuições ao ecossistema.

> [!CAUTION]
> Por segurança, trate os servidores MCP como qualquer outra dependência do projeto. Antes de usar um servidor, revise o código-fonte, verifique o publicador e considere as implicações de segurança. Use somente servidores confiáveis e tenha cuidado ao conceder acesso a recursos ou operações confidenciais.

## Revise a configuração do MCP

O arquivo `.vscode/mcp.json` configura os servidores MCP disponíveis neste espaço de trabalho do VS Code.

1. Abra `.vscode/mcp.json` no Codespace.
2. Confirme que já há um servidor `github` configurado:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

Essa configuração vem do modelo do projeto. Ela permite que o Copilot leia o backlog de issues sem instalar nada localmente: o VS Code se conecta ao servidor MCP remoto do GitHub por HTTP, e você se autentica na primeira vez que o Copilot usa uma ferramenta.

## Adicione o servidor MCP do Playwright

Adicione um segundo servidor. O [servidor MCP do Playwright][playwright-mcp-server] fornece ao Copilot um navegador controlável para testar a funcionalidade.

1. Em `.vscode/mcp.json`, adicione `playwright` ao lado de `github`. O arquivo deve ficar assim:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. Salve o arquivo.

Ao contrário do servidor remoto `github`, o servidor `playwright` é **local**: o VS Code o inicia no computador executando `npx @playwright/mcp@latest`. A opção `--headless` executa o navegador sem uma janela visível, o que é necessário em um Codespace sem ambiente gráfico.

> [!NOTE]
> O projeto Tailspin Toys já usa o Playwright nos testes de ponta a ponta, portanto o navegador geralmente já está instalado. Se o Copilot informar que o navegador está ausente, peça que execute `npx playwright install chromium` e tente novamente.

## Inicie o servidor e confirme que ele é confiável

O VS Code inicia os servidores MCP **sob demanda**: na primeira vez que o Copilot precisar das ferramentas do servidor, o VS Code o iniciará e pedirá que você confirme que confia nele.

1. Em `.vscode/mcp.json`, selecione **Start**, exibido acima da entrada `playwright`, para iniciar o servidor e confirmar a configuração.
2. Se o VS Code pedir que você confirme que confia no servidor, revise a configuração e escolha a opção para confiar nele.

Iniciar o servidor manualmente é opcional. Se você não fizer isso, o VS Code iniciará o servidor e pedirá que você confirme que confia nele quando o Copilot precisar das ferramentas.

## Teste a filtragem

Com o servidor conectado e o aplicativo em execução, peça ao Copilot que exercite a funcionalidade:

```text
Usando o servidor MCP do Playwright, abra um navegador para o aplicativo em execução em http://localhost:4321 e verifique a nova funcionalidade de filtragem de jogos:

1. Acesse a página de jogos e informe quantos jogos estão listados.
2. Aplique um filtro de categoria e confirme que a lista mostra somente os jogos dessa categoria.
3. Limpe o filtro e aplique um filtro de editora. Confirme que a lista mostra somente os jogos dessa editora.
4. Combine um filtro de categoria com um de editora e confirme que os resultados correspondem aos dois filtros.

Informe o que observou em cada etapa e destaque qualquer comportamento inesperado.
```

O Copilot abrirá um navegador pelo servidor MCP do Playwright, seguirá as etapas e apresentará um relatório. Compare o resultado com os critérios de aceitação da issue. Se houver um problema, faça perguntas complementares ou peça que o Copilot corrija o código antes de abrir o pull request.

O servidor MCP do Playwright usa a [árvore de acessibilidade][playwright-mcp-server] da página, não capturas de tela. Assim, o agente usa elementos estruturados e identificados — botões, links e itens de lista — de maneira semelhante à tecnologia assistiva. Uma verificação funcional rápida também pode servir como uma análise básica de acessibilidade.

> [!NOTE]
> Para o teste, o aplicativo precisa estar em execução em `http://localhost:4321`. Se você tiver parado o servidor de desenvolvimento, inicie-o antes de enviar o prompt. Na primeira vez que o Copilot usar o servidor MCP do Playwright, talvez seja necessário baixar um navegador. Se o agente informar que falta um navegador, peça que execute `npx playwright install chromium` e tente novamente.

## Publique a branch e crie um pull request

Depois de confirmar que a funcionalidade funciona, abra um pull request (PR) para que a equipe possa revisá-la. Primeiro, publique a branch `filtering-vscode`.

1. Abra o painel **Source Control** no Codespace e revise as alterações feitas pelo Copilot.
2. Selecione **+** para preparar as alterações.
3. Use o botão **Sparkle** para gerar uma mensagem de commit.

   ![Painel Source Control com as alterações do Copilot](../../../_images/ex3-source-control-changes.png)

4. Selecione **Publish** para enviar a branch ao repositório.

## Crie o pull request

Você pode criar um pull request no GitHub.com ou pela interface de linha de comando do GitHub. Como já está trabalhando com o GitHub Copilot, peça ao Copilot que encontre a issue relacionada e crie um PR vinculado a ela.

1. Abra o painel Copilot Chat e selecione **New Chat** para iniciar uma sessão.
2. Na lista de agentes, confirme que **Agent** está selecionado para permitir o uso das ferramentas do GitHub.
3. Peça ao Copilot que crie o PR:

   ```plaintext
   Encontre a issue do repositório relacionada à filtragem por categoria e editora. Crie um pull request para a branch atual e associe-o à issue correta.
   ```

4. Selecione **Continue** quando necessário para permitir que o Copilot reúna informações e execute ações. Na primeira utilização de uma ferramenta do GitHub, talvez seja solicitado que você se autentique.
5. Observe o Copilot pesquisar as issues, encontrar a correta e criar o PR.
6. Selecione o link fornecido pelo Copilot para revisar o pull request, mas **não o mescle ainda**.

## Resumo e próximos passos

Neste exercício, você:

- aprendeu o que é o Model Context Protocol (MCP) e como os servidores MCP ampliam as ferramentas do Copilot.
- adicionou o servidor MCP do Playwright ao espaço de trabalho.
- usou o servidor para testar a filtragem em um navegador antes de publicá-la.
- publicou a branch e abriu um pull request para o trabalho de filtragem.

Você usou um servidor MCP para testar uma funcionalidade, mas o MCP é apenas uma das maneiras de ampliar o Copilot. Em seguida, você [criará um agente personalizado][next-lesson] para tarefas específicas, como revisões de acessibilidade.

## Recursos

- [O que é MCP e por que todo mundo está falando dele?][mcp-blog-post]
- [Servidor MCP do Microsoft Playwright][playwright-mcp-server]
- [Servidor MCP do GitHub][github-mcp-server]
- [Registro de MCP do GitHub][mcp-registry]
- [Servidores MCP no VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
