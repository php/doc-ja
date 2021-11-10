# PHP マニュアルの改善方法

PHP マニュアルに興味を持って頂き、ありがとうございます。  
改善方法は複数あります。状況に応じて、以下に示す方法で御対応をお願い致します。

## Pull Request を送る場合

マニュアルの日本語訳に問題があり、Pull Request を送ることで修正可能な場合は、以下のやり方で修正箇所を特定して Pull Request を送って下さい。

- A) たとえば、以下のページで間違いを見つけたとします。
  * https://www.php.net/manual/ja/oop5.intro.php
- B) 間違っている docbook を github 上で検索して特定する
  * 上記のページの一部分を github の検索窓に入力すると、docbook の候補が複数出てくるはずです。
    - 日本語で検索したほうが特定しやすいと思います。
  * 例: https://github.com/php/doc-ja/search?q=PHP+%E3%81%AB%E3%81%AF%E5%AE%8C%E5%85%A8%E3%81%AA%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%83%A2%E3%83%87%E3%83%AB%E3%81%8C%E6%90%AD%E8%BC%89%E3%81%95%E3%82%8C%E3%81%A6%E3%81%84%E3%81%BE%E3%81%99
- C) 上記で特定した docbook を修正し、Pull Request を出す
  * このリポジトリを fork し、修正する
  * または、docbook のページの鉛筆のアイコンをクリックし、修正を提案する
    - 例: https://github.com/php/doc-ja/blob/master/language/oop5.xml
- D) Pull Request の内容について
  * Pull Request を日本語で送っても全く問題ありません。
  * また、コミットログに日本語を書いても全く問題ありません。
    - 過去のコミットログは英語になっています
      * メンテナが英語版とコミットの粒度を合わせているから、という以上の理由はありません。

## issue で問題を報告する場合

マニュアルに 「何かしらの問題があるが、修正方法がわからない場合」 は、[issue に登録をお願いします](https://github.com/php/doc-ja/issues/new)

- 但し、[既に報告された内容がないかどうか](https://github.com/php/doc-ja/issues?q=is%3Aissue+) を必ず確認して下さい。
- 以下のような問題を登録することを想定しています
  * 未訳のドキュメントがあり、日本語訳を追加して欲しいという要望
  * 日本語版に関する既知の問題
    - ドキュメント化されていない機能がある、など
  * その他、日本語版で修正されていない問題があるものの、修正方法がわからないもの
- Pull Request と同じく、日本語で報告しても全く問題ありません。

## 未訳部分の翻訳を追加する場合

メンテナが inactive になったり、[master になっている英語版](https://github.com/php/doc-en) の更新ペースに追いつけなくなったり、需要を掴みきれていない等の理由で、日本語で読みたい部分が大量に未翻訳だったりするかもしれません。

それが一定の量にのぼる場合は、以下のやり方で未訳部分の翻訳を纏めて Pull Request するのが良いと思います。

- A) たとえば、FFI のマニュアルを翻訳したいとします
  * https://www.php.net/manual/en/book.ffi.php
- B) 未翻訳部分の docbook を、英語版のリポジトリで検索して特定する
  * 上記のページの一部分を github の検索窓に入力すると、大体どこらへんを翻訳したらよいかがわかるはずです
    - 例: https://github.com/php/doc-en/search?q=ffi
  * PECL 拡張モジュールの場合は、[/reference 以下](https://github.com/php/doc-en/tree/master/reference) のどこかになるはずです
- C) このリポジトリをforkし、以下のやり方で英語版から未訳ファイルを追加する

```
$ mkdir phpdoc-ja
$ cd phpdoc-ja
$ git clone https://github.com/php/doc-en.git en
$ git clone https://github.com/[you]/[your-forked-doc-ja].git ja
$ tree -d -L 1
.
├── en
└── ja
$ cp -R en/reference/ffi ja/reference/
```

- D) ja/reference/ffi/ 以下を翻訳して push し、このリポジトリに対して Pull Request を送る
  * [英語版の Revision 情報を追加しなければいけないという作法](https://github.com/php/doc-ja/blob/master/README_Maintain_HOWTO.md#%E6%9C%AA%E8%A8%B3%E3%81%AE%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%82%92%E6%97%A5%E6%9C%AC%E8%AA%9E%E7%89%88%E3%81%AB%E8%BF%BD%E5%8A%A0%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95) はありますが、Pull Request を送る段階では必須ではないと思います
    - メンテナがおそらく、後から追加してくれるでしょう
