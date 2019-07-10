# Visual Studio

Visual Studioに関する覚書

# ショートカットキーを変更する

[環境] - [キーワード] からショートカットキーを設定できる

## 設定メモ

|項目|内容|
|---|---|
|キーボードマップ|`Visual C++ 6`|
|エディターコンテキストメニュー, コードウィンドウ, ヘッダーコードファイルの切り替え|`F4`|

# 拡張機能

- [Configuration Transform](https://marketplace.visualstudio.com/items?itemName=GolanAvraham.ConfigurationTransform)
    - app.configをdebug用とrelease用で切り替えることができる
    - ASP.netの開発ツールを入れておかないと、この拡張機能で作成したapp.debug.config/app.release.configを含むプロジェクトがビルドできない

# nugetパッケージのオフラインインストール

- パッケージソースに`nuget.org`が設定されている場合、例えローカルパッケージであっても、オフラインインストールができないので注意


# ビルドイベントでファイルコピー

```
XCOPY /Y /I /E /D {source} {dest}
```

|オプション|説明|
|:-:|---|
|/Y|上書き確認なし|
|/I|コピー先にディレクトリを作成する|
|/E|空ディレクトリもコピーする|
|/D|新しい場合にコピーする|


# C++

# デバッグ実行画面を自動で閉じないようにする

[リンカー] - [システム] - [サブシステム]に、`コンソール (/SUBSYSTEM:CONSOLE)` を設定する

# SDLチェックを無効にする

- SDL（Security Development Lifecycle）チェックが有効な場合、`strcpy()`や`scanf()`が警告ではなくエラーとして扱われる.
- `strcpy()`や`scanf()`等は`_CRT_SECURE_NO_WARNINGS`を定義すれば警告抑制でエラー回避できるが、`deprecated`属性が指定した関数等の使用時はビルドに失敗する（警告ではなくエラーとなる）
- SDLチェックを無効にすると、VisualStudio特有のエラーチェックを無効化し、警告として扱われるようになる.
- `_CRT_SECURE_NO_WARNINGS`を指定すると`strcpy()`や`scanf()`等の警告は抑制されるが、SDLチェックを無効にした場合、`strcpy()`や`scanf()`等は警告となる.


# Win32(x86), x64

- プラットフォームが混在している場合、ビルドはできるが実行はできない（エラーとなる）らしい
- 基本的にEXEとDLLのプラットフォームは合わせる必要がある

## 64bit OS

|EXE|DLL|実行可否|Note|
|:-:|:-:|:-:|---|
|x64|-|OK|-|
|x64|x64|OK|-|
|x64|win32(x86)|NG|EXEとDLLでCPUアーキテクチャが異なる|
|win32(x86)|-|OK|-|
|win32(x86)|x64|NG|EXEとDLLでCPUアーキテクチャが異なる|
|win32(x86)|win32(x86)|OK|-|

## 32bit OS

|EXE|DLL|実行可否|Note|
|:-:|:-:|:-:|---|
|x64|-|NG|x64EXEは実行できない|
|x64|x64|NG|x64EXEは実行できない|
|x64|win32(x86)|NG|x64EXEは実行できない|
|win32(x86)|-|OK|-|
|win32(x86)|x64|NG|EXEとDLLでCPUアーキテクチャが異なる|
|win32(x86)|win32(x86)|OK|-|

## Any CPU ？

- .NET用
- 起動または呼び出し元に応じてCPUプロセスが異なる
    - 64bitOSから実行されたAnyCPU EXEは、64bitプロセスとして実行する
    - 32bitOSから実行されたAnyCPU EXEは、32bitプロセスとして実行する
    - 64bitプロセスから呼び出されたAnyCPU DLLは、64bitプロセスとして実行する
    - 32bitプロセスから呼び出されたAnyCPU DLLは、32bitプロセスとして実行する
- 32bitOSで、AnyCPU EXEからx86 DLLは呼び出せる
- 64bitOSで、AnyCPU EXEからx86 DLLは呼び出せない？

# プラットフォーム（x86 or x64）を確認する

VisualStudioの開発者用コマンドプロントで、下記コマンドを実行する
```
> dumpbin /headers path/to/file
```

# DLLのエクスポート関数を確認する

VisualStudioの開発者用コマンドプロントで、下記コマンドを実行する
```
> dumpbin /exports path/to/file
```

# 依存ライブラリを確認する

- VisualStudioの開発者用コマンドプロントで、下記コマンドを実行する
    ```
    > dumpbin /dependents path/to/file
    ```

- Dependency Walkerを使う
    - [Dependency Walker ダウンロード](http://www.dependencywalker.com/)
    - GUIツール

- The Windows Deployment Toolを使う（Qtライブラリ限定）
    - Qt用コマンドプロンプトで下記コマンドを実行すると、依存しているQtライブラリが確認できる
        ```
        > windeployqt path/to/file
        ```


# UTF-8を使う

- ソースコードが**BOMありUTF-8**なら、コンパイラが文字コードを自動判別してくれる（らしい）
- **BOMなしUTF-8**の場合、コンパイルオプションで文字コードを指定する

    |オプション|説明|
    |---|---|
    |/source-charset:utf-8|ソースコードの文字コードをUTF-8に設定する|
    |/execution-charset:utf-8|実行プログラムの文字コードをUTF-8に設定する|
    |/utf-8|ソースコード及び実行プログラムの文字コードをUTF-8に設定する|
    
- コンソールプログラムに対し、`/execution-charset:utf-8`や`/utf-8`を指定すると、コマンドプロンプトが文字化けする
- コンパイルオプションは、[プロパティ] - [C/C++] - [コマンドライン] ページの「追加のオプション」に指定する

# コンパイラオプション

- [コンパラオプション一覧 (Microsoft Docs)](https://docs.microsoft.com/ja-jp/cpp/build/reference/compiler-options-listed-by-category)

# `std::min()/std::max()`がエラーになる

`windows.h`で`min/max`がマクロ定義されているため、algorithmヘッダの`std::min()/std::max()`がマクロ置換されてしまい、コンパイルエラーとなる.

`NOMINMAX`を定義することで、マクロ展開が抑制される.

- [windows.hのmin/maxマクロ回避策４パターン](https://yohhoy.hatenadiary.jp/entry/20120115/p1)

# C++（CLRプロジェクト）

## ソースファイルでstdafx.hのインクルードが必要となる

- 「プリコンパイル済みヘッダー」が"使用"になっており、「プリコンパイル済みヘッダーファイル」として"stdafx.h"が指定されているため、stdafx.hをインクルードしていないとコンパイルエラーとなる
- 「必ず使用されるインクルードファイル」に"stdafx.h"を指定すると、ソースファイルへの`#include "stdafx.h"`の記述は不要となる
