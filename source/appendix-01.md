# 認証と権限について

総合課題で題材としたような掲示板アプリを考えると、
ユーザ認証の機能が必要になります。

GraphQL自体の仕様には認証は含まれておらず、
外部での実装次第とされています。

GraphcoolではEmail/passwordを使った認証機能が提供されているため、
それを使ったサンプルを紹介します。

## standard-todos

LimeGreenJSに認証と権限の機能を加えたTODO管理アプリがあります。

<https://limegreenjs.axlight.com/>

を開いてOFFICIALのstandard-todosを見つけましょう。

"RUN APP"で実行して、アプリが表示されるのを確認してください。

## 権限

standard-todosで採用した権限モデルはownershipと呼ばれる基本的なもので、
下記のような振る舞いをします。

- ログインしてTODOを作成するとそのTODOのownerとなる
- ownerが設定されたTODOはownerのみが削除(もしくは編集)できる
- TODOを作成時にprivate設定ができ、その場合はownerのみがそのTODOを見ることができる
- ログインせずにTODOを作成するとowner未設定になり、誰でも削除(もしくは編集)できる

権限の設定はGraphcoolのpermissionで設定するとともに、
クライアントサイドでもそのpermissionを想定したクエリを発行することにより、
エラーを避けたり、わかりやすいUXとしたりする。

## 自分でgraphcoolを設定する

standard-todosを動かすためには、
simple-todosに加えて下記の設定をします。

### 認証の設定

GraphcoolのINTEGRATIONSからEmail-Password Authを有効にしましょう。

### 権限の設定

GraphcoolのPERMISSIONSで次のように設定しましょう。

- User
  - Everyone Read: ON
  - Everyone Create: ON
  - Everyone Update: OFF
  - Everyone Delete: OFF
- File
  - Everyone Read: ON
  - Everyone Create: ON
  - Everyone Update: OFF
  - Everyone Delete: OFF
- Task
  - Everyone Read: ON (下記のPermission Queryを設定する)
```
query ($node_id: ID!) {
  SomeTaskExists(
    filter: {
      id: $node_id
      OR: [{
        private: false
      }, {
        private: null
      }]
    }
  )
}
```
  - Everyone Create: ON
  - Everyone Update: ON (下記のPermission Queryを設定する)
```
query ($node_id: ID!) {
  SomeTaskExists(
    filter: {
      id: $node_id
      owner: null
    }
  )
}
```
  - Everyone Delete: ON (下記のPermission Queryを設定する)
```
query ($node_id: ID!) {
  SomeTaskExists(
    filter: {
      id: $node_id
      owner: null
    }
  )
}
```
  - Authenticated Read: ON (下記のPermission Queryを設定する)
```
query ($node_id: ID!, $user_id: ID!) {
  SomeTaskExists(
    filter: {
      id: $node_id
      owner: {
        id: $user_id
      }
    }
  )
}
```
  - Authenticated Update: ON (下記のPermission Queryを設定する)
```
query ($node_id: ID!, $user_id: ID!) {
  SomeTaskExists(
    filter: {
      id: $node_id
      owner: {
        id: $user_id
      }
    }
  )
}
```
  - Authenticated Delete: ON (下記のPermission Queryを設定する)
```
query ($node_id: ID!, $user_id: ID!) {
  SomeTaskExists(
    filter: {
      id: $node_id
      owner: {
        id: $user_id
      }
    }
  )
}
```

## 参考情報

- https://www.graph.cool/docs/tutorials/auth/authorization-for-a-cms-miesho4goo/
- https://www.graph.cool/docs/reference/auth/overview-ohs4aek0pe
