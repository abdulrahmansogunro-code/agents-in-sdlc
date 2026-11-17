---
title: "レッスン 8 - 機能の PR を作成してマージする"
description: "フィルター機能、指示、スキルの更新、QA プロファイル、テストをまとめてレビューし、PR を作成して Agent Merge を使います。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

フィルター機能の実装、指示の更新、スキルの更新、品質保証 (QA) プロファイル、テストは、すべて 1 つのブランチに保存されています。まとめてレビューし、プル リクエストを作成しましょう。星評価の PR は自分でマージしましたが、今回は **Agent Merge** にプロセスを任せます。

> [!NOTE]
> 通常は、機能、指示の更新、スキルの更新、QA エージェントを複数の PR に分けます。ワークショップを簡潔に進めるため、フィルター機能と品質ワークフローは、1 つの会話とブランチで作業し、この PR にまとめます。

このレッスンでは、次の内容を学習します。

- Agent Merge と、マージ ライフサイクルを自動化する方法を確認します。
- 機能全体の変更と検証結果を調べます。
- フィルター機能の PR を作成します。
- レビュー後にのみ Agent Merge を有効にし、PR がマージされたことを確認します。

## シナリオ

フィルター機能の作業では、Copilot を使って計画、実装、検証を行いました。Tailspin Toys では、マージの許可を開発者が管理しながら、PR に関する残りの作業を自動化したいと考えています。

## Agent Merge とは

**Agent Merge** は、プル リクエストをマージするために必要な残りの作業を自動化します。有効にすると、Copilot は失敗した継続的インテグレーション (CI) チェックの修正、レビュー コメントへの対応、必要に応じたリベースなど、PR を妨げている問題に取り組みます。その後、リポジトリで許可されていれば、GitHub の自動マージを有効にします。

これまでは **Merge pull request** を自分で選択していました。Agent Merge にその作業を任せることもできます。有効にする前に、作業内容をレビューして準備ができていることを確認してください。

## Agent Merge で PR を管理する

作成したコードをまとめてレビューし、PR を作成してから、Agent Merge に残りのプロセスを任せます。

1. Codespace に戻ります。
2. `/agent` を入力してエージェントのダイアログを開きます。
3. オプションの一覧から **Default** を選択し、<kbd>Enter</kbd> を押します。
4. `/pr create` コマンドで新しい PR を作成します。
5. `/pr agentmerge` を使って Agent Merge を有効にします。
6. Copilot が PR の継続的インテグレーションを監視します。すべて成功すると、マージが実行されます。
7. Copilot から「PR #14 was squash-merged successfully.」のようなメッセージが表示されたことを確認します。

> [!IMPORTANT]
> Agent Merge は、必須の承認、ブランチ保護、マージ キュー、リポジトリ設定、権限の不足を回避しません。ブロックされた場合は、報告された理由を確認し、リポジトリで許可されていればレビュー済みの変更を手動でマージしてください。

## まとめと次のステップ

コードの生成、テストと検証、プル リクエストの処理など、開発プロセスの一部を自動化しました。このレッスンでは、次の内容を行いました。

- Agent Merge と、マージ ライフサイクルを自動化する方法を確認しました。
- 機能全体の変更と検証結果を調べました。
- フィルター機能の PR を作成しました。
- レビュー後にのみ Agent Merge を有効にし、PR がマージされたことを確認しました。

次に、コンテキスト、モデル、共有、cloud agent への任意の委任に使う[便利な Copilot CLI のスラッシュ コマンド][next-lesson]を確認します。

## リソース

- [Copilot CLI でプル リクエストを管理する][manage-prs]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
