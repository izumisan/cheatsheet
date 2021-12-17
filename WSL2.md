# WSL2

2021年8月くらいのアップデートで、Windows10 Homeでもコマンド一つでWSL2がインストールできるようになった.

# WSL2 & Ubuntu のインストール

1. PowerShellで下記コマンドを実行する（要管理者権限）
    ```
    > wsl --install
    ```
    - 上記コマンド１つで、仮想化の有効化やUbuntuのダウンロード・インストールまで実行される
1. PC再起動
    - ここで、`error: 0x80370102` が出たので、下記を参考にBIOSで仮想化を有効にした
        - `F10` でBIOS起動し、`Virtualization Technology` を`Enabled` に変更
    - [Windows Subsystem for Linux のトラブルシューティング - Microsoft Docs](https://docs.microsoft.com/ja-jp/windows/wsl/troubleshooting)
    - [【WSL2】wsl2のインストールで0x80370102 エラーが出たときの対処方法【HP】](https://monkey999por.hatenablog.com/entry/2020/10/01/221243)
1. Ubuntu rootユーザのユーザ名＆パスを設定する
1. パッケージの更新
    ```bash
    # パッケージ一覧の更新とアップデート
    $ sudo apt update
    $ sudo apt upgrade
    ```
    - `sudo apt update && sudo apt upgrade`でも可

# 初期設定

## 日本語化

1. 日本語パックのインストール
    ```bash
    $ sudo apt install -y language-pack-ja
    ```
    - `locale -a`で`ja_JP.utf8`が表示されればok
1. 日本語ロケールの設定
    ```bash
    $ sudo update-locale LANG=ja_JP.utf8
    ```

## gcc, cmakeのインストール

- gcc, make等のビルドツール
    ```bash
    $ sudo apt install build-essential
    ```
- cmake
    ```bash
    $ sudo apt install cmake
    ```

## 入力補間時等のWindows通知音（ビープ音）を無効にする

- Ubuntuターミナルでは、入力補間時のタブ押下時やその他操作時に「タララーン」と通知音が鳴りまくってしまう
- `.inputrc`ファイルに次の一行を追加することで、音が鳴らなくなる
    ```
    set bell-style none
    ```

# Windows Terminal

Windows用ターミナルアプリ

- インストール
    - Microsoft Storeからインストール
- 開始ディレクトリをUbuntuホームに設定する
    - デフォルトでは、windowsのユーザディレクトリになっていて使いにくい
    - [設定] - [開始ディレクトリ] にUbuntuのホームディレクトリをWindowsパス形式で設定する
        - `\\wsl$\Ubuntu\home\<user-name>`

# VSCode拡張機能 (Remote - WSL)

- Ubuntu側でVSCodeの使い勝手を良くする拡張機能
    1. Windows側のVSCodeから、`Remote-WSL`の拡張機能をインストールする
    1. Ubuntu側から`code .`でVSCodeを起動すると、初期設定が自動で行われる
- この拡張機能を入れなくてもVSCodeは利用できるが、ターミナルのHOMEはWindows設定のまま(ユーザフォルダ)だったり、改行コードもWindowsに合わせてCRLFだったりするので、使い勝手は良くない.
- この拡張機能により、Windows側とUbuntu側がVSCodeの設定や拡張機能が別々に管理される（っぽい）

# Remote-WSLをオフラインPCで利用する

1. VSCodeのバージョンに対応したvscode-serverをDownloadする
    1. Windows側のVSCodeのコミットIDを確認する
    1. 次のURLからvscode-serverを入手する
        `https://update.code.visualstudio.com/commit:${commit_id}/server-linux-x64/stable`
1. vscode-serverのオフラインセットアップ
    1. ubuntu側HOMEで、`$ code .`を実行する
        - `Remote-WSL`の初期設定のため自動でDLを試みるが、オフライン環境なのでErrorとなる
        - `~/.vscode-server/`が作成されている
    1. `.vscode-server/`を下記構成となるように、DLしたvscode-serverを`~/.vscode-server/bin/{commit_id}/`内に展開する
        ```
        ~/.vscode-server/
            bin/
                {commit_id}/
                    bin/
                    LICENSE
                    package.json
                     :
        ```
- 参考
    - [How can I install vscode-server in linux offline - stack overflow](https://stackoverflow.com/questions/56671520/how-can-i-install-vscode-server-in-linux-offline)

# wslコマンド

wslコマンドは、コマンドプロンプトやPowerShell等Windows側で使用する.
`wsl.exe --shutdown`のように`.exe`を付けることで、Linux側からwslコマンドを実行することができる.

- Linuxコマンドを実行する
    ```
    > wsl {Linuxコマンド}
    ```
- Linuxのインストール・アップデート等
    - `wsl --install`
        - デフォルトではUbuntuをインストールする
        - `-d`オプションでディストリビューションの指定が可能
    - `wsl --list -v`
        - インストール済みのディストリビューションを表示する
    - `wsl --list -o`
        - インストール可能なディストリビューションを表示する
    - `wsl --update`
        - Linuxカーネルのアップデート
- wslを終了する
    ```
    > wsl --shutdown
    ```

# ディストリビューションのインポート/エクスポート

- ディストリビューションをexportする
    ```
    # wsl --export {ディストリビューション名} {出力ファイル名.tar}
    > wsl --export Ubuntu ./export-ubuntu.tar
    ```
- ディストリビューションをimportする
    ```
    # wsl --import {ディストリビューション名} {インポート先} {exportしたtarファイル}
    > wsl --import ubuntu2 ~/wsl/ubuntu2 path/to/export-ubuntu.tar
    ```
    - `> wsl -l -v`でインポートしたディストリビューションがリスト表示されていればok
- インポートしたディストリビューションの起動
    ```
    # wsl -d {ディストリビューション名} -u {ユーザ名}
    > wsl -d ubuntu2 -u root
    ```
    - インポートしたディストリビューションのデフォルトユーザはrootになっているので、ユーザ名を指定して起動する必要がある
- インポートしたディストリビューションのデフォルトユーザを変更する
    - `/etc/wsl.conf`を作成し、デフォルトユーザを指定する
        ```
        [user]
        default=default-user-name
        ```
- 参考
    - [【備忘録】WSL2でのimport, exportとログイン設定 - Qiita](https://qiita.com/koji_hattori/items/1480d25aca8cdf5ac4a1)
    - [WSL の起動時デフォルト ユーザ変更 - みねっちょのマイコン関係ブログ](https://minettyo.com/entry/wsl_defaultuser)
    - [WSL での詳細設定の構成 - Microsoft Docs](https://docs.microsoft.com/ja-jp/windows/wsl/wsl-config)

# Windows - WSL(Ubuntu) 間のファイルアクセス

- Windows側からWSL側ファイルにアクセス
    - ネットワークフォルダ`\\wsl$\Ubuntu\`で、Ubuntuのルートディレクトリにアクセス可能（Ubuntuが起動している場合）
- WSL側からWindows側ファイルにアクセス
    - WindowsのCドライブは、`/mnt/c/`にマウントされている

# Link

- [WSL 開発環境を設定するためのベスト プラクティス - Microsoft Docs](https://docs.microsoft.com/ja-jp/windows/wsl/setup/environment)
- [WSL2を日本語化するときにやったこと](https://zenn.dev/ryuu/articles/wsl2-locale-jp)
- [WSL2のUbuntu 20.04を日本語化する](https://qiita.com/myalpine/items/fb45b222924b2e61ea9f)

