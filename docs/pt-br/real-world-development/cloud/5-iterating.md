---
title: "Exercício 5: Iterar sobre o trabalho do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

## Revise o trabalho

Durante este workshop, você trabalhou com o GitHub Copilot em tarefas para melhorar a experiência do usuário e adicionar funcionalidades. Você pediu ao Copilot que documentasse o código, criasse uma funcionalidade de jogos relacionados para a equipe de design avaliar e implementasse recursos de acessibilidade, incluindo controles de alto contraste e modo claro. Agora, revise o código e, se necessário, dê feedback ao Copilot.

### Cenário

Os fundamentos do desenvolvimento de software e das práticas de desenvolvimento e operações (DevOps) não mudam com a inteligência artificial generativa. Sempre revise o código gerado e siga o processo normal de DevOps. Antes de habilitar a revisão da equipe, examine as sugestões do GitHub Copilot para a documentação, os jogos relacionados e os recursos de acessibilidade.

## Segurança e o agente de nuvem do GitHub Copilot

Como o agente de nuvem trabalha de forma assíncrona e sem supervisão direta, há restrições de segurança:

- O Copilot tem acesso de leitura ao repositório e acesso de gravação **somente** à branch que usará para o código.
- O agente de nuvem é executado no GitHub Actions em um ambiente separado e temporário.
- Um ser humano precisa aprovar a execução de workflows do GitHub Actions.
- [O acesso a recursos externos é limitado por padrão][agent-firewall], inclusive a servidores MCP.

## Revise a documentação gerada

Comece pelo primeiro pull request (PR) criado pelo agente de nuvem do GitHub Copilot: o PR que adiciona documentação ao código. Use a interface padrão de PR do GitHub.com.

> [!NOTE]
> Ao abrir o PR, você poderá ver um aviso de que o Copilot foi bloqueado por um firewall. Isso é **esperado**, pois o acesso do Copilot a recursos externos, incluindo servidores MCP, é limitado por padrão. Se quiser, você pode [personalizar ou desabilitar o firewall do agente de nuvem][agent-firewall].

1. Acesse o repositório no GitHub.com.
2. Selecione **Pull Requests** para abrir a lista de pull requests.
3. Abra o PR com um título semelhante a **Add missing documentation**.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando, o PR terá a indicação **[WIP]**. Aguarde a conclusão do trabalho; isso pode levar alguns minutos.

4. Quando o PR estiver pronto, selecione a guia **Files changed** e revise as alterações.

   ![Guia Files changed de um pull request](../../../_images/shared-pr-files-changed.png)

5. Examine o código atualizado, que inclui comentários TypeScript Documentation (TSDoc) e outra documentação. As alterações exatas podem variar. Procure comentários TSDoc, convenções de TypeScript e cabeçalhos de comentários, orientações provenientes dos arquivos de instruções personalizados que você examinou no Exercício 2.
6. Quando terminar a revisão, volte à guia **Conversation** e role a página para baixo.
7. Procure um indicador de que alguns workflows estão aguardando aprovação.
8. Se houver workflows aguardando aprovação, selecione **Approve and run workflows**.

   ![Botão Approve and run workflows no pull request](../../../_images/shared-approve-workflows.png)

9. Os workflows serão adicionados à seção de verificações do PR. Confirme se as verificações do projeto para o aplicativo Astro foram aprovadas. Isso pode levar alguns minutos.

## Peça alterações ao GitHub Copilot

Você também pode mencionar o Copilot em comentários do pull request ou em comentários associados a linhas do código. O Copilot lê esses comentários e inicia outra sessão para tratar das solicitações. Como os resultados não são determinísticos, não há um prompt único. Você pode pedir, por exemplo, para:

- adicionar cabeçalhos de comentários no início dos arquivos de código com uma descrição breve.
- adicionar comentários TSDoc a arquivos TypeScript e Astro.
- criar um README que descreva a estrutura do aplicativo Astro.

1. Adicione um comentário solicitando uma alteração na documentação gerada e mencione **@copilot**. Use uma das ideias acima ou outra sugestão.
2. Selecione **View Session** para acompanhar o trabalho do Copilot. Observe que ele inicia uma nova sessão para implementar as alterações.
3. Selecione **Back to pull request** para voltar ao pull request.

   ![Opção para voltar ao pull request](../../../_images/ex7-back-to-pr.png)
4. Quando o Copilot terminar, confira se um novo commit foi adicionado ao PR.
5. Selecione **Files changed** e revise as alterações.

Continue iterando até que o resultado esteja satisfatório. Depois, marque o PR como pronto para revisão e mescle-o na branch principal.

![Opção para marcar um pull request como pronto para revisão](../../../_images/ex7-ready-for-review.png)

## Revise a funcionalidade de jogos relacionados

Agora, revise o PR criado pelo Copilot para mostrar jogos relacionados na página de detalhes de cada jogo.

1. Acesse o repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Abra o PR com um título semelhante a **Show related games on the game details page**.
4. Selecione **Files changed** e revise o código gerado.
5. Quando terminar a revisão, volte à guia **Conversation** e role a página para baixo.
6. Procure um indicador de que há workflows aguardando aprovação.
7. Se houver workflows aguardando aprovação, selecione **Approve and run workflows**.

   ![Botão Approve and run workflows no pull request](../../../_images/shared-approve-workflows.png)

8. Confirme se as verificações do projeto para o aplicativo Astro foram aprovadas. Isso pode levar alguns minutos.
9. **Opcional:** faça um teste manual da funcionalidade no Codespace. Abra o terminal e execute estes comandos, substituindo `<branch-name>` pelo nome da branch criada pelo Copilot, por exemplo, `copilot/fix-8`:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

O Copilot criou a funcionalidade de jogos relacionados. Assim como no outro PR, você pode pedir alterações por meio de um novo comentário na guia **Conversation**. Por exemplo, solicite um limite diferente de jogos relacionados ou cabeçalhos de comentários e documentação TSDoc. Observe que esse trabalho foi atribuído antes da atualização das instruções personalizadas.

## Revise os recursos de acessibilidade

Por fim, revise os recursos de acessibilidade implementados pelo agente personalizado. Esse PR deve incluir o modo de alto contraste solicitado no Exercício 3 e o modo claro solicitado no painel central de agentes do Exercício 4.

1. Acesse o repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Abra o PR com um título semelhante a **Add high contrast mode to website**.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando, o PR terá a indicação **[WIP]**. Aguarde a conclusão do trabalho, que pode levar alguns minutos.

4. Selecione **Files changed** e revise o código gerado.
5. Examine a implementação, principalmente:
   - os controles da interface para alternar entre os modos.
   - o uso do local storage para salvar as preferências.
   - as alterações de folhas de estilo em cascata (CSS) ou de estilo dos modos de alto contraste e claro.
   - os recursos de acessibilidade, como rótulos Accessible Rich Internet Applications (ARIA) e navegação por teclado.
   - o código JavaScript/TypeScript que gerencia a alternância entre modos.

6. Quando terminar a revisão, volte à guia **Conversation** e role a página para baixo.
7. Procure um indicador de que há workflows aguardando aprovação.
8. Se houver workflows aguardando aprovação, selecione **Approve and run workflows**.

   ![Botão Approve and run workflows no pull request](../../../_images/shared-approve-workflows.png)

9. Confirme se as verificações do projeto para o aplicativo Astro foram aprovadas. Isso pode levar alguns minutos.
10. **Opcional:** teste manualmente os recursos de acessibilidade no Codespace. Abra o terminal e execute os comandos a seguir, substituindo `<branch-name>` pelo nome da branch criada pelo Copilot:

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Inicie o aplicativo e teste os controles de alto contraste e modo claro no navegador. Confirme se as configurações continuam aplicadas após recarregar a página.

O agente personalizado de acessibilidade orientou o Copilot na implementação desses recursos. Se encontrar problemas ou oportunidades de melhoria de acessibilidade, mencione **@copilot** em um comentário para solicitar alterações, como nos PRs anteriores.

## Exercício opcional: continue delegando

O agente de nuvem é útil para tarefas reais do backlog que você pode delegar enquanto trabalha em outras atividades. Para praticar, crie algumas issues no repositório e atribua-as ao Copilot. Por exemplo:

- criar um formulário de interesse de apoiadores na página de detalhes do jogo.
- implementar paginação na lista de jogos.
- adicionar validação de entrada e tratamento de erros aos auxiliares de acesso a dados.

## Resumo

Você concluiu o percurso do agente de nuvem. Nestas lições, você:

- **Inspecionou os arquivos de instruções personalizados do repositório** para ver como influenciam o trabalho do agente de nuvem.
- **Atribuiu issues ao agente de nuvem do Copilot** e acompanhou a configuração do ambiente, o planejamento e a execução assíncrona.
- **Criou e usou um agente personalizado** de acessibilidade para adicionar controles de alto contraste e modo claro.
- **Usou a página de agentes do Copilot como painel central** para acompanhar e orientar a sessão de acessibilidade em andamento.
- **Revisou e ajustou os pull requests do agente de nuvem**, mencionando `@copilot` para solicitar alterações e aprovando workflows.

## Revisão e próximos passos

Você concluiu o percurso do agente de nuvem. Os outros ambientes complementam o que você praticou:

- 🖥️ **[Percurso do VS Code](../../vscode/)** — explore o modo de agente do Copilot Chat e a integração com MCP diretamente no IDE.
- 💻 **[Percurso do CLI](../../cli/)** — entregue duas alterações revisadas pelo terminal com os modos Plan e Autopilot, skills de agente, um agente personalizado de QA, Playwright MCP, Agent Merge e uma ponte opcional `/delegate` para o agente de nuvem.

No seu repositório, experimente estas ideias:

- atribua ao agente de nuvem uma issue de refatoração ou de cobertura de testes.
- crie um agente personalizado para outro domínio.
- configure `copilot-setup-steps.yml` para outra pilha de tecnologias.

## Recursos

- [GitHub Copilot][github-copilot]
- [Sobre agentes do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o workflow de configuração do agente de nuvem][cloud-agent-best-practices]
- [Configurar o firewall do agente de nuvem do Copilot][agent-firewall]

---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
