---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前の演習では、GitHub Copilot cloud agent にユーザー体験の改善や機能追加に関する 3 つの作業を依頼しました。cloud agent は非同期かつ自律的に動作しますが、作業を監視することも重要です。

cloud agent に割り当てた作業を管理する方法はいくつかあります。GitHub.com の[エージェント ページ][agents-page]では、オープンなプル リクエスト (PR) があるすべてのエージェント作業を確認できます。実行内容を調べたり、進行中のセッションに追加の指示を送ったりできます。

このレッスンでは、次の内容を学習します。

- エージェント ページで cloud agent の作業を監視します。
- 実行中のセッションに追加の機能を依頼します。

## シナリオ

エージェントに高コントラスト モードを作成するよう依頼した後、チームはライト モードも追加することにしました。サイトのスタイルを更新し、切り替え機能を追加する作業をすでに進めているため、あわせて実装するのが適切です。エージェントに指示を送り、高コントラストに加えてライト モードも作成するようにします。

## Copilot cloud agent の作業を確認する

Copilot cloud agent に割り当てた作業の現在の状態を確認します。

1. [Copilot agents ページ](https://github.com/copilot/agents)を開きます。
2. メイン ペインと左ペインの両方に表示される作業の一覧を確認します。次のような、Copilot に割り当てた作業が表示されます。
   - コードベースのドキュメントの更新
   - ゲームを変更する API の生成
   - Web サイトへの高コントラスト モードの追加
3. 実行中の作業を選択し、Copilot が行った操作を確認します。たとえば、次のような操作が表示されます。
   - リポジトリからのコードのチェックアウト
   - Copilot が作業する環境の作成
   - MCP サーバーの設定
   - 割り当てられた作業を完了するための各種操作

> [!NOTE]
> 表示される具体的な手順は、Copilot の作業状況や進め方によって異なります。

4. 右側に表示される PR ペインも確認します。ここでは、PR と変更されたファイルを確認し、作業をさらに監視できます。

## cloud agent に追加の指示を送る

実行中の作業を確認できたので、高コントラスト モードに取り組んでいる Copilot にライト モードも追加するよう依頼します。

1. 高コントラスト モードの作業を示すセッションを選択します。Copilot が付けた名前や作業状態によって、表示されるタイトルは異なります。

   ![ミッション コントロールのアクセシビリティ セッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが完了し、作業が始まったことを示すまで、数分間セッションを確認します。Copilot のメッセージが表示され始めたら、作業が始まったことを確認できます。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを入力します。

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![cloud agent の作業画面で、Steer active session while Copilot is working ダイアログが強調表示されています](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot がプロンプトを受け取り、作業の流れに追加したことを確認します。

## Copilot に作業を任せる

更新した作業に Copilot が取り組みます。メッセージを送信した時点で実行していた手順が終わると、新しい依頼が作業の流れに加わります。

これまでと同様、完了まで数分かかります。その間に休憩して、ここまでに学んだことを振り返りましょう。

## まとめと次のステップ

Copilot cloud agent の作業を監視して指示するための中心的な場所である、Copilot agents ページを確認しました。ミッション コントロールでは、進行中または完了したすべての作業を追跡し、実行内容をレビューして、進行中の作業の範囲を変更したり、追加の指示を送ったりできます。

このレッスンでは、次の内容を行いました。

- ミッション コントロールとエージェント ページを使って、cloud agent の作業を監視しました。
- 実行中のセッションに追加の機能を依頼しました。

Copilot がアクセシビリティ機能を実装している間に、[Copilot が作成した PR を改善する][next-lesson]作業に進みます。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタム エージェントについて][custom-agents]

---

| [← 前のレッスン: カスタム エージェント][previous-lesson] | [次のレッスン: Copilot の作業を改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
