# EditorConfig

異なるエディタ・IDE間で文字コードや改行コード等スタイルを保つテキストエディタープラグイン.

有名どころのエディタ・IDEではデフォルトで対応しているため、プラグインは不要. デフォルト対応していなくても、多数のエディタ・IDE用のプラグインが準備されている.

# 公式サイト
- [EditorConfig](https://editorconfig.org/)

# プラグイン

- Visual Studio
    - 不要
- Visual Studio Code
    - [EditorConfig for Visual Studio Code (Marketplace)](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)
- Qt Creator
    - [EditorConfig Plugin for QtCreator (GitHub)](https://github.com/editorconfig/editorconfig-qtcreator)

# `.editorconfig`設定例

```ini
root = true

[*]
end_of_line = crlf
charset = utf-8
indent_style = space
indent_size = 4
trim_trailing_whitespace = false
insert_final_newline = false

[*.md]
trim_trailing_whitespace = false
insert_final_newline = true

[*.{h,c,cpp}]
trim_trailing_whitespace = true
insert_final_newline = true
```

- iniフォーマットベースで設定する
- `.gitignore`のように、`.editorconfig`が存在するディレクトリの下位ディレクトリに対し、この設定が有効となる
    - `root = true` が設定されている`.editorconfig`より上位階層は検索されない
    - `root = true` は先頭で指定する必要がある
- セクション部分で、対象とするファイルを指定する
- `#`でコメント

# ファイル指定

ワイルドカードが利用できる

|記述|説明|
|---|---|
|*|任意の文字列. ただし、パス区切り文字はマッチしない|
|**|任意の文字列|
|?|任意の1文字|
|foo|"foo"というファイル|
|!foo|"foo"というファイルを除くファイル|
|{foo,bar,baz}|"foo", "bar", "baz"というファイル|

- `.editorconfig`と同ディレクトリのファイルのみ指定する場合は `[./*]` と指定する

# 設定項目

- `charset`
    - `latin1`
    - `utf-8`
    - `utf-8-bom`
    - `utf-16be`
    - `utf-16le`
    - ※`shift_jis`には対応していない（指定できない）
- `end_of_line`
    - `lf`
    - `crlf`
    - `cr`
- `indent_style`
    - `space`
    - `tab`
- `indent_size`
- `tab_width`
    - `indent_size`より優先される. 省略時は`indent_size`となる
- `trim_trailing_whitespace`
    - 行末の空白を除去するか否か
    - `true`
    - `false`
- `insert_final_newline`
    - ファイルを改行で終端させる
    - `true`
    - `false`
