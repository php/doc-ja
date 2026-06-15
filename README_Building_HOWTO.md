# PHPマニュアル のビルド方法

PHPのマニュアルは、DocBook と呼ばれるフォーマットで記述されており、[PhD という PHPマニュアル のためのツール](https://wiki.php.net/doc/phd) によってその DocBook から HTML や chm、epub などの複数の形式にビルドできる。

この記事では、実際の PHPマニュアル をリポジトリから取ってきてビルドする方法を紹介する。PhD は manpage 形式や epub 等、多様な形式がビルドできるが、ここでは HTML および chm のみについて触れる。

## a) ビルドするときに使うPHPについて

まず、PHP をインストールしなければはじまらない。  
現在の PhD は PHP 8.1 以降で動作する。新しめの PHP を入れておけば、HTML 版も chm も問題なくビルドできるはずだ。

PHP をインストールするときは、PhD のために DOM, libXML2, XMLReader, SQLite3 を有効にしておかなければならない。ただ、これらは デフォルトで有効になっているので、無効にしないよう注意しよう。

## b) PhD とマニュアルのソースを取得する

ビルドには次の 4 つのリポジトリが必要になる。作業用のディレクトリを作り、その中にまとめてクローンしよう。

```
$ mkdir phpdoc-ja
$ cd phpdoc-ja
$ git clone https://github.com/php/doc-base.git doc-base
$ git clone https://github.com/php/doc-en.git en
$ git clone https://github.com/php/doc-ja.git ja
$ git clone https://github.com/php/phd.git phd
```

- `doc-base` … 各言語のソースを 1つの XML にまとめ、検証するためのツール群
- `en` … 英語版のマニュアルソース。日本語に翻訳されていない箇所は英語版が使われるため、日本語版のビルドにも必要
- `ja` … 日本語版のマニュアルソース
- `phd` … DocBook を HTML や chm へ変換するレンダラ

以降のコマンドは、この `phpdoc-ja` ディレクトリの中で実行する。

## c) HTML版の PHPマニュアルをビルドする

まず `doc-base/configure.php` で、各リポジトリのソースを 1つの XML (`.manual.xml`) にまとめる。`--with-lang=ja` で日本語版を指定する。`--enable-xml-details` は、XML に万が一文法エラーがあったときに細かい情報を出力するためのモノだ。

```
$ php doc-base/configure.php --with-lang=ja --enable-xml-details
```

続いて PhD の `render.php` で HTML を生成する。phd は結構メモリを使うので、`memory_limit` の値を大きめにしておいた方がよいかもしれない。

```
$ php phd/render.php -f xhtml -P PHP -d doc-base/.manual.xml
```

成功すれば、`output/php-chunked-xhtml/` 以下にマニュアルが生成される。その中の `index.html` をブラウザで開けば閲覧できる。

## d) chm版の PHPマニュアルをビルドする

chm 版も流れは同じだ。`configure.php` に `--enable-chm` を付けると、chm特有のコンテンツが生成物に含まれる。`--with-lang` や `-L` オプションでの言語指定も忘れずに。

まあ、`--enable-chm` がなくても、chm特有のヘルプコンテンツが入らないだけで、皆が見たいメインのコンテンツは欠落しないので、問題はないのだけれども。

```
$ php doc-base/configure.php --enable-chm --with-lang=ja
$ php phd/render.php -f chm -P PHP -L ja -d doc-base/.manual.xml
```

成功すると、`output/php-chm` 以下に chm のコンテンツが生成される。

```
$ ls output/php-chm/
php_manual_ja.hhc  php_manual_ja.hhk  php_manual_ja.hhp  res
```

chm 形式のファイルは LZX 形式で圧縮されており、Linux や Mac では chm 形式は生成できないので、以下、Windows 上で chm ファイルをコンパイルする必要がある。

ここからは Windows での作業だ(\*1) 。まず、[HTML Help Workshop](http://msdn.microsoft.com/en-us/library/ms669985.aspx) をインストールし、 `output/php-chm/php_manual_ja.hhp` を File -> Open で開く。

その後、File -> Compile を 選択し、 `php_manual_ja.hhp` をダイアログで選択し、OK を押すと `php_manual_ja.hhp` がある フォルダに `php_manual_ja.chm` が生成されるはずだ(\*2)。

(\*1) Windows 10 および、Windows Server 2016 で確認している  
(\*2) 実は、この手順で chm を生成すると、chm の検索が機能しない。きちんと機能させるためには、DBCSFix.exe というアジア系言語のためのバッチを適用し、適切なロケールで HTML Help Compiler を起動して生成する必要がある。これらをWindowsのビルド環境で手当するのは少し大変なので、そこまで手当した生成物が欲しい場合は、[php.net から取得](https://www.php.net/download-docs.php) したほうが良い。詳細を知りたい場合は、[バッチプログラムのソースコード](https://github.com/php/doc-base/blob/master/scripts/build-chms.php) を読んでみよう
