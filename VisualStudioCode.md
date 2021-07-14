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

- ~~Markdown PDF~~
    - MarkdownからPDFを作成できる
    - 数式など、他の拡張機能を使っていると上手くPDF化できない
    - Markdown Preview Enhancedの方が対応範囲が広い
    - Markdown Preview Enhancedで代用可能

- ~~Markdown Checkboxes~~
    - Markdownでチェックボックスを表現できる
    - Markdown All in One, Markdown Preview Enhancedで代用可能

- ~~Markdown+Math~~
    -  LaTeXで数式がかける
    -  Markdown All in One, Markdown Preview Enhancedで代用可能

- ~~Markdown All in One~~
    - キーボードショートカット、チェックボックス、数式レンダリングなど、いろいろ入っている
    - 左のエクスプローラー部にOUTLINEが表示されるのが地味に便利.

- **Markdown Preview Enhanced**
    - チェックボックスや数式レンダリング等に対応
    - Graphvizやmermaid等、いろいろなダイアグラムに対応している
    - プレビュー画面はデフォルトのものとは別
    - [公式ドキュメント](https://shd101wyy.github.io/markdown-preview-enhanced/#/)が充実している 
    - Google Chromeがインストールされているなら、PDFファイルも作成可能

- Past Image
    - クリップボードに保存されたイメージをmarkdownに直接貼り付けるる（クリップボード画像のファイル保存＋markdownリンク作成）できる
    - 「`Windows` + `Shift` + `S`」で、範囲指定でキャプチャーできる

Markdown関連で機能ごとに複数の拡張機能をいれたりしていたけど、VSCodeの基本機能で十分だったりする.  
保険でMarkdown Preview Enhancedを入れておけば、だいたい何とかなる.

## Git関連

- ~~Git History~~
    - ロググラフを可視化する
- Git Graph
    - ロググラフを可視化する
    - Git Historyより軽くて、機能が充実している
- Git Tree Compare
- GitLens
    - デフォルト設定だといろいろと画面がうるさくなるので、設定をいじったほうが良い

## CMake関連

- CMake
    - インテリセンス（コード補間）
- CMake Tools
    - configureやbuildが、コマンドやツールボタンから実行できる

## コーディング関連

- EditorConfig for VS Code

## 作図関連

- PlantUML
    - テキストベースでUMLダイアグラムを作図できる
    - 要java
- Draw.io Integraion
    - Draw.ioの作図がVSCodeでできる
    - オフライン環境に対応している
    - svg, png にエクスポート可能
- Markmap
    - Markdownでマインドマップが作図できる

## その他

- Rainbow CSV
    - csvファイルをカラム毎に色分けする
    - 地味にいい
- Excel Viewer
    - csvファイルやxlsxファイルを表形式で表示する
- Polacode
    - ソースコードをきれいなキャプチャー画像として保存する
        1. コマンドパレットから`polacode`タブを起動する
        1. 対象のソースコードをコピーして、Polacodeのテキストエリア部分にペーストする
        1. アイコンクリック
- Sort lines
    - 選択箇所をソートする

