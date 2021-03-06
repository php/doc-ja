# PHPマニュアル 日本語版

このリポジトリは、[PHPマニュアル 日本語版](https://www.php.net/manual/ja/) のソースとなる docbook を管理するリポジトリです。

## PHP マニュアルに間違いを見つけたら？

PHP マニュアルに間違いを見つけた場合、メンテナンスの担当者(メンテナ) へ報告すると修正されます。  

[メンテナへ報告する方法は複数あります](https://gist.github.com/mumumu/8464d879ccb939365d729cda242dbf14#php-%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB-%E3%81%AB%E9%96%93%E9%81%95%E3%81%84%E3%82%92%E8%A6%8B%E3%81%A4%E3%81%91%E3%81%9F%E3%82%89)が、ここでは github 上で Pull Request を送る方法を示します。

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

## メンテナ向けの注意

元々 PHP Manual の docbook は git.php.net で管理されていましたが、[php-src](https://github.com/php/php-src) にバックドアを仕込むコミットがなされた事案が発生したことから、2021/03/29 より、github で直接管理されることになりました。

そのため、git.php.net にミラーするための特別な作法も不要になっています。github でソースコードを管理する作法で、もろもろ作業頂いて問題ありません。
