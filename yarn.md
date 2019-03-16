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

# プロジェクトの初期化

# パッケージのインストール

```sh
# package.jsonに従いインストールする
> yarn install

# オフラインモードでインストールする
> yarn install --offline

# インストールしたファイルが削除されていないかを確認する
> yarn install --check-files

# パッケージを指定してインストールする
> yarn add パッケージ名
> yarn add パッケージ名 --dev
> yarn add パッケージ名 --optional
> yarn add パッケージ名 --optional
```

## 依存関係の種別

- `dependencies`
    - 通常の依存関係
    - 実行時に必要なパッケージ
- `devDependencies`
    - 開発用パッケージ
- `optionalDependencies`
    - 省略可能なパッケージ
- `peerDependencies`
    - パッケージ公開時用


# パッケージ情報

```sh
# インストールされているパッケージ一覧を表示する
> yarn list

# 深さ0までのパッケージ一覧を表示する
> yarn list --depth=0

# パッケージ情報を表示する
> yarn info パッケージ名
```

# パッケージのアップデート

```sh
# 全てのパッケージを最新バージョンにアップデートする
> yarn upgrade

# 指定したパッケージをアップデートする
> yarn upgrade パッケージ名
> yarn upgrade パッケージ名@バージョン
> yarn upgrade パッケージ名@タグ名
```

# パッケージのアンインストール

```
> yarn remove パッケージ名
```

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
