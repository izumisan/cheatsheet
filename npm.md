# npm

- Node Package Manager
- JavaScript系のパッケージ管理ツール
- Node.jsに同梱されている

# `npm init`

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
- `-g`オプションでグローバルインストール
    ```
    > npm install -g パッケージ名
    ```
    - ローカルインストール
        - カレントディレクトリの`node_modules`にインストールする
    - グローバルインストール
        - システムディレクトリの`node_modules`にインストールする

# パッケージ情報

- インストール済みのパッケージ一覧を表示する
    ```
    > npm list
    > npm ls
    ```
- `-g`オプションで、グローバルインストールのパッケージ一覧を表示する
    ```
    > npm list -g
    ```

# パッケージのアップデート

# パッケージのアンインストール

# パッケージの検索

# npmbox

npmboxを使うと依存モジュールを含めてパッケージ化できるので、npmboxでパッケージを作成し、オフラインPCに持っていけば、オフラインPCでもnpmパッケージを利用できる

## npmboxのインストール

```
> npm install npmbox
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
