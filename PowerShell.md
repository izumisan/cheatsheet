# PowerShell Tips

# 文字コード

- PowerShell ISEでps1スクリプトを作成すると文字コードはUTF-8(BOM付)のようなので、
ps1スクリプトはUTF-8(BOM付)が無難
    - UTF-8(BOMなし)では、ISEや標準出力で文字化けしてしまう
- UTF-8(BOM付)以外では、Shift_JIS, UTF-16BE, UTF-16LEが文字化けせずに実行できるらしい。

# 実行ポリシー

|value|local script|remote script|
|---|:-:|:-:|
|Restricted|-|-|
|AllSigned|V*|V*|
|RemoteSigned|V|V*|
|Unrestricted|V|V|

\* 署名付きのみ実行可能

- `RemoteSigned`にしておけば良い

```ps
# 実行ポリシーを確認する
> Get-ExecutionPolicy
```
```ps
# システムの実行ポリシーを変更する
# （レジストリ変更, 要管理者権限）
> Set-ExecutionPolicy xxx

# プロセスレベルで実行ポリシーを変更する
# （管理者権限不要）
> Set-ExecutionPolicy RemoteSigned -Scope Process
```
```ps
# 実行ポリシーを指定してPowerShellを起動する
> powershell -ExecutionPolicy RemoteSigned

# 実行ポリシーを指定してPowerShellスクリプトを実行する
> powershell -ExecutionPolicy RemoteSigned -File path/to/file.ps1
```

# ヘルプ

```ps
> help コマンドレット
```

# 起動引数

- `Param()`により、起動引数を宣言する
- `Param()`により起動引数を明示的に宣言していない場合、自動変数 `$Args` に起動引数が格納されている

# Strict Mode

```ps
> Set-StrictMode -Version Latest
```

# Error Action Preference

```ps
# エラー発生時に実行停止する
> $ErrorActionPreference = "Stop" 
```

|Value|Description|
|---|---|
|Continue（既定値）|エラーメッセージを表示し、実行を続行する|
|Stop|エラーメッセージを表示し、実行を停止する|
|Inquire|エラーメッセージを表示し、続行するかどうかの確認メッセージを表示する|
|Suspend||
|SilentlyContinue||

# try-catch-finally

- `$ErrorActionPreference`に`Stop`を指定している場合、try-catch構文が使用できる.
- 例外オブジェクトは、自動変数`$_`や`$error[0]`で参照できる

```ps
try {
    ...
} catch {
    ...
} finally {
    ...
}
```

# 標準出力への表示を抑制する

- `$null`にリダイレクトする
- .NET APIの場合、`[void]`を指定することでメソッドの戻り値を捨てても戻り値が標準出力に表示されなくなる


# ハッシュ値を取得する

```ps
# Get-FileHashでハッシュ値を取得する
# - Hashプロパティで参照可能
# - 既定のアルゴリズムはSHA-1
> echo (Get-FileHash path/to/file).Hash

# アルゴリズム指定
> echo (Get-FileHash path/to/file -Algorithm [SHA1|SHA256|MD5]
```

# zip圧縮

```ps
> Compress-Archive -Path 圧縮元 -DestinationPath 出力先
```

- `-Force`オプションで、`-DestinationPath`で指定したファイルが既に存在している場合でも上書きする
