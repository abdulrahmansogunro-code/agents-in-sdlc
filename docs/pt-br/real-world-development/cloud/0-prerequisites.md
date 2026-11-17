---
title: "Exercício 0: Pré-requisitos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de começar os exercícios do agente de nuvem do Copilot, prepare o ambiente. Você criará uma cópia própria do repositório Tailspin Toys e iniciará um [Codespace][codespaces] para editar arquivos de instruções e revisar o trabalho do agente de nuvem.

## Configure o repositório do laboratório

Para criar uma cópia do repositório que será usado no workshop, crie uma instância a partir do [modelo][template-repository]. A nova instância conterá os arquivos necessários para os exercícios.

1. Em uma nova janela do navegador, acesse o [modelo do Tailspin Toys][tailspin-template].
2. Crie uma cópia do repositório selecionando **Use this template** na página do modelo e, em seguida, **Create a new repository**.

   ![Botão Use this template na página do repositório modelo](../../../_images/ex0-use-template.png)

3. Se você estiver participando de um evento conduzido pelo GitHub ou pela Microsoft, siga as instruções dos mentores. Caso contrário, crie o repositório em uma organização na qual você tenha acesso ao GitHub Copilot.

   ![Configurações do repositório criado a partir do modelo](../../../_images/ex0-repository-settings.png)

4. Anote o caminho do repositório criado (**organization-or-user-name/repository-name**), pois você precisará dele durante o workshop.

## Crie um Codespace

Em seguida, você usará um Codespace para os exercícios.

[GitHub Codespaces][codespaces] é um ambiente de desenvolvimento na nuvem que permite escrever, executar e depurar código diretamente no navegador. Ele oferece um ambiente de desenvolvimento integrado (IDE) com suporte a várias linguagens, extensões e ferramentas.

1. Acesse o repositório recém-criado.
2. Selecione o botão verde **Code**.

   ![Botão Code no repositório](../../../_images/ex0-code-button.png)

3. Selecione a guia **Codespaces** e, em seguida, o botão **+** para criar um Codespace.

   ![Criação de um novo Codespace](../../../_images/ex0-create-codespace.png)

A criação do Codespace pode levar alguns minutos, embora seja mais rápida do que instalar todos os serviços manualmente. Você pode usar esse tempo para explorar outros recursos do GitHub Copilot, que serão abordados em seguida.

> [!CAUTION]
> Você voltará ao Codespace em um exercício futuro. Por enquanto, mantenha-o aberto em uma guia do navegador.

> [!NOTE]
> O workshop foi criado para ser executado em um Codespace ou em um [contêiner de desenvolvimento][dev-containers] local. Ambos oferecem os pré-requisitos necessários para facilitar os exercícios. Para trabalhar localmente, abra o repositório clonado no VS Code e selecione **Reopen in Container** quando solicitado. O VS Code criará o mesmo contêiner de desenvolvimento usado pelo Codespace.

## Resumo

Parabéns, você criou uma cópia do repositório do laboratório e iniciou a criação do Codespace que usará enquanto trabalha com o agente de nuvem do Copilot.

## Próxima etapa

Adicione instruções personalizadas que o agente de nuvem seguirá. Continue para [Exercício 1: Instruções personalizadas][next-lesson].

## Recursos

- [Visão geral do GitHub Codespaces][codespaces]
- [Criar um repositório a partir de um modelo][template-repository]
- [Guia de início rápido do Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers
[next-lesson]: ../1-custom-instructions/
