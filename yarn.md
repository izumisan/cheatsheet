# yarn

- JavaScriptのパッケージマネージャー
- npmと互換あり
- パッケージをキャッシュに貯めておくので、再インストールがnpmより高速
- 公式ページ - yarn
    - https://yarnpkg.com/ja/

# インストール

npmからインストールできる

```
> npm install yarn
```

## npmによるインストールについて

特に気にする必要ないが、yarn公式ではnpmからのインストールは推奨していない

https://yarnpkg.com/ja/docs/install#alternatives-stable


> 注意: npm から Yarn をインストールすることは一般的にはお勧めしません。 Node ベースのパッケージマネージャで Yarn をインストールする場合は、パッケージは署名されておらず、整合性のチェックはベーシックな SHA1 ハッシュのみで行われており、システム全体にまたがるアプリケーションをインストールする場合にはセキュリティリスクとなります。
>
> これらの理由から、使用中の OS に最も適した方法で Yarn をインストールすることを強くお勧めします。

# 初期化（yarn init）

# パッケージのインストール

# パッケージ情報

# パッケージのアップデート

# パッケージのアンインストール

# パッケージの検索

# タスクの実行

```sh
# package.jsonに定義したfooスクリプトを実行する
> yarn run foo

# runは省略可能
> yarn foo

# スクリプト一覧を表示する
> yarn run
```

# npmコマンドとの比較

|npm|yarn|
|---|---|
|npm install|yarn install|
|`npm install パッケージ名`|`yarm add パッケージ名`|
|`npm install --global パッケージ名`|`yarn global add パッケージ名`|
|npm outdated|yarn outdated|
|`npm update`|`yarn upgrade`|
|`npm uninstall パッケージ名`|`yarn remove パッケージ名`|
|npm run スクリプト名|yarn run スクリプト名<br>yarn スクリプト名|

# 参考

- [公式ドキュメント - yarn](https://yarnpkg.com/ja/docs)
