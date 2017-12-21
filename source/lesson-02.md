# GraphQLとは

GraphQLはFacebookが開発したAPI用クエリ言語です。
クエリ言語の仕様だけでなく、ライブラリ、サーバ&クライアント実装もあります。

GraphQLはRESTベースの「開発スタイル」の問題を解決するものです。
すなわち、クライアントサイドとサーバサイドに開発が分断されているような
大規模チームにおける開発サイクルの遅さの課題を改善するため、
クエリ設計の自由度をクライアントサイドに持たせることができます。
サーバサイドではクエリを表現するためのスキーマだけを定義することになります。

GraphQLは特定のデータベースに依存するものではありません。
データベースレイヤの上に構築されるラッパーレイヤの位置付けであり、
REST APIもデータベースレイヤの一つとして扱います。

GraphQLは2016年あたりから本格的に注目され、実際にプロダクトでも利用されています。
元来は大規模チームにおける課題を解決するアプローチでしたが、
単一エンドポイントとなることによるパフォーマンス改善や
様々な実装を伴ったエコシステムの発展によって、
小規模なチームでもメリットが生まれています。

一方、GraphQLが不要なシーンや適さないシーンもあります。
例えば、ハッカソンなどにおけるラピッドプロトタイピングにおいては、
RESTで設計する方が速いだろうなどと言われています。

## GraphQL概観

[公式ドキュメント](http://graphql.org/learn/)に簡単な例が載っているので参考になります。

例えば、

```
{
  "me": {
    "name": "Luke Skywalker"
  }
}
```

のようなJSONを返して欲しい時のクエリは、

```
{
  me {
    name
  }
}
```

のようになります。GraphQLのクエリはJSONのkey部分を残したような形になります。
このクエリを実現するためのスキーマは次のようになります。

```
type Query {
  me: User
}

type User {
  id: ID
  name: String
}
```

Userはオブジェクトタイプでそのフィールドにidとnameがあります。
IDやStringはスカラータイプでGraphQLで規定されたものです。
オブジェクトタイプは入れ子にできるので、スキーマ全体としては有向グラフになります。（ループがなければツリーになります）


### クエリの書き方

<http://graphql.org/learn/queries/>を参照して、クエリの書き方を学びましょう。

### スキーマの書き方

<http://graphql.org/learn/schema/>を参照して、クエリの書き方を学びましょう。

## GraphQLサービス

GraphQLを実際に採用している例としてGitHub APIがあります。

<https://developer.github.com/v4/>

また、GraphQLをBaaSとして提供するサービスもあります。

- [GraphCMS](https://graphcms.com/)
- [Graphcool](https://www.graph.cool/)
- [Reindex](https://www.reindex.io/)
- [Scaphold](https://scaphold.io/)
- [AWS AppSync](https://aws.amazon.com/jp/appsync/)

今後も類似のサービスが登場してくることでしょう。