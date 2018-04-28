# Markdown Preview Enhanced (MPE)

高機能なMarkdownプレビューを提供する拡張機能.

[公式ドキュメント](https://shd101wyy.github.io/markdown-preview-enhanced/#/)も充実している.

# シンタックスハイライトで行番号

```cpp {.line-numbers}
#include <iostream>
int main()
{
    std::cout << "Hello World." << std::endl;
    return 0;
}
```

# 注釈

ほげほげ [^1]

[^1]: ほげほげ注釈


# Diagram

- フローチャート by flowchart.js
- シーケンス図 by js-sequence-diagrams
- Mermaidレンダリング
- PlantUMLレンダリング
- GraphVizレンダリング
- 他

# import

`@import "file"`とすると、ファイル拡張子に応じて良い感じに表示してくれる.

## csvファイル

@import "mpe/sample.csv"

## cppファイル

@import "mpe/main.cpp"

## pngファイル

@import "images/octocat.png"

サイズ指定可能
@import "images/octocat.png" {width="100px" height="100px" title="オクトキャット"}

## mdファイル

@import "README.md"

## mermaidファイル

TODO

## dotファイル

TODO

## plantuml(puml)ファイル

TODO
