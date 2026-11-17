---
title: "练习 1 - 自定义指令（云智能体）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：Copilot 云智能体 →][next-lesson]

使用生成式人工智能 (AI) 时，上下文至关重要。如果任务必须以特定方式完成，或者 Copilot 需要了解一些背景信息，就应确保它可以访问相关上下文。[指令文件][instruction-files]可以提供这些指导，帮助 Copilot 理解不仅要做什么，还要如何完成。

本练习将：

- 查看如何通过存储库自定义指令和按路径指定的指令文件，将项目上下文、编码准则和文档标准传递给 Copilot。
- 向 `.github/copilot-instructions.md` 添加一项新的全局存储库标准。

> [!NOTE]
> 与 VS Code 和 CLI 工作流不同，本练习不会使用更改前后的提示进行演示。Copilot 云智能体会异步处理 GitHub 议题，因此难以实时并排展示指令的影响。稍后审查云智能体创建的拉取请求时，可以看到指令文件产生的效果。

## 指令文件

### 场景

Tailspin Toys 团队有一套开发实践准则和要求：

- 数据层必须始终包含单元测试。
- 用户界面 (UI) 应采用暗色模式并具有现代风格。
- 应通过 TSDoc 文档注释为代码添加文档。
- 每个文件开头都应添加说明该文件用途的注释块。

使用指令文件可以确保 Copilot 获取正确信息，并遵循这些实践完成任务。

### 自定义指令

自定义指令可向 Copilot 提供上下文和偏好，帮助它理解代码风格和要求。可以指定首选编码规范、库以及注释风格，也可以为整个存储库或特定文件类型提供项目级或任务级上下文。

指令文件有两种：

- `.github/copilot-instructions.md`：每次针对该存储库提出请求时，都会发送这一个指令文件。内容应是适用于大多数 Copilot 聊天或 CLI 请求的项目级信息，例如技术栈、项目概述、最佳实践和全局指导。
- `.github/instructions/*.instructions.md`：可针对特定任务或文件类型创建指令，例如 TypeScript、Astro、UI 组件或单元测试。

> [!NOTE]
> 在 IDE 中，指令文件仅用于 Copilot Chat 的代码生成，不适用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体在生成代码时，都会使用存储库级指令和带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> 此外，Copilot 还支持其他标准的指令文件，包括 AGENTS.md 和 CLAUDE.md。

### 管理指令文件的最佳实践

本研讨会不会全面介绍如何创建指令文件，但示例项目展示了常见做法：

- 将 `copilot-instructions.md` 用于项目级指导，例如项目说明、目录结构和全局编码标准。
- 使用 `*.instructions.md` 为文件类型（例如单元测试、Astro 组件和数据层）或特定任务提供指导。
- 使用自然语言，确保指导清晰，并提供代码应如何编写或避免如何编写的示例。

创建指令文件没有唯一的正确方式，正如使用 AI 也没有唯一方式一样。通过实践可以找到适合项目的方法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应有一组完善的指令文件。查看本项目时，可以看到其中包含 UI 更新和 Astro 等多种任务的指令。
>
> Copilot 也可以帮助生成指令文件。不同界面提供的入口有所不同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。相关课程会在需要时说明具体用法。
>
> 若要查找模板或起点，请查看 [awesome-copilot][awesome-copilot]，其中包含指令文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 查看项目中的自定义指令文件

花些时间查看存储库自带的指令文件：一个核心 `copilot-instructions.md` 文件，以及一组用于不同任务的 `*.instructions.md` 文件。可以在编辑器或 GitHub 网页界面中打开这些文件。

1. 打开 `.github/copilot-instructions.md`。
2. 查看项目简介，以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。留意 **Code standards** 下的 **GitHub Actions Workflows** 指导。这些内容适用于 Copilot 在此存储库中的所有交互。
3. 打开 `.github/instructions` 文件夹并查看其中的文件，包括 Astro 文件、Drizzle 数据层、测试等方面的指令。
4. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` 字段；它定义了相对于存储库根目录的 glob，决定指令适用于哪些文件。此处，任何 TypeScript 测试文件（例如匹配 `**/*.test.ts` 的文件）都符合条件。
5. 查看此项目针对单元测试的具体指令。
6. 最后，打开 `.github/instructions/drizzle.instructions.md` 并滚动到末尾。查看它指向其他指令文件（如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将较大的指令集拆分成可复用的小文件，并让 Copilot 参考范例。相关路径相对于指令文件所在位置，而不是存储库根目录。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分介绍了项目编码标准，但目前尚未要求为代码添加文档。接下来会添加 TSDoc 文档注释和文件注释头的规则。

## 添加新的存储库标准

接下来只需编辑一处：添加全局项目规则，要求使用 TSDoc 文档注释和文件级注释头。稍后在本工作流中分配议题时，云智能体会读取并遵循这项标准。

编辑前先创建一个分支。云智能体会读取议题目标分支中的指令，但仍建议单独提交本次更改：

1. 在 Codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

如前所述，`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。添加编码标准可以改善代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分，该部分应位于约第 27 行。查看现有编码标准；目前尚未包含代码文档规则。
3. 在现有标准下方添加以下 Markdown 内容，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 指令文件可以放在存储库级的 `.github/copilot-instructions.md` 中，为整个项目提供指导；也可以放在 `*.instructions.md` 文件中，针对特定语言、文件类型或任务提供指导。刚添加的文档注释规则属于项目级标准，因此存储库级文件是合适的位置。

## 提交、推送并合并指令更新

云智能体会读取议题目标分支中的指令。下一练习中将向 Copilot 分配议题，它会从 `main` 分支创建新分支。因此，必须先将指令更新合并到 `main`，云智能体才能读取。

1. 暂存并提交更改：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 合并到 `main` 的拉取请求并完成合并。之后，云智能体处理下一练习中的议题时就会读取这些指令。

> [!TIP]
> 如果希望在本研讨会中直接使用 `main`，可以跳过分支操作，直接提交到 `main`。此处创建分支是为了模拟真实项目中的处理方式。

## 总结与后续步骤

你查看了 Copilot 如何读取项目指令文件中的上下文，并在 `.github/copilot-instructions.md` 中添加了全局存储库标准。之后的练习会展示云智能体创建的拉取请求 (PR) 如何遵循此标准。

接下来，[将第一个议题分配给 Copilot 云智能体][next-lesson]。

## 资源

- [GitHub Copilot 的自定义指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot：指令文件和其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
