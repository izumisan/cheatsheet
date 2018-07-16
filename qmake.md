# qmake

# 変数

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

# VisualStudio

- .vcprojファイルを作成する
    ```
    > qmake -tp vc
    ```
- サブディレクトリから再帰的に.vcprojファイルを作成 & .slnファイルを作成する
    ```
    > qmake -tp vc -r
    ```
