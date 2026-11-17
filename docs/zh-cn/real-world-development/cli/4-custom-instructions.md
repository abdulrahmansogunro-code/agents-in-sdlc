---
title: "第 4 课 - 使用自定义指令引导 Copilot"
description: "查看存储库指令，添加文档标准，并将其应用于筛选功能代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

使用生成式人工智能 (AI) 时，上下文至关重要。如果任务必须以特定方式完成，应确保 Copilot 能获取相应指导。[指令文件][instruction-files]不仅描述想要什么代码，也描述代码应如何组织。现在筛选功能已完成，你将查看 Copilot 使用的指令、添加一项文档标准，并将其应用于代码。

本课将：

- 了解存储库指令和按路径指定的指令文件如何传递给智能体。
- 更新指令文件，确保遵循编码标准。
- 观察指令文件如何影响代码。

## 场景

Tailspin Toys 团队有一套开发实践准则和要求：

- 注释应解释意图和不明显的决策，而不是复述代码。
- `db/` 和 `src/lib/` 中导出的函数应使用 TSDoc/JSDoc 说明其用途、参数和返回值；如果有可注入的 `db` 参数，也要说明。
- 可复用的 Astro 组件应说明其 `Props` 接口；相关代码更改时，注释也应保持更新。
- 保留现有格式和 lint 指南。

通过使用指令文件，可以确保 Copilot 获取正确信息，并按照这些实践执行任务。

## 指令文件

自定义指令可向 Copilot 提供上下文和偏好，帮助它理解代码风格和要求。可以指定首选编码规范、库以及注释风格。指令可以应用于整个存储库，也可以针对特定文件类型提供任务级上下文。

指令文件有两种：

- `.github/copilot-instructions.md`：每次针对该存储库提出请求时，都会发送这一个指令文件。内容应是适用于大多数请求的项目级信息。
- `.github/instructions/*.instructions.md`：为特定语言、文件类型或任务提供指导。

> [!NOTE]
> 其他指令格式及其支持情况因环境而异。依赖特定格式前，请查看[自定义指令支持参考][custom-instructions-support]。

## 查看项目中的自定义指令文件

此起始项目已包含一组指令文件。先查看现有文件，再进行更改，以了解更改的效果。

1. 返回 Codespace。
2. 在 Codespaces 编辑器（而不是终端）中打开 `.github/copilot-instructions.md`。
3. 查看文件，留意其中的项目简介和编码指导。这些指令适用于 Copilot 在此存储库中的每次交互。
4. 打开 `.github/instructions` 文件夹并查看其中的文件，包括 Astro 文件、Drizzle 数据层、测试等方面的指令。
5. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` 字段；它定义了指令适用文件的 glob。
6. 打开 `.github/instructions/drizzle.instructions.md`，查看它指向其他指令文件和项目现有文件的链接。这样可以将较大的指令集拆分成可复用的小文件，并让 Copilot 参考范例。

## 更新指令以符合团队准则

现有文件已是很好的起点，但仍缺少一项内容。更新核心 `copilot-instructions.md` 文件，确保新生成的 TypeScript 代码包含 TSDoc 注释。Copilot CLI 会在每次新建对话时加载存储库指令；保存后，退出并恢复筛选对话，让 Copilot 在保留功能上下文的同时加载新指导。

1. 在 `.github/copilot-instructions.md` 中找到 **Code formatting guidance** 部分，该部分应位于约第 35 行。
2. 在该部分末尾添加以下项目符号：

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

3. 如果筛选对话仍处于打开状态，输入 `/exit` 退出。Copilot CLI 会自动保存对话。
4. 在存储库根目录的 `game-filters-cli` 分支上恢复已保存的对话：

   ```bash
   copilot --resume
   ```

   如果系统提示，请选择筛选对话，并确认当前检出的是 `game-filters-cli` 分支。
5. 要求 Copilot 应用更新后的指导：

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

6. 输入 `/diff` 并查看已更改的 TypeScript 文件。留意新增的 TSDoc 注释，并确认这些注释准确解释了代码。

## 总结与后续步骤

你了解了 Copilot CLI 如何读取指令文件中的上下文，并将新标准应用到功能中。本课中，你：

- 了解了存储库指令和按路径指定的指令文件如何传递给智能体。
- 更新了指令文件，确保遵循编码标准。
- 观察了指令文件对代码的影响。

接下来，[自定义并运行可复用的 quality-checks 技能][next-lesson]，确保以一致的方式运行 lint 和测试。

## 资源

- [为 Copilot CLI 添加自定义指令][instruction-files]
- [自定义指令支持][custom-instructions-support]
- [创建有效自定义指令的最佳实践][instructions-best-practices]
- [Awesome Copilot：指令文件和其他资源集合][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
