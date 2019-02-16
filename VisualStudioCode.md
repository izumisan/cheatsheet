# Visual Studio Code

# 保存場所

## Windows

- 設定ファイル  
    `{ユーザフォルダ}\AppData\Roaming\Code\User\settings.json`

- 拡張機能（Extension）  
    `{ユーザフォルダ}\.vscode\extensions\`


# 拡張機能

## Markdown関連

- ~~Auto-Open Markdown Preview~~
    - mdファイルを開くと自動でプレビューを開く
    - ファイル比較する時にも自動でプレビューが開くので、便利な場合と邪魔な場合がある
    - Markdown All in Oneで代用可能

- Markdown PDF
    - MarkdownからPDFを作成できる
    - 数式など、他の拡張機能を使っていると上手くPDF化できない
    - Markdown Preview Enhancedの方が対応範囲が広い

- ~~Markdown Checkboxes~~
    - Markdownでチェックボックスを表現できる
    - Markdown All in One, Markdown Preview Enhancedで代用可能

- ~~Markdown+Math~~
    -  LaTeXで数式がかける
    -  Markdown All in One, Markdown Preview Enhancedで代用可能

- **Markdown All in One**
    - キーボードショートカット、チェックボックス、数式レンダリングなど、いろいろ入っている
    - 左のエクスプローラー部にOUTLINEが表示されるのが地味に便利.

- **Markdown Preview Enhanced**
    - チェックボックスや数式レンダリング等に対応
    - Graphvizやmermaid等、いろいろなダイアグラムに対応している
    - プレビュー画面はデフォルトのものとは別
    - [公式ドキュメント](https://shd101wyy.github.io/markdown-preview-enhanced/#/)が充実している 

- Past Image
    - クリップボードに保存されたイメージをmarkdownに直接貼り付けるる（クリップボード画像のファイル保存＋markdownリンク作成）できる
    - 「`Windows` + `Shift` + `S`」で、範囲指定でキャプチャーできる

Markdown関連で、機能ごとに複数の拡張機能をいれたりしていたけど、Markdown All in OneとMarkdown Preview Enhancedの2つさえ入れていれば、Markdown周りはほぼカバーされる.

## Git関連

- Git History
- Git Tree Compare
- GitLens

## その他

- Rainbow CSV
    - csvファイルをカラム毎に色分けする
    - 地味にいい
- Excel Viewer
    - csvファイルやxlsxファイルを表形式で表示する
- PlantUML
    - テキストベースでUMLダイアグラムを作図できる
    - 要java
- Polacode
    - ソースコードをきれいなキャプチャー画像として保存する
        1. コマンドパレットから`polacode`タブを起動する
        1. 対象のソースコードをコピーして、Polacodeのテキストエリア部分にペーストする
        1. アイコンクリック

