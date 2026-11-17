---
title: "演習 1 - カスタム指示 (Cloud agent)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を使うときは、コンテキストが重要です。作業の方法に決まりがある場合や、Copilot に知っておいてほしい背景情報がある場合は、その情報を利用できるようにします。[指示ファイル][instruction-files]を使うと、Copilot に何をしてほしいかだけでなく、どのように実行するかも伝えられます。

この演習では、次の内容を学習します。

- リポジトリのカスタム指示とパス別の指示ファイルを使って、プロジェクト固有のコンテキスト、コーディング ガイドライン、ドキュメント標準が Copilot に伝わる仕組みを確認します。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加します。

> [!NOTE]
> VS Code および CLI ハーネスとは異なり、この演習では変更前後のプロンプトを実行しません。Copilot cloud agent は GitHub issue に対して非同期に動作するため、影響をリアルタイムで並べて示すのは困難です。このハーネスの後半で、cloud agent が作成したプル リクエストをレビューするときに、指示ファイルの効果を確認します。

## 指示ファイル

### シナリオ

Tailspin Toys には、開発作業に関するガイドラインと要件があります。たとえば、次のようなものです。

- データ レイヤーには、常にユニット テストが必要です。
- ユーザー インターフェイス (UI) はダーク モードにし、現代的な見た目にします。
- コードには TSDoc doc コメントでドキュメントを追加します。
- 各ファイルの先頭に、ファイルの役割を説明するコメント ブロックを追加します。

指示ファイルを使い、Copilot がこれらの開発慣行に沿って作業できるようにします。

### カスタム指示

カスタム指示では、コーディング スタイルや要件に関するコンテキストを Copilot に提供できます。これにより、より適切な提案やコード スニペットを得られます。好みのコーディング規約、ライブラリ、コメントの書き方などを指定できます。リポジトリ全体に適用する指示も、特定のファイル形式や作業だけに適用する指示も作成できます。

指示ファイルには次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリに関するすべての要求で Copilot に送られる単一の指示ファイルです。多くの Copilot のチャットまたは CLI 要求に関係する、プロジェクト全体の情報を記載します。技術スタック、開発対象の概要、ベスト プラクティス、全体に適用する指針などが該当します。
- `.github/instructions/*.instructions.md` は、特定の作業やファイル形式に対するガイドラインを記載します。TypeScript や Astro などの言語、UI コンポーネントの作成、新しいユニット テストなどを対象にできます。

> [!NOTE]
> 統合開発環境 (IDE) では、指示ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、リポジトリ レベルの指示と `applyTo` フロントマターを持つ `*.instructions.md` ファイルの両方を使ってコードを生成します。
>
> Copilot は AGENTS.md や CLAUDE.md など、ほかの標準形式の指示ファイルにも対応しています。詳細は [カスタム指示のサポート情報][custom-instructions-support]を参照してください。

### 指示ファイルを管理するためのベスト プラクティス

指示ファイルの作成方法を詳しく扱うことは、このワークショップの範囲外です。ただし、サンプル プロジェクトには代表的な構成例が含まれています。基本的な方針は次のとおりです。

- `copilot-instructions.md` には、開発対象の説明、プロジェクトの構造、全体に適用するコーディング標準など、プロジェクト レベルの指針を記載します。
- `*.instructions.md` には、ユニット テスト、Astro コンポーネント、データ レイヤーなどのファイル形式や、特定の作業に対する指示を記載します。
- 自然な言葉を使い、明確な指針と、コードの望ましい例・望ましくない例を示します。

指示ファイルの作成方法も、AI の使い方と同じく一つに決まっているわけではありません。プロジェクトに合う方法を試しながら見つけてください。

> [!TIP]
> GitHub Copilot を使うプロジェクトには、十分な指示ファイルを用意することをお勧めします。このプロジェクトには、[UI の更新][ui-instructions]や [Astro][astro-instructions]など、さまざまな作業向けのファイルがあります。
>
> Copilot に指示ファイルを作成させることもできます。利用する環境によって方法は異なります（たとえば、VS Code の **Configure Chat → Generate Agent Instructions**、Copilot CLI の `/init` など）。必要な場合は、各環境向けのレッスンで説明します。
>
> テンプレートや出発点を探している場合は、指示ファイル、カスタム エージェント、その他のリソースをまとめた [awesome-copilot][awesome-copilot] を確認してください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム指示ファイルを確認する

リポジトリに含まれる指示ファイルを確認します。中心となる `copilot-instructions.md` と、さまざまな作業向けの `*.instructions.md` ファイルがあります。エディターまたは GitHub の Web UI で開いてください。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの概要と、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** の **GitHub Actions Workflows** に関する指針も確認してください。これらの指示は、Copilot とのあらゆるやり取りに適用されます。
3. `.github/instructions` フォルダーを開き、Astro ファイル、Drizzle データ レイヤー、テストなどに関する指示を確認します。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドが、リポジトリ ルートからの相対パスとして、どのファイルに指示を適用するかを決める glob であることを確認します。ここでは、たとえば `**/*.test.ts` に一致する TypeScript のテスト ファイルが対象です。
5. このプロジェクトでユニット テストを作成する際の指示を確認します。
6. `.github/instructions/drizzle.instructions.md` を開き、末尾までスクロールします。`unit-tests.instructions.md` などの指示ファイルや、プロジェクト内の既存ファイルへのリンクを確認します。これにより、大きな指示を再利用できる小さなファイルに分け、Copilot にコード生成時の参考例を示せます（ここに記載されたパスはリポジトリ ルートではなく、指示ファイルからの相対パスです）。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはプロジェクトのコーディング標準が記載されていますが、コード内のドキュメントに関する要件はまだありません。次の手順で TSDoc doc コメントとファイル コメント ヘッダーのルールを追加します。

## リポジトリ全体に適用する標準を追加する

この演習で行う編集は、コード内のドキュメントを TSDoc doc コメントとファイル レベルのコメント ヘッダーで記載するという、プロジェクト全体のルールの追加です。後の演習で issue を割り当てるとき、cloud agent はこの指示を参照します。

編集の前に作業ブランチを作成します。cloud agent は issue の対象ブランチにある指示を読み取りますが、ここでは変更を整理してコミットします。

1. Codespace のターミナルで、新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

前述のとおり、`.github/copilot-instructions.md` は Copilot にプロジェクト レベルの情報を伝えるファイルです。リポジトリのコーディング標準を記載し、コード提案の質を高めます。

1. `.github/copilot-instructions.md` をもう一度開きます。
2. 27 行目付近にある **Code formatting requirements** セクションを探します。プロジェクトのコーディング標準が記載されていますが、コード内のドキュメントのルールはありません。そのため、生成されたヘルパーに doc コメントがありませんでした。
3. 既存の標準の直下に、次の Markdown を追加します。ファイル コメント ヘッダーと TSDoc doc コメントを追加するよう Copilot に指示します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 前のレッスンで確認したように、指示ファイルはリポジトリ レベル（`.github/copilot-instructions.md`）にも、特定の言語、ファイル形式、作業向けの `*.instructions.md` にも作成できます。doc コメントのルールのようにプロジェクト全体に適用する標準は、リポジトリ レベルのファイルに記載します。

## 指示の変更をコミット、プッシュ、マージする

cloud agent は issue の対象ブランチから指示ファイルを読み取ります。次の演習で Copilot に割り当てる issue は `main` からブランチを作成するため、cloud agent が新しい指示を使えるよう、変更を `main` に取り込みます。

1. 変更をステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` に向けたプル リクエストを作成し、マージします。次の演習で issue に割り当てるとき、cloud agent はこの指示を読み取ります。

> [!TIP]
> このワークショップでは `main` に直接作業してもかまいません。その場合はブランチ作成を省略し、変更を `main` にコミットしてください。ここでは、実際のプロジェクトで行う方法に合わせてブランチを作成しています。

## まとめと次のステップ

このプロジェクトで Copilot が指示ファイルからコンテキストを取得する仕組みを確認し、`.github/copilot-instructions.md` にリポジトリ全体の標準を追加しました。このハーネスの後半で、cloud agent が作成するプル リクエストにこの標準が反映されていることを確認します。

次に、[最初の issue を Copilot cloud agent に割り当てます][next-lesson]。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [Copilot 向けのカスタム指示を改善する 5 つのヒント][copilot-instructions-five-tips]
- [Awesome Copilot — 指示ファイルやその他のリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
