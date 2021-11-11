# PHPマニュアル 日本語版

このリポジトリは、[PHPマニュアル 日本語版](https://www.php.net/manual/ja/) のソースとなる docbook を管理するリポジトリです。

## PHP マニュアルに間違いを見つけたら？

PHP マニュアルに間違いや問題を見つけた場合、メンテナンスの担当者(メンテナ) へ報告すると、修正などの対応が行われます。  

[メンテナへ報告する方法は複数あります](https://github.com/php/doc-ja/blob/master/README_About_ThisManual.md#php-%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB-%E3%81%AB%E9%96%93%E9%81%95%E3%81%84%E3%82%92%E8%A6%8B%E3%81%A4%E3%81%91%E3%81%9F%E3%82%89)が、github で報告する場合、Pull Request を送るか、issue で報告するかの対応をお願いします。

詳細は [https://github.com/php/doc-ja/blob/master/CONTRIBUTING.md#php-%E3%83%9E%E3%83%8B%E3%83%A5%E3%82%A2%E3%83%AB%E3%81%AE%E6%94%B9%E5%96%84%E6%96%B9%E6%B3%95](https://github.com/php/doc-ja/blob/master/CONTRIBUTING.md) を参照して下さい。

## 翻訳を追加したい人へ

PHP マニュアルの翻訳は、言語機能と、PHP に同梱されている拡張機能以外については基本メンテナンスしない方針です。

未翻訳部分の翻訳を追加したい場合は、[未訳部分の翻訳を追加する場合](https://github.com/php/doc-ja/blob/master/CONTRIBUTING.md#%E6%9C%AA%E8%A8%B3%E9%83%A8%E5%88%86%E3%81%AE%E7%BF%BB%E8%A8%B3%E3%82%92%E8%BF%BD%E5%8A%A0%E3%81%99%E3%82%8B%E5%A0%B4%E5%90%88) を参照して下さい。

## メンテナに興味がある人へ

PHP マニュアルのメンテナは、以下を行います。

* [英語版のコミット](https://github.com/php/doc-en/commits/master) を翻訳し、日本語版に反映させる
* このリポジトリの Pull Request や issue に対応する

PHP マニュアルのメンテナンスに興味がある方は、[PHP マニュアル 日本語版について](https://github.com/php/doc-ja/blob/master/README_About_ThisManual.md) をお読み頂き、必要なアクションを取って下さい。

## メンテナ向けの注意

元々 PHP Manual の docbook は git.php.net で管理されていましたが、[php-src](https://github.com/php/php-src) にバックドアを仕込むコミットがなされた事案が発生したことから、2021/03/29 より、github で直接管理されることになりました。

そのため、git.php.net にミラーするための特別な作法も不要になっています。github でソースコードを管理する作法で、もろもろ作業頂いて問題ありません。
