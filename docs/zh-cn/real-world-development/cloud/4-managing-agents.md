---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前几个练习中，你让 Copilot 云智能体处理了三项不同任务，改善用户体验并添加新功能。云智能体虽然可以异步自主工作，但监控这些任务仍然很重要。

可以通过多种工具管理分配给云智能体的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个控制中心，可以查看所有带有未关闭拉取请求 (PR) 的智能体任务、检查执行情况，甚至在会话进行中调整工作方向。

本课将：

- 查看智能体页面并监控云智能体任务。
- 在会话进行时提供指导，要求添加其他功能。

## 场景

将任务分配给智能体以实现高对比度模式后，团队认为也可以顺便添加浅色模式。既然正在修改网站样式并添加切换功能，就适合一并实现。你将引导智能体，让它同时添加浅色模式和高对比度模式。

## 查看 Copilot 云智能体任务

查看当前分配给 Copilot 云智能体的所有任务的状态。

1. 打开 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主区域和左侧区域中的任务列表。列表中应包含已分配给 Copilot 的任务，例如：
   - 为代码库补充文档。
   - 生成用于修改游戏的 API。
   - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，查看 Copilot 已执行的操作，例如：
   - 从存储库检出代码。
   - 为 Copilot 创建工作环境。
   - 设置模型上下文协议 (MCP) 服务器。
   - 执行完成任务所需的其他步骤。

> [!NOTE]
> 显示的具体步骤会根据 Copilot 的工作状态和执行方案而变化。

4. 另请查看右侧显示的拉取请求区域，了解 PR 和已更改的文件。

## 引导云智能体

查看当前任务后，在智能体处理高对比度模式期间，要求它同时添加浅色模式切换功能。

1. 选择与添加高对比度模式相关的会话。会话标题取决于 Copilot 使用的名称和当前工作状态。

   ![智能体控制中心中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，直到设置完成并开始执行任务。此时会出现类似下方的消息。
3. 在 **Steer active session while Copilot is working** 对话框中输入以下提示：

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![智能体页面中的云智能体任务，突出显示 Steer active session while Copilot is working 对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示。
5. 留意 Copilot 如何确认收到提示并将其加入工作流程。

## 让 Copilot 继续工作

和之前一样，Copilot 会继续处理更新后的任务。收到消息时，它会先完成当前步骤，再将新请求加入工作流程。

这可能需要几分钟，可以利用这段时间回顾目前学到和探索的内容。

## 总结与后续步骤

本课介绍了 Copilot 智能体页面，这是监控和引导 GitHub Copilot 云智能体任务的中心位置。在此控制中心可以跟踪所有正在进行和已完成的任务、审查执行情况，并调整正在进行的任务。

本课中，你：

- 查看了智能体控制中心和智能体页面，以监控云智能体任务。
- 引导正在进行的会话，要求添加其他功能。

Copilot 正在完成功能实现。接下来[迭代 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
