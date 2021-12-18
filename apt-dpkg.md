# apt & dpkg

`apt`は、オンライン環境でパッケージをダウンロード＆インストールする時に使用する

`dpkg`は、パッケージ（debファイル）からインストールする時に使用する

# apt

- パッケージリストを更新する
    ```bash
    > sudo apt update
    ```
- インストール済みパッケージをアップデートする
    ```bash
    > sudo apt upgrade
    ```
- パッケージを検索する
    ```bash
    > apt search <package-name>
    ```
- インストール済みのパッケージ一覧を表示する
    ```bash
    > apt list --installed
    ```
- パッケージをインストールする
    ```bash
    > sudo apt install <package-name>
    ```
- パッケージを削除する
    ```bash
    > sudo apt remove <package-name>
    > sudo apt remove --pruge <package-name>
    ```
    - パッケージを削除しても設定ファイルは残るので、再インストールにより設定情報を引き継げる
    - `--purge`オプションをつけると、設定ファイルも含めて完全に削除する
- キャッシュされているdebファイルを削除する
    ```bash
    > sudo apt clean
    ```

# dpkg

- インストール済みのパッケージ一覧を表示する
    ```bash
    > dpkg -l
    > dpkg -l <pattern>
    ```
- パッケージをインストールする
    ```bash
    > sudo dpkg -i path/to/file.deb
    
    # -G: 新しいパッケージがインストール済みの場合はスキップする
    > sudo dpkg -iG path/to/file.deb

    # --no-act: 実際にインストールしない. 依存関係等の確認のみ.
    > sudo dpkg --no-act -iG path/to/file.dev
    ```
    - `--no-act`オプションは、全てのオプションの前に指定しなければならない
- パッケージをアンインストールする
    ```bash
    > sudo dpkg -r <package-name>

    # 設定ファイルを含めて完全に削除する
    > sudo dpkg -P <package-name>
    ```
- インストールが完了していない（中断している）パッケージを確認する
    ```bash
    > dpkg -C
    ```
    - `dpkg -l`でも確認可能 
        - 一覧表示の左側が`ii`ではなく`iU`とかになっているパッケージは、依存パッケージが不足していて、インストールが中断されているパッケージを示す


# オフラインPCへのパッケージインストール

- 基本的には、debファイルをオフライン端末に持っていき、`sudo dpkg -iG *.deb`を実行すれば良い
- debファイルの入手方法はいろいろあるが、依存するパッケージを全て準備する必要があり、かなり骨が折れる
- `apt`のキャッシュから回収する方法等があるが、現状のおすすめは、以下の`pkgdownload`スクリプトを使う方法
    - [wickerscripts - GitHub](https://github.com/yusuphwickama/wickerscripts)
    - オンライン端末で `> pkgdownload <package-name>`を実行して、debファイルを固めたtar.gzファイルを入手する
    - オフライン端末に展開し、`> sudo dpkg -iG *.deb`を実行する
    - 依存関係の階層が深い場合、依存関係が解決できずにインストールが中断されるが、中断されたパッケージを再度`pkgdownload`で入手してインストールする
    - この入手とインストールを何回か繰り返せばインストール完了するはず
