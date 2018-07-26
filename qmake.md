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
- subdirs
    - SUBDIRSでサブディレクトリを指定する

## CONFIG

- debug
- release
- c++11
- c++14
- ordered
- console
- dll / shared
- static / staticlib
- app_bundle : mac用
- lib_bundle : mac用

## INCLUDEPATH

## HEADERS

## SOURCES

## DEFINES

## LIBS

## DESTDIR

## DLLDESTDIR

## QT

適用するQtモジュールを指定する

## QMAKE_PRE_LINK

ビルド前コマンド

## QMAKE_POST_LINK

ビルド後コマンド

## \_PRO_FILE_

proファイルパス
## \_PRO_FILE_PWD_

proファイルのディレクトリ

# VisualStudio

- .vcprojファイルを作成する
    ```
    > qmake -tp vc
    ```
- サブディレクトリから再帰的に.vcprojファイルを作成 & .slnファイルを作成する
    ```
    > qmake -tp vc -r
    ```
