表示されたファイル中で相対リンクと画像パスを定義して、読者がリポジトリ中の他のファイルにアクセスしやすくできます。

相対リンクは、現在のファイルに対する相対的なリンクです。 たとえばREADMEファイルをリポジトリのルートに置いていて、別のファイルを_docs/CONTRIBUTING.md_に置いているなら、READMeファイル中の_CONTRIBUTING.md_への相対リンクは以下のようになります。

```
[このプロジェクトへのコントリビューションガイドライン](docs/CONTRIBUTING.md)
```

{% data variables.product.product_name %}は相対リンクあるいは画像パスを、現在のブランチに基づいて変換するので、リンクやパスは常にうまく働きます。 The path of the link will be relative to the current file. Links starting with `/` will be relative to the repository root. `./`や`../`といった相対リンクのオペランドはすべて利用できます。

相対リンクは、リポジトリをクローンするユーザにも扱いやすいです。 絶対リンクはリポジトリのクローンではうまく働かないかもしれません。リポジトリ内の他のファイルを参照するには、相対リンクを使うことをおすすめします。
