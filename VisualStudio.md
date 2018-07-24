# Visual Studio

Visual Studioの関する覚書

# C++

## UTF-8を使う

- ソースコードが**BOMありUTF-8**なら、コンパイラが文字コードを自動判別してくれる（らしい）
- **BOMなしUTF-8**の場合、コンパイルオプションで文字コードを指定する

    |オプション|説明|
    |---|---|
    |/source-charset:utf-8|ソースコードの文字コードをUTF-8に設定する|
    |/execution-charset:utf-8|実行プログラムの文字コードをUTF-8に設定する|
    |/utf-8|ソースコード及び実行プログラムの文字コードをUTF-8に設定する|
    
- コンソールプログラムに対し、`/execution-charset:utf-8`や`/utf-8`を指定すると、コマンドプロンプトが文字化けする
- コンパイルオプションは、[プロパティ] - [C/C++] - [コマンドライン] ページの「追加のオプション」に指定する

## Tips

- [コンパラオプション一覧 (Microsoft Docs)](https://docs.microsoft.com/ja-jp/cpp/build/reference/compiler-options-listed-by-category)

