# PHPマニュアル 日本語版 用語集

ここには、PHP マニュアル 日本語版で「統一した」訳語を当てている単語を記録しています。  
以下の単語の訳がブレていたら、issue または Pull Request で報告してください。

機械的に検出できる訳語・表記（長音の有無など）は [build/prh.yml](build/prh.yml) で管理しており、CI（Textlint）で検出されます。

- visibility
  * 「アクセス権」で統一
  * protected/private/public を付けた、メソッドやプロパティが可視な範囲のこと
  * 但し、「非対称可視性プロパティ」(Asymmetric Property Visibility)は 例外
- extension
  * 拡張モジュール ( [#24](https://github.com/php/doc-ja/issues/24) )
- internal function / builtin function
  * 内部関数 / ビルトイン関数
    - 実際には同じ意味だが、英語版でも別々に使われている
- coercive mode
  * 自動変換モード
    - strict モードと対になるモード
    - strict モードの対比の文脈で、coercive を「強制する」と訳さない
- language construct
  * 言語構造
- nullable
  * nullable のままにする。訳さない。
    - null を受け入れる何か、という意味だが、PHP マニュアル日本語版では「訳さない」で統一。
- numeric string
  * 数値形式の文字列
- preload
  * opcache の文脈の場合、「事前ロード」で統一
- userland
  * 関数の文脈では、「PHP でユーザーが使える」関数
    - ユーザーに公開されている関数、ということ
- Standard
  * 移行ガイドの文脈での Standard は「標準ライブラリ」で統一する
    - php-src で言うところの ext/standard に入っている関数全てを指す
    - Standard PHP Librady (SPL) は別にあるが、「標準ライブラリ」でいいことにする
- parameters / arguments
  * 原則として「引数」に統一
    - 「パラメータ」「引数」の訳し分けは不要（原文の時点で基準なく揺れている）
  * 区別が必要な場面では「仮引数」「実引数」
    - 仮引数 (parameter): 関数やメソッドの定義での宣言
      * 参考: https://developer.mozilla.org/ja/docs/Glossary/Parameter
    - 実引数 (argument): 呼び出し側が渡す値
      * 参考: https://developer.mozilla.org/ja/docs/Glossary/Argument
    ```php
    // $parameters は仮引数
    function test(array $parameters) {}
    // [1234] は実引数
    test([1234]);
    ```
  * 本ルールは新たな訳文のみへ適用
    - 既存の訳文の「パラメータ」をこの方針だけのために書き換える必要はない
  * 本ルールは関数の文脈での parameter / argument にのみ適用
    - ini 設定・SQL のバインド・URL のクエリなど、関数以外の文脈は対象外
- override (OOP)
  * 「オーバーライド」で統一 ( [#26](https://github.com/php/doc-ja/issues/26) )
    - 継承の文脈（メソッド、プロパティ、定数の再定義）では「上書き」を使わない
    - 「上書き」はファイルや設定値、配列の値を書き換える文脈 (overwrite) でのみ使う
