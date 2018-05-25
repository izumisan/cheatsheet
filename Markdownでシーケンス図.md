# Markdownでシーケンス図

Markdown Preview Enhancedが[js-sequence-diagrams](https://bramp.github.io/js-sequence-diagrams/)を利用したシーケンス図に対応しているようなので、試してみた。

# Example
```sequence
Andrew->China: Says Hello
Note right of China: China thinks\nabout it
China-->Andrew: How are you?
Andrew->>China: I am good thanks!
```

# Example（手書き風）
```sequence {theme="hand"}
Andrew->China: Says Hello
Note right of China: China thinks\nabout it
China-->Andrew: How are you?
Andrew->>China: I am good thanks!
```

# Example 2
```sequence
Title: タイトル
# コメント
A->B: 同期メッセージ
B-->A: 応答（同期）
B->>C: 非同期メッセージ
C-->>B: 応答（非同期）
B->B: 処理
Note right of B: ノート
```

# Example 3
```sequence
# Example of a comment.
Note left of A: Note to the\n left of A
Note right of A: Note to the\n right of A
Note over A: Note over A
Note over A,B: Note over both A and B
```

# Syntax

- 基本
    ```
    アクター名 -> アクター名: メッセージ名
    ```

- メッセージタイプ
    |記述|定義|矢印|
    |---|---|---|
    |A->B|同期メッセージ|閉矢印、実線|
    |A-->B|同期応答|閉矢印、点線|
    |A->>B|非同期メッセージ|開矢印、実線|
    |A-->>B|非同期応答|開矢印、点線|

- ノート
    ```
    Note left of HOGE: テキスト
    Note right of HOGE: テキスト
    Note over HOGE: テキスト
    Note over HOGE,FUGA: テキスト
    ```

# メモ

- 生存区間（activation）, loop, alt等は表現できない？