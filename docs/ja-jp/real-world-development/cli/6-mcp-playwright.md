---
title: "レッスン 6 - Playwright MCP で機能を検証する"
description: "Copilot CLI の Playwright MCP を確認または設定し、ブラウザーでフィルター機能を試します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

これまでに説明したように、コードを書くこと以外にも開発には多くの作業があります。データや外部サービスを使い、Copilot が利用できる自動化機能を追加することもあります。MCP サーバーを使うと、Copilot CLI に組み込まれている機能を超えて、さらに多くのツールやサービスを利用できます。

このレッスンでは、次の内容を学習します。

- Model Context Protocol (MCP) とは何か、Copilot CLI がどのように使うかを確認します。
- Playwright MCP サーバーがまだ利用できない場合は追加します。
- エージェントにブラウザーを操作させ、フィルター機能を試します。

## シナリオ

ユニット テストやエンドツーエンド テストは重要ですが、ユーザー インターフェイス (UI) の更新を検証するには、実際に操作する必要があります。Copilot が利用者と同じように Web サイトを使えるようにし、変更が期待どおりに動作する確信を高めます。

## Model Context Protocol (MCP) とは

[Model Context Protocol (MCP)][mcp-blog-post] は、AI エージェントが外部のツールやサービスと通信するための方法です。MCP を使うと、AI エージェントは外部ツールやサービスとリアルタイムに通信し、最新情報にアクセスしたり、依頼に応じた操作を実行したりできます。

ツールやリソースには、AI エージェントと外部のツールやサービスをつなぐ MCP サーバーを介してアクセスします。各 MCP サーバーは、エージェントが利用できるツールやリソースを提供します。

よく使われている MCP サーバーには、次のものがあります。

- **[GitHub MCP Server][github-mcp]**: GitHub リポジトリ、issue、プル リクエストを管理する API を利用できます。
- **[Playwright MCP Server][playwright-mcp-server]**: Playwright によるブラウザー自動化機能を利用できます。

ほかにも多くの MCP サーバーがあります。GitHub は、エコシステム内のサーバーを見つけやすくし、貢献を促すために [MCP registry][mcp-registry] を公開しています。

> [!CAUTION]
> MCP サーバーも、プロジェクトのほかの依存関係と同様に扱ってください。使用する前にソース コードを確認し、公開元を検証して、セキュリティへの影響を検討してください。

## Playwright MCP サーバーを追加する

Copilot が利用者と同じように Web サイトを操作できるように、Playwright MCP サーバーがまだ利用できない場合は追加します。

> [!NOTE]
> Copilot CLI で Playwright MCP がすでに設定されている場合は、セットアップ手順を省略して次のセクションに進みます。

1. Codespace に戻ります。
2. Copilot CLI で次のコマンドを入力し、MCP サーバーの追加ダイアログを開きます。

   ```plaintext
   /mcp add
   ```

3. 名前に `playwright` と入力し、<kbd>Tab</kbd> を押します。
4. <kbd>Enter</kbd> を押してサーバーの種類に **STDIO** を指定し、<kbd>Tab</kbd> を押します。
5. **Command** ダイアログに次のコマンドを貼り付けます。

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. <kbd>Control</kbd>+<kbd>S</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) を押して、新しい MCP サーバーを保存します。
7. <kbd>Esc</kbd> を押して MCP ダイアログを閉じます。

## Playwright を使って Copilot に機能を試させる

先ほどは機能が期待どおりに動作することを手動で確認しました。今度は、Copilot が利用できる Playwright MCP サーバーを使って同じ確認を行います。

1. 次のプロンプトを使い、Playwright MCP サーバーで機能を検証するよう Copilot に依頼します。

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> 通常、Copilot は指示しなくても Playwright MCP サーバーを判断して使います。使うツールを明示すると、適切な方向に導き、結果の一貫性を高められます。

2. Copilot がブラウザーで機能を確認する手順を実行する様子を見ます。
3. 結果のレポートを読み、すべてが期待どおりに動作するか確認します。

Copilot はサーバーを起動し、Playwright で Web サイトを操作して、サーバーを停止した後、レポートを返します。

## まとめと次のステップ

Copilot CLI から Playwright MCP サーバーを使って、実際のブラウザーで機能を確認しました。このレッスンでは、次の内容を行いました。

- Model Context Protocol (MCP) とは何か、Copilot CLI がどのように使うかを確認しました。
- Playwright MCP サーバーがまだ利用できない場合に追加しました。
- エージェントにブラウザーを操作させ、フィルター機能を試しました。

次に、スキルとブラウザー ツールを組み合わせる[QA カスタム エージェントを作成します][next-lesson]。

## リソース

- [MCP とは何か、なぜ注目されているのか][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [Copilot CLI に MCP サーバーを追加する][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
