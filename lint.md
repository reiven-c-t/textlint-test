

# 読みやすい文章を書くための日本語添削ツール導入: textlint編

ブログやレポートなどの文章を書くとき、なんかしっくりこないことってありますよね?

そんな時に、Markdown形式の文章を簡単にチェックしてくれるツールを紹介します.

特にこの記事では、主にIT系の記事を書くブロガーが、記事アップロード前にMarkdown形式で書いた自分の文章を
ローカル環境でチェックするためにtextlintを使う際のお進めpackageとその設定を紹介します.


Markdown形式については、こちらの記事をどうぞ.

[a url="" title=""]

## 私の(あなたの)文章が読みにくい理由

ブログやレポートの文章を書き終えて、自分の文章を見て見ると、.

- 「表記に違和感がある」
- 「文章がつい長くなる」
- 「WordPressやword pressみたいに表記が揺れている」

そんなことってありませんか?

文章を書く時、とりあえずだら〜っと文章を書いて、後から読み返して見ると、そういういうことがよくあります.

上のような問題を、プログラムで解決し、文章の質を上げる方法を紹介します.

## 文章構成ツールとは

最近だとプロの物書き以外でも、ブログやSNSなどで文章を書く機会が多いでしょう.

プロの物書きなら、担当の編集などに、文章をチェックしてもらえるかもしれません。
しかし、普通、ブログやSNSに、個人が文章を投稿する際、プロから文章のチェックを受けることは難しいでしょう.

そんな時、上で挙げたような「表記の違和感」「文章の長さ」などをプログラムで簡単にチェックできれば、
文章をよりよくできるでしょう.


そこで、この記事では技術系のレポートやブログを書く際役に立つ、文章の添削ツールの導入方法を紹介します.

現在よく用いられている、日本語の添削ツールには、textlintとRedPenの2種類があります.

この記事では、textlintを実際に使える状態にするまでの導入方法を紹介します.


### 日本語校正ツールtextlintとは

textlintとは、JavaScript(Node.js)で動く英語・日本語向けの文章添削ツールです。
主にMarkdown形式のテキストを添削・自動修正してくれます.

作者も日本の方のようです.

[a url="http://efcl.info/2015/09/10/introduce-textlint/" title="textlint作者のページ"]

textlintの特徴として、必要な機能を自分で選択してインストールできるという点があります。
ただ、この点が結構面倒で、textlintをインストールしただけでは使えません。
自分で、機能をインストールしないといけません.

この記事では、主にIT系の記事を書くブロガーが、ブログアップロード前に自分の文章を
ローカル環境でチェックするためにtextlintを使う際のお進めpackageと設定を紹介します.

なにはともあれ、まずtextlintをインストールしましょう。
textlintはNode.jsを使って動いているので、まず、Node.jsをインストールします。
インストールのしかたはこちらをどうぞ.

[a url="https://liginc.co.jp/Web/programming/Node.js/85318" title="Node.js"]

Node.jsをインストールした後、Macならターミナル、Windowsならコマンドプロンプト、Linuxなら端末から、.

npm i -g textlint

で、textlintをインストールしてください.

これで、textlint自体のインストールが終わりました.

次に、textlintのお進めのパッケージです.

文章添削として、欲しい機能として次のものを想定します.

- 技術用語が間違っていたら指摘・修正
- タイトル文字に関して字数を超えていたら修正
- 文章に過剰な句点が含まれていた際に指摘
- 全角・半角アルファベットが混在していたら指摘・修正
- 文章中に不自然なアルファベットが存在したら指摘・修正
- 括弧記号の手前に句読点がある場合指摘・修正
- 連続した三点リーダーの数が偶数でなければ指摘・修正
- 連続したダッシュ(-)記号の数が偶数でなければ指摘・修正
- 連続した句読点()が存在したら指摘
- 連続した中黒(・)が存在したら指摘
- 連続した長音符(ー)が存在したら指摘
- 表記揺れを検査

以上の機能をざっくり簡単にインストールし、簡単に使う方法を紹介します.

インストールするパッケージとしては、.

- textlint-rule-spellcheck-tech-word(技術用語修正)
- textlint-rule-preset-ja-technical-writing(日本語技術用語修正)
- textlint-rule-max-length-of-title(タイトル文字数チェック)
- textlint-rule-max-comma(文章内の句読点の個数チェック)
- textlint-rule-no-mixed-zenkaku-and-hankaku-alphabet(全角・半角アルファベットの指摘)
- textlint-rule-ja-unnatural-alphabet(不自然なアルファベットチェック)
- textlint-rule-general-novel-style-ja(日本語小説スタイル準拠の確認)
- textlint-rule-prh(表記揺れ修正)

です.

コードとしては、npm i -g textlint textlint-rule-spellcheck-tech-word textlint-rule-preset-ja-technical-writing textlint-rule-max-length-of-title textlint-rule-max-comma textlint-rule-no-mixed-zenkaku-and-hankaku-alphabet textlint-rule-ja-unnatural-alphabet textlint-rule-general-novel-style-ja textlint-rule-prh

とターミナルなどに入力し、enterで実行するだけです。
上のコマンドでは
npm i -g
としていますが、-gはグローバルを意味しており、
-gをつけることでPCのどのフォルダからも使えます.

逆に-gをつけなければ、インストールしたフォルダからしかtextlintは使えません.

Node.js界隈は開発速度が早いので、どんどん新しいパッケージが出ますが、
そのぶん依存関係が複雑になりがちです.

ですので、上のような-gとそうでない一部のフォルダのみでの使用など細かく別れていてややこしいですよね.

あるいは、下のpackage.jsonをDLし、DLしたディレクトリにターミナルなどでアクセスし、.

npm install 
場合によっては、
sudo  npm install.

すると、そのディレクトリのみではありますが、textlintを実行できます.

サンプルとして、testという名前のフォルダに、lint.mdというマークダウン形式で書いた添削したい文書を保存しておきます.

この実行環境一式をそろえたzipファイルをこちらに置いておきます。テストしたい場合はどうぞ.

textlintの使い方ですが、ターミナルなどで、
textlint --rule {使いたいパッケージ} --rule {使いたいパッケージ} {添削したいファイルのパス}
で実行できます。
なお、パッケージ名は、たいていtextlint-rule-...と始まりますが、使いたいパッケージ名を指定する際は、
textlint-rule-を省略できます。
なので、たとえばtextlint-rule-spellcheck-tech-wordを使う場合、
--rule spellcehck-tech-word
と書けます.

とりあえず、
testフォルダにターミナルなどでアクセスし、
textlint --rule spellcheck-tech-word lint.md
と実行してみてください。
いっぱいエラーが出るはずです(笑).

さて、ここまで一応textlintやそのパッケージをインストールし終えたわけですが、
ここからtextlintを便利に使う方法を紹介します.

## textlintを便利に使う:textlintの設定ファイル編

textlintを使用するときに、
--rule {使いたいパッケージ}
と毎回指定するのは面倒ですよね?

そこで、このrule指定を環境ファイルにし、textlint起動時に自動で読み込む方法を紹介します.

まず、textlintで添削したいファイルがあるフォルダに
.textlintrcという名前のテキストファイルを作成します.

textlintrcというファイルでは、JSON記法を用いて、
使用したいルールや、ルールの調整を指定できます。
たとえば、次のようにルール指定できます。
{
  "rules": {
    "spellcheck-tech-word": false,
    "max-length-of-title": {
    "#": 25,
    "##": 30
    },
    "max-comma": {
        "max" : 3
    },
    "preset-ja-technical-writing": true,
    "no-mixed-zenkaku-and-hankaku-alphabet": true,
    "ja-unnatural-alphabet": true,
    "ja-hiragana-fukushi": true,
    "general-novel-style-ja": {
      // 各段落の先頭に許可する文字 (false: チェックしない)
      "chars_leading_paragraph": false,
      // 閉じ括弧の手前に句読点()を置かない
      "no_punctuation_at_closing_quote": true,
      // 疑問符(？)と感嘆符(！)の直後にスペースを置く
      "space_after_marks": true,
      // 連続した三点リーダー(……)の数は偶数にする
      "even_number_ellipsises": true,
      // 連続したダッシュ(――)の数は偶数にする
      "even_number_dashes": true,
      // 連続した句読点()を許可しない
      "appropriate_use_of_punctuation": true,
      // 連続した中黒(・)を許可しない
      "appropriate_use_of_interpunct": true,
      // 連続した長音符(ー)を許可しない
      "appropriate_use_of_choonpu": true,
      // マイナス記号(ー)は数字の前にしか許可しない
      "appropriate_use_of_minus_sign": true,
      // アラビア数字の桁数は2桁まで (false: チェックしない)
      "max_arabic_numeral_digits": false
    },
    "prh": {
      "rulePaths" :["/usr/local/lib/node_modules/prh/rules/media/Web+DB_PRESS.yml"]
    }
  }
}

基本的には、
"ルール名": 値(使用ならtrue,不使用ならfalseなど)を記述していくだけです.

ターミナルなどの実行フォルダが、textlintrcファイルがあるフォルダであれば、ルールの記述を省略できます.

上の例では、testフォルダに.textlintrcファイルを追加して置いたので、
ターミナルでtestフォルダに移動した状態でtextlint lint.mdを実行すると
ルール指定なしで添削されます.

## textlintを便利に使う: 自動修正編

ここまで、textlintの基本的な使い方を紹介しました.

ただ、ここまで紹介した方法では文章の簡単な表記揺れや句読点の調整などを検知して知らせてくれますが、修正は自分でしなければなりません.

しかしtextlintの一部のruleでは、文章のエラー検知だけでなく、文章の自動修正もやってくれる機能があります。その方法を紹介します.

やることは、簡単です.

textlint --fix {修正したいファイル名}.

とターミナルで入力すると、表記揺れや句読点などは、自動で修正してくれます！



