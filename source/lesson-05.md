# LimeGreenJSの使い方

## 概要

Reactの環境構築は初心者には難しい場合があります。
導入時はCRA (create-react-app)を使うと簡単にできますが、
実際にそのアプリを公開する場合には様々な技術を使うことになります。

LimeGreenJSは、React/GraphQLで開発したアプリを
公開できるようにするサービスです。
GitHubと連携しており、コードをpushするだけでアプリを公開できます。
LimeGreenJSはGraphQLのバックエンドを内包せず、
既存のバックエンドサービスを使うことを前提にしています。

LimeGreenJSはビルドとWebサーバの機能を提供します。
標準的なApolloのパッケージやwebpackの設定が含まれています。
現在はカスタマイズできませんが、将来的にはできるようになる見込みです。

## LimeGreenJSへのアクセス

下記のLimeGreenJSのサイトにアクセスします。

<https://limegreenjs.axlight.com/>

このサイトを使うには
GitHubアカウントでログインして使用の許可をする必要があります。

## Hello Worldの実行

最も簡単なHello Worldのアプリを実行してみましょう。

OFFICIALのHello Worldを見つけて、"RUN APP"ボタンを押すと
アプリを実行することができます。
新しいウインドウが開いてHelloが表示されることを確認しましょう。

"SHOW CODE"ボタンを押すとGitHubのページが開いてソースコードを見ることができます。
ファイルを開いてソースコードを確認しましょう。

## Hello Worldの変更

LimeGreenJSの使い方を学ぶためにHello Worldを変更してみましょう。

1. SHOW CODEで表示したGitHubのページでforkする(右上のボタン)
2. forkされた自分のリポジトリでjsファイルを開く
3. Editボタンを押して編集画面に入る
4. ソースコードの"World"の文字を別のものに置き換えてみる
5. 保存する(commit)
6. LimeGreenJSのサイトに行き、リロードする
7. Mineタブから自分のHello Worldを探してRUN APPする

変更されたアプリが表示されれば成功です。

## ローカル開発

上記のGitHubでのソースコード編集は、ローカル開発に慣れている場合は
むしろ不便なことがあります。
普段のエディタとgitコマンドを使う場合を練習してみましょう。

1. LimeGreenJSでOFFICIALのhot module replacementを探す
2. SHOW CODEしてforkする
3. forkしたリポジトリをローカルにcloneする
4. cloneしたリポジトリのディレクトリに入り、npx limegreenjs devを実行する
5. <http://localhost:8080> にアクセスして動作を確認する
6. 4のlimegreenjsを起動したまま、jsファイルを編集する
7. jsファイルを保存するとすぐにアプリの画面が更新されることを確認する
8. commitしてpushする
9. LimeGreenJSのサイトに行き、リロードする
10. Mineタブから該当アプリを探してRUN APPする

## 課題

1. LimeGreenJSにアクセスする
2. hello-worldをいじる
3. hot-module-replacementをいじる
