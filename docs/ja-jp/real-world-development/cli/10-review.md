---
title: "レッスン 10 - まとめと次のステップ"
description: "Copilot CLI のワークフロー、2 つのプル リクエスト、再利用できるカスタマイズ、追加リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Tailspin Toys の一連のワークフローで GitHub Copilot CLI を使いました。次の内容を行いました。

- Codespace を準備し、Copilot CLI をインストールし、プロジェクトを確認して、登録済みのフィルター issue を見つけました。
- 星評価を追加し、転送されたブラウザーで結果を確認して、最初のプル リクエスト (PR) を手動でマージしました。
- フィルター機能の issue から始め、Plan モードで方法を決め、Autopilot モードで実装して、Interactive モードでレビューしました。
- カスタム指示でエージェントを導き、既存の `quality-checks` スキルをカスタマイズして、ユニット テスト、lint、型チェックを実行しました。
- Playwright の Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーでフィルター機能を確認しました。
- 品質保証 (QA) 用のカスタム エージェントを作成して選択し、要件、テスト カバレッジ、スキルの結果、ブラウザーでの証拠を評価しました。
- フィルター機能全体の変更をレビューし、フィルター機能の PR で Agent Merge を許可しました。
- コンテキスト、モデル、共有、cloud agent への任意の委任に使うスラッシュ コマンドを確認しました。

## リリースした内容

このワークショップでは、更新済みの `main` からそれぞれ独自のブランチを作成し、2 つの PR を作ります。

1. **星評価:** 既存の `starRating` と、評価がない場合の状態をゲーム カードに表示します。
2. **フィルター機能と品質ワークフロー:** フィルター機能を実装し、指示を更新して機能に適用し、`quality-checks` のレポートをカスタマイズし、QA プロファイルを作成して、関連するテストを追加します。

フィルター機能の計画から PR の作成までは、同じ会話とブランチを使いました。ワークショップを簡潔に進めるため、これらの作業を 1 つの PR にまとめています。

## さまざまな検証方法

自動テスト、自分でのブラウザー確認、MCP を使った Copilot によるブラウザー操作を通して、コードを検証しました。`quality-checks` スキルはユニット テスト、lint、型チェックを実行し、カスタマイズした形式で結果を報告しました。QA はこれらの結果と、要件やテスト カバレッジのレビューをまとめて PR の確認に使いました。

追加するテストは、実際に不足しているカバレッジを補うものである必要があります。QA の実行時にテスト追加が不要と判断される場合もあります。マージを許可する前にコードと証拠をレビューし、変更後は影響を受ける証拠を更新してください。

## ベスト プラクティス

Copilot に与えるコンテキストとツールは、作業結果に影響します。このワークショップでは、指示を更新し、スキルをカスタマイズし、QA プロファイルを作成し、MCP サーバーを設定しました。会話をまたいでこれらのカスタマイズを再利用し、チームのニーズに合わせて調整してください。指示は標準を設定し、スキルは繰り返し可能なタスクを説明し、カスタム エージェントは専門的な役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけで判断せず、実際の変更とツールの結果を確認してください。

タスクに合った**モードとモデル**を選びます。実装前に方法を検討するときは **Plan**、範囲の小さい変更で作業に関与し続けるときは **Interactive**、範囲が明確なタスクを任せるときは **Autopilot** を使います。定型的な編集には速いモデルを、複雑な作業には高性能なモデルを選びます。

環境と同じくらい、コンテキストも重要です。何を、なぜ、どのように作るかを明確に伝えることで、出力を大きく改善できます。

## さらに確認する

主なワークフローは完了しました。Copilot CLI には、ほかにも次のような機能があります。

- `/review` でコード レビュー エージェントに変更を分析してもらいます。
- `/rubber-duck` で問題を説明し、別の視点からの意見を得ます。
- `/fleet` で独立したサブタスクを並行して調整します。
- `/worktree` で別のタスクを分離します。
- `/delegate` で Copilot cloud agent にタスクを送信します。

## 次のステップ

ツールの使い方を上達させるには、使い続けるのが一番です。製品コード、趣味のコード、長い間作りたいと思っていた小さなアプリなどで活用してください。チームと知識を共有し、お互いの経験から学びましょう。ドキュメントも引き続き確認してください。

ターミナルから Tailspin Toys を拡張する場合は、オプションの[Foundry Backer Concierge シリーズ][foundry]に進みます。ほかの環境でのワークショップを確認するには、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、[Copilot cloud agent ワークショップ][cloud]を参照してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI のカスタマイズ][customize-cli]
- [Copilot CLI でプル リクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
