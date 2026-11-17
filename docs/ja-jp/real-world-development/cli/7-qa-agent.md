---
title: "レッスン 7 - QA エージェントを作成して使う"
description: "issue の要件、quality-checks スキル、Playwright MCP を組み合わせる QA カスタム エージェントを作成します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

`quality-checks` スキルで自動チェックを実行し、Playwright MCP でブラウザー上のフィルター機能を確認しました。次に、明確な品質保証 (QA) プロセスを持つカスタム エージェントに、これらの機能をまとめます。

このレッスンでは、次の内容を学習します。

- カスタム エージェントが指示、スキル、MCP ツールを使う方法を確認します。
- 再利用可能な QA プロファイルを作成して調べます。
- QA エージェントを選択し、フィルター機能の issue に照らして結果をレビューします。

## シナリオ

Tailspin Toys では、プル リクエスト (PR) を作成する前に、要件、コード品質、自動チェック、テスト カバレッジ、ブラウザーでの動作を一貫してレビューしたいと考えています。カスタム エージェントを使うと、QA の手順を調整し、再利用可能なレポートを作成できます。

## カスタム エージェントとは

カスタム エージェントは、Markdown プロファイルで定義する Copilot の専門的な役割です。プロファイルには、エージェントの目的、指示、利用できるツールを記載します。このワークショップでは `.github/agents/qa.agent.md` に QA の役割を定義し、Copilot CLI で選択します。

これまでに使ったカスタマイズには、それぞれ異なる役割があります。リポジトリの指示はチームの標準を説明し、`quality-checks` スキルは繰り返し実行するチェックをまとめ、Playwright MCP はブラウザー操作ツールを提供します。QA プロファイルは、これらの機能をどう使って要件を評価し、結果を報告するかを Copilot に伝えます。既存の機能を置き換えるものではなく、別の会話も必要ありません。

## QA プロファイルを作成する

機能の PR を開く前に、再利用可能な QA プロファイルを Copilot に作成させます。プロファイルには QA が行うチェックと、守るべき範囲の両方を定義します。

1. Codespace に戻り、フィルター機能の会話が Interactive モードであることを確認します。
2. 既定のエージェントに、次のプロンプトでカスタム エージェントを作成するよう依頼します。

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## プロファイルを確認する

新しいエージェントを使う前に、意図した QA の流れと制約がプロファイルに反映されているか確認します。これにより、検証だけを依頼したのに不完全または範囲が広すぎるエージェントが機能を変更する事態を防げます。

1. `/diff` を入力し、`.github/agents/qa.agent.md` を開きます。
2. フロントマターを読みます。`description` は必須です。`name` は任意ですが、含めるとエージェントの表示名が明確になります。
3. プロファイルの指示を読み、QA が要件から始め、リポジトリの指示に従い、`quality-checks` スキルを実行して、Playwright MCP を使うことを確認します。
4. QA が根拠を示して報告し、実装コードを変更する前に確認を求め、変更のコミットやプル リクエストの作成をしないことを確認します。
5. これらの役割や制約が抜けている場合は、続ける前に既定のエージェントに修正を依頼します。

## issue に対して QA を実行する

Copilot CLI は会話の開始時にプロジェクトのエージェントを読み込みます。プロファイルの作成後に同じフィルター機能の会話を再開し、QA を選択すると、issue と計画時の決定を引き続き利用できます。

1. 次のプロンプトを使ってエージェントを有効にします。

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 作成したばかりのエージェントは、利用可能なエージェントの一覧にまだ表示されない場合があります。エージェントは存在しており、上記のコマンドで有効にできます。

2. 次のプロンプトで、QA エージェントに機能をレビューするよう依頼します。

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA エージェントが作業を開始します。
4. 作業が完了したら、レポートを読みます。

## まとめと次のステップ

再利用可能な専門的役割をワークフローに加え、その結果をレビューしました。このレッスンでは、次の内容を行いました。

- カスタム エージェントが指示、スキル、MCP ツールを使う方法を確認しました。
- 再利用可能な QA プロファイルを作成して調べました。
- QA エージェントを選択し、フィルター機能の issue に照らして結果をレビューしました。

実装、スキルの更新、QA プロファイル、テスト、検証レポートの準備ができました。次に、これらを[機能の PR にまとめ、Agent Merge を使います][next-lesson]。

## リソース

- [Copilot CLI 用のカスタム エージェントを作成する][create-agents]
- [カスタム エージェントの設定][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
