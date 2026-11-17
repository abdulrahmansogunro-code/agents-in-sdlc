---
title: "レッスン 2 - 星評価を追加する: 手軽な変更"
description: "Copilot CLI でゲーム カードに小さな変更を加え、転送されたブラウザーで確認して、最初のプル リクエストとしてマージします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Copilot CLI をインストールし、会話を試しました。次は、プロジェクトに最初の変更を加えます。変更は小さく保ちます。各ゲームのデータには星評価がありますが、ホーム ページのゲーム カードにはまだ表示されていません。エージェントに評価を表示させ、変更をレビューし、最初のプル リクエストとしてマージします。

このレッスンでは、次の内容を学習します。

- 機能ブランチで目的を絞った Copilot の会話を開始します。
- エージェントにプロジェクトの小さな変更を依頼します。
- `/diff` で変更をレビューします。
- アプリケーションを実行し、転送されたブラウザーで変更を確認します。
- 最初のプル リクエストを作成してマージします。

## シナリオ

Tailspin Toys の各ゲームには星評価を設定でき、ゲームの詳細ページにはすでに表示されています。しかし、ホーム ページのゲーム カードにはタイトル、カテゴリー、発行元、説明しか表示されていません。最初の練習として、エージェントに各カードで既存の評価を表示させます。これは小さく完結しているため、最初のセッションに適しています。

## 会話の構成

**会話**は、Copilot CLI でタスクに取り組む場所です。Copilot app とは異なり、通常の CLI 会話では、ターミナルで現在チェックアウトされているリポジトリと Git ブランチを使います。保存した会話を後から再開できますが、ファイルとブランチはディスク上の通常の Git 状態のままです。

会話では、プロンプトとエージェントの応答、ファイルを調べて編集するエージェントのツール操作、`/diff` で確認できる変更の 3 つが表示されます。

## 会話を開始して変更を依頼する

機能の実装を始めるため、新しい会話を開始します。

1. Codespace に戻ります。
2. ターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
3. まだ起動していない場合は、次のコマンドを使って Copilot を起動します。

   ```bash
   copilot --yolo
   ```

4. `/new` スラッシュ コマンドを実行し、<kbd>Enter</kbd> を押して新しいセッションが始まったことを確認します。
5. 次のプロンプトを使って変更を依頼します。

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot はプロジェクトを調べ、ゲームの詳細表示に使うファイルを探して、必要なコードを作成します。これで Copilot CLI を使って機能を追加できました。

## 差分をレビューする

小さな変更でも、マージする前に AI が生成した変更をレビューする必要があります。Copilot CLI で変更を確認します。

1. `/diff` を入力し、変更されたすべてのファイルを調べます。
2. ゲーム カードに評価がある場合は数値が、`starRating` が `null` の場合は `No rating yet` が表示されることを確認します。
3. 両方の状態がテストされていることを確認します。
4. Copilot が実行したチェックの結果を確認し、失敗があれば修正を依頼します。
5. レビューが終わったら、<kbd>Esc</kbd> を押して差分画面を閉じます。

> [!NOTE]
> Copilot を含む生成 AI ツールは確率的に動作するため、生成されるコードは正確には同じにならない場合があります。特定の実装に一致することではなく、動作をレビューしてください。

## 変更を確認する

コードを読むだけで動作すると判断するのではなく、Copilot に Web サイトを起動させ、Codespaces で転送されたブラウザーから更新されたユーザー インターフェイス (UI) を確認します。

1. Copilot にアプリケーションの起動を依頼します。

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces でポート `4321` が利用可能になったら **Open in Browser** を選択します。
3. ゲーム カードに 5 段階評価が表示されることを確認します。
4. Copilot に戻り、起動したサーバーを停止するよう依頼します。

   ```plaintext
   Stop the development server you started.
   ```

## 最初のプル リクエストを作成してマージする

これで機能が完成しました。新しいコードをプロジェクトにマージするため、プル リクエスト (PR) を作成します。

1. 既定のエージェントに変更をコミットするよう依頼します。

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. `/pr create` を入力します。Copilot CLI は PR の作成時に既存のコミットをプッシュし、PR の URL を表示します。
3. Copilot CLI が表示した URL を、<kbd>Command</kbd> (Mac) または <kbd>Ctrl</kbd> (Windows/Linux) を押しながら選択して PR を開きます。
4. 変更されたファイルとチェック結果をレビューします。
5. 準備ができたら **Merge pull request** を選択し、マージを確定します。
6. Codespace に戻り、`/exit` で Copilot CLI を終了します。
7. ローカルの `main` を更新します。

   ```bash
   git checkout main
   git pull
   ```

## まとめと次のステップ

GitHub Copilot CLI を使って、最初の変更をリリースしました。このレッスンでは、次の内容を行いました。

- 機能ブランチで目的を絞った Copilot の会話を開始しました。
- エージェントにゲーム カードの小さな変更を依頼しました。
- `/diff` で変更をレビューしました。
- 転送されたブラウザーでアプリケーションを実行し、星評価を確認しました。
- 最初のプル リクエストを作成してマージしました。

次は、[フィルター機能の issue から始め、Plan モードと Autopilot モードを使って][next-lesson]、より大きな機能を作成します。

## リソース

- [GitHub Copilot CLI について][about-copilot-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
