# Markdown（VSCode向け）

<!-- コメント -->

# 見出し1

## 見出し2

### 見出し3

#### 見出し4

##### 見出し5

###### 見出し6

# リスト（箇条書き）

ハイフン、アスタリスク、プラスで箇条書き.

- リスト
- リスト
- リスト
* リスト
* リスト
* リスト
+ リスト
+ リスト
+ リスト

# 番号付きリスト

1. リスト
1. リスト
1. リスト
    1. リスト
    1. リスト
1. リスト
1. リスト


# チェックボックス（要拡張機能）

- [ ] OFF
- [x] ON

# コードブロック（pre記法）

バッククォート3つ

```
pre記法
```


# インライン（code記法）

バッククォートで文字列を囲むと`インライン`となる.


# シンタックスハイライト

バッククォート3つの後に言語名を指定.

```cpp
class Hoge
{
public:
    Hoge();
    ~Hoge();

private:
    fuga();
}
```

```cs
public class Hoge
{
    // コンストラクタ
    public Hoge()
    {
    }
}
```

# テーブル

## デフォルト

|header|header|header|
|-|-|-|
|item|item|item|
|item|item|item|
|item|item|item|

## アライメント指定

|左寄せ|中央寄せ|右寄せ|
|:-|:-:|-:|
|a|b|c|
|a|b|c|
|a|b|c|


# 引用

> 引用  
> 引用  
> 引用

> 引用
>> 引用
>>
> 引用

# 展開（`<details>`）

<details>
ここが展開される.
</details>

<details>
<summary>ここを展開する</summary>
summaryタグでタイトルを指定する.
</details>

# アライメント（`<div>`）

Markdown記法でアラインメント指定できないのでhtmlの`<div>`タグで記載する.

```html
<div style="text-align: center">テキスト</div>
```

<div style="text-align: left">
左寄せ
</div>

<div style="text-align: center">
中央寄せ
</div>

<div style="text-align: right">
右寄せ
</div>

# 文字装飾

## イタリック（斜体）

アスタリスク又はアンダースコア1つでイタリック（斜体）

*italic*

_italic_

*イタリック*

_イタリック_

## ボールド（強調）

アスタリスク又はアンダースコア2つでボールド（強調）

**bold**

__bold__

**ボールド**

__ボールド__

## イタリック＋ボールド

アスタリスク又はアンダースコア3つでイタリック＋ボールド

***italic + bold***

___italic + bold___

***イタリック＋ボールド***

___イタリック＋ボールド___

## 取り消し線

チルダ2つで取り消し線

~~取り消し線~~

## 文字色（`<font>`）

```html
<font color="Red">テキスト</font>
```

<font color="Red">Red</font>

<font color="Yellow">Yellow</font>

<font color="Blue">Blue</font>

<font color="Green">Green</font>

# リンク

## ハイパーリンク

```
[ラベル](URL)
```

[Googleへのリンク](https://www.google.co.jp/)

```
[ラベル][リンク名]

[リンク名]: URL
```

[Googleへのリンク2][google]

[google]: https://www.google.co.jp/

[別ファイルへのリンク（README）][hoge]

[hoge]: README.md

## ページ内リンク（アンカーリンク）

リンク元
```
[ラベル](#linkname)
```

リンク先
```
<a id="linkname">
リンク先
</a>
```

[ジャンプします](#linkname)

<a id="linkname">
ジャンプ先です
</a>

## 画像リンク

```
![名称](path)
![名称](path "タイトル")
```

![octocat](images/octocat.png "オクトキャット")

## 画像リンク（サイズ指定）（`<img>`）

```html
<img width="xxx" height="xxx" src="path"/>
```

<img width="100" height="100" src="images/octocat.png" title="100x100"/>

