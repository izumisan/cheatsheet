# Markdownでmermaid

Markdown Preview Enhancedが[mermaid](https://mermaidjs.github.io/)を利用したダイアグラムに対応しているようなので試してみた。

# 1. フローチャート（graph）

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

```mermaid
graph LR
    A[Square Rect] -- Link text --> B((Circle))
    A --> C(Round Rect)
    B --> D{Rhombus}
    C --> D
```

# 2. シーケンス図（sequenceDiagram）

```mermaid
sequenceDiagram
    Alice->>Bob: Hello Bob, how are you?
    Bob-->>John: How about you John?
    Bob--x Alice: I am good thanks!
    Bob-x John: I am good thanks!
    Note right of John: Bob thinks a long<br/>long time, so long<br/>that the text does<br/>not fit on a row.

    Bob-->Alice: Checking with John...
    Alice->John: Yes... John, how are you?
```

## おためし

- 線種

```mermaid
sequenceDiagram
    # コメント

    A->B: 実線
    B-->A: 点線

    A->>B: 実線矢印
    B-->>A: 点線矢印

    A-x B: 実線矢印x
    B--x A: 点線矢印x

    A->>A: ループ
```

- 実行区間とノート

```mermaid
sequenceDiagram
    # 矢印に+-を付加すると実行区間を指定できる
    A->>+B: メッセージ1
    B->>-A: メッセージ2

    # activate, deactivateでも可能だが、+-があるので利用機会はない？
    A->>B: メッセージ3
    activate B
    B->>A: メッセージ4
    deactivate B 

    # 入れ子、ノート
    A->>+B: メッセージ5
    note right of B: テキスト
    A->>+B: メッセージ6
    B-->>-A: メッセージ7
    B-->>-A: メッセージ8
    Note over A,B: テキスト
```

- 繰り返し（loop）

```mermaid
sequenceDiagram
    A->>B: メッセージ
    loop リスト要素
        A->>B: メッセージ
        B-->>A: メッセージ
    end
```

- 条件分岐（alt）

```mermaid
sequenceDiagram
    A->>B: メッセージ
    alt YES
        A->>B: メッセージ
        B-->>A: メッセージ
    else NO
        A->>B: メッセージ
        B-->>A: メッセージ
    end
```

- 条件（opt）

```mermaid
sequenceDiagram
    A->>B: メッセージ
    opt 条件
        B->>A: メッセージ
    end
```

# 3. ガントチャート（gantt）

```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title Adding GANTT diagram functionality to mermaid
    section A section
    Completed task : done, des1, 2014-01-06,2014-01-08
    Active task : active,  des2, 2014-01-09, 3d
    Future task :          des3, after des2, 5d
    Future task2 :         des4, after des3, 5d
    section Critical tasks
    Completed task in the critical line :crit, done, 2014-01-06,24h
    Implement parser and jison          :crit, done, after des1, 2d
    Create tests for parser             :crit, active, 3d
    Future task in critical line        :crit, 5d
    Create tests for renderer           :2d
    Add to mermaid                      :1d
```

# 4. クラス図（classDiagram）（MPE未対応？）

```mermaid
classDiagram
Class01 <|-- AveryLongClass : Cool
Class03 *-- Class04
Class05 o-- Class06
Class07 .. Class08
Class09 --> C2 : Where am i?
Class09 --* C3
Class09 --|> Class07
Class07 : equals()
Class07 : Object[] elementData
Class01 : size()
Class01 : int chimp
Class01 : int gorilla
Class08 <--> C2: Cool label
```

# 5. Gitグラフ（gitGraph）（MPE未対応？）

```mermaid
gitGraph:
options
{
    "nodeSpacing": 150,
    "nodeRadius": 10
}
end
commit
branch newbranch
checkout newbranch
commit
commit
checkout master
commit
commit
merge newbranch
```
