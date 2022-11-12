# PHPマニュアル 日本語版 用語集

ここには、PHP マニュアル 日本語版で「統一した」訳語を当てている単語を記録しています。  
以下の単語の訳がブレていたら、issue または Pull Request で報告してください。

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
- unserialize
  * アンシリアライズ ( [#21](https://github.com/php/doc-ja/issues/21) )
    - 「デシリアライズ」や「アンマーシャリング」にはしない
- nullable
  * nullable のままにする。訳さない。
    - null を受け入れる何か、という意味だが、PHP マニュアル日本語版では「訳さない」で統一。
- serialize
  * シリアライズ / シリアル化
    - 「マーシャリング」にはしないこと
- メソッドや変数に付ける static
  * static メソッド / static 変数 とする ( [#45](https://github.com/php/doc-ja/issues/45 ), [#46](https://github.com/php/doc-ja/issues/46) )
    - 静的変数や静的メソッドなどとはしない
- numeric string
  * 数値形式の文字列
- preload
  * opcache の文脈の場合、「事前ロード」で統一
- userland
  * 関数の文脈では、「PHP でユーザーが使える」関数
    - ユーザーに公開されている関数、ということ
- throw Exception
  * 例外をスローする
    - 例外を「投げる」とはしない
    - Throwable を throw するという文脈ではすべてこれに統一する
