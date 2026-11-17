---
title: "Exercício 1 - Instruções personalizadas (agente de nuvem)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Pré-requisitos][previous-lesson] · [Próxima lição: Agente de nuvem do Copilot →][next-lesson]

O contexto é essencial ao trabalhar com inteligência artificial generativa. Se uma tarefa precisa ser feita de uma maneira específica — ou se há informações de contexto que o Copilot deve conhecer — disponibilize essas informações. Os [arquivos de instruções][instruction-files] fornecem essa orientação para que o Copilot entenda não apenas *o que* você quer que ele faça, mas também *como*.

Neste exercício, você vai:

- explorar como o contexto específico do projeto, as diretrizes de programação e os padrões de documentação chegam ao Copilot por meio de instruções personalizadas do repositório e de arquivos de instruções associados a caminhos.
- adicionar um novo padrão para todo o repositório em `.github/copilot-instructions.md`.

> [!NOTE]
> Diferentemente dos percursos de VS Code e CLI, você não fará uma comparação entre prompts antes e depois. O agente de nuvem do Copilot trabalha de forma assíncrona em issues do GitHub, por isso é mais difícil demonstrar o efeito lado a lado em tempo real. Você verá a influência do arquivo de instruções mais adiante, ao revisar os pull requests produzidos pelo agente.

## Arquivos de instruções

### Cenário

Como toda boa equipe de desenvolvimento, a Tailspin Toys tem diretrizes e requisitos para suas práticas:

- A camada de dados sempre precisa de testes unitários.
- A interface do usuário deve usar o modo escuro e ter uma aparência moderna.
- O código deve incluir comentários TypeScript Documentation (TSDoc).
- O início de cada arquivo deve conter um bloco de comentários que descreva a finalidade do arquivo.

Os arquivos de instruções ajudam a garantir que o Copilot tenha o contexto necessário para seguir essas práticas.

### Instruções personalizadas

As instruções personalizadas fornecem contexto e preferências ao Copilot, ajudando-o a entender seu estilo de programação e seus requisitos. Elas podem especificar convenções de programação, bibliotecas e os tipos de comentários a usar. É possível criar instruções para todo o repositório ou para tipos específicos de arquivos e tarefas.

Há dois tipos de arquivos de instruções:

- `.github/copilot-instructions.md` é um arquivo único enviado ao Copilot em **todas** as solicitações do repositório. Ele deve conter informações sobre o projeto relevantes para a maioria das solicitações de chat ou CLI, como a pilha de tecnologias, uma visão geral do projeto, práticas recomendadas e orientações gerais.
- `.github/instructions/*.instructions.md` pode conter diretrizes para tarefas ou tipos de arquivo específicos, como TypeScript, Astro, componentes de interface ou testes unitários.

> [!NOTE]
> Em um ambiente de desenvolvimento integrado (IDE), os arquivos de instruções são usados na geração de código pelo Copilot Chat, não em sugestões de conclusão de código ou de próxima edição.
>
> O Copilot Chat, o Copilot CLI e o agente de nuvem do Copilot usam as instruções do repositório e os arquivos `*.instructions.md` com frontmatter `applyTo`.
>
> O Copilot também [oferece suporte a outros formatos de arquivos de instruções][custom-instructions-support], incluindo AGENTS.md e CLAUDE.md.

### Práticas recomendadas para gerenciar arquivos de instruções

Uma discussão completa sobre como criar arquivos de instruções está fora do escopo deste workshop, mas os exemplos do projeto mostram uma abordagem representativa:

- Mantenha `copilot-instructions.md` focado nas orientações do projeto, como a descrição, a estrutura e os padrões globais de programação.
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
2. Observe a breve descrição do projeto e seções como **Agent notes**, **Code standards**, **Scripts** e **Repository Structure**. Em **Code standards**, observe as orientações aninhadas sobre **GitHub Actions Workflows**. Elas se aplicam a todas as interações com o Copilot.
3. Abra a pasta `.github/instructions`. Há instruções para arquivos Astro, a camada de dados Drizzle, testes e outros tópicos.
4. Abra `.github/instructions/unit-tests.instructions.md`. Observe o campo `applyTo`, que define um glob relativo à raiz do repositório para determinar quais arquivos correspondem às instruções. Neste caso, ele corresponde a arquivos de teste TypeScript, como `**/*.test.ts`.
5. Observe as instruções específicas para criar testes unitários neste projeto.
6. Abra `.github/instructions/drizzle.instructions.md` e vá até o final. Observe os links para outros arquivos de instruções, como `unit-tests.instructions.md`, e para arquivos existentes do projeto. Assim, você pode dividir conjuntos de instruções maiores em arquivos menores e reutilizáveis e indicar exemplos para o Copilot. Os caminhos são relativos ao arquivo de instruções, não à raiz do repositório.

> [!NOTE]
> A seção **Code formatting requirements** em `copilot-instructions.md` descreve os padrões de programação, mas ainda não exige documentação no código. Nas próximas etapas, você adicionará regras para comentários TSDoc e cabeçalhos de comentários nos arquivos.

## Adicione um padrão para o repositório

Agora, adicione uma regra para todo o projeto: a documentação deve usar comentários TSDoc e um cabeçalho de comentário no início do arquivo. O agente de nuvem usará essa regra nas issues que você atribuir mais adiante.

Antes de editar, crie uma branch. O agente de nuvem lê as instruções da branch de destino da issue, mas você também fará um commit organizado das alterações.

1. No terminal do Codespace, crie e selecione uma branch:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

2. Abra novamente `.github/copilot-instructions.md`.
3. Localize a seção **Code formatting requirements**, que deve estar perto da linha 27. Observe que ela ainda não define regras de documentação no código.
4. Adicione estas linhas Markdown logo abaixo dos padrões existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

5. Salve `copilot-instructions.md`.

> [!TIP]
> Como você viu na lição anterior, as instruções podem ser criadas na raiz do repositório (`.github/copilot-instructions.md`) para orientações globais ou em arquivos `*.instructions.md` para linguagens, tipos de arquivo e tarefas específicas. O arquivo do repositório é o local adequado para padrões globais, como a regra de comentários de documentação.

## Confirme e mescle a atualização das instruções

O agente de nuvem lê os arquivos de instruções da branch de destino da issue. No próximo exercício, o agente criará uma branch a partir de `main`, portanto suas alterações precisam chegar a `main` para que ele possa usá-las.

1. Prepare e confirme a alteração:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Envie a branch:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. Em github.com, abra um pull request de `custom-instructions-cloud` para `main` e faça a mesclagem.

> [!TIP]
> Se preferir trabalhar diretamente em `main` neste workshop, você pode ignorar as etapas de branch e confirmar as alterações diretamente em `main`. A branch foi incluída para refletir o fluxo de trabalho usado em um projeto real.

## Resumo e próximos passos

Você explorou como o Copilot usa o contexto dos arquivos de instruções e adicionou um novo padrão para todo o repositório em `.github/copilot-instructions.md`. Você verá esse padrão nos pull requests que o agente de nuvem gerar nas próximas atividades.

Em seguida, você [atribuirá sua primeira issue ao agente de nuvem do Copilot][next-lesson].

## Recursos

- [Arquivos de instruções para personalizar o GitHub Copilot][instruction-files]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [5 dicas para escrever instruções melhores para o Copilot][copilot-instructions-five-tips]
- [Awesome Copilot — coleção de arquivos de instruções e outros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
