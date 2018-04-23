# Config設定

configは、システム、グローバル、ローカルの3段階があり、この順番で優先度が高くなる（system < global < local）.

システム設定は、基本的に使用する必要はない.

## 設定内容を確認する

一覧表示
```
> git config --list
> git config -l
```

特定の項目
```
> git config <項目名>
```

## 設定を削除する

```
> git config --unset <削除する項目名>
```

## 名前とメールアドレスを登録する（`user.name`, `user.email`）

```
> git config --global user.name "xxxxx"
> git config --global user.email "xxxxx"
```

## 改行コードを自動変換しないようにする（`core.autocrlf`, `core.safecrlf`）

改行コードを自動で変換しない
```
> git config --global core.autocrlf false
```

改行コードが混在していても自動で変換しない
```
> git config --global core.safecrlf true
```

## git statusで日本語ファイル名を文字化けしないようにする（`core.quotepath`）

```
> git config --global core.quotepath false
```

## エディタを設定する（`core.editor`）

（例）エディタにsakuraを指定する (UTF-8指定)

```
> git config --global core.editor "'C:/xxx/xxx/sakura.exe' -CODE=4"
```

## Fast-Fowardに関して設定する（`merge.ff`, `pull.ff`）

marge時Fast-Fowardしないようにする（＊）
```
> git config --global merge.ff false
```
＊ default設定を--no-ffにしているだけなので、--ffオプションをつければFast-Fowardとなる.

pull時はFast-Fowardする
```
> git config --global pull.ff only
```

## push時のdefault挙動を設定する（`push.default`）

push.default設定値

|設定値|説明|
|---|---|
|nothing|何もしない|
|matching|ローカルとリモートで同名のブランチを全てプッシュする|
|upstream|カレントブランチにupstreamが設定されている場合、プッシュする|
|simple|カレントブランチにupstreamが設定されており、かつブランチ名が一致する場合、プッシュする|
|current|upstreamの設定有無に係わらず、カレントブランチをプッシュする|

（例）simpleを設定する（推奨）
```
> git config --global push.default simple
```

# 変更を元に戻す

## ステージングを解除する（git reset）

```
> git reset
> git reset HEAD <ファイル名1> <ファイル名2> ...
```

## 変更を破棄する（git checkout）

```
> git checkout 
> git checkout -- <ファイル名1> <ファイル名2> ...
```

# コミット内容を変更する

## 直前のコミットを修正する（git commit --amend）

```
git commit --amend
```

- 直前のコミット内容を修正する場合、修正内容をステージングした後、「--amend」オプションをつけてコミットすると、そのコミットは直前のコミットに統合される.
- コミットメッセージのみを修正する場合、ステージングが存在しない状況で「commit --amend」すると、エディタが起動し、コミットメッセージを修正することができる。

## 過去のコミットを打ち消すコミットを作る（git revert）

```
git revert <commit>
```

## 過去のコミットを修正する（git rebase -i）

```
> git rebase -i <commit>
```

```
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
```

|コマンド|説明|
|---|---|
|pick||
|reword|コミットメッセージを修正する.|
|edit|コミット自体を編集する.|
|squash|直前のコミットに統合する. コミットメッセージは残す.|
|fixup|直前のコミットに統合する. コミットメッセージは破棄する.|
|exec||

`edit`等でコミット内容を変更した際は、以下のコマンドで変更を保存する.

```
> git commit --amend
```

`rebase`を続ける場合は、以下のコマンドを実行する.

```
> git rebase --continue
```

`rebase`を中断する場合は、以下のコマンドを実行する.
```
> git rebase --abort
```

# .gitignore

- /を含まない指定（例: hoge）

    .gitignore以下の全サブディレクトリ下にあるhogeファイルを無視する.

- 先頭が/で始まる指定（例: /hoge）

    .gitignoreがあるディレクトリを基準としたhogeファイルを無視する.

- 末尾が/で終わる指定（例: hoge/）

    .gitignore以下の全サブディレクトリ下にあるhogeディレクトリを無視する.

- 先頭が/で始まり、末尾が/で終わる指定（例: /hoge/）

    .gitignoreがあるディレクトリを基準としたhogeディレクトリを無視する.

- !で始まる指定（例: !hoge）

    gitignore指定を否定する.

## 参考

```
# 特定の拡張子のファイルを無視する場合は、/をつけない.
*.obj

# 特定のファイルを無視する場合は、先頭に/をつける.
/hoge.txt

# 特定のディレクトリを無視する場合は、先頭と末尾に/をつける.
/bin/
```

