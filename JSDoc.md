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
```js
/**
 * 長い説明文で改行が必要な場合、
 *    半角スペース4つでインデントする
 *
 * @return 長い説明文の改行時、説明文の先頭で
 *         インデントを合わせるのは推奨していません
 */
function() {
    ...
}
```


# アノテーション（JSDocタグ）

## 使用頻度が高そうなタグ

|タグ|説明|
|---|---|
|[@file](http://usejsdoc.org/tags-file.html)|ファイル説明|
|[@type](http://usejsdoc.org/tags-type.html)|変数の型|
|[@param](http://usejsdoc.org/tags-param.html)|関数の引数|
|[@return](http://usejsdoc.org/tags-returns.html)|戻り値|
|[@throws](http://usejsdoc.org/tags-throws.html)|スローする例外説明|
|[@static](http://usejsdoc.org/tags-static.html)||
|[@constant](http://usejsdoc.org/tags-constant.html)||
|[@class/@constructor](http://usejsdoc.org/tags-class.html)|クラス説明|
|[@description](http://usejsdoc.org/tags-description.html)||
|[@todo](http://usejsdoc.org/tags-todo.html)|タスク|
|[@ignore](http://usejsdoc.org/tags-ignore.html)|ドキュメントから除外する|

## `@param`

- `@param {型名} 変数名 説明文`

```js
/**
 * 関数の説明文
 * @param {string} bar 引数barの説明文
 * @param {number} baz 引数bazの説明文
 */
function foo( bar, baz ) {
    ...
}
```

## `@type`

- `@type {型名}`

```js
/**
 * fooの説明文
 * @type {string}
 */
var foo;
```
