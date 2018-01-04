# simple-blog解説

LimeGreenJSにGraphCMSを使った簡単なブログアプリが登録されています。

## 実行する

<https://limegreenjs.axlight.com/>

を開いてOFFICIALのsimple-blogを見つけましょう。

"RUN APP"で実行して、ブログが表示されるのを確認してください。

## コードを読む

"SHOW CODE"でGitHubのページを開きましょう。
README.mdを除くとファイルは4つあります。

- index.html: 最初にロードされるhtmlです。jsファイルはバンドルされたものが追記されます。
- index.js: エントリーポイントのjsです。App.jsを呼び出します。
- App.js: メインのjsです。React/GraphQLをセットアップします。
- ArticleList.js: ブログ記事一覧を表示するReactコンポーネントです。内部でArticleItemというコンポーネントも定義しています。

ArticleItemは記事を表示するコンポーネントで表示のみの仕事をします。
ArticleListはArticleItemを繰り返すコンポーネントで
基本的には表示のみの仕事をしますが、GraphQLの呼び出しの
ローディング時やエラー時の表示も担当しています。

queryにGraphiQLで試したクエリと同じものが指定されています。
最後にgraphqlというHigh-order ComponentがqueryとArticleListを繋ぐことにより
完成します。
このgraphqlというHoCには色々カスタマイズする機能があります。
詳細は[リファレンス](https://www.apollographql.com/docs/react/basics/queries.html#api)を参照しましょう。

## 自分のGraphCMSで動作させる

simple-blogをforkして自分のGraphCMSとつなげてみましょう。

1. GraphCMSのSETTINGSを開き、ENDPOINTSのSimple EndpointのURLをコピーする
2. forkしたsimple-blogのApp.jsのHttpLinkのuriを上記のURLに変更する
3. LimeGreenJSをリロードして、該当アプリをRUN APPする

想定通りのコンテンツが表示されることを確認してください。

## 課題

1. コードを実行して、よく読む
2. URLを変更して自分のGraphCMSにつなげる
3. (余裕があれば)少しコードをいじってみる
