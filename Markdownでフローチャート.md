# Markdownでフローチャート

Markdown Preview Enhancedが[flowchart.js](http://flowchart.js.org/)を利用したフローチャートに対応しているようなので、試してみた。

## Example 1

```flow
st=>start: Start
e=>end: End
op1=>operation: My Operation
sub1=>subroutine: My Subroutine
cond=>condition: Yes or No?
io=>inputoutput: catch something...

st->op1->cond
cond(yes)->io->e
cond(no)->sub1(right)->op1
```

## Example 2

```flow
st=>start: Start
e=>end: End
op1=>operation: My Operation
op2=>operation: Stuff
sub1=>subroutine: My Subroutine
cond=>condition: Yes or No?
c2=>condition: Good idea
io=>inputoutput: catch something...

st->op1(right)->cond
cond(yes, right)->c2
cond(no)->sub1(left)->op1
c2(yes)->io->e
c2(no)->op2->e
```

# おためし：for文

```c
for ( int i = 0; i < 10; ++i )
{
    処理;
}
```

```flow
start=>start: 開始
end=>end: 終了
初期化=>operation: i = 0
判定=>condition: i < 10
インクリメント=>operation: ++i
処理=>operation: 処理

start->初期化->判定
判定(yes,right)->処理(right)->インクリメント(right)->判定
判定(no)->end
```

# Syntax

- Nodeの定義

    ```
    Node名=>部品名: ラベル
    ```

    - Node名は日本語でもいけるっぽい

    - 部品名一覧
        |部品名|定義|形状|
        |---|---|---|
        |start|開始点|円、楕円、角丸四角|
        |end|終了点|円、楕円、角丸四角|
        |operation|処理|長方形|
        |subroutine|定義済み処理|左右が二重線の長方形|
        |inputoutput|入出力|平行四辺形|
        |condition|条件分岐|ひし型|
        
- フロー定義

    ```
    Node名->Node名->Node名(right)->Node名(left)
    ```

- 条件分岐
    ```
    Node名(yes)->Node名
    Node名(no, right)->Node名
    ```
