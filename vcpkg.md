# vcpkg

- Github
    - https://github.com/microsoft/vcpkg
- ドキュメント
    - https://vcpkg.readthedocs.io/en/latest/README/

# セットアップ

1. クローン  
    Githubリポジトリ(https://github.com/microsoft/vcpkg)をクローンする

1. ビルド  
    `bootstrap-vcpkg.bat` を実行すると `vcpkg.exe` が生成される

1. （任意）VisualStudioに統合する  
    以下のコマンド実行で、vcpkgがVisualStudioに統合される
    ```
    > ./vcpkg.exe integrate install
    ```

# インストール

- 利用可能なパッケージを検索する
    ```
    > vcpkg search xxx
    ```
- パッケージをインストールする
    ```sh
    > vcpkg install パッケージ名
    > vcpkg install パッケージ名 --triplet=xxx
    > vcpkg install パッケージ名:xxx

    # protobufの場合
    > vcpkg install protobuf:x64-windows
    > vcpkg install protobuf:x64-windows-static
    ```
    - コマンド実行により、ソースのダウンロードとビルドが実行される
        - 依存関係は自動で解決してくれる
        - ビルドした生成物は、`installed`及び`packages`ディレクトリ下に格納される
    - triplet
        - x64-windows-static
        - x64-windows
        - x86-windows
        - etc.
    - 利用可能なtripletは、`vcpkg help triplet` コマンドや、クローンしたリポジトリの`triplets`ディレクトリ下で確認可能
- パッケージをエクスポートする
    ```
    > vcpkg export パッケージ名 --nuget
    > vcpkg export パッケージ名 --zip
    > vcpkg export パッケージ名 --7zip
    ```

# バージョン指定してインストール

vcpkg下に配置できるライブラリのバージョンは一つのみ.
特定バージョンのライブラリを利用する場合は、個別にvcpkgをクローンし、`ports`ディレクトリ下の各パッケージの`profile.cmake`を書き換える....らしい

# triplet file (configuration)

see. https://vcpkg.readthedocs.io/en/latest/users/triplets/


