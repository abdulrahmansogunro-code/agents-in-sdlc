---
title: "Exercício 1 - Instruções personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Pré-requisitos][previous-lesson] · [Próxima lição: Modo de agente →][next-lesson]

O contexto é essencial ao trabalhar com inteligência artificial generativa. Se uma tarefa precisa ser feita de uma maneira específica — ou se há informações de contexto que o Copilot deve conhecer — disponibilize essas informações. Os [arquivos de instruções][instruction-files] fornecem orientação para a geração de código.

Neste exercício, você vai:

- explorar como o contexto específico do projeto, as diretrizes de programação e os padrões de documentação chegam ao Copilot por meio de instruções personalizadas do repositório e de arquivos de instruções associados a caminhos.
- gerar a primeira parte dos dados para a filtragem — um auxiliar de editoras — usando as instruções atuais.
- adicionar um novo padrão para todo o repositório em `.github/copilot-instructions.md`.
- executar novamente o mesmo prompt e observar o código gerado seguir o novo padrão.
- confirmar as instruções e a parte da filtragem na branch `main` para que o Copilot use as instruções atualizadas no próximo exercício.

> [!CAUTION]
> O código gerado pode não seguir todos os padrões definidos. O Copilot é não determinístico. O objetivo é observar a tendência de mudança após atualizar as instruções, não obter resultados idênticos caractere por caractere.

## Arquivos de instruções

### Cenário

A Tailspin Toys tem diretrizes e requisitos para suas práticas de desenvolvimento:

- A camada de dados sempre precisa de testes unitários.
- A interface do usuário deve usar o modo escuro e ter uma aparência moderna.
- O código deve incluir comentários TypeScript Documentation (TSDoc).
- O início de cada arquivo deve conter um bloco de comentários que descreva a finalidade do arquivo.

Os arquivos de instruções ajudam a garantir que o Copilot tenha o contexto necessário para seguir essas práticas.

### Instruções personalizadas

As instruções personalizadas fornecem contexto e preferências ao Copilot para que ele entenda melhor o estilo de programação e os requisitos do projeto. Elas podem especificar convenções de programação, bibliotecas e tipos de comentários. É possível criar instruções para todo o repositório ou para tipos específicos de arquivos e tarefas.

Há dois tipos de arquivos de instruções:

- `.github/copilot-instructions.md` é um arquivo único enviado ao Copilot em **todas** as solicitações do repositório. Ele deve conter informações sobre o projeto relevantes para a maioria das solicitações, como a pilha de tecnologias, uma visão geral do projeto, práticas recomendadas e orientações gerais.
- `.github/instructions/*.instructions.md` pode conter diretrizes para tarefas ou tipos de arquivo específicos, como TypeScript, Astro, componentes de interface ou testes unitários.

> [!NOTE]
> Em um IDE, os arquivos de instruções são usados na geração de código pelo Copilot Chat, não em sugestões de conclusão de código ou de próxima edição.
>
> O Copilot Chat, o Copilot CLI e o agente de nuvem do Copilot usam as instruções do repositório e os arquivos `*.instructions.md` com frontmatter `applyTo`.
>
> O Copilot também [oferece suporte a outros formatos de arquivos de instruções][custom-instructions-support], incluindo AGENTS.md e CLAUDE.md.

### Práticas recomendadas para gerenciar arquivos de instruções

Os exemplos do projeto mostram uma abordagem representativa:

- Mantenha `copilot-instructions.md` focado nas orientações do projeto, como descrição, estrutura e padrões globais.
- Use arquivos `*.instructions.md` para fornecer instruções específicas para tipos de arquivo (testes unitários, componentes Astro, camada de dados) ou tarefas.
- Use linguagem natural e orientações claras, com exemplos de código correto e incorreto.

Não há uma única maneira correta de criar arquivos de instruções ou usar inteligência artificial. Faça experiências para descobrir o que funciona melhor para o projeto.

> [!TIP]
> Todo projeto que usa o GitHub Copilot deve ter um conjunto sólido de arquivos de instruções. Explore os arquivos do projeto, que incluem orientações para [alterações na interface][ui-instructions] e [Astro][astro-instructions].
>
> O Copilot também pode ajudar a gerar arquivos de instruções. Cada interface oferece essa opção de uma maneira diferente, como **Configure Chat → Generate Agent Instructions** no VS Code ou `/init` no Copilot CLI. A lição do ambiente em uso indica a opção relevante.
>
> Para encontrar modelos ou um ponto de partida, explore o [awesome-copilot][awesome-copilot], um repositório com arquivos de instruções, agentes personalizados e outros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explore os arquivos de instruções personalizadas do projeto

Leia os arquivos de instruções incluídos no repositório: um `copilot-instructions.md` principal e vários arquivos `*.instructions.md` para tarefas diferentes. Abra-os no editor ou na interface Web do GitHub.

1. Abra `.github/copilot-instructions.md`.
2. Observe a descrição do projeto e seções como **Agent notes**, **Code standards**, **Scripts** e **Repository Structure**. Em **Code standards**, observe as orientações aninhadas sobre **GitHub Actions Workflows**. Elas se aplicam a todas as interações com o Copilot.
3. Abra a pasta `.github/instructions`. Há instruções para arquivos Astro, a camada de dados Drizzle, testes e outros tópicos.
4. Abra `.github/instructions/unit-tests.instructions.md`. Observe o campo `applyTo`, que define um glob relativo à raiz do repositório para determinar quais arquivos correspondem às instruções. Neste caso, arquivos de teste TypeScript, como `**/*.test.ts`.
5. Observe as instruções específicas para criar testes unitários neste projeto.
6. Abra `.github/instructions/drizzle.instructions.md` e vá até o final. Observe os links para outros arquivos de instruções, como `unit-tests.instructions.md`, e para arquivos existentes do projeto. Os caminhos são relativos ao arquivo de instruções, não à raiz do repositório.

> [!NOTE]
> A seção **Code formatting requirements** em `copilot-instructions.md` descreve os padrões de programação, mas ainda não exige documentação no código. Nas próximas etapas, você adicionará regras para comentários TSDoc e cabeçalhos de comentários nos arquivos.

## Crie uma branch para as alterações

Crie uma branch para trabalhar nas alterações.

1. Volte ao Codespace usado no exercício anterior.
2. Abra um terminal pressionando <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Crie e selecione uma branch:

   ```bash
   git checkout -b custom-instructions
   ```

## Use o Copilot Chat antes de atualizar as instruções

Para observar o efeito das instruções personalizadas, envie primeiro um prompt com o arquivo de instruções atual. Depois, atualize-o e envie o mesmo prompt novamente para comparar.

1. Volte ao Codespace, abra o painel Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa.
2. Feche as guias de editor abertas em exercícios anteriores para que o Copilot use somente o contexto desejado.
3. Abra `src/lib/publishers.ts` para indicar onde o auxiliar deve ficar.
4. Na lista de agentes da visualização Chat, selecione **Agent** para que o Copilot possa alterar arquivos.

   ![Seletor de agente na visualização Chat](../../../_images/shared-chat-mode-selector.png)

5. Envie este prompt:

   ```plaintext
   Crie ou atualize src/lib/publishers.ts com um auxiliar de acesso a dados que retorne uma lista de todas as editoras, com nome e id de cada uma. Aplique as alterações aos arquivos.
   ```

6. Observe o Copilot explorar o projeto e aplicar as alterações, que podem incluir o arquivo auxiliar e os testes.
7. Observe que a função sugerida é tipada, recebe um cliente `db` como primeiro argumento e retorna uma matriz tipada de editoras. Essas convenções vêm de `.github/instructions/drizzle.instructions.md`, que se aplica a `src/lib/*.ts`.
8. Observe se o código sugerido não inclui comentários TSDoc nem um cabeçalho de comentário no arquivo.

> [!CAUTION]
> Como o Copilot é não determinístico, talvez ele adicione comentários mesmo sem essa orientação. Tudo bem: o objetivo é observar a melhora da consistência depois de atualizar as instruções.

## Adicione um padrão para o repositório

Adicione orientações de programação ao arquivo `.github/copilot-instructions.md` para melhorar as sugestões de código.

1. Abra novamente `.github/copilot-instructions.md`.
2. Localize a seção **Code formatting requirements**, que deve estar perto da linha 27. Observe que ela ainda não exige documentação no código.
3. Logo abaixo dos padrões existentes, adicione estas linhas Markdown:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Salve `copilot-instructions.md`.

> [!TIP]
> As instruções do repositório (`.github/copilot-instructions.md`) são o local adequado para padrões globais, como a regra de comentários de documentação. Use arquivos `*.instructions.md` para linguagens, tipos de arquivo ou tarefas específicas.

## Execute o prompt novamente e observe a diferença

Envie o mesmo prompt mais uma vez para verificar se as novas instruções mudam o código sugerido.

1. Volte ao Copilot Chat e selecione **New Chat** para limpar o contexto.
2. Selecione `src/lib/publishers.ts` para que o Copilot use o arquivo correto como contexto.
3. Envie o mesmo prompt usado anteriormente:

   ```plaintext
   Crie ou atualize src/lib/publishers.ts com um auxiliar de acesso a dados que retorne uma lista de todas as editoras, com nome e id de cada uma. Aplique as alterações aos arquivos.
   ```

4. Observe se o arquivo proposto começa com um bloco de comentários semelhante a este:

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. Observe se a função proposta agora inclui um comentário TSDoc semelhante a este:

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

Você orientou o Copilot a seguir um novo padrão de programação e aplicá-lo ao código que será usado no próximo exercício.

## Confirme as instruções e envie a branch

Os arquivos de instruções são controlados pelo mesmo sistema de controle de versão que os demais arquivos do repositório. Confirme e envie a branch.

1. Abra um terminal pressionando <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
2. Confirme que as instruções e as alterações do auxiliar estão presentes:

   ```bash
   git status
   ```

3. Prepare e confirme as instruções e todos os arquivos alterados pelo Copilot para criar a base do auxiliar:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # If git status shows additional supporting updates (for example tests), add those files too.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Envie a branch ao repositório:

   ```bash
   git push -u origin custom-instructions
   ```

## Crie e mescle um pull request

Depois de enviar a branch, crie um pull request associado à issue do backlog sobre as instruções. O Copilot pode encontrar a issue, criar o PR e mesclá-lo.

> [!NOTE]
> Este é o primeiro exercício em que o Copilot executa ações no GitHub em seu nome. O modelo do projeto já configura as ferramentas do GitHub. Na primeira vez que o Copilot usar uma delas, o VS Code talvez peça que você entre no GitHub. Siga as instruções para permitir o acesso. Você aprenderá como essa conexão funciona — por meio do Model Context Protocol (MCP) — em um exercício posterior.

1. Abra o Copilot Chat no Codespace.
2. Pressione <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) para abrir a visualização Copilot Chat e confirme que **Agent** está selecionado na lista de agentes.
3. Peça ao Copilot que encontre a issue relacionada à atualização dos arquivos de instruções e crie um PR a partir da branch atual. Explique que o PR fecha a issue e inclui a base do auxiliar de editoras:

   ```plaintext
   Encontre a issue relacionada à atualização do arquivo de instruções. Crie um pull request a partir da branch atual, indique que o PR fecha essa issue e mencione também que adicionamos a base do auxiliar de editoras para o trabalho de filtragem.
   ```

4. Aguarde o Copilot encontrar a issue e criar o PR.
5. Quando solicitado a permitir ações do GitHub em seu nome, revise o comando e selecione **Allow** se for apropriado.
6. Depois da criação do PR, peça ao Copilot que o mescle e volte à branch principal local:

   ```plaintext
   Mescle o PR em main. Depois, volte para main localmente e baixe o código mais recente para atualizar o repositório.
   ```

7. Quando solicitado a permitir ações no GitHub e comandos de shell, revise o comando e selecione **Allow** se for apropriado.

Você criou e mesclou um pull request com a ajuda do GitHub Copilot.

## Resumo e próximos passos

Você explorou como o Copilot usa o contexto dos arquivos de instruções e usou o Copilot Chat no VS Code para:

- enviar um prompt de geração de código e observar o resultado com as instruções existentes.
- adicionar um novo padrão para todo o repositório em `.github/copilot-instructions.md`.
- executar o mesmo prompt novamente e observar o código sugerido seguir o novo padrão.
- confirmar as instruções e a base do auxiliar na `main` para que o próximo exercício possa usá-las.

Em seguida, você aplicará essas instruções no [modo de agente][next-lesson] para adicionar uma funcionalidade em diferentes partes do código.

## Recursos

- [Arquivos de instruções para personalizar o GitHub Copilot][instruction-files]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [5 dicas para escrever instruções melhores para o Copilot][copilot-instructions-five-tips]
- [Instruções pessoais personalizadas para o GitHub Copilot][personal-instructions]
- [Awesome Copilot — coleção de arquivos de instruções e outros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
