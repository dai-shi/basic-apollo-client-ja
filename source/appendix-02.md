# GraphQL subscriptionsについて

GraphQLで即時性を向上するための仕様としてGraphQL subscriptionsがあります。

[June 2018](https://github.com/facebook/graphql/releases/tag/June2018)からGraphQLの仕様にも入っています。
また、GraphcoolとApolloでもサポートされています。

## simple-chat

LimeGreenJSにGraphQL subscriptionsを使った簡単なチャット風アプリがあります。

<https://limegreenjs.axlight.com/>

を開いてOFFICIALのsimple-chatを見つけましょう。

"RUN APP"で実行して、アプリが表示されるのを確認してください。

## apollo client

apollo clientの設定は[公式ドキュメント](https://www.apollographql.com/docs/react/advanced/subscriptions.html#subscriptions-client)の通り、次のようになります。

```
const httpLink = new HttpLink({
  uri: '...',
});
const wsLink = new WebSocketLink({
  uri: '...',
  options: {
    reconnect: true
  },
});
const link = split(
  ({ query }) => {
    const { kind, operation } = getMainDefinition(query);
    return kind === 'OperationDefinition' && operation === 'subscription';
  },
  wsLink,
  httpLink,
);
```

## subscription

GraphQLのsubscriptionは次のように直感的です。

```
subscription Message {
  Message {
    mutation
    node {
      id
      createdAt
      text
      author
    }
  }
}
```

## subscribeToMore

React Apolloを使う際には、subscribeToMoreという機能があり、
簡単にsubscription結果をマージすることができます。

[公式ドキュメント](https://www.apollographql.com/docs/react/advanced/subscriptions.html#subscribe-to-more)を参考にしつつ、simple-chatのコードを読んでみましょう。

## 自分でgraphcoolを設定する

simple-chatを動かすためには下記の設定をします。

### スキーマの設定

```
type Message @model {
  id: ID! @isUnique
  createdAt: DateTime!
  text: String!
  author: String
}
```

### 権限の設定

GraphcoolのPERMISSIONSでMessageの権限は全てONにしましょう。

## 参考情報

- https://www.graph.cool/docs/reference/graphql-api/subscription-api-aip7oojeiv/
- https://www.apollographql.com/docs/react/advanced/subscriptions.html
