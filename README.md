# PHPマニュアル 日本語版 mirror

このリポジトリは、[PHPマニュアル 日本語版](https://www.php.net/manual/ja/) のソースとなる docbook を github 上に mirror したものです。
この mirror の upstream は以下に置かれています。

http://git.php.net/?p=doc/ja.git

このリポジトリは Pull Request を受け付けるためだけに存在しています。

## PHP マニュアルに間違いを見つけたら？

PHP マニュアルに間違いを見つけた場合、メンテナンスの担当者(メンテナ) へ報告すると修正されます。  

メンテナへ報告する方法は複数ありますが、ここでは github 上で Pull Request を送る方法を示します。

- A) たとえば、以下のページで間違いを見つけたとします。
  * https://www.php.net/manual/ja/oop5.intro.php
- B) 間違っている docbook を github 上で検索して特定する
  * 上記のページの一部分を github の検索窓に入力すると、docbook の候補が複数出てくるはずです。
  * 例: https://github.com/php/doc-ja/search?q=PHP+%E3%81%AB%E3%81%AF%E5%AE%8C%E5%85%A8%E3%81%AA%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%83%A2%E3%83%87%E3%83%AB%E3%81%8C%E6%90%AD%E8%BC%89%E3%81%95%E3%82%8C%E3%81%A6%E3%81%84%E3%81%BE%E3%81%99
- C) 上記で特定した docbook を修正し、Pull Request を出す
  * このリポジトリを fork し、修正する
  * docbook のページの鉛筆のアイコンをクリックし、修正を提案する
    - https://github.com/php/doc-ja/blob/bffc173b11c31f800e39141587b1f4f9d2fc8f95/language/oop5.xml

## メンテナ向けの注意

PHP マニュアルのコミット権限を持つメンテナであっても、このリポジトリに直接 write することは出来ません。
github で pull request を受け付けた場合、以下の手順で upstream となる git.php.net にpush するようにお願いします。

- pull request URL に ".patch" を付け足す
  * 例: https://github.com/php/doc-en/pull/293.patch
- 上記の patch をダウンロードする
  * wget https://patch-diff.githubusercontent.com/raw/php/doc-en/pull/293.patch
- patch をローカルで適用する
  * git am 293.patch
- コミットメッセージに、自動クローズのメッセージを付記してコミットする
  * git commit --am
  * コミットメッセージに "Closes php/doc-en#293" とする
- git.php.net に push する
  * git push origin master
  * 上記のコミットメッセージが github にミラーされ、Pull Request も閉じられる

このフローを面倒だと思った人もいるでしょう。これは [php-src](https://github.com/php/php-src) 向けの現状のメンテナンスフローと同じです。
php-src では、複数のブランチから複雑なマージや rebase を経てメンテナンスが行われているため、上記でも問題になっていません。

PHP マニュアルの場合は、php-src よりももう少し緩い、自動化されたフローが検討されています。
