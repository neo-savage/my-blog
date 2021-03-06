---
slug: "/don't-recommend-starter"
date: "2020-09-08"
title: "初心者がGatsbyをスタータープロジェクトから始めることをおすすめしない理由"
category: ["Gatsby"]
featuredImage: F-don't-recommend-starter.png
published: true
---

# はじめに

Gatsby の特徴として、[Starter Library](https://www.gatsbyjs.com/starters/?v=2) がありますね。  
公開されているスタータープロジェクトの数は日に日に増えており、現在では 435 ものスターターが公開されており、誰でも無料で使用することができます。(2020/09/07)

Gatsby との比較候補として Next.js が挙げられますが、Next.js にこのようなスターターライブラリーは存在しないため、1 つの大きな差別化要素になっています。  
スタータープロジェクトはローカルに落としてくるだけで、既に様々な機能が実装された WEB サイトが手に入ります。自分で一から実装する必要がないため、よく分からないうちはこのお手軽さに飛びついて、「後はこれを必要に応じてカスタマイズすればもうブログ完成じゃん」と安易に考えてしましいがちです。  
今回はその考えの落とし穴と、効率的なスタータープロジェクトの使い方について説明していきます。

# 初心者が Gatsby をスタータープロジェクトから始めることをおすすめしない理由

すごく上から目線な記事の書き方になってしまっていますが、これは私自身もかつてやってしまっていたことでもあります。最近、周りの方々も同じような道を歩んでいるのを見て、もどかしい気持ちになったので、同じ道を歩んで欲しくはないという思いで今この記事を書いています。  
それでは本題に入り、初心者が Gatsby をスタータープロジェクトから始めることをおすすめしない理由をお伝えしていきます。

## 【理由その 1】 結局、コードを読んで理解するのに膨大な時間を使わなければならない

スターターライブラリーの中から良さそうなスタータープロジェクト見つけ、それをローカルに落としてきたとします。サーバーを立ち上げ、無事に画面を表示することが出来ました。ひとしきりサイトを徘徊し、ここまでの容易さに感動したあと、次にあなたがやろうとするのはサイトのカスタマイズでしょう。  
例えば、タイトルを変えようとしてみたり、記事をいじってみたり。何でもいいですが、Gatsby には WordPress のような GUI エディタはありません。あなたはこの綺麗に完成したサイトから目を背け、編集したい部分のコードをたくさんのディレクトリとファイルの中から探し当て、該当箇所を編集する必要があります。  
これは想像以上に根気のいる作業です。ある程度プログラミングの経験がある人や勘の鋭い人であれば、ディレクトリ名やファイル名からなんとなく役割を理解し、実際に想定していた部分を編集することが出来るかもしれません。
１箇所でも実際に編集してみればその大変さが分かります。しかしあなたはカスタマイズに満足するまで、永遠とこの作業を繰り返す必要があります。尋常じゃない忍耐力がなければ途中で挫折してしまうでしょう。

**カスタマイズするというのは、想像以上に大変なことなのです。**

## 【理由その 2】 コードを読もうとしても、何をしているのか分からない

React を触ったことがなく SSG についてよく知らないかたは、カスタマイズすることの大変さが分かった時点で、諦めてしまうと思います。しかし React を触ったことがある場合、基本的に画面に表示される全ては要素の React のコンポーネントであるため、全く分からないということは無いのではないかと思います。  
しかし React 経験者ですら、スタータープロジェクトのコードを読んで理解することは難しいでしょう。例えば、`src/pages/` 配下に
置かれているコンポーネントが、画面の 1 ページと連動していることは何となくでもすぐに分かるかと思います。ですがその次に、データをどこから取得しているのかを辿ろうとした場合、途端に分からなくなります。ここがこの考え方にある大きな落とし穴です。  
Gatsby は build-in で、様々なモダンフロントエンドのテクノロジーを内包しています。

- WebPack
- Plugins(Node.js packages)
- Redux
- Graphql

上記 3 つに関しては、馴染みのある方も多いかもしれません、しかし Graphql についてはどうでしょうか。Graphql はまだまだ日本で浸透している印象はありません。  
Graphql は Facebook が開発したクエリ言語で、REST API に代わるフロントエンドの新たなデータ取得方法です。この Graphql の理解無しにスタータープロジェクトのコードを読み進めることは出来ません。なぜなら多くのスタータープロジェクトは Graphql を使用してデータを取得しているからです。  
もちろん、探せば中には馴染みのある REST API 形式でデータを取得しているものもあるでしょう。しかし、その制限の中でスターターを探そうとすると極端に数が減るはずです。  
また、データ取得部分も Graphql から REST API に変更することも出来ますが、この Graphql の内部処理は基本的に Gatsby と plugin が隠蔽しているため、ましてやそもそも Gatsby がよく分からない状態だと、影響範囲を追えなくなると思います。  
次に、先ほどから出てきていますが、plugin の話に移ります。  
Gatsby には plugin というコンセプトがあり、自分で実装せずとも plugin をインストールすることでミニマルな機能を後から追加していくことができます。  
スタータープロジェクトにはデフォルトでたくさんの plugin がインストールされていることが多いです。これら plugin の処理 は Gatsby のビルド時に実行されます。私たちが主に見る src フォルダにはその Gatsby の config ファイル上と package.json 上でしか存在を確認出来ず、したがって普通のプログラムを読むようにトレースしていくことが出来ません。  
何かよく分からないけどプログラムがどこかで実行されていることに何となく気付き、その正体が plugin であると分かれば、後は plugin のドキュメントを読めば詳細な情報が入手できます。  
ただスタータープロジェクトの状態からそこまで辿りつけるとは思えません。

## 【理由その 3】 カスタマイズでは応用が効かない

Gatsby に内包されている技術スタックを知らずともなんとかスタータープロジェクトを改修し、自分好みのレイアウトで自分の記事を更新出来るようになったとしましょう。おめでとうございます。かなり苦労されたと思います。しかし、そこまでの苦労をしてわざわざ Gatsby でブログを作る必要があったのでしょうか。世の中にはたくさんのブログサービスがあり、その中からあえて Gatsby でブログを作りたいというのですから、何かしら理由があると思います。個人的には、以下が理由です。

- React や TypeScript の恩恵を受けたい
- 爆速なサイトを作りたい
- SEO を気にしたい(meta タグなど)
- サーバーやデータベースを管理したくない
- WordPress が嫌なお客様へ提案したい

このあたり人によって違うかと思いますが、特に将来的に案件で使いたいといった考えがある場合、スターターのカスタマイズだけでは要件を満たせないことも多いでしょう。Gatsby のライフサイクルや API、plugin を知っている必要があります。個人的にはブログを作りたいだけなら他のサービスやフレームワークでもいいと思っていますので、それらサービスへやフレームワークへのアンチテーゼや技術的な探究心などが無いまま積み上がったジェンガの上の方だけを弄ったとしてそれらの要求が満たせるのか疑問です。

それではここからは、私がおすすめするスタータープロジェクトの使い方についてご説明していきたいと思います。

# スタータープロジェクトを、ごく局所的に参照する用途で使用する

まず、最初はデフォルトのスターターから始めることを強くおすすめします。理由は後述します。Gatsby はデフォルトのスターターでも、不要なコンポーネントやコードが含まれていますので、不要な分は全て削除し、画面を白紙の状態にします。ここから、例えばヘッダーを作りたいなと思えば、スタータープロジェクトからヘッダーコンポーネントを探し、参照しつつ、実装します。公式のチュートリアル等のドキュメントや、他の開発者のブログを参考にするのもおすすめします。  
「作成し終わったものの、ページに反映されないのは、なぜだろう」→「`src/pages` 配下のページコンポーネントで import する必要があるのか」と、ページの概念やコンポーネントの概念を一つずつ学んでいきます。  
「ブログを表示させたい、記事のデータはどうやって取得できるのだろう」となれば、同じようにスタータープロジェクトや、その他記事などを参照します。  
ここで言いたいのは、このようにして一つ一つ自分の手で、調べながら実装していく方が結果的に近道だと言うことです。スタータープロジェクトから始めたり、チュートリアルの手順に沿っていくだけではいまいち身につかないのです。  
「〇〇をしたければ〇〇をする」といった思考の因果関係を蓄積が知識になっていきます。  
私は今もこのやり方で、少しずつ Gatsby を学習していると同時に、開発を進めています。基本的に調べても情報が出てこないとか、同じようなことをしているスタータープロジェクトが見つからない場合、それは主にやり方を違っている場合か、よほど珍しい、あるいは新しい技術の組み合わせとかであると思います。なのでそういった機能は一旦後回しにして、まずは基本的な機能を実装しましょう。ある程度出来たら公開し、また少しずつ実装していけば良いのです。

# ある程度 Gatsby を使いこなせる状態になり、また爆速でサイトを作る必要が出てきた場合に使用する。

一旦、サイトやブログの作り方が分かってくると、後は何度作ろうとも同じようなことの繰り返しであることに気がつき始めると思います。毎回毎回同じようなことをするのは誰でも疲れますね。しかしこれがお仕事である場合、そうやって疲れている暇はありません。ここで出番です。私たちにはスタータープロジェクトがあります。良さそうなスターターを見つけたら、クローンした後必要な部分だけ爆速で改修し、納品してしまいましょう。ここまでくればスターターは何をどうすれば良いかよく分からないブラックボックスではなく、強烈なあなたの武器となります。自分好みのスターターを開発してストックしたり、スターターライブラリに公開するのも良いかもしれません。

# おわりに

スタータープロジェクトの強力な使い方を理解していただけたでしょうか。一つのご提案として受け止めていただけたら嬉しいです。まだまだ Gatsby や成長期のフレームワークです。このサイトのようにシンプルなものであれば十分作成できますが、細かな機能が沢山ついたリッチな WEB サイトやブログを作りたいといった要件では工数の関係上あまりお勧めできません。しかし Gatsby は現状最先端のフロントエンドフレームワークのうちの一つだと思っています。アーリーアダプターならではの楽しみや刺激を楽しめます。焦らず一つずつが肝です。一緒に Gatsby のコミュニティを盛り上げましょう。
