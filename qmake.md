# qmake

# 基本

## 変数参照

- 変数の参照：`$$HOGE`, `$${HOGE}`
- 環境変数の参照：`$$(PWD)`, `$(PWD)`
    - `$$(...)`は、qmake時に展開される
    - `$(...)`は、Makefileで処理される時に展開される（$(...)がMakefileに出力される）
- qmakeプロパティの参照：`$$[QT_VERSION]`

# 変数（qmakeプロパティ）

## TARGET

## TEMPLATE

- app
- lib
    - `CONFIG`で`dll`又は`static`を指定する
- subdirs
    - SUBDIRSでサブディレクトリを指定する

## CONFIG

- c++11 / c++14 / c++17
- build_all
    - `debug_and_release`と合わせて指定することにより、ビルド時、debugビルド、releaseビルドが共に行われる
- ordered
    - `TEMPLATE=subdirs`の場合に使用する
    - `SUBDIRS`に指定したプロジェクト順にビルドを行う
- console
- dll / shared
- static / staticlib
- app_bundle : mac用
- lib_bundle : mac用
- no_keywords
    - moc用キーワード（`signals`, `slots`, `emit`）を無効にする（3rdパーティとキーワードが被った場合に使用）
    - `no_keywords`でも、`Q_SIGNALS`, `Q_SLOTS`, `Q_EMIT`で、Qtシグナル/スロットが利用できる

## INCLUDEPATH

## HEADERS

## SOURCES

## DEFINES

- マクロ定義

## LIBS

- ライブラリを指定する
- `-L`, `-l`オプションが有効
    - `-L`: ライブラリディレクトリ
    - `-l`: ライブラリ名（xxx.lib, libxxx.a）

## PRE_TARGETDEPS

- appプロジェクト側で、依存する（リンクする）スタティックライブラリを指定する
- appビルド時、ライブラリ側が更新されている場合、再リンクされる

## DESTDIR

- ビルドターゲット（*.exe, *.lib, *.dll等）の出力先

## DLLDESTDIR

- dllファイルの出力先

## DEF_FILE

- モジュール定義ファイル（*.def）を指定する
- windows only

## QT

- 適用するQtモジュールを指定する
    - core
    - gui
    - quick
    - testlib

## QMAKE_PRE_LINK

- ビルド前コマンド

## QMAKE_POST_LINK

- ビルド後コマンド

## QMAKE_PROJECT_DEPTH

```
QMAKE_PROJECT_DEPTH = 0
```
- proファイルからincludeされるpriファイルの階層（includeネスト）が深い場合やディレクトリ階層が複雑な場合、qmakeでよくわからないエラーに悩まされる場合がある
- この場合、`QMAKE_PROJECT_DEPTH = 0` を指定すると、解消する
- `QMAKE_PROJECT_DEPTH = 0` を指定すると、makefileには相対パスではなく絶対パスで出力されるようになる
- [Undocumented QMake](https://wiki.qt.io/Undocumented_QMake) 参照

## QT_ARCH

- ターゲットアーキテクチャ
    - 32bitターゲットの場合、`i386`
    - 64bitターゲットの場合、`x86_64`

## OUT_PWD

- Makefileの出力先ディレクトリ

## \_PRO_FILE_

- proファイルパス

## \_PRO_FILE_PWD_

- proファイルのディレクトリ

# サンプル集

- ビルド構成による切り替え
    ```
    CONFIG(debug, debug|relase) {
        # for debug
    } else {
        # for release
    }
    ```
- コンパイラによる切り替え
    ```
    # 複数行ver
    msvc {
        # Visual Studio用オプション設定
    }
    mingw {
        # MINGW用オプション設定
    }

    # 一行ver
    msvc: xxxx
    mingw: xxxx
    ```
- debugビルド/releaseビルドを同時に実施する
    ```
    CONFIG += debug_and_release build_all
    ```

- ターゲットアーキテクチャ（32bit/64bi）による切り替え
    ```
    contains(QT_ARCH, i386): message("32bit")
    contains(QT_ARCH, x86_64): message("64bit")
    ```


# VisualStudio向け

- .vcprojファイルを作成する
    ```
    > qmake -tp vc
    ```
- サブディレクトリから再帰的に.vcprojファイルを作成 & .slnファイルを作成する
    ```
    > qmake -tp vc -r
    ```
- UTF-8を指定する
    ```
    QMAKE_CXXFLAGS += /source-charset:utf-8
    QMAKE_CXXFLAGS += /execution-charset:utf-8
    ```
