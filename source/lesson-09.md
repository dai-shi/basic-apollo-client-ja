# simple-todos解説

LimeGreenJSにGraphCMSを使った簡単なTODO管理アプリが登録されています。

## 実行する

<https://limegreenjs.axlight.com/>

を開いてOFFICIALのsimple-todosを見つけましょう。

"RUN APP"で実行して、ブログが表示されるのを確認してください。

## コードを読む

"SHOW CODE"でGitHubのページを開きましょう。
README.mdを除くとファイルは4つあります。

- index.html: 最初にロードされるhtmlです。jsファイルはバンドルされたものが追記されます。
- index.js: エントリーポイントのjsです。App.jsを呼び出します。
- App.js: メインのjsです。React/GraphQLをセットアップします。
- TodoList.js: TODOのリストを表示するコンポーネントです。全TODOを取得するGraphQLのクエリを呼び出します。
- TodoItem.js: TODOのアイテムを表示するコンポーネントです。Deleteボタンを押すと当該アイテムを削除するmutationを呼び出します。
- NewTodoForm.js: 新しいTODOを追加するためのコンポーネントです。Addボタンを押すと新規追加するmutationを呼び出します。

## 自分のGraphcoolで動作させる

simple-todosをforkして自分のGraphcoolとつなげてみましょう。

1. GraphcoolのENDPOINTSを開き、SimpleのURLをコピーする
2. forkしたsimple-todosのApp.jsのHttpLinkのuriを上記のURLに変更する
3. LimeGreenJSをリロードして、該当アプリをRUN APPする

想定通りのコンテンツが表示されることを確認してください。
コンテンツの追加や削除も試して、
Graphcool側のDATAが更新されることを確認してください。

## 課題

1. コードを実行して、よく読む
2. URLを変更して自分のGraphcoolにつなげる
3. (余裕があれば)少しコードをいじってみる
