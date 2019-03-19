# JSDoc

JavaScriptにアノテーション（JSDocタグ）を追加することで、APIドキュメントを自動生成することができる。


- @use JSDoc - 公式サイト
    - http://usejsdoc.org/
- JSDoc 3 - GitHub
    - https://github.com/jsdoc3/jsdoc


# インストール

```
> npm install jsdoc
```

- npm以外にもいろいろある


# 使い方

`jsdoc`コマンドでjsファイルを指定する。

```sh
# npm
> ./node_modules/.bin/jsdoc foo.js

# yarn
> yarn jsdoc foo.js
```

# コメントスタイル

```js
/** 一行スタイル */
function foo() {
    ...
}
```

```js
/**
 * 複数行スタイル
 */
function() {
    ...
}
```

# アノテーション（JSDocタグ）

使用頻度が高いもの

|タグ|説明|
|---|---|
|`@file`|ファイル説明|
|`@type`|変数の型|
|`@param`|関数の引数|
|`@return`|戻り値|

