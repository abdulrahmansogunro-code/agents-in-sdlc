---
title: "レッスン 4 - カスタム指示で Copilot を導く"
description: "リポジトリの指示を確認し、ドキュメント標準を追加して、フィルター機能のコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を使うときは、コンテキストが重要です。タスクの進め方に決まりがある場合、その指針を Copilot が利用できるようにします。[指示ファイル][instruction-files]では、作成するコードだけでなく、その構成方法も伝えられます。フィルター機能を実装したので、Copilot が参照した指示を確認し、ドキュメント標準を追加してコードに適用します。

このレッスンでは、次の内容を学習します。

- リポジトリの指示とパス別の指示ファイルがエージェントに伝わる仕組みを確認します。
- コーディング標準に従うよう、指示ファイルを更新します。
- 指示ファイルがコードに与える影響を確認します。

## シナリオ

Tailspin Toys には、開発作業に関するガイドラインと要件があります。たとえば、次のようなものです。

- コメントにはコードを繰り返すのではなく、意図や自明でない判断を記載します。
- `db/` と `src/lib/` のエクスポートされた関数には、目的、パラメーター、戻り値を説明する TSDoc/JSDoc を記載します。該当する場合は、注入可能な `db` 引数も説明します。
- 再利用可能な Astro コンポーネントには `Props` コントラクトを記載し、関連するコードの変更に合わせてコメントを最新の状態に保ちます。
- 既存のフォーマットと lint の指針を維持します。

指示ファイルを使い、Copilot がこれらの慣行に沿って作業できるようにします。

## 指示ファイル

カスタム指示を使うと、コーディング スタイルや要件に関するコンテキストを Copilot に伝えられます。これにより、より適切な提案やコード スニペットを得られます。好みのコーディング規約、ライブラリ、コメントの書き方などを指定できます。リポジトリ全体に適用する指示も、特定のファイル形式や作業だけに適用する指示も作成できます。

指示ファイルには次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリに関するすべての要求で Copilot に送られる単一の指示ファイルです。多くの要求に関係する、プロジェクト レベルの情報を記載します。
- `.github/instructions/*.instructions.md` は、特定の言語、ファイル形式、作業に対するガイドラインを記載します。

> [!NOTE]
> ほかの形式の指示とそのサポート状況は、利用する環境によって異なります。特定の形式に依存する前に、[カスタム指示のサポート情報][custom-instructions-support]を確認してください。

## このプロジェクトのカスタム指示ファイルを確認する

スターター プロジェクトには、すでに指示ファイルが含まれています。変更前にその内容を確認し、変更後の影響と比較します。

1. Codespace に戻ります。
2. Codespaces エディターで（ターミナルではなく）`.github/copilot-instructions.md` を開きます。
3. プロジェクトの概要とコーディング ガイドラインを確認します。この指示は、このリポジトリで Copilot とやり取りするたびに適用されます。
4. `.github/instructions` フォルダーを開き、Astro ファイル、Drizzle データ レイヤー、テストなどの指示を確認します。
5. `.github/instructions/unit-tests.instructions.md` を開き、先頭の `applyTo` フィールドを確認します。このフィールドは、指示を適用するファイルを決める glob を指定します。
6. `.github/instructions/drizzle.instructions.md` を開き、ほかの指示ファイルや既存のプロジェクト ファイルへのリンクを確認します。指示を再利用できる小さなファイルに分け、Copilot に参考例を示せます。

## チームのガイドラインに合わせて指示ファイルを更新する

スターター ファイルにはまだ不足があります。新たに生成する TypeScript に TSDoc コメントを追加するよう、`.github/copilot-instructions.md` を更新します。

1. `.github/copilot-instructions.md` で、35 行目付近にある **Code formatting guidance** セクションを探します。
2. 末尾に次の項目を追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

変更は自動的に保存されます。

## 更新した指示を使う

Copilot CLI は、会話の開始時にリポジトリの指示を読み込みます。更新した指示を使ってもフィルター機能のコンテキストを失わないよう、会話を終了して再開します。

1. フィルター機能の会話が開いている場合は、`/exit` を入力して終了します。Copilot CLI は会話を自動的に保存します。
2. リポジトリのルートで `game-filters-cli` ブランチに切り替わっていることを確認し、保存済みの会話を再開します。

   ```bash
   copilot --resume
   ```

   選択を求められた場合は、フィルター機能の会話を選び、`game-filters-cli` ブランチがチェックアウトされていることを確認します。

3. 更新した指示を適用するよう Copilot に依頼します。

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. `/diff` を入力し、変更された TypeScript ファイルを確認します。新しい TSDoc コメントが追加され、コードを正しく説明していることを確認します。

## まとめと次のステップ

Copilot CLI が指示ファイルからコンテキストを取得する仕組みを確認し、新しい標準を機能に適用しました。このレッスンでは、次の内容を行いました。

- リポジトリの指示とパス別の指示ファイルがエージェントに伝わる仕組みを確認しました。
- コーディング標準に従うよう、指示ファイルを更新しました。
- 指示ファイルがコードに与える影響を確認しました。

次は、lint とテストを一貫して実行できるよう、再利用可能な `quality-checks` スキルを[カスタマイズして実行します][next-lesson]。

## リソース

- [Copilot CLI のカスタム指示を追加する][instruction-files]
- [カスタム指示のサポート情報][custom-instructions-support]
- [カスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [Awesome Copilot — 指示ファイルやその他のリソース集][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
