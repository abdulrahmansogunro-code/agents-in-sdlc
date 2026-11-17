---
title: "レッスン 9 - GitHub Copilot CLI のスラッシュ コマンド"
description: "コンテキスト管理、モデル選択、セッション共有、cloud agent への任意の委任に使うスラッシュ コマンドを確認します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

多くの CLI ツールと同様に、GitHub Copilot CLI にも操作に使うスラッシュ コマンドが用意されています。これらのコマンドを使うと、高度な機能、内部情報、追加の設定オプションを利用できます。これまでに `/diff`、`/mcp`、`/skills`、`/agent`、`/pr` などのコマンドを使いました。ここでは、ほかの便利なコマンドをいくつか確認します。

このレッスンでは、次の内容を学習します。

- `/context` と `/compact` を使い、Copilot が会話のコンテキストを管理する方法を確認します。
- `/model` を使い、利用可能なモデルを確認します。
- `/share` でセッションをエクスポートまたは共有する方法を学びます。
- 並列作業、worktree、cloud agent への委任に使う任意のコマンドを確認します。

## シナリオ

CLI の主なワークフローを終えました。ここでは、コンテキストの管理、モデルの切り替え、セッションの共有、[Copilot cloud agent][about-cloud-agent]への任意の作業委任など、追加機能を確認します。

## Copilot CLI のコンテキストを確認する

大規模または複雑なタスクに取り組むと、モデルの最大コンテキスト ウィンドウに達することがあります。Copilot CLI は必要に応じて会話を自動的に圧縮します。また、スラッシュ コマンドを使って自分で確認したり圧縮したりできます。

1. Codespace に戻ります。Copilot CLI をまだ起動していない場合は、リポジトリのルートから起動します。
2. 次のコマンドを入力します。

   ```plaintext
   /context
   ```

3. モデル、現在のトークン使用量、システム指示、ツール、メッセージ、空き領域にコンテキストがどのように分けられているかを確認します。
4. 会話を圧縮します。

   ```plaintext
   /compact
   ```

5. もう一度 `/context` を入力し、結果を比較します。会話が短い場合は、大きな違いが見られないことがあります。

> [!NOTE]
> コンテキスト ウィンドウが埋まると、Copilot CLI は自動的にコンテキストを圧縮します。自分でタイミングを選ぶ場合は `/compact` を使います。関係のない別のタスクに切り替えるために新しい会話を始める場合は、代わりに `/clear` または `/new` を使います。

## モデルを選ぶ

モデルごとに得意分野が異なり、開発者によって好みも異なります。Copilot CLI では、利用可能なモデルを一覧表示し、使うモデルを選択できます。

1. 次のコマンドを入力します。

   ```plaintext
   /model
   ```

2. 利用可能なモデルと使用状況の情報を確認します。
3. 現在のモデルを使い続けるか、別のモデルを選択するか、<kbd>Esc</kbd> を押して一覧を閉じます。

## セッションを共有する

チームで協力し、知識を共有することで、AI ツールの活用方法を改善できます。`/share` コマンドを使うと、セッションを Markdown または HTML ファイルにエクスポートしたり、共有リンクを作成したり、GitHub gist を公開したりできます。

1. `/help` を入力し、インストール済みのバージョンで利用できる `/share` オプションを確認します。
2. セッションを共有する場合は、目的に合った出力先を選択します。たとえば `/share file` を使うと、Markdown ファイルとしてローカルにエクスポートできます。
3. エクスポートした内容を誰かに送信したり公開したりする前に確認します。セッションのエクスポートには、プロンプト、応答、プロジェクトの詳細が含まれる場合があります。

リンクや gist の公開は任意です。チームが共有を意図していないリポジトリや会話の内容は公開しないでください。

## オプション: 作業の並列化や委任

ワークショップの主要な内容は完了しました。Copilot CLI には、大規模なタスク向けのコマンドもあります。

- `/fleet` は、独立したサブタスクをサブエージェントに分配して並列に実行できます。
- `/worktree` は、別のタスク用に分離された Git worktree を作成できます。
- `/delegate` は、タスクを Copilot cloud agent に送信できます。cloud agent は非同期に作業し、プル リクエストを作成する場合があります。

これらのコマンドを使うと、新しい worktree やリモートの作業が作成される場合があるため、任意の機能としています。試すときは、範囲を明確にした新しいタスクから始め、通常のワークフローで結果をレビューしてください。非同期エージェントの作業について詳しく知りたい場合は、[cloud agent ワークショップ][cloud-workshop]に進んでください。

## まとめと次のステップ

Copilot CLI のスラッシュ コマンドを使うと、設定を変更し、セッションを共有し、内部の処理を確認できます。このレッスンでは、次の内容を行いました。

- `/context` と `/compact` を使い、Copilot が会話のコンテキストを管理する方法を確認しました。
- `/model` を使い、利用可能なモデルを確認しました。
- `/share` でセッションをエクスポートまたは共有する方法を学びました。
- 並列作業、worktree、cloud agent への委任に使う任意のコマンドを確認しました。

Copilot CLI には、ほかにも多くのスラッシュ コマンドがあります。次に、[学んだことと、今後のステップ][next-lesson]を振り返りましょう。

## リソース

- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI のコンテキスト管理][context-management]
- [Copilot cloud agent について][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
