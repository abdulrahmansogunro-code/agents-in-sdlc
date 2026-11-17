---
title: "演習 4 - カスタム エージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタム エージェントとは

GitHub Copilot の[カスタム エージェント][custom-agents-concept]を使うと、開発ワークフロー内の特定の作業や分野に合わせた AI アシスタントを作成できます。リポジトリの `.github/agents` フォルダーに Markdown ファイルでエージェントを定義し、Copilot に特定の作業を効果的に行わせるための指示、ベスト プラクティス、コーディング パターン、分野固有の知識を提供します。チームの専門知識を再利用できるエージェントとして記録できます。たとえば、[Web Content Accessibility Guidelines (WCAG)][wcag] 準拠を確認するアクセシビリティ エージェント、安全なコーディング慣行に従うセキュリティ エージェント、一貫したテスト パターンを維持するテスト エージェントを作成できます。

カスタム エージェントは、プロジェクトの `.github/agents` フォルダー内、または `~/.copilot/agents` にある Markdown ファイルで定義します。各ファイルには、少なくとも `name` と `description` を含む YAML フロントマターと、エージェントの動作、専門知識、指示を定義する Markdown プロンプトを記述します。

### カスタム エージェントとエージェント スキルの違い

カスタム エージェントと[エージェント スキル][agent-skills-concept]には、役割の重なる部分があります。どちらも主に Markdown ファイルで定義し、AI に作業方法を伝えます。分かりやすく言うと、**カスタム エージェントは作業者、スキルはツール**です。

カスタム エージェントは独自のコンテキスト ウィンドウを持ち、作業の一部としてスキルやほかのエージェントを調整します。このラボのアクセシビリティ カスタム エージェントは、アクセシビリティ ガイドラインに沿ってサイトをレビューし、更新します。その作業の中で、プル リクエスト ワークフローのスキルや、テストを実行・管理するスキルを呼び出すこともできます。

> [!NOTE]
> カスタム エージェントの作成方法に決まった正解はありません。AI を使うほかの作業と同じように、利用する環境やシナリオに合わせて試し、改善してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず、すべての利用者がクラウドファンディング プラットフォームを使えるように取り組んでいます。最近、現在のダーク テーマでは文字と背景のコントラストが不十分で、読みにくいというフィードバックがありました。このアクセシビリティの課題に対処するため、デザイン チームは利用者が切り替えられる高コントラスト モードを求めています。

アクセシビリティは重要なため、できるだけ早く実装できるよう、カスタム エージェントを使って機能を生成します。

この演習では、次の内容を学習します。

- 既存のアクセシビリティ カスタム エージェントを確認します。
- Copilot Chat のアクセシビリティ エージェントを使って、高コントラスト モードを実装します。

## アクセシビリティ カスタム エージェントを確認する

アクセシビリティ用のカスタム エージェントは、あらかじめ作成されています。Copilot にどのような指針を与えるかを理解するため、内容を確認します。

Codespace に戻り、アクセシビリティ作業用に `main` から新しいブランチを作成して切り替えます。演習 3 のフィルター機能 PR とはブランチを分けます。

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. `.github/agents/accessibility.md` を開きます。
2. `name` と `description` フィールドを含む YAML フロントマターを確認します。

> [!CAUTION]
> カスタム エージェントには、`name` と `description` を含むフロントマターが必要です。

3. 続くセクションを読み、アクセシブルな Web サイトのコード生成に関する主な責任、アクセシビリティのベスト プラクティス、HyperText Markup Language (HTML)、Cascading Style Sheets (CSS)、JavaScript のコード例、よくある問題を確認します。

## Copilot Chat でカスタム エージェントを使う

VS Code の Copilot Chat ビュー下部にあるエージェント ドロップダウンには、`.github/agents` に定義されたすべてのカスタム エージェントが表示されます。カスタム エージェントを選ぶと、そのエージェントの指示とツールに合わせてチャット セッションが設定されます。

> [!TIP]
> **Copilot Chat を開く**
>
> 以下の演習を始める前に、Codespace に戻り、Copilot Chat パネルを開いて **New Chat** を選択し、新しい会話を始めます。モードとモデルの選択は演習によって異なります。必要な場合は、各手順で説明します。

1. Chat ビューのエージェント ドロップダウンで、まだ選択されていない場合は **Agent** を選択します。

   ![Chat ビューのエージェント ピッカーのスクリーンショット](../../../_images/shared-chat-mode-selector.png)

2. Chat ビュー下部のエージェント ドロップダウンを選択します。既定では、現在のエージェントとして **default** が表示されています。
3. 利用可能なエージェントの一覧から **Accessibility agent** を選択します。
4. アクセシビリティ エージェントに次のプロンプトを送信します。

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

5. Copilot Chat がコードベースを調べ、変更を提案して、プロジェクト ファイルを編集します。編集内容は、ファイル パスと差分とともにチャットに表示されます。
6. 編集が進むと、**Files changed** の表示が更新され、このセッション中にエージェントが変更したファイルを確認できます。

> [!NOTE]
> この作業には数分かかる場合があります。Copilot は実際にリポジトリを変更し、Astro コンポーネント、CSS、関連するテストなどの既存ファイルを編集します。

次の演習では、進行中の作業をレビューし、エージェントに追加の指示を送ります。

## まとめと次のステップ

特定の作業や分野向けに調整できる GitHub Copilot の[カスタム エージェント][custom-agents]を確認しました。カスタム エージェントを使うと、チームの専門知識や標準を再利用できるエージェントとして記録し、Copilot に効果的な作業方法を伝えられます。

この演習では、次の内容を確認しました。

- カスタム エージェントの定義方法
- Copilot Chat の agent mode でカスタム エージェントを使う方法

次は、エージェントの作業を[監視して調整し][next-lesson]、変更をレビューしながら、同じセッションにライト モードの切り替え機能を追加します。

## リソース

- [カスタム エージェントについて][custom-agents]
- [IDE でカスタム エージェントを作成する][creating-custom-agents-ide]
- [VS Code のカスタム エージェント][custom-agents-vscode]
- [カスタム エージェントの設定][custom-agents-config]
- [awesome-copilot のカスタム エージェント][awesome-copilot-agents]

---

| [← 前のレッスン: Playwright MCP サーバーで機能をテストする][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
