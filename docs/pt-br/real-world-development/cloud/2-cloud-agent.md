---
title: "Exercício 2 - Agente de nuvem do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Instruções personalizadas][previous-lesson] |
|:--|

É comum que as organizações tenham dívida técnica: problemas de segurança não resolvidos, código legado que precisa de atualização ou solicitações de funcionalidades que ficaram no backlog por falta de tempo. O agente de nuvem do GitHub Copilot pode atualizar código e adicionar funcionalidades de forma autônoma. Quando termina, ele cria um pull request de rascunho para revisão por um desenvolvedor. Assim, você pode delegar tarefas repetitivas e se concentrar em atividades de maior impacto.

Neste exercício, você vai explorar como:

- personalizar o ambiente de geração de código.
- garantir que as operações sejam realizadas com segurança.
- criar issues com escopo claro.
- atribuir issues ao Copilot.

## Cenários

A Tailspin Toys tem dívida técnica relacionada à documentação: o código não tem comentários no padrão TypeScript Documentation (TSDoc) para funções exportadas. A primeira tarefa é adicionar esses comentários.

A equipe de design também quer melhorar a descoberta de jogos. Ela quer exibir jogos relacionados — outros títulos da mesma categoria — na página de detalhes de cada jogo. Por enquanto, precisa apenas de uma implementação que permita testar a experiência do usuário. Essa tarefa pode ficar no backlog enquanto outras issues têm prioridade mais alta.

Esses tipos de tarefas podem ser delegados ao agente de nuvem do Copilot, que trabalha de forma assíncrona enquanto você se dedica a outras atividades. Depois, você pode revisar o trabalho e confirmar se o resultado está correto.

## Conheça o agente de nuvem do GitHub Copilot

O [agente de nuvem do GitHub Copilot][copilot-agents] executa tarefas em segundo plano de maneira semelhante a um desenvolvedor. Por exemplo, você pode [atribuir uma issue do GitHub ao Copilot][assign-issue]. O Copilot cria um pull request (PR) de rascunho para acompanhar o andamento, configura um ambiente e começa a trabalhar. Você pode examinar a sessão enquanto ela está em andamento ou depois de concluída. Quando a solução estiver pronta para revisão, o Copilot mencionará você no pull request.

## A importância de instruções com escopo definido

O GitHub Copilot não é mágico: ainda é preciso pensar. Mesmo tarefas aparentemente simples podem ter complexidades, por isso [defina o escopo das tarefas com atenção][cloud-agent-best-practices]. Trate o Copilot como um parceiro de programação com inteligência artificial: trabalhe em etapas, aprenda, experimente e adapte o processo. Os fundamentos do desenvolvimento de software não mudam com a inteligência artificial generativa.

## Instruções personalizadas neste repositório

As lições anteriores apresentaram instruções personalizadas e como elas orientam o Copilot. Antes de atribuir trabalho ao agente de nuvem, leia os arquivos de instruções do repositório. Isso ajudará você a perceber o efeito deles mais tarde.

Abra os seguintes arquivos na interface Web do GitHub ou em um Codespace:

- `.github/copilot-instructions.md`: revise a seção **Code standards**, principalmente as expectativas para convenções TypeScript e comentários TSDoc.
- `.github/instructions/unit-tests.instructions.md`: observe o frontmatter `applyTo`, que limita essas instruções aos arquivos `**/*.test.ts`.

Na próxima seção, quando você atribuir a issue `Code lacks documentation` ao agente de nuvem, observe se o pull request inclui comentários TSDoc, segue as convenções de TypeScript e adiciona cabeçalhos de comentários. Essas orientações vêm dos arquivos de instruções. Você revisará os pull requests em um exercício posterior.

## Configure o ambiente de desenvolvimento do agente de nuvem

O desenvolvimento de código normalmente exige um ambiente específico e a execução de scripts de configuração, seja qual for a pessoa ou o agente que fará o trabalho. O agente de nuvem usa o [GitHub Actions][github-actions] e permite configurar um workflow especial em `.github/workflows/copilot-setup-steps.yml`, executado antes do início do trabalho.

Esse workflow já está configurado para o workshop. Ele instala o Node.js e as dependências do projeto, os navegadores do Playwright para testes de ponta a ponta e configura o banco de dados SQLite migrado e com dados para o aplicativo Astro:

```yaml
name: "Copilot Setup Steps"

# Allows you to test the setup steps from your repository's "Actions" tab
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Set the permissions to the lowest permissions possible needed for *your steps*. Copilot will be given its own token for its operations.
    permissions:
      # If you want to clone the repository as part of your setup steps, for example to install dependencies, you'll need the `contents: read` permission. If you don't clone the repository in your setup steps, Copilot will do this for you automatically after the steps complete.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Frontend / app setup - Node.js (the whole app is now Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migrate + seed the local SQLite database so builds and tests have data.
      - name: Set up the database
        run: npm run db:setup
```

O arquivo segue o formato dos demais workflows do GitHub e contém alguns detalhes importantes:

- Há um único job, `copilot-setup-steps`, executado no GitHub Actions antes de o Copilot iniciar o trabalho no pull request.
- O gatilho `workflow_dispatch` permite executar o workflow manualmente na guia **Actions** do repositório. Isso ajuda a testar se a configuração funciona sem esperar o Copilot executá-la.

## Atribua uma tarefa de documentação

A documentação pode ficar desatualizada ou inexistente, o que reduz a produtividade e dificulta a manutenção do código. O agente de nuvem do Copilot pode criar essa documentação em segundo plano. Você revisará o trabalho em um exercício futuro.

1. Em uma nova guia do navegador, acesse o repositório em github.com.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de diálogo de nova issue.
4. Selecione **Blank issue**.
5. No campo **Title**, digite `Code lacks documentation`.
6. No campo **Description**, digite:

   ```plaintext
   Nossa organização exige comentários TSDoc nas funções e métodos quando eles forem úteis. No entanto, atualizações recentes não seguiram esse padrão. Precisamos atualizar o código existente para incluir comentários de documentação quando eles esclarecerem o comportamento.
   ```

7. Selecione **Create** para criar a issue.
8. À direita, selecione **Assign to Copilot** para abrir a caixa de diálogo de atribuição.

   ![Opção Assign to Copilot em uma issue do GitHub](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.

   ![Detalhes da atribuição da issue ao Copilot](../../../_images/ex4-assign-copilot-details.png)

10. Selecione a guia **Pull Requests**.
11. Abra o pull request (PR) recém-criado, com um título semelhante a `[WIP]: Code lacks documentation`. Se ele não aparecer na lista, aguarde um ou dois minutos e atualize a página.
12. Aguarde o Copilot criar uma lista de tarefas.

> [!NOTE]
> A lista de tarefas pode levar alguns minutos para aparecer no PR. O Copilot está criando o ambiente, executando o workflow descrito anteriormente, analisando o projeto e definindo uma abordagem.

13. Revise a lista de tarefas que o Copilot pretende executar.
14. Percorra a linha do tempo do pull request e procure uma atualização indicando que o Copilot começou a trabalhar na issue.
15. Selecione o botão **View session**.

   ![Botão View session na linha do tempo do pull request](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Talvez seja necessário atualizar a página para ver o indicador atualizado.

16. Percorra a sessão ao vivo e observe como o Copilot explora o código, analisa o estado do projeto, planeja a abordagem e cria código.

O trabalho pode levar alguns minutos. Uma das vantagens do agente de nuvem é executar tarefas de forma assíncrona para que você possa se concentrar em outras atividades. Enquanto ele trabalha, atribua outra tarefa ao agente e continue com os exercícios.

## Adicione uma seção de jogos relacionados à página de detalhes

Uma vantagem do agente de nuvem é permitir que você divida o trabalho: enquanto ele executa uma tarefa, você pode cuidar de outra. Atribua ao agente a implementação da seção de jogos relacionados.

1. Volte ao repositório em github.com.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de diálogo de nova issue.
4. Selecione **Blank issue**.
5. No campo **Title**, digite `Show related games on the game details page`.
6. No campo **Description**, digite:

   ```markdown
   Queremos ajudar as pessoas a descobrir mais jogos exibindo jogos relacionados na página de detalhes de cada jogo. A equipe de design quer explorar a experiência do usuário e fazer testes de aceitação. Requisitos:

   - Adicione um auxiliar de acesso a dados em `src/lib/` que retorne outros jogos da mesma categoria do jogo informado, excluindo o próprio jogo.
   - Exiba uma seção "Related games" na página de detalhes do jogo usando o auxiliar.
   - Trate o caso em que não há jogos relacionados.
   - Crie testes unitários para o novo auxiliar.
   - Antes de criar o PR, confirme que todos os testes foram aprovados.
   ```

7. Selecione **Create** para criar a issue.
8. À direita, selecione **Assign to Copilot** para abrir a caixa de diálogo de atribuição.

   ![Opção Assign to Copilot em uma issue do GitHub](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.

Pouco depois, um emoji de olhos aparecerá no primeiro comentário da issue para indicar que o Copilot começou a trabalhar.

![Emoji de olhos no comentário da issue indica que o Copilot está trabalhando](../../../_images/ex4-issue-eyes-emoji.png)

O agente de nuvem está trabalhando na segunda solicitação. Como ele funciona de maneira assíncrona, não é necessário acompanhar cada etapa; revise o resultado quando estiver concluído. Enquanto isso, continue para criar e usar agentes personalizados.

## Resumo e próximos passos

Neste exercício, você explorou o [agente de nuvem do GitHub Copilot][copilot-agents]. Com ele, é possível atribuir issues ao Copilot para execução assíncrona. Use-o para resolver dívida técnica, criar funcionalidades ou ajudar a migrar código entre frameworks.

Você explorou como:

- personalizar o ambiente de geração de código.
- garantir que as operações sejam realizadas com segurança.
- criar issues com escopo claro.
- atribuir issues ao Copilot.

Enquanto o agente de nuvem trabalha, você pode criar e usar agentes personalizados. O [agente de nuvem também pode usar servidores do Model Context Protocol (MCP)][cloud-agent-mcp] e recebe instruções personalizadas, que foram abordadas em lições anteriores.

## Recursos

- [Sobre o agente do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o workflow de configuração do agente de nuvem][cloud-agent-best-practices]

| [Próxima lição: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
