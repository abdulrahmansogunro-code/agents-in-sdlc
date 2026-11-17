---
title: "Lição 3 - Modos de agente: Plan e Autopilot"
description: "Use Plan para definir uma abordagem, Autopilot para implementar a filtragem a partir de uma issue e Interactive para revisar o resultado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Começamos adicionando uma pequena funcionalidade ao projeto. Alterações maiores exigem um processo mais robusto. O GitHub Copilot CLI foi criado para se integrar ao fluxo de trabalho da organização e ajudar a desenvolver as soluções certas da maneira certa. Nesta e nas próximas lições, você seguirá um processo típico de desenvolvimento orientado por agentes: partirá de uma issue, criará uma funcionalidade, verificará o código e o comportamento e, por fim, fará a mesclagem no projeto.

> [!NOTE]
> Você usará a mesma conversa e branch durante o fluxo de trabalho da funcionalidade. Em geral, seriam usadas branches ou PRs diferentes para os vários tipos de alteração, mas neste workshop vamos simplificar para destacar os conceitos principais.

Nesta lição, você vai:

- iniciar uma conversa do Copilot a partir de uma issue do GitHub.
- definir os requisitos no modo Plan.
- implementar a funcionalidade no modo Autopilot.
- revisar o código.
- validar manualmente a funcionalidade em um navegador encaminhado.

Ao continuar o trabalho, você atualizará as instruções do repositório, personalizará a skill existente `quality-checks`, adicionará validação com MCP, criará um agente de QA e abrirá o PR da funcionalidade.

## Cenário

O catálogo do Tailspin Toys está crescendo, e os visitantes precisam filtrar os jogos por categoria e editora. A issue do backlog descreve a funcionalidade, mas detalhes como a combinação de categorias precisam ser definidos antes da implementação. Você usará o modo Plan para decidir esses pontos e, em seguida, autorizará uma implementação com escopo definido no modo Autopilot.

## Contexto

Adicionar agentes de programação com inteligência artificial ao fluxo de desenvolvimento não muda os fundamentos — na verdade, eles se tornam ainda mais importantes. Muitos desenvolvedores seguem um fluxo parecido com este:

1. Comece por uma issue que descreva o trabalho necessário.
2. Crie um plano do que precisa ser desenvolvido.
3. Desenvolva e revise o código.
4. Execute os testes para validar o código.
5. Valide manualmente a nova funcionalidade.
6. Crie um pull request (PR).
7. Depois da revisão do código e da aprovação da integração contínua, mescle o código.

> [!NOTE]
> Os detalhes exatos variam conforme a equipe e a organização, mas a maioria dos fluxos segue alguma variação do processo acima.

Ao seguir esse processo padrão, você garante que o código gerado por IA atenda aos requisitos e passe pelas mesmas revisões que o código escrito manualmente.

## Modos de conversa

O **modo de conversa** controla o nível de autonomia do agente. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar entre os modos:

- **Interactive**: você e o agente trabalham em conjunto. O agente sugere alterações e aguarda sua orientação antes de continuar.
- **Plan**: o agente cria primeiro um plano e não pode editar os arquivos do projeto.
- **Autopilot**: o agente trabalha de forma autônoma, escrevendo código, executando testes e iterando até considerar a tarefa concluída.

Comece no modo Plan, revise o plano e depois use Autopilot para implementá-lo.

## Comece pela issue

Antes de iniciar o trabalho de filtragem, volte ao Codespace e confirme que o repositório e o terminal estão prontos.

1. Volte ao Codespace. Se estiver parado, reinicie-o antes de continuar.
2. Confirme que o PR das avaliações por estrelas foi mesclado.
3. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
4. Atualize `main` e crie uma branch para o trabalho de filtragem:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicie o Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pressione <kbd>Tab</kbd> duas vezes para abrir a guia **Issues**.
7. Pressione <kbd>A</kbd> para exibir todas as issues.
8. Use as setas para destacar a issue **Allow users to filter games by category and publisher**.
9. Pressione <kbd>C</kbd> para adicionar a issue ao prompt e voltar à guia **Session**.

O prompt agora começa com `#7` (ou um número semelhante). O caractere `#` permite incluir no contexto uma issue ou um pull request do GitHub.

## Planeje a filtragem

O planejamento permite definir a abordagem antes de delegar a implementação de uma funcionalidade ou tarefa ao Copilot. É recomendável reservar um tempo para planejar trabalhos complexos. Alterne para o modo Plan e peça ao Copilot que crie o plano.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para mudar para o modo Plan. Confirme que o indicador abaixo do prompt exibe **Plan**.
2. Depois da referência à issue adicionada na etapa anterior, digite este prompt:

   ```plaintext
   Crie um plano para implementar esta funcionalidade.
   ```

O Copilot explorará o projeto e definirá a melhor abordagem para o plano.

3. O Copilot pode fazer perguntas sobre o funcionamento da filtragem. Responda de acordo com suas preferências.
4. Quando o plano estiver concluído, pressione <kbd>Control</kbd>+<kbd>E</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para expandi-lo.
5. Percorra o plano e revise-o.
6. Peça ao Copilot que altere qualquer parte que não corresponda às suas decisões.

## Aprove o Autopilot

Com o plano escrito e revisado, implemente-o usando o modo Autopilot. Esse modo permite que o Copilot itere até considerar a tarefa concluída.

1. Selecione **Accept plan and build on autopilot (recommended)** ou a opção com rótulo semelhante na versão instalada.
2. Confirme que o indicador abaixo do prompt exibe **Autopilot**.
3. Acompanhe o Copilot enquanto ele segue o plano, gera código e executa testes.

> [!NOTE]
> A aprovação pode iniciar a implementação imediatamente, portanto revise o plano antes. Se o Copilot informar que faltam dependências ou que há conflito de porta, resolva o problema de configuração antes de considerar as verificações concluídas.

## Revise e verifique a implementação

Assim como qualquer outro código, o código gerado precisa ser revisado antes da mesclagem. Revise-o e execute o site para conferir o resultado.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para entrar no modo Interactive. Confirme que o indicador não exibe **Plan** nem **Autopilot**.
2. Digite `/diff` e inspecione a implementação da filtragem e os testes.
3. Compare o resultado com a issue e com as decisões tomadas durante o planejamento.
4. Depois da revisão, pressione <kbd>Esc</kbd> para sair da visualização do diff.
5. Revise os resultados das verificações do projeto e peça ao Copilot que corrija as falhas.

## Explore a nova funcionalidade

O código parece correto, mas será que funciona? Peça ao Copilot que inicie o aplicativo e abra o site pela porta encaminhada do Codespaces.

1. Peça ao Copilot que inicie o aplicativo:

   ```plaintext
   Inicie o aplicativo para que eu possa experimentar a filtragem no navegador. Informe a URL e mantenha o servidor em execução.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Experimente filtrar por categoria, por editora e pelas combinações definidas no plano.
4. Confirme se o comportamento de redefinição e de resultados vazios corresponde à issue e às suas decisões.
5. Volte ao Codespace e peça ao Copilot que pare o servidor de desenvolvimento iniciado.

## Resumo e próximos passos

Você usou diferentes modos de conversa para desenvolver e revisar uma funcionalidade. Nesta lição, você:

- iniciou uma conversa do Copilot a partir de uma issue do GitHub.
- definiu os requisitos no modo Plan.
- implementou a funcionalidade no modo Autopilot.
- revisou o código.
- validou manualmente a funcionalidade em um navegador encaminhado.

Em seguida, você [usará instruções personalizadas][next-lesson] para garantir que o código siga as práticas documentadas.

## Recursos

- [Autopilot no GitHub Copilot CLI][autopilot]
- [Referência de comandos do Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
