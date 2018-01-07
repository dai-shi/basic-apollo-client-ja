# Graphcoolセットアップ

GraphcoolはGraphQLのバックエンドサービスです。
Graphcoolは最も有名なサービスの一つで、先進的な取り組みをしています。
仕様も頻繁に変わっています。

Graphcoolの主流はCLIに移行しているようですが、
今回はGUIを使って簡単なTODO管理アプリを作ってみましょう。

TODOはtitleとdescriptionで構成されて、追加や削除ができるものです。

## アカウントの作成

<https://www.graph.cool/>

を開いて、右上のOPEN CONSOLEからサインアップしてください。

## プロジェクトの作成

新しいプロジェクトを作成しましょう。
プロジェクト名は何でも構いません。

## スキーマの作成

SCHEMAのTYPESで下記のスキーマを追加しましょう。

```
type Task @model {
  id: ID! @isUnique
  createdAt: DateTime!
  title: String!
  description: String
}
```

元からあるスキーマは消さずに残してください。

右側のエリアでTaskのtypeをGUIで確認できます。

PERMISSIONSからTaskの全パーミッションがonになっていることを確認しましょう。

## コンテンツの作成

アプリとしての動作を確認するために事前にコンテンツを作成しておきましょう。

DATA / Taskを開いて、titleを入力しチェックボタンで追加されます。

## GraphiQL

GraphcoolにもGraphiQLが組み込まれています。
PLAYGROUNDを開いて、クエリを組み立ててみましょう。
SCHEMAのドロワーでDocsも確認できます。

今回の題材で実際に使うクエリは下記です。試してみましょう。

```
{
  allTasks(orderBy: createdAt_DESC) {
    id
    title
    description
  }
}
```

また、今回はmutationも使いますので、下記も試しておきましょう。

```
mutation createTask($title: String!, $description: String) {
  createTask(title: $title, description: $description) {
    id
    title
    description
  }
}
```

これは、QUERY VARIABLEも使いますので、そのエリアを開いてJSON形式で入力してください。例えば、下記のようにします。

```
{"title":"あいうえお","description":"かきくけこ"}
```

## 課題

1. スキーマの作成とサンプルデータ追加
2. GraphiQLを使ってクエリ動作確認
3. GraphiQLを使ってmutation動作確認
