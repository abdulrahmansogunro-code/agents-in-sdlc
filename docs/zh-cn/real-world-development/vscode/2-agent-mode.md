---
title: "练习 2 - 使用 Copilot 智能体模式添加功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

即使是最简单的应用更新，通常也需要修改多个文件并执行测试等操作。开发者的工作流程通常包括：查找所有相关文件、进行修改、运行测试、调试、发现遗漏的文件并继续修改……后面还有许多步骤。

Copilot 智能体模式可以帮助完成这些工作。

Copilot 智能体模式能够在集成开发环境 (IDE) 中更自主地工作。它会先探索现有项目结构，进行必要修改，运行测试等任务，并自动修复发现的问题。现在了解如何使用智能体模式为网站添加新功能。

> [!NOTE]
> 智能体模式和云智能体的名称相似，但它们适用于不同的工作方式。智能体模式在 IDE 中执行任务，适合快速反馈和交互；云智能体则像团队中的同事一样异步工作，通过议题和拉取请求与你协作。

本练习将了解：

- Copilot 智能体模式如何探索项目、识别相关文件并协调更改。
- GitHub Copilot 智能体模式如何跨用户界面 (UI) 和数据层实现新功能。
- 合并到代码库前，如何审查 Copilot 智能体模式生成的更改和测试。

## 场景

游戏列表不断扩大，希望用户能按类别和发行商筛选。上一练习已添加发行商辅助函数，现在将使用 Copilot 智能体模式完成剩余的数据层、UI 和测试工作。

## 运行 Tailspin Toys 网站

修改任何内容之前，先探索 Tailspin Toys 网站，了解现有功能。

该网站是一个以开发者为主题的桌游众筹平台。用户可以浏览游戏列表并查看游戏详情。整个网站是一个 Astro 应用，会在构建时将页面渲染为静态 HTML。页面在 frontmatter 中使用 Drizzle ORM 直接查询本地 SQLite 数据库；没有独立的后端 API 或客户端 UI 框架。可复用的数据访问辅助函数位于 `src/lib/`，交互功能由使用标准 DOM API 的小型 Astro `<script>` 实现。

### 启动网站

项目提供了 `npm run dev` 任务，用于启动单个 Astro 开发服务器。通过以下步骤在 GitHub Codespace 中运行网站：

1. 返回 Codespace。上一练习后应已切回 `main`。
2. 在 Codespace 中按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux）打开新终端。
3. 为筛选功能创建并切换到新分支：

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 运行以下命令启动网站：

   ```bash
   npm run dev
   ```

   Astro 开发服务器就绪后，会显示类似以下内容的横幅：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> 如果弹出提示询问是否在浏览器窗口中打开 `http://localhost:4321`，请选择 **x** 将其关闭。

5. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），然后在终端中选择 Astro 服务器地址 `http://localhost:4321`，打开网站。

> [!NOTE]
> 在 Codespace 中选择终端里的 localhost 链接时，会自动重定向到 `https://<your-codespace-name>-4321.app.github.dev/`。这是连接到 Codespace 中网站服务器的专用隧道。

### 探索网站

网站运行后，可以查看其主要功能：

- **主页**：显示桌游列表，包括标题、图片和描述。
- **游戏详情页**：选择游戏后会打开详情页，其中包含标题、描述、发行商和类别等信息。

## 使用 Copilot 查看待办事项

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。不同练习的模式和模型选择可能不同，相关步骤会在需要时说明。

网站的初始实现已经可以使用，但还需要添加更多功能。先查看待办事项列表。通过模板创建项目时，系统已自动创建议题；让 GitHub Copilot 显示这些议题。

1. 在 Chat 视图的智能体下拉列表中选择 **Agent**。该智能体可以自主规划并跨文件实现更改、运行终端命令和调用工具。

   ![Chat 视图中的智能体选择器截图](../../../_images/shared-chat-mode-selector.png)

2. 从可用模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 本研讨会作者并未偏好某个模型。编写研讨会时使用的是 Claude Sonnet 4.5，因此将其列入说明，以便代码建议尽可能一致。不过，大型语言模型 (LLM) 的输出具有概率性，因此建议可能与说明中的内容不同。这是正常且预期的情况。

> [!NOTE]
> 由于大型语言模型 (LLM) 具有概率性，Copilot 可能会使用不同的模型上下文协议 (MCP) 命令，但仍应能完成任务。

3. 发送以下提示，让 Copilot 显示 GitHub 存储库中的待办事项：

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. 选择 **Continue**，运行列出所有议题的命令。
5. 查看生成的议题列表。

Copilot 还会根据它认为对用户最有用的程度为议题排序。

## 查看指令文件

让智能体生成代码之前，先查看用于提供工作上下文的指令文件。项目的[用户界面 (UI) 指令文件](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)介绍了如何为网站添加功能。

1. 在 Codespace 中打开 `.github/instructions/ui.instructions.md`。
2. 查看文件中介绍的总体指导，包括：
   - 架构概述。
   - 组件设计、可测试性和无障碍原则。
   - 指向各文件类型具体指令的链接，包括：
     - Astro
     - Tailwind CSS
     - Drizzle

> [!TIP]
> 指令文件可以引用其他指令文件和项目文件。路径相对于指令文件所在位置，因此可以复用指令、拆分复杂内容，并提供示例和模板。

## 实现筛选功能

完成筛选功能至少需要更新三个部分：

- 在数据层 (`src/lib/`) 添加或完善筛选逻辑。
- 添加或更新筛选行为测试。
- 更新游戏列表页，添加筛选 UI。

此外，合并前还需要运行并通过测试。Copilot 智能体模式可以完成这些任务。

1. 可以继续使用当前 Copilot 对话，也可以选择 **New Chat** 开始新对话。
2. 选择 **Add Context**、**Instructions** 和 **ui** 指令文件。

   ![选择 UI 指令文件的示例截图](../../../_images/ex3-select-instructions-file.png)

3. 确认 Chat 视图的智能体下拉列表中仍选择了 **Agent**。

   ![Chat 视图中的智能体选择器截图](../../../_images/shared-chat-mode-selector.png)

4. 确认仍选择 **Claude Sonnet 4.5** 模型。
5. 使用以下提示，让 Copilot 根据待办事项中的相关议题实现功能：

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. 观察 Copilot 如何探索项目并查找相关文件，包括数据层辅助函数、UI 和测试，然后修改文件并运行测试。

   ![Copilot 探索项目文件的截图](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot 会执行多个步骤，例如探索项目、修改文件和运行测试。根据任务和代码库的复杂程度，这可能需要几分钟。过程中编辑器可能会出现 **Keep** 和 **Undo** 按钮。Copilot 完成后，每项更改都会显示相应按钮，因此无需在它工作时立即选择。

7. Copilot 提示运行测试时，选择 **Continue**。

   ![Copilot Chat 面板提示用户确认运行测试的对话框截图](../../../_images/ex3-agent-mode-run-tests.png)

8. 过程中可能会暂停，也可能出现测试失败。这没有关系；Copilot 会在生成代码和运行测试之间反复迭代，直至任务完成且未发现错误。

   ![Copilot 智能体模式完整 Chat 会话截图](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 检查生成的代码是否存在潜在问题。

> [!CAUTION]
> 务必审查 Copilot 或其他 AI 工具生成的代码。

10. 返回运行网站的浏览器并试用新功能。
11. 确认功能正常且已审查代码后，在 Copilot Chat 窗口中选择 **Keep**。

## 总结与后续步骤

本练习介绍了如何使用 GitHub Copilot 智能体模式为 Tailspin Toys 网站添加功能。你了解了：

- GitHub Copilot 智能体模式如何跨 UI 和数据层实现新功能。
- Copilot 智能体模式如何探索项目、识别相关文件并协调更改。
- 合并到代码库前，如何审查 Copilot 智能体模式生成的更改和测试。

接下来，[使用 Playwright MCP 服务器测试功能][next-lesson]，然后创建拉取请求。

### 拓展练习：实现分页

随着游戏列表不断增长，需要添加分页。运用本练习学到的技能，提示 Copilot 更新网站并实现分页。编写提示时可考虑：

- 遵循现有最佳实践，包括使用项目现有指令文件。
- 确定分页方式，例如是否允许用户选择每页大小，或使用固定值。
- 为 Copilot 提供实现所需的指导。
- 通过反复迭代向 Copilot 提出更改请求并提供上下文。这是正常的协作流程。

## 资源

- [Copilot ask、edit 和 agent 模式：功能和适用场景][choose-mode]
- [VS Code 中的智能体模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
