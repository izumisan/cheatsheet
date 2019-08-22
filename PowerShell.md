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
