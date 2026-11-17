---
title: "练习 1 - 自定义指令（VS Code）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：智能体模式 →][next-lesson]

使用生成式人工智能 (AI) 时，上下文至关重要。如果任务必须以特定方式完成，或者 Copilot 需要了解一些背景信息，就应确保它可以访问相关上下文。[指令文件][instruction-files]是提供代码生成指导的重要方式。

本练习将：

- 查看如何通过存储库自定义指令和按路径指定的指令文件，将项目上下文、编码准则和文档标准传递给 Copilot。
- 使用当前指令生成筛选功能的第一个数据切片（发行商辅助函数）。
- 向 `.github/copilot-instructions.md` 添加一项新的全局存储库标准。
- 再次运行相同提示，观察生成的代码如何遵循新标准。
- 将指令更新和筛选功能代码提交到 `main`，供下一练习使用。

> [!CAUTION]
> 生成的代码可能不完全遵循设置的标准，因为 Copilot 的输出具有概率性。本练习的重点是观察更新指令前后行为的趋势，而不是让输出逐字一致。

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

- `.github/copilot-instructions.md`：每次针对该存储库提出请求时，都会发送这一个指令文件。内容应是适用于大多数请求的项目级信息，例如技术栈、项目概述、最佳实践和全局指导。
- `.github/instructions/*.instructions.md`：可针对特定任务或文件类型创建指令，例如 TypeScript、Astro、UI 组件或单元测试。

> [!NOTE]
> 在 IDE 中，指令文件仅用于 Copilot Chat 的代码生成，不适用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体在生成代码时，都会使用存储库级指令和带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> Copilot 还支持其他标准的指令文件，包括 AGENTS.md 和 CLAUDE.md。

### 管理指令文件的最佳实践

本练习不会全面介绍如何创建指令文件，但示例项目展示了常见做法：

- 将 `copilot-instructions.md` 用于项目级指导，例如项目说明、目录结构和全局编码标准。
- 使用 `*.instructions.md` 为文件类型（例如单元测试、Astro 组件和数据层）或特定任务提供指导。
- 使用自然语言，确保指导清晰，并提供代码应如何编写或避免如何编写的示例。

创建指令文件没有唯一的正确方式，正如使用 AI 也没有唯一方式一样。通过实践可以找到适合项目的方法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应有一组完善的指令文件。查看本项目时，可以看到其中包含 UI 更新和 Astro 等多种任务的指令。
>
> Copilot 也可以帮助生成指令文件。不同界面提供的入口有所不同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。相关练习会在需要时说明具体用法。
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
4. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` 字段；它定义了相对于存储库根目录的 glob。此处，任何 TypeScript 测试文件（例如匹配 `**/*.test.ts` 的文件）都符合条件。
5. 查看此项目针对单元测试的具体指令。
6. 最后，打开 `.github/instructions/drizzle.instructions.md` 并滚动到末尾。查看它指向其他指令文件（如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将较大的指令集拆分成可复用的小文件，并让 Copilot 参考范例。相关路径相对于指令文件所在位置，而不是存储库根目录。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分介绍了项目编码标准，但目前尚未要求为代码添加文档。接下来会添加 TSDoc 文档注释和文件注释头的规则。

## 为更改创建分支

遵循最佳实践，为本次更改创建分支。

1. 返回上一练习中使用的 Codespace。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新终端。
3. 创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions
   ```

## 更新指令前先使用 Copilot Chat

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。不同练习的模式和模型选择可能不同，相关步骤会在需要时说明。

先在当前指令文件下发送提示，然后更新指令并再次发送相同提示，以查看自定义指令的效果。

1. 关闭之前练习中打开的编辑器标签页，让 Copilot 只获取需要的上下文。
2. 打开 `src/lib/publishers.ts`，让 Copilot 知道辅助函数应放在哪里。
3. 在 Chat 视图的智能体下拉列表中选择 **Agent**，以便 Copilot 修改文件。

   ![Chat 视图中的智能体选择器截图](../../../_images/shared-chat-mode-selector.png)

4. 发送以下提示：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot 会探索项目并应用代码更改，通常会同时修改辅助函数文件和测试。
6. 留意生成的辅助函数是带类型的函数，其第一个参数为 `db` 客户端，并返回带类型的发行商数组。这来自 `.github/instructions/drizzle.instructions.md` 中适用于 `src/lib/*.ts` 的数据层规范。
7. 注意生成的代码**缺少** TSDoc 文档注释和文件级注释头。

> [!CAUTION]
> Copilot 具有概率性，因此它有时会自行添加文档注释。这也没问题；本练习要观察的是更新指令后的一致性改进。

## 添加新的存储库标准

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

## 重新发送提示并观察变化

使用更新后的指令再次发送相同提示，查看 Copilot 是否遵循新标准。

1. 返回 Copilot Chat 并选择 **New Chat**，清除当前对话上下文。
2. 再次打开 `src/lib/publishers.ts`，让 Copilot 聚焦正确的文件。
3. 发送之前完全相同的提示：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 留意生成的文件现在会以类似以下注释块开头：

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. 留意生成的函数现在包含类似以下 TSDoc 注释：

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

你已引导 Copilot 遵循新的项目标准，并将其应用于真实代码。下一练习会继续使用这段代码。

## 提交指令并推送分支

指令文件和其他存储库文件一样，需要通过源代码管理。提交并推送此分支。

1. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新终端。
2. 在终端中运行以下命令，确认指令和辅助函数更改均已存在：

   ```bash
   git status
   ```

3. 暂存并提交指令更新，以及 Copilot 为辅助函数基础所做的所有更改：

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # 如果 git status 显示其他支持性更改（例如测试），也要添加这些文件。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. 将分支推送到存储库：

   ```bash
   git push -u origin custom-instructions
   ```

## 创建并合并拉取请求

分支推送完成后，创建拉取请求 (PR) 并将其关联到待办事项中的文档标准议题。Copilot 可以使用已连接到项目的 GitHub 工具查找议题、创建用于关闭该议题的 PR，然后合并 PR。

> [!NOTE]
> 这是第一次让 Copilot 代表你操作 GitHub。项目模板已配置 GitHub 工具，无需额外设置。Copilot 首次使用 GitHub 工具时，VS Code 可能会提示登录 GitHub。按照提示完成授权。后续练习会介绍这种连接如何通过模型上下文协议 (MCP) 实现。

1. 在 Codespace 中打开 Copilot Chat。
2. 按 <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd>（Windows/Linux）打开 Copilot Chat 视图，并确认智能体选择器中已选择 **Agent**。
3. 要求 Copilot 查找与更新指令文件相关的议题，并从当前分支创建 PR；PR 描述中应同时说明指令更新和新的发行商辅助函数基础：

   ```text
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot 会查找议题并创建 PR。
5. Copilot 请求代表你执行 GitHub 操作时，检查相应操作，并在适当时选择 **Allow**。
6. PR 创建后，使用以下提示要求 Copilot 合并 PR 并将分支切回 `main`：

   ```text
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. Copilot 请求代表你执行 GitHub 操作和 shell 命令时，检查相应操作，并在适当时选择 **Allow**。

现在已经在 GitHub Copilot 的帮助下创建并合并了拉取请求。

## 总结与后续步骤

你了解了 Copilot 如何读取项目指令文件中的上下文，并在 VS Code 中使用 Copilot Chat：

- 发送代码生成提示，并观察 Copilot 如何根据现有指令生成代码。
- 在 `.github/copilot-instructions.md` 中添加全局存储库标准。
- 再次发送相同提示，观察生成的代码如何遵循新标准。
- 将指令更新和辅助函数基础提交到 `main`，供下一练习继续使用。

接下来，在[智能体模式][next-lesson]中运用这些指令，让 Copilot 跨代码库添加新功能。

## 资源

- [GitHub Copilot 自定义指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [GitHub Copilot 个人自定义指令][personal-instructions]
- [Awesome Copilot：指令文件和其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
