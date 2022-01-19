# メンテナ向け: PHPマニュアル のメンテナンス方法

PHPマニュアルのコミット権限を得たら、DocBook を直接編集し、リポジトリにコミットすることが出来ます。  
ここでは、その具体的な方法を示します。

PHPマニュアルのコミット権限を得たい方は、[こちらをまず読んで下さい](https://github.com/php/doc-ja/blob/master/README_About_ThisManual.md)。

## まずはビルドから

まずは PHPマニュアル をビルドする環境を整えなければ始まりません。
それを整える方法は [PHPマニュアル のビルド方法](https://github.com/php/doc-ja/blob/master/README_Building_HOWTO.md) を参照して下さい。

## 購読すべきメーリングリストやリポジトリ

PHPマニュアルのメンテナであれば、以下は最低限購読すべきです。  
これらは、PHPマニュアル の更新のタイミングや、ドキュメントに関する議論の動向をウォッチするために必要です。

- php.net 本家のMLのうち、ドキュメントに関するもの
  * Documentation discussion (&lt;phpdoc at lists.php.net&gt;)
    - phpdoc-subscribe at lists.php.net にメールを出せば購読できます
  * Documentation changes and commits (&lt;doc-cvs at lists.php.net&gt;)
    - doc-cvs-subscribe at lists.php.net にメールを出せば購読できます
      * GitHub 経由のコミットや、それにまつわるコメントなどもこのMLに forward されるので、英語版マニュアルの GitHub は watch する必要は現状ありません
  * Documentation bugs (&lt;doc-bugs at lists.php.net&gt;)
    - doc-bugs-subscribe at lists.php.net にメールを出せば購読できます

- GitHub の 日本語版マニュアルの Watch
  * メンテナであれば、https://github.com/php/doc-ja の `All Activity` を Watch するのが望ましいです。
    - そうすることで、日本語版マニュアルに関する活動をすべてウォッチできます。

- phpdoc ja ML
  * [http://ml.php.gr.jp/mailman/listinfo/php-doc](http://ml.php.gr.jp/mailman/listinfo/php-doc)
    - 日本語のメーリングリストです
    - バグ報告を受け付けていますが、過疎っています...

## PHPマニュアルの構造

PHPマニュアルは、以下のような構造になっています。

```
$ mkdir phpdoc-ja
$ cd phpdoc-ja
$ git clone https://github.com/php/doc-base.git doc-base
$ git clone https://github.com/php/doc-en.git en
$ git clone https://github.com/php/doc-ja.git ja
$ tree -d -L 1
.
├── doc-base
├── en
└── ja
```

- doc-base
  * ドキュメントの共通ファイルやスニペットが入ったもの
- en
  * 英語版PHPマニュアル
    - 各国語版に存在しない未翻訳のファイルは、ここから補います。
- ja
  * 日本語版PHPマニュアル
    - 私達はここを触ります

## 翻訳すべきファイルを俯瞰する方法

revcheck.html というファイルを生成し、お好きなブラウザで開いて確認します。

```
php doc-base/scripts/revcheck.php ja > revcheck.html
```

- `revcheck.html#files` に表示されているファイルが、基本的に更新すべきファイルです。
  * `language-snippets.ent` という、共通のスニペットを格納したファイルだけは例外です。
    - 未訳部分のスニペットも多数含まれているので、リビジョン番号が合っていれば(後述)更新は不要です
- `revcheck.html#untranslated` に表示されているファイルが、未翻訳のファイルです。

## PHPマニュアルを更新するタイミング

PHPマニュアルは、PHPの開発者が必要に応じて、またはドキュメントのバグ修正という形で更新していきます。
更新されるたびに、[ML (Documentation changes and commits)](https://news-web.php.net/php.doc.cvs/) にメールが届きます。それを見て、必要な xml ファイルを更新し、コミットしていきます。

## PHPマニュアルを更新する方法

- A) `revcheck.html` で更新すべきファイルを確認します。
- B) 更新するファイルを任意のエディタで開きます
- C) diff を見ながら、ファイルを更新します
  * `revcheck.html` から、更新すべきファイルの diff のリンクが辿れます。
- D) 日本語版の 以下の `EN-Revision` の部分に記されているハッシュを、英語版のものと合わせます
  * ここと日本語版のリビジョン番号を比較して、`revcheck.html` は更新すべきファイルを判断しているので、必ず行って下さい
    - ルールはシンプルです
      * 日本語版のリビジョンのハッシュが古ければ、更新対象です。
      * 日本語版のリビジョンより英語版のハッシュが古い、または等しければ、更新不要です。

```
<?xml version="1.0" encoding="utf-8"?>
<!-- $Revision$ -->
<!-- EN-Revision: fd95e727f8aa9818d630db6cf0d314b2286dde11 Maintainer: mumumu Status: ready -->
```

- E) 更新が終わったら、以下のコマンドで、ビルドエラーが出ないかを確認します

```
$ php doc-base/configure.php --with-lang=ja --enable-xml-details
```

- F) (オプション) 必要に応じて、マニュアル全体を生成してみて、表示を確認すると良いでしょう
  * 以下のコマンドで、output ディレクトリ以下にマニュアルが生成されます。

```
$ phd -f xhtml -L ja -P PHP -d doc-base/.manual.xml
```

- G) ビルドに問題がなければ、リポジトリにコミットします。

```
$ git add path/to/xxxx.xml
$ git commit
```

## 未訳のファイルを日本語版に追加する方法

`revcheck.html#untranslated` に表示されているファイルが、未翻訳のファイルです。

英語版のマニュアルから、日本語版にファイルをコピーします。

```
$ cp en/path/to/xxxx.xml ja/path/to/xxxx.xml
```

後は、更新する場合とほぼ同じですが、日本語版の xxxx.xml の XML 宣言の後ろに Revision と EN-Revision コメントを付け足して下さい。

```
<?xml version="1.0" encoding="utf-8"?>
<!-- $Revision$ -->
<!-- EN-Revision: fd95e727f8aa9818d630db6cf0d314b2286dde11 Maintainer: mumumu Status: ready -->
```

最後にビルドエラーが出ないかを確認し、コミットします。  
push は必要に応じて任意のブランチに行って下さい。

```
$ php doc-base/configure.php --with-lang=ja --enable-xml-details
$ git addpath/to/xxxx.xml
$ git commit
$ git push origin master
```
