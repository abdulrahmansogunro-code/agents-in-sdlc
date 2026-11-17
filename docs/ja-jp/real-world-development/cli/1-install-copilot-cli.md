---
title: "レッスン 1 - GitHub Copilot CLI をインストールする"
description: "Codespace に Copilot CLI をインストールして認証し、使い方を確認して、登録済みのフィルター issue を見つけます。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

[GitHub Copilot CLI][about-copilot-cli] は、ターミナルで動作する強力なエージェント型コーディング アシスタントです。コードベースを探索し、コードを生成し、コマンドを実行し、外部ツールを利用できます。これらをすべてコマンド ラインから行えるため、作業に集中できます。まずはツールをインストールしましょう。使い慣れたツールでインストールできます。

このレッスンでは、次の内容を学習します。

- npm を使って GitHub Copilot CLI をインストールします。
- GitHub アカウントで認証します。
- ワークショップのリポジトリを信頼し、簡単な会話を試します。
- GitHub MCP サーバーを使って、フィルター機能の issue を見つけます。

## シナリオ

チームでは、増え続けるバックログに対応するため、AI エージェントを使い始めています。Copilot CLI を使うと、多くの開発者が日常的に使うターミナルで、その機能を利用できます。このレッスンでは、インストールと認証を済ませ、ワークショップの残りで使える状態にします。

## Copilot CLI をインストールする

Copilot CLI は [npm][install-cli]、WinGet、Homebrew を使ってインストールできます。GitHub Codespaces には Node.js があらかじめインストールされているため、このレッスンでは npm を使います。

1. Codespace に戻り、ターミナルを開きます。
2. Node.js がインストールされており、バージョン要件を満たしていることを確認します。

   ```bash
   node --version
   ```

   バージョン 24 以上が表示されます。

3. Copilot CLI をグローバルにインストールします。

   ```bash
   npm install -g @github/copilot
   ```

4. インストールを確認します。

   ```bash
   copilot --version
   ```

   バージョン番号が表示されます。

## GitHub で認証する

Copilot CLI を初めて起動すると、GitHub アカウントでの認証が求められます。

1. Copilot CLI を起動します。

   ```bash
   copilot
   ```

2. 認証を求められた場合は、デバイス コードの手順に従って認証し、Copilot CLI を承認します。
3. Copilot CLI に次のプロンプトが表示されます。

   ```plaintext
   Copilot can read files in this folder and, with your permission, edit them or run code and shell commands. It will remember your permissions for the rest of this session.

   Do you trust the files in this folder?
   ```

4. 表示されたパスが Tailspin Toys リポジトリであることを確認し、**Yes, and remember this folder for future sessions** を選択して「はい」と回答します。

> [!NOTE]
> Codespace では、GitHub セッションを通じてすでに認証されている場合があります。認証を求められずに Copilot CLI が起動した場合は、そのまま進めてください。

## 基本を確認する

通常のシェル プロンプトでは、コマンドは Codespace で直接実行されます。Copilot CLI の起動後は、自然言語をエージェントに送信し、スラッシュ コマンドで会話を操作します。

1. `/model` を入力し、矢印キーで **Auto** を選択して <kbd>Enter</kbd> を押します。もう一度 <kbd>Enter</kbd> を押して確定します。
2. `/help` を入力して、インストール済みのバージョンで使用できるコマンドを確認し、<kbd>Esc</kbd> を押してヘルプ画面を閉じます。
3. Copilot に簡単な質問をして、すべてが動作していることを確認します。

   ```plaintext
   What are the key files in this project?
   ```

4. 回答を読み、Copilot が回答の前にリポジトリを探索することを確認します。
5. `/mcp list` を入力し、組み込みの GitHub MCP サーバーが利用可能であることを確認します。
6. Copilot にフィルター機能の issue を見つけるよう依頼します。

   ```plaintext
   Using GitHub MCP, find the issue in this repository titled "Allow users to filter games by category and publisher." Give me its URL and a short summary. Don't change anything.
   ```

7. 表示された URL を開いて issue を読みます。最初の変更を行った後、この issue を使います。

> [!TIP]
> 通常の Copilot CLI セッションは、ターミナルで現在チェックアウトされているブランチを使います。自動的に worktree が作成されるわけではありません。各変更の前に機能用のブランチを作成します。

## ワークショップ用のショートカットを使う

通常、Copilot CLI は許可されていないツールを使う前に確認します。このワークショップでは、`--yolo` を付けて再起動します。これにより、Codespace 内で承認プロンプトが省略され、演習に集中できます。

> [!CAUTION]
> `--yolo` は、すべてのツール、パス、URL に対する自動許可（`--allow-all-tools`、`--allow-all-paths`、`--allow-all-urls`）を有効にします。Codespace や仮想マシン (VM) のような隔離された環境でのみ使い、日常の開発で既定の設定としてエイリアスにしないでください。詳細は[ツールの使用を許可または禁止する方法][allow-all-warning]を参照してください。

`--enable-all-github-mcp-tools` を指定すると、後のレッスンで issue やプル リクエストを操作するために使う、読み取りと書き込みの GitHub MCP ツールが有効になります。Codespace によってローカル コンピューターへのアクセスは制限されますが、認証済みの GitHub リソースには実際にアクセスできます。変更を公開またはマージする前にレビューしてください。

1. `/exit` で Copilot CLI を終了します。
2. リポジトリのルートから再起動します。

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. プロジェクトについてもう一つ簡単な質問をして、会話が動作することを確認してから `/exit` で終了します。

Copilot は会話を自動的に保存します。後で指示を変更したりエージェントを追加したりした後、`copilot --resume` を使うと、同じ機能用の会話とブランチに戻れます。

## まとめと次のステップ

このレッスンでは、次の内容を行いました。

- npm を使って GitHub Copilot CLI をインストールしました。
- GitHub アカウントで認証しました。
- ワークショップのリポジトリを信頼し、簡単な会話を試しました。
- 組み込みの GitHub MCP サーバーを使って、フィルター機能の issue を見つけました。

次は、ゲーム カードに星評価を表示する[最初の変更][next-lesson]に取りかかります。

## リソース

- [GitHub Copilot CLI のインストール][install-cli]
- [GitHub Copilot CLI について][about-copilot-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
