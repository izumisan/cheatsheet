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

## 改行コードに関する設定（`core.autocrlf`, `core.safecrlf`）

改行コードの自動変換設定
```
> git config --global core.autocrlf <設定値>
```

|設定|チェックアウト時|コミット時|
|:-:|:-:|:-:|
|true|LF->CRLF|CRLF->LF|
|input|変換しない(MacやLinuxの場合)<br>LF->CRLF(Windowsの場合)|CRLF->LF|
|false|変換しない|変換しない|
\* Windowsの場合、trueとinputに差異はない.


Gitでは、開発環境の違いによる改行コード問題に対応するため、リポジトリ内の改行コードはLFを推奨している。`core.autocrlf`を設定することで、Windowsにおいては、チェックアウト時にCRLFに、コミット時にLFに自動的に変換するようにすることができる。

プロジェクトの開発環境がWindowsのみの場合、CRLFのままリポジトリに記録しても問題ないので、`core.autocrlf=false`でも良い。

なお、Gitはソースコード管理ツールのため、バイナリファイルの管理は苦手なので、trurもしくはinputの場合、バイナリファイルを壊してしまう可能性がある。
.gitattributeファイルで個別に設定すれば回避は可能だが、.gitattributesに`"* text=auto"`が指定されていると、core.autocrlfの設定より**gitattributesの設定が優先される**。

### 結局、どうする？

- core.autocrlf=true（windowsにおけるinput含む）の場合、.gitattributesファイルが適切に指定されていないとファイルを壊してしまう可能性があるので、自動変換しない設定が適当か...
- この場合、`"* text=auto"`が指定された.gitattributesファイルの有無によって改行コードが混在する可能性はあるが、改行コードはエディタで対処できるのでファイルを壊してしまうよりはずっとマシか.
- よって、結論としては次の設定が利口かな...
    |OS|core.autocrlf|
    |---|---|
    |Windows|false|
    |Linux, Mac|input or false|
- 上記設定をいきつつ、改行コードが問題になりそうだったら.gitattributesファイルでガチガチに強制しろということかな.


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

# ローカルの変更を元に戻す

## ステージングを解除する（`git reset`）

```
> git reset
> git reset HEAD <ファイル名1> <ファイル名2> ...
```

## 変更を破棄する（`git checkout`）

```
> git checkout 
> git checkout -- <ファイル名1> <ファイル名2> ...
```

# コミット内容を変更する

## 直前のコミットを修正する（`git commit --amend`）

```
> git commit --amend
```

- 直前のコミット内容を修正する場合、修正内容をステージングした後、「--amend」オプションをつけてコミットすると、そのコミットは直前のコミットに統合される.
- コミットメッセージのみを修正する場合、ステージングが存在しない状況で「commit --amend」すると、エディタが起動し、コミットメッセージを修正することができる。

## 過去のコミットを修正する（`git rebase -i`）

```
> git rebase -i <commit>
```

- `git rebase -i`で指定したコミット以降のコミットを編集する
- コマンド実行により、コミットを編集するエディタが起動する
- コミット履歴は、通常の`git log`と表示順が異なり、下の方が新しいコミット
- 並び順を入れ替えるとコミット順序が入れ替わる

```bash
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
|reword|コミットメッセージを修正する|
|edit|コミット自体を編集する|
|squash|指定したコミットを直前のコミットに統合する. コミットメッセージは残る|
|fixup|指定したコミットを直前のコミットに統合する. コミットメッセージは破棄され、統合されたコミットメッセージが残る|
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

## 過去のコミットを打ち消すコミットを作る（`git revert`）

```
> git revert <commit>
```

# ブランチを間違えたコミットを修正する

branchBにコミットすべきところ、間違えてbranchAにコミットしてしまったのを修正する

1. branchAからbranchBを作成する
1. branchAから間違えたコミットを取り除く（reset）
1. branchAにbranchBをマージする

# 追跡ファイル（Git管理ファイル）に対する操作

## ファイルを残したままインデックスのみ削除する

```
> git rm --chached <file>
```

## 追跡ファイルの変更を無視する

- ローカルの変更を無視するようになる（変更していないものとみなす）
    - 登録する
        ```
        > git update-index --asume-unchanged <ファイル名>
        ```
    - 解除する
        ```
        > git update-index --no-asume-unchanged <ファイル名>
        ```

- ローカルの変更を保持する
    - 登録する
        ```
        > git update-index --skip-worktree <ファイル名>
        ```
    - 解除する
        ```
        > git update-index --no-skip-worktree <ファイル名>
        ```

## ファイルの状態を確認する（`git ls-files`）

- 追跡ファイルを確認する
    ```
    > git ls-files
    ```

- 未追跡ファイル（un-tracked）を確認する
    ```
    > git ls-files --others
    > git ls-fiels -o
    ```

- 無視ファイル（ignoreファイル）を確認する
    ```
    > git ls-files --ignored
    > git ls-files -i
    ```

- 変更ファイル（未ステージング）を確認する
    ```
    > git ls-files --modified
    > git ls-files -m
    ```

- ステージングファイルを確認する
    ```
    > git ls-files --stage
    > git ls-files -s
    ```

- 追跡無視ファイル（assume-unchanged, skip-worktree）を確認する
    ```
    > git ls-files -v
    ```

# リモート操作

## リモートリポジトリの確認

```
> git remote -v
```

## プッシュ（push）

```
> git push <リモート名> <ローカルブランチ名>:<リモートブランチ名>
```

- 例： リモート（origin）に対し、ローカルのmasterブランチをリモートのmasterブランチ（origin/master）にプッシュする
    ```
    > git push origin master:master
    ```

- ローカルとリモートでブランチ名が等しい場合、ブランチ名は省略形が使える
    ```bash
    # git push origin master:masterの省略形
    > git push origin master
    ```

- 引数を省略した場合、リモートは'origin'、ブランチは'master'として解釈（推測）される
    ```bash
    # カレントブランチが、origin/masterにプッシュされる
    > git push
    ```
    引数を省略して単に`git push`すると、**カレントブランチ**が**origin/master**にプッシュされてしまうので、configでpushのデフォルト挙動を設定しておいた方が良い.

## リモートリポジトリを登録する

```
> git remote add <リモート名> <URL>
```

- 例
    ```bash
    # hogeブランチを'origin'という名前（識別子）で、
    # リモートブランチとして登録する.
    > git remote add origin https://xxx/xxx/xxx/hoge.git
    ```

## 追跡ブランチ（upstream）を登録する

```bash
# カレントブランチのupstreamとして、origin/hogeブランチを設定する
> git branch --set-upstream-to=origin/hoge
```

- 追跡ブランチを確認する
    ```
    > git branch -vv
    ```

## プル（pull）

`git pull`は、①リモートのリポジトリの内容をローカルのリポジトリに取り込み（`git fetch`）、その後、②カレントブランチに取り込んだブランチをマージする（`git merge FETCH_HEAD`）。

つまり、カレントブランチに対し、マージ処理が行われていることに注意する。

`git push`の逆操作として`git pull`と記載されている場合があるが、これは間違い。`git push`の逆操作（対操作）は`git fetch`である。

## リモートリポジトリのブランチをローカルリポジトリに取り込む

`git clone`直後や、他者が`push`したブランチ等、リモートにはあるがローカルにはないブランチを取り込みたい場合、`git fetch`でorigin/xxxx（ローカルリポジトリのリモート追跡ブランチ）を更新した後、`git branch xxxx origin/xxxxx`（origin/xxxxxを起点にしてxxxxブランチを作成）する。

後はいつも通り、`git checkout xxxx`でよい。

なお、ブランチ作成＋チェックアウトはオプション`-b`でいけるので、`git checkout -b xxxx origin/xxxx`でも良い。

# タグ

- タグ（コメントなし）の作成
    ```
    > git tag タグ名
    > git tag タグ名 コミットID
    ```

- タグ（コメントあり）の作成
    ```
    > git tag -a タグ名 -m コメント
    ```

- ローカルのタグをリモートに反映する
    ```
    > git push リモートリポジトリ タグ名
    ```

- ローカルの全てのタグをリモートに反映する
    ```
    > git push リモートリポジトリ --tags
    ```

- リモートをタグを取得する
    ```
    > git pull リモートリポジトリ --tags
    ```

- ローカルのタグを削除する
    ```
    > git tag -d タグ名
    ```

- リモートのタグを削除する
    ```
    > git push リモートリポジトリ :削除したタグ名
    ```

- タグ一覧を確認する
    ```
    > git tag
    ```

- タグを内容を確認する
    ```
    > git show タグ名
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

## 設定例

```bash
# 特定の拡張子のファイルを無視する場合は、/をつけない.
*.obj

# 特定のファイルを無視する場合は、先頭に/をつける.
/hoge.txt

# 特定のディレクトリを無視する場合は、先頭と末尾に/をつける.
/bin/
```

## .gitignoreのテンプレート

- [github / gitignore](https://github.com/github/gitignore)

## gitignore (global)

- $HOME/.config/git/ignore

特定のプロジェクトに依存せず、自分の環境に依存する除外設定は上記ファイルに書く.

ちなみに、core.excludesfileに.gitignore_globalを設定するのは、いまいち（非推奨とまでは言わないが、gitの流儀に反する？）らしい.

## exclude

- GIT_PROJECT_ROOT/.git/info/exclude

プロジェクト依存だが、他者と共有したくない除外設定は、上記ファイルに書く.

# .gitattributes

設定例
```
*           text=auto
*.txt       text
*.vcproj    text eol=crlf
*.sh        text eol=lf
*.jpg       -text
*.exe       binary
```

- `*   text=auto`
    - 全てのファイルに対し、text属性にautoを設定する
    - つまり、Gitがテキストファイルと判定したファイルに対し、改行コードの変換はGitに任せる
- `*.txt   text`
    - 拡張子がtxtのファイルに対し、text属性を付与する
- `*.vcproj    text eol=crlf`, `*.sh    text eol=lf`
    - 拡張子がvcprojのファイルに対しtext属性を付与し、改行コードをCRLFに強制する
    - 拡張子がshのファイルに対しtext属性を付与し、改行コードをLFに強制する
    - `core.autocrlf=true`であっても、改行コードはeolで設定したコードになる
- `*.jpg    -text`
    - 拡張子がjpgのファイルに対し、text属性を除外する
    - つまり、改行コードの自動変換が行われないようになる
- `*.exe    binary`
    - 拡張子がexeのファイルをバイナリファイルとして扱う
    - `binary`は、`-crlf -diff`の省略形

## attributes (global)

適当な場所にファイルを作成し、`core.attributesfile`に設定する

```bash
# ＄HOMEに.gitattributesがある場合
> git config --global core.attributesfile ~/.gitattributes
```

# リポジトリ中のCRLFをLFに統一する

## CRLFのファイルを確認する

```
> git grep --cached -l -I $'\r$'
```

## 参考
- [Git for Windows でレポジトリー上の CR LF を LF に変換する手順](http://tech.nitoyon.com/ja/blog/2014/03/28/git-crlf-to-lf/)
- [git repository 中の CRLF を LF に一括変換する](https://kokufu.blogspot.jp/2017/03/git-repository-crlf-lf.html)

# その他

- 未追跡ファイルを削除する
    ```
    > git clean
    ```

- Gitで管理しているファイルのアーカイブ（エクスポート）
    ```sh
    # archive.zipとしてエクスポート
    > git archive HEAD --output=archive.zip

    # Hogeディレクトリのみエクスポート
    > git archive HEAD Hoge --output=Hoge.zip
    ```

- 特定のファイルを除外してアーカイブ
    ```sh
    # .gitattributesに"export-ignore"を指定して以下を実行
    > git archive HEAD --worktree-attributes --output=archive.zip
    ```
