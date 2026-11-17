---
title: "演習 3 - カスタム エージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタム エージェントとは

GitHub Copilot の[カスタム エージェント][custom-agents-concept]を使うと、開発ワークフロー内の特定の作業や分野に合わせた AI アシスタントを作成できます。リポジトリの `.github/agents` フォルダーに Markdown ファイルでエージェントを定義し、特定の作業を効果的に行うための指示、ベスト プラクティス、コーディング パターン、分野固有の知識を Copilot に提供します。チームの専門知識を再利用できるエージェントとして記録できます。たとえば、[Web Content Accessibility Guidelines (WCAG)][wcag] 準拠を確認するアクセシビリティ エージェント、安全なコーディング慣行に従うセキュリティ エージェント、一貫したテスト パターンを維持するテスト エージェントを作成できます。

カスタム エージェントは、プロジェクトの `.github/agents` フォルダー内、または `~/.copilot/agents` にある Markdown ファイルで定義します。各ファイルには、少なくとも `name` と `description` を含む YAML フロントマターと、エージェントの動作、専門知識、指示を定義する Markdown プロンプトを記述します。

### カスタム エージェントとエージェント スキルの違い

カスタム エージェントと[エージェント スキル][agent-skills-concept]には、役割の重なる部分があります。どちらも主に Markdown ファイルで定義し、AI に作業方法を伝えます。分かりやすく言うと、**カスタム エージェントは作業者、スキルはツール**です。

カスタム エージェントは独自のコンテキスト ウィンドウを持ち、作業の一部としてスキルやほかのエージェントを調整します。このラボのアクセシビリティ カスタム エージェントは、アクセシビリティ ガイドラインに沿ってサイトをレビューし、更新します。その作業の中で、プル リクエスト ワークフローのスキルや、テストを実行・管理するスキルを呼び出すこともできます。

> [!NOTE]
> カスタム エージェントの作成方法に決まった正解はありません。AI を使うほかの作業と同じように、利用する環境やシナリオに合わせて試し、改善してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

この演習では、カスタム エージェントを使って次の内容を学習します。

- カスタム エージェントの定義方法
- カスタム エージェントへの作業の割り当て

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず、すべての利用者がクラウドファンディング プラットフォームを使えるように取り組んでいます。最近、現在のダーク テーマでは文字と背景のコントラストが不十分で、読みにくいというフィードバックがありました。このアクセシビリティの課題に対処するため、デザイン チームは利用者が切り替えられる高コントラスト モードを求めています。

アクセシビリティは重要なため、できるだけ早く実装する必要があります。カスタム エージェントを使って機能を生成します。

## アクセシビリティ カスタム エージェントを確認する

アクセシビリティ用のカスタム エージェントは、あらかじめ作成されています。Copilot にどのような指針を与えるかを理解するため、内容を確認します。

Codespace に戻り、アクセシビリティ カスタム エージェントのファイルを確認します。

1. `.github/agents/accessibility.md` を開きます。
2. `name` と `description` フィールドを含む YAML フロントマターを確認します。

> [!CAUTION]
> カスタム エージェントには、`name` と `description` を含むフロントマターが必要です。

3. 続くセクションを読み、アクセシブルな Web サイトのコード生成に関する主な責任、アクセシビリティのベスト プラクティス、HyperText Markup Language (HTML)、Cascading Style Sheets (CSS)、JavaScript のコード例、よくある問題を確認します。

## Issue を作成して割り当てる

ミッション コントロールは、環境内のエージェントを管理する場所です。Copilot cloud agent に作業を割り当て、進捗を監視し、実行中のセッションに追加の指示を送れます。まず、高コントラスト モードの作成を Copilot に依頼します。

1. リポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい issue のダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Add high contrast mode to website` と入力します。
6. **Description** に次のテキストを入力します。

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して、割り当てダイアログを開きます。
9. 一覧から **Accessibility agent** を選択します。

   ![カスタム エージェントの割り当て画面で、エージェントと Accessibility が強調表示されています](../../../_images/ex5-select-custom-agent.png)

10. **Assign** を選択します。
11. Copilot がバックグラウンドで作業を開始します。

## まとめと次のステップ

GitHub Copilot の[カスタム エージェント][custom-agents]を確認しました。カスタム エージェントを使うと、チームの専門知識や標準を再利用できるエージェントとして記録し、特定の作業や分野に合わせて Copilot を導けます。

この演習では、次の内容を確認しました。

- カスタム エージェントの定義方法
- カスタム エージェントへの作業の割り当て

Copilot が高コントラスト モードを実装している間に、ミッション コントロールから[エージェント セッションを監視し、調整します][next-lesson]。

## リソース

- [カスタム エージェントについて][custom-agents]
- [組織でカスタム エージェントを使用するための準備][org-custom-agents]
- [エンタープライズでカスタム エージェントを使用するための準備][enterprise-custom-agents]

---

| [← 前のレッスン: GitHub Copilot cloud agent][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
