# npm

- Node Package Manager
- JavaScript系のパッケージ管理ツール
- Node.jsに同梱されている

# 初期化（`npm init`）

- カレントディレクトリをnpmの管理ディレクトリとして初期化する
- 実行により、`package.json`が作成される

# パッケージのインストール

- パッケージをインストールする
    ```
    > npm install パッケージ名
    > npm i パッケージ名
    ```
- バージョンを指定する
    ```
    > npm install パッケージ名@1.0.0
    ```
- グローバルインストール（`-g`オプション）
    ```
    > npm install -g パッケージ名
    ```
    - ローカルインストール
        - カレントディレクトリの`node_modules`にインストールする
    - グローバルインストール
        - システムディレクトリの`node_modules`にインストールする
- `package.json`からパッケージを一括インストール（復元）
    ```sh
    # package.jsonがあるディレクトリで下記を実行
    > npm install
    ```
- インストールオプション
    ```
    > npm install パッケージ名 --no-save
    > npm install パッケージ名 --save
    > npm install パッケージ名 --save-optional
    > npm install パッケージ名 --save-dev
    ```
    - `--no-save`
        - インストールパッケージを`package.json`に記録しない
    - `--save`
        - インストールパッケージを`dependencies`として記録する
        - npm5以降で、デフォルトオプション
    - `--save-optional`
        - 必須ではないパッケージをインストールする場合に指定する
        - インストールパッケージを`optionalDependencies`として記録する
    - `--save-dev`
        - 開発者が使用するパッケージをインストールする場合に指定する
        - インストールパッケージを`devDependencies`として記録する

# パッケージ情報

- インストール済みのパッケージ一覧を表示する
    ```
    > npm list
    > npm ls
    ```
- グローバルインストールしたパッケージ一覧を表示する（`-g`オプション）
    ```
    > npm list -g
    ```
- 第一階層のみ表示する
    ```
    > npm list --depth=0
    ```

# パッケージのアップデート

- 最新版の有無を確認する
    ```
    > npm outdated
    > npm outdated -g
    ```
- パッケージをアップデートする
    ```
    > npm update パッケージ名
    > npm update パッケージ名 -g
    ```
- 全てのパッケージをアップデートする
    ```
    > npm update
    ```

# パッケージのアンインストール

- パッケージをアンインストールする
    ```
    > npm uninstall パッケージ名
    > npm uninstall パッケージ名 -g
    ```
- アンインストールオプション
    ```
    > npm uninstall --save
    > npm uninstall --save-optional
    > npm uninstall --save-dev
    ```

# パッケージの検索

- パッケージを検索する
    ```
    > npm search パッケージ名
    ```
- パッケージのバージョンを表示する
    ```sh
    # 最新バージョンを表示する
    > npm info パッケージ名 version
    # インストール可能なバージョン一覧を表示する
    > npm info パッケージ名 versions
    ```

# タスクの実行

- タスクは、`package.json`の`scripts`に記述する
- タスクを実行する
    ```sh
    # fooタスクを実行する
    > npm run foo
    ```
- タスク一覧を表示する
    ```
    > npm run
    ```

#　ディレクトリの表示

- ルートディレクトリを表示する
    ```
    > npm root
    > npm root -g
    ```
- コマンドディレクトリを表示する
    ```
    > npm bin
    > npm bin -g
    ```

# npmbox

npmboxを使うと依存モジュールを含めてパッケージ化できるので、npmboxでパッケージを作成しオフラインPCに持っていけば、オフラインPCでもnpmパッケージを利用できる

## npmboxのインストール

```sh
# npmboxをグローバルインストール
> npm install -g npmbox
```

コマンド実行により、`npmbox.npmbox`ファイルが作成される

## npmboxのオフラインインストール

`npmbox.npmbox`ファイルを使って、オフラインPCに`npmbox`パッケージをインストールする

1. `npmbox.npmbox`ファイルを展開する
    ```
    > tar --no-same-owner --no-same-permissions -xvzf npmbox.npmbox
    ```
1. `.npmbox.cache`から`npmbox`をインストールする
    ```
    > npm install --global --cache ./.npmbox.cache --optional --cache-min 99999999999 --shrinkwrap false npmbox
    ```
    途中でエラーが出る場合はキャッシュをクリアする
    ```
    > npm cache clean
    ```

## npmboxでパッケージ化

```
> npmbox パッケージ名
```
コマンド実行により、`パッケージ名.npmbox`が作成される

## npmboxパッケージ（npmboxファイル）からインストール

```
> npmunbox xxxxx.npmbox
```

# yarn

TODO
