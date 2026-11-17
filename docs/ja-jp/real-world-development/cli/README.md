---
slug: ja-jp/real-world-development/cli
title: "GitHub Copilot CLI"
description: "Copilot CLI のモード、カスタマイズ、MCP ツール、プル リクエストの自動化を学びながら、Tailspin Toys に 2 つの変更を加え、検証して公開します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

**[GitHub Copilot CLI][about-copilot-cli]** を使うと、ターミナルで GitHub Copilot をエージェント型のコーディング アシスタントとして利用できます。コードベースを探索し、コードを生成し、コマンドを実行し、外部ツールに接続できます。すべてコマンド ラインから行えるため、グラフィカル エディターに切り替えずに作業を続けられます。

このワークショップでは、Tailspin Toys の一連の開発ワークフローを体験します。

1. GitHub Codespaces でプロジェクトを準備し、Copilot CLI をインストールして、基本を確認します。
2. 星評価の小さな変更を加え、ブラウザーで確認して、最初のプル リクエスト (PR) を手動でマージします。
3. フィルター機能の issue から始め、Plan モードで実装方法を決め、Autopilot モードで実装し、Interactive モードでレビューします。
4. リポジトリの指示を更新し、フィルター機能の作業に反映します。
5. 既存の `quality-checks` スキルをカスタマイズして、プロジェクトのチェックを実行します。
6. Playwright の Model Context Protocol (MCP) サーバーを追加し、ブラウザーでフィルター機能を確認します。
7. 品質保証 (QA) 用のカスタム エージェントを作成し、要件、テスト カバレッジ、検証結果をレビューします。
8. フィルター機能全体の変更をレビューし、Agent Merge を使って PR を処理します。
9. コンテキスト、モデル、共有、任意の cloud agent への委任に使うスラッシュ コマンドを確認します。

ワークショップでは、星評価の変更と、指示の更新、スキルの更新、QA プロファイル、テストを含むフィルター機能の変更の、2 つの PR を作成します。各ツールを学ぶ間も作業を引き継げるよう、フィルター機能と品質ワークフローは同じ会話とブランチで進めます。

## レッスン

| レッスン | トピック | 説明 |
| ------ | ----- | ----------- |
| [0. 前提条件][ex0] | セットアップ | リポジトリと Codespace を作成します |
| [1. Copilot CLI のインストール][ex1] | インストール | Copilot CLI をインストールして認証し、基本を確認します |
| [2. 星評価を追加する: 手軽な変更][ex2] | 最初の変更 | 既存の評価と評価がない場合の表示を追加し、最初の PR をマージします |
| [3. エージェント モード: Plan と Autopilot][ex3] | エージェント モード | issue から機能を計画し、Autopilot で実装して、Interactive モードでレビューします |
| [4. カスタム指示で Copilot を導く][ex4] | コンテキスト | 指示を確認、更新し、フィルター機能に適用します |
| [5. quality-checks スキルをカスタマイズして使う][ex5] | 繰り返し可能なチェック | 既存のスキルを確認し、結果の形式を変更して実行します |
| [6. Playwright MCP で機能を検証する][ex6] | ブラウザーでの確認 | CLI で MCP を設定し、フィルター機能の動作を確認します |
| [7. QA エージェントを作成して使う][ex7] | 要件とカバレッジ | 専門エージェントのプロファイルを作成して選択し、最終的な検証結果を集めます |
| [8. 機能の PR を作成してマージする][ex8] | レビューとマージ | 変更全体をレビューし、PR を作成して Agent Merge を使います |
| [9. GitHub Copilot CLI のスラッシュ コマンド][ex9] | CLI 機能 | コンテキスト、モデル、共有、cloud agent への任意の委任を確認します |
| [10. まとめと次のステップ][ex10] | まとめ | ワークフロー、再利用できるカスタマイズ、追加リソースを確認します |
| [オプション: Foundry を組み込む][foundry] | ホスト型エージェント | モデルを準備し、カタログに基づくエージェントをデプロイして、Web サイトに接続します |

## 前提条件

このワークショップに参加する前に、次の準備をしてください。

- [ ] 有効な **Copilot Student、Pro、Pro+、Business、Enterprise** プランを利用できる GitHub アカウント
- [ ] リポジトリと Codespace を作成する権限
- [ ] ターミナルまたはコマンド ラインの基本的な知識

> [!TIP]
> 有料プランを利用していない場合でも、認定学生は [GitHub Education][student-plan] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使うエージェント、MCP、コードレビュー、Copilot CLI の機能が含まれています。

> [!NOTE]
> Copilot Business または Copilot Enterprise を利用している場合は、管理者が組織で Copilot CLI を有効にしていることを確認してください。

## 始める

**[前提条件から始める →][ex0]**

[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[student-plan]: https://github.com/education/students
[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-cli/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-cli-power-tools/
[ex10]: 10-review/
[foundry]: 8-foundry-agent/
