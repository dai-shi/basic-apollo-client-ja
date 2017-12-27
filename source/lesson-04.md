# Apolloとは

JavaScriptフレームワーク「Meteor」を開発したMDGが開発している
GraphQLのライブラリです。
サーバーとクライアントの両方とも開発されています。

<https://www.apollographql.com>

クライアントは複数のターゲットに向けて開発されています。
- [React(React Native含む)](https://www.apollographql.com/docs/react/)
- [Angular](https://www.apollographql.com/docs/angular/)
- [ネイティブのiOS](https://www.apollographql.com/docs/ios/)
- [ネイティブのAndroid](https://github.com/apollographql/apollo-android)

JavaScriptのクライアントは他のライブラリとも統合できます。
- [Vue.js](https://github.com/akryum/vue-apollo)
- [Meteor](https://www.apollographql.com/docs/react/recipes/meteor.html)
- [Ember](https://www.apollographql.com/docs/react/basics/integrations.html#ember)
- [Polymer](https://www.apollographql.com/docs/react/basics/integrations.html#polymer)

本レッスンではReact向けクライアントについてのみ扱います。

## Apolloクライアント概観

React向けApolloクライアントは複数のパッケージから構成されています。

- apollo-client: viewによらない共通機能、ApolloClientを提供
- apollo-cache-inmemory: キャッシュ機能(v2から分離)
- apollo-link-http: 通信機能(v2から分離)
- react-apollo: Reactのbinding、ApolloProviderを提供
- graphql-tag: graphqlをテンプレート文字列で書けるようにする
- graphql: FacebookのGraphQLを扱うライブラリ

### ApolloClient

アプリの起動時にApolloClientを初期化します。

```
import { ApolloClient } from 'apollo-client';
import { HttpLink } from 'apollo-link-http';
import { InMemoryCache } from 'apollo-cache-inmemory';

const client = new ApolloClient({
  link: new HttpLink({ uri: 'https://api.example.com/graphql' }),
  cache: new InMemoryCache()
});
```

基本的にはuri以外は変更することは少ないです。
詳細なオプションは[こちら](https://www.apollographql.com/docs/react/basics/setup.html#ApolloClient)を参照してください。

### ApolloProvider

ApolloClientをReactコンポーネントで使えるようにするProviderです。

```
import { ApolloProvider } from 'react-apollo';

ReactDOM.render(
  <ApolloProvider client={client}>
    <MyAppComponent />
  </ApolloProvider>,
  document.getElementById('root')
);
```

これにより、下位のコンポーネントでクエリを実行できるようになります。
graphql-tagを使うと以下のように書けます。

```
import { graphql } from 'react-apollo';
import gql from 'graphql-tag';

const MyRenderComponent = (...) => ...;

const query = gql`
  {
    ...foo
  }
`;

export default graphql(query)(MyRenderComponent);
```

クエリを実行した結果はコンポーネントのpropsとして与えられるため、
あとは通常のReactとして処理をすれば良いことになります。

## 例題アプリ

公式の例題が下記にあるので、詳しくコードを見たり、動かして見たりすることができます。

<https://github.com/apollographql/react-apollo/tree/master/examples/base>

## 課題

1. [Introduction](https://www.apollographql.com/docs/react/)に記載されている1-7の特徴を読む
2. [Setup](https://www.apollographql.com/docs/react/basics/setup.html)に記載されているコードサンプルを読む
3. (余裕があれば)公式の例題アプリを動作させてみる
