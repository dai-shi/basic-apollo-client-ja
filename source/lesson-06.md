# GraphCMSセットアップ

GraphCMSはGraphQLのバックエンドサービスです。
GraphQLのスキーマを詳しく知らなくても、GUIで組み立てることができるため、
練習のために導入してみましょう。

今回は簡単なブログを想定したアプリを題材にします。

## アカウントの作成

<https://graphcms.com>

を開いてSign Upからアカウントを作成してください。

## プロジェクトの作成

新しいプロジェクトを作成しましょう。
プロジェクト名は何でも構いません。

## モデルの作成

MODELSからADD CONTENTボタンを押して、新規にモデルを作成してください。

- Display Name: Article
- API ID: Article
- Description: 空でも良い
- Primary Field: ID

次に作成したArticleにFieldを追加しましょう。

ブログ記事のタイトルです。

- Field type: Text, Single Line
- Diplay Name: Title
- API ID: title

その他はデフォルトのままで。

ブログ記事の本文です。

- Field type: Content, Multi Line
- Diplay Name: Content
- API ID: content

ブログ記事の日時です。

- Field type: Date, Date & Time
- Diplay Name: Date
- API ID: date

ブログ記事のカバー画像です。

- Field type: Asset, Asset Grid
- Diplay Name: Cover
- API ID: cover

CoverはAssetとConnectしておく必要がありますので、Connectを押して有効にしてください。

また、Asset全体の読み込み権限を付与するためにPermissionsのRを有効にしてください。

## スキーマの確認

SETTINGSを開くとEXPORT DATAというところに
DOWNLOAD SCHEMAというボタンがあります。
押してファイルをダウンロードしましょう。

開くとGraphQLのスキーマ宣言があります。
自分で作成したArticleだけに注目して見てください。
想定通りにできたいたでしょうか。

@modelなどの`@`がついた宣言は今は気にしないものとしましょう。

## コンテンツの作成

アプリとしての動作を確認するために事前にコンテンツを作成しておきましょう。

CONTENT / Articleを開いて、"+"ボタンを押して記事を追加しましょう。
3記事くらい追加しておくと良いでしょう。
また、カバー写真も追加してみてください。

## GraphiQL

GraphCMSにもGraphiQLが組み込まれています。
API EXPLORERを開いて、クエリを組み立ててみましょう。

はじめは補完機能を使いながらゼロから組み立ててみるのが良いでしょう。

慣れてきたら最後に下記のクエリが動くかを確認してください。

```
{
  allArticles(orderBy: date_ASC) {
    id
    title
    date
    content
    cover {
      url
    }
  }
}
```

## 課題

1. モデルの作成およびスキーマの確認
2. サンプル記事の作成
3. GraphiQLを使ってクエリ確認
