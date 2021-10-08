# PHPマニュアル のビルド方法

PHPのマニュアルは、DocBook と呼ばれるフォーマットで記述されており、[PhD という PHPマニュアル のためのツール](https://wiki.php.net/doc/phd) によってその DocBook から HTML や CHM、PDF などの複数の形式にビルドできる。

この記事では、実際の PHPマニュアル をリポジトリから取ってきてビルドする方法を紹介する。PhD は PDF や manpage形式、epub 等多様な形式がビルドできるが、ここでは HTML および chm のみについて触れる。

## a) ビルドするときに使うPHPについて

まず、PHP をインストールしなければはじまらない。  
PHP 5.3 以降であれば、HTML 版も chm も問題なくビルドできるはずだ。

PHP をインストールするときも、PhD のために DOM, libXML2, XMLReader, SQLite3 は有効にしていなければならない。ただ、これらは デフォルトで有効になっているので、無効にしないよう注意しよう。

かつ、7.4.0 以降は非推奨になっている PEAR コマンドをインストールする必要がある。それには、PHP を `--with-pear` オプションを付けてコンパイルするか、[PEAR マニュアル](https://pear.php.net/manual/en/installation.getting.php) にもある通り、以下のように go-pear.phar を用いる必要がある。

```
$ wget http://pear.php.net/go-pear.phar
$ php go-pear.phar
```

## b) PhD をインストール(git 経由)

git と PEAR を予めインストールしておいて、PhD と `PhD_PHP` をpearコマンド経由でインストール(\*1)する。  
`PhD_PHP` は chm をビルドするのに必要だ。

git と PHP をインストールしておいて、以下のコマンドでインストールすると良い。
但し、途中で指定する XML の api, release タグの記述が PEAR コマンドに合わないため、[patch が必要](https://gist.github.com/mumumu/b2b77b15e702bc24a5233acc98ac913a) な点に注意すること。

```
$ git clone https://github.com/php/phd.git
$ cd phd
$ wget https://gist.githubusercontent.com/mumumu/b2b77b15e702bc24a5233acc98ac913a/raw/b6de89e378296d6f0bfa4e21d564ebf85a539ff5/phd_package_xml.patch
$ patch -p1 < phd_package_xml.patch
$ pear config-set preferred_state devel
$ pear install package.xml package_generic.xml package_php.xml
```

(\*1) PhD は composer にも対応しているが、依存ライブラリとして何かをすることはないので、PEAR 経由でのインストールが現状は良い... のだが、既に述べた通り、PEAR が PHP 7.4 からデフォルトで入らなくなってしまったので悩ましい  

## b-1) PhD をインストール(PEAR チャンネル経由: 非推奨)

念の為述べておくが、PEAR チャンネル経由でも PhD はインストール可能だ。だが、PhD はもう3年近くリリースが行われておらず、PHP 8.0.0 以降に取り込まれた union 型などの新しいシグネチャをマニュアルで表現することが不可能になっている。

そのため、PEAR チャンネル経由の PhD のインストールは推奨しないし、ここでも説明しない。

## c) マニュアルのソースをリポジトリから取得

次にマニュアルのソースをリポジトリから取ってくる。作業用のディレクトリを作って、リポジトリを git からチェックアウトする。

```
$ mkdir phpdoc-ja
$ cd phpdoc-ja
$ git clone https://github.com/php/doc-base.git doc-base
$ git clone https://github.com/php/doc-en.git en
$ git clone https://github.com/php/doc-ja.git ja
```

## d) HTML版の PHPマニュアルをビルドする

--enable-xml-details は、XMLに万が一文法エラーがあったときに細かい情報を出力するためのモノだ。また、phd は結構メモリを使うので、`memory_limit` の値を大きめにしておいた方がよいかもしれない。

```
$ php doc-base/configure.php --with-lang=ja --enable-xml-details
$ phd -f xhtml -L ja -P PHP -d doc-base/.manual.xml
```

成功すれば、 output ディレクトリ以下にマニュアルが生成される。

## e) chm 版の PHPマニュアルをビルドする

以下のコマンドで何も考えなくても chm 版をビルドできる。--enable-chm は、chm特有のコンテンツを生成物に含めるために必要だ。 また、--with-lang や -L オプションで言語の指定も忘れずに。

まあ、--enable-chm がなくても、chm特有のヘルプコンテンツが入らないだけで、皆が見たいメインのコンテンツは欠落しないので、問題はないのだけれども。

```
$ php doc-base/configure.php --enable-chm --with-lang=ja
$ phd -f chm -P PHP -L ja -d doc-base/.manual.xml
```

成功すると、output/php-chm 以下に chm のコンテンツが生成される。

```
$ ls output/php-chm/
php_manual_ja.hhc  php_manual_ja.hhk  php_manual_ja.hhp  res
```

chm 形式のファイルは LZX 形式で圧縮されており、Linux や Mac では chm 形式は生成できないので、以下、Windows 上で chm ファイルをコンパイルする必要がある。

ここからは Windows での作業だ(\*1) 。まず、[HTML Help Workshop](http://msdn.microsoft.com/en-us/library/ms669985.aspx) をインストールし、 `output/php-chm/php_manual_ja.hhp` を File -> Open で開く。

その後、File -> Compile を 選択し、 `php_manual_ja.hhp` をダイアログで選択し、OK を押すと `php_manual_ja.hhp` がある フォルダに `php_manual_ja.chm` が生成されるはずだ(\*2)。

(\*1) Windows 10 および、Windows Server 2016 で確認している  
(\*2) 実は、この手順で chm を生成すると、chm の検索が機能しない。きちんと機能させるためには、DBCSFix.exe というアジア系言語のためのバッチを適用し、適切なロケールで HTML Help Compiler を起動して生成する必要がある。これらをWindowsのビルド環境で手当するのは少し大変なので、そこまで手当した生成物が欲しい場合は、[php.net から取得](http://www.php.net/download-docs.php) したほうが良い。詳細を知りたい場合は、[バッチプログラムのソースコード](http://svn.php.net/viewvc/phpdoc/doc-base/trunk/scripts/build-chms.php?revision=333535&view=markup) を読んでみよう
