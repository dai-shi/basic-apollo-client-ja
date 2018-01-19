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

## 自分でgraphcoolを設定する

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
  - Everyone Read: ON
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


