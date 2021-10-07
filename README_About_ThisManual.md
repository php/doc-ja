# PHP マニュアル 日本語版について

ここでは、PHPを使うと必ず一度は目にするであろう [PHPマニュアル](https://www.php.net/manual/ja/) について記していきます。
PHPマニュアルのメンテナンスの前提となる基本知識や、修正方法などについて記していきます。

## この文書の著者 

[mumumu](https://twitter.com/mumumu) です。PHPマニュアル のメンテナの一人です。

## 基本知識

PHPマニュアル はPHP 5系から現在 (このエントリが更新されている時の最新は 8.0.11) に至るまでの歴史が蓄積されており、非常に巨大なマニュアルです。これは [DocBook](http://www.docbook.org/) を使って書かれており、それを適宜各ロケールの翻訳者がボランティアで英語以外の各国語に置き換えていっています。それが php.net のインフラでビルドされ、1日に1回 (正確には毎日午後3時 JST) 世界中に公開されていくという具合です。

Docbook は、SGML 由来であることによって文書構造が複雑であることや、タグの構造が壊れてしまうと即ビルドが失敗してしまうなどの欠点によって、他のフォーマットに置き換えようという話がこれまで出なかったわけではありません。ですが、DocBook の多彩な表現力にとってかわることと、現在までの巨大な蓄積を効率的に置き換えられる代替案を誰かが示せない限り、移行していくことはないでしょう。

PHPマニュアルは 長らく [Subversion](http://subversion.apache.org/) で管理されてきましたが、4年以上に渡る議論や作業の末、2020年末に [git](https://git-scm.com/) へ移行しました。その成果として、[github 経由](https://github.com/php/doc-ja) でもバグ報告が可能になっています。

## PHP マニュアル に間違いを見つけたら？

既に述べたとおり、PHP マニュアル はボランティアベースで作られているため、常に完全な翻訳を維持できているわけではありません。現在でもたくさんの未訳部分が残っていますし、人間がやるモノである以上、常に間違いが存在し得ます。

間違いを見つけた場合には、どこに問い合わせればよいでしょう？ 複数の選択肢がありますが、私のおすすめの順に以下に選択肢を示します。

### 1. github

修正内容はコードで語りたい、という方は、github がお勧めです。2020年12月末から、PHPマニュアル は git で管理されるようになり、github 経由でもバグ報告を行うことが可能になりました。

報告のやり方は、 [github の README.md](https://github.com/php/doc-ja/blob/master/README.md) を参照して下さい。  
リポジトリそのものは、下記にあります。

https://github.com/php/doc-ja

### 2. PHPユーザーズ Slack

[日本語でPHPの雑談をするための Slackチーム](https://phpusers-ja.slack.com/) が存在します。そこに #phpmanual というチャンネルがあり、PHPマニュアル のメンテナも join しており、直接話すことが可能になっています。

メンテナが時々つぶやいたりもしていますし、間違いの指摘や、これを翻訳して欲しい！などの要望も日本語で可能です。

参加方法は [Slackin](https://slackin-phpusers-ja.herokuapp.com/) から join するか、[日本語で PHP の話をする Slack のグループを作ったよ](https://www.msng.info/archives/2016/02/phpusers-ja-on-slack.php) を参照して下さい。

### 3. 日本PHPユーザー会 の ML

[日本 PHP ユーザー会](http://www.php.gr.jp) では [php-doc ML](http://ml.php.gr.jp/mailman/listinfo/php-doc) というメーリングリストをホストしており、ここを通じて PHPマニュアルに関する問い合わせや間違いの指摘などを受け付けています。ここで頂く多くの情報が、PHP マニュアル 日本語版の質の向上に大きく寄与していることは言うまでもありませんし、初期の頃からの多くの方々の協力によって現在のマニュアルは存在し、かつ維持されています。

### 4. bugs.php.net

[PHP のバグトラッカー](http://bugs.php.net/) で Documentation Problem と記して英語でバグ報告をするのもアリです。
とはいえ、インターフェイスが英語で、英語版のメンテナも見ているものなので、英語で報告するのが望ましいのが弱点です。

## PHP マニュアル の様々なフォーマット

PHPマニュアル は XHTML や Windows の標準的なヘルプ形式である [chm](http://ja.wikipedia.org/wiki/Microsoft_Compiled_HTML_Help) に対応したフォーマットが公開されていますが、Docbook からこれらの形式をビルドするための [PhD](https://github.com/php/phd) というツールが整備されています。

PhD を使えばHTML形式のビルドは行えるようになっていますが、chm 形式については、それをビルドするのに Windows マシンの助けが必要です。PHP マニュアル のビルド方法については、以下に纏めておいたので参考にしてください。

[PHPマニュアル のビルド方法](https://github.com/php/doc-ja/blob/master/RREADME_Building_HOWTO.md)

## PHPマニュアル のコミット権限を得るには？

PHPマニュアルをいろいろ見ていくと、継続して改善すべきだというモチベーションが強まってくるかもしれません。Slack や PHP-doc ML で指摘しまくっていてそれにも飽き足らないという人は、コミット権限を得て自分で直すことも考えてもよいかもしれません。以下は、そういうモチベーションが高い人向けです。

PHPマニュアルのコミット権限を得るには、[php.net のページで英語で申請をする](http://www.php.net/git-php.php) 必要があります。これを php.net の中の人が見てコミット権限を与えるかを決めているわけですが、彼らは何回か patch を提出した実績か、もしくは既存のコミッタの推薦があることを求めて来ます。patch については日本語版の PHP マニュアル の patch でも問題ないはずです。

基本的には [PHPユーザーズ Slack](https://phpusers-ja.slack.com/) や [php-doc ML](http://ml.php.gr.jp/mailman/listinfo/php-doc) に話を通してから申請し、既存の PHP マニュアル 日本語版のコミッタからの推薦を得た方が早く話が進むと思います (自分も php-doc ML 経由で [高木さん](http://d.hatena.ne.jp/takagimasahiro) の推薦を貰いました) 。

尚、申請ページでは、最初から最後までちゃんと文章を読んでから申請フォームを埋めないと **必ず失敗するようになっています** ので気を付けてください。

PHPマニュアルのコミット権限を得たら、DocBook を直接編集し、リポジトリにコミットすることが出来ます。  
具体的な方法は、以下を参照して下さい。

[メンテナ向け: PHPマニュアル のメンテナンス方法](https://github.com/php/doc-ja/blob/master/README_Building_HOWTO.md)
