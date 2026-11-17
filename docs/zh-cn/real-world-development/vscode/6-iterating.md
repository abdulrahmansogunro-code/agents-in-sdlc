---
title: "练习 6 - 迭代 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
next: false
---

| [← 上一课：监控和管理智能体][previous-lesson] |
| :-- |

## 审查工作

在本实验中，你使用 GitHub Copilot 完成了多项任务，以改善用户体验：使用智能体模式跨客户端和服务器实现筛选功能，使用 Playwright MCP 服务器在浏览器中手动测试，然后使用自定义智能体实现高对比度和浅色模式切换，并在会话进行时引导智能体扩展工作。现在将本地更改发布，并按照团队常规流程进行审查。

### 场景

生成式人工智能 (AI) 不会改变软件设计和 DevOps 的基本原则。Copilot 生成的内容仍需经过正式审查。接下来将 Codespace 中的无障碍更改推送到分支、创建拉取请求，并在让团队其他成员参与前仔细检查差异。

## 发布无障碍功能

你在[练习 4][exercise-4]和[练习 5][exercise-5]中通过无障碍自定义智能体实现的高对比度和浅色模式切换，已作为已提交的更改保存在 Codespace 中。将它们推送到分支并创建拉取请求，供团队其他成员审查。

1. 返回 Codespace。
2. 在 VS Code 中打开 **Source Control** 视图。
3. 确认无障碍更改已提交。如果练习 5 后仍有未提交更改，请暂存并提交，使用清晰的提交消息，例如 `Add high-contrast and light-mode toggles`。
4. 选择 **Publish Branch** 发布分支，也可以使用 **...** 菜单 → **Push**。
5. VS Code 会提供在 github.com 上打开新分支的选项。接受提示，或手动打开存储库并选择分支横幅中的 **Compare & pull request**。
6. 设置清晰的标题（例如 `Add high-contrast and light-mode toggles`）和简短描述，说明更改内容及原因。
7. 选择 **Create pull request**。
8. 拉取请求 (PR) 创建后，选择 **Files changed** 选项卡，全面审查更改。重点查看：
   - 用于切换模式的用户界面 (UI) 组件。
   - 使用本地存储保存用户偏好。
   - 高对比度和浅色模式的 CSS 或样式更改。
   - 无障碍属性（可访问的富互联网应用程序 (ARIA) 标签、键盘导航等）。
   - 管理模式切换的 JavaScript/TypeScript 代码。

9. 返回 **Conversation** 选项卡。
10. 如果工作流正在等待批准，请选择 **Approve and run workflows**。

    ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

11. 等待工作流完成。正常情况下，所有工作流都会通过。

> [!TIP]
> 想要第二种意见来审查无障碍功能吗？可以在 PR 评论中提及 `@copilot`，并提出“审查此 PR 是否存在其他 WCAG 问题”或“建议改进键盘导航”等请求。Copilot 会启动新会话处理评论。

## 可选练习：继续在本地探索

在 IDE 中与智能体迭代是一项需要反复练习的技能。可以从 VS Code 启动以下后续会话：

- 在游戏详情页添加支持者意向表单。
- 为游戏列表页实现分页。
- 为 `src/lib/` 中的数据访问辅助函数添加输入验证和错误处理。
- 扩展无障碍智能体的范围，例如审查整个网站中的键盘焦点顺序。

## 总结

恭喜，已完成 VS Code 工作流。本系列课程中，你：

- **使用 Playwright MCP 手动测试了功能。** 添加 Playwright MCP 服务器，并让 Copilot 在创建拉取请求前驱动浏览器验证筛选功能。
- **使用智能体模式协调多层更改。** 在一次会话中添加筛选功能，涉及客户端、服务器和测试。
- **使用了自定义智能体。** 从智能体选择器中选择无障碍自定义智能体，并观察它如何根据存储库要求实现高对比度模式。
- **管理并引导了智能体会话。** 内联审查建议的更改、接受所需内容，并发送后续提示添加浅色模式。
- **通过拉取请求完成了整个流程。** 发布本地工作，并按照团队的方式全面审查更改。

## 回顾与后续步骤

必需的 VS Code 工作流到此结束，可以在此完成研讨会。

如果想进一步了解 Copilot 智能体功能，其他工作流会从不同界面探索相关场景：

- 💻 **[CLI 工作流](../../cli/)**：从终端交付两个经过审查的更改，并使用 Plan 和 Autopilot 模式、技能、自定义 QA 智能体、Playwright MCP、Agent Merge 和上下文感知交接。
- ☁️ **[云智能体工作流](../../cloud/)**：将议题分配给云智能体、通过智能体页面监控会话，并异步迭代拉取请求。

也可以继续扩展已完成的工作。[awesome-copilot][awesome-copilot]提供了更多可用于项目的指令文件、自定义智能体和技能。

若要进行可选扩展，[可选：集成 Foundry][exercise-7]会使用 VS Code 和 Microsoft Foundry Toolkit 准备模型、部署 Backer Concierge 并将其连接到网站。

## 资源

- [GitHub Copilot][github-copilot]
- [VS Code 中的 Copilot Chat][copilot-chat-vscode]
- [使用智能体模式][agent-mode]

---

| [← 上一课：监控和管理智能体][previous-lesson] |
|:--|

[previous-lesson]: ../5-managing-agents/
[exercise-4]: ../4-custom-agents/
[exercise-5]: ../5-managing-agents/
[exercise-7]: ../7-foundry-toolkit/
[github-copilot]: https://github.com/features/copilot
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
[awesome-copilot]: https://github.com/github/awesome-copilot
