# マクロ（C言語／C++）

# 定義済みマクロ

- `_MSC_VER`
    |Visual Studio|_MSC_VER|
    |:-:|:-:|
    |Visual Studio 2010|1600|
    |Visual Studio 2012|1700|
    |Visual Studio 2013|1800|
    |Visual Studio 2015|1900|
    |Visual Studio 2017|1910|
- `__cplusplus`
    |C++規格|__cplusplus|
    |:-:|:-:
    |C++98<br>C++03|199711L|
    |C++11|201103L|
    |C++14|201402L|
    |C++17|201703L|
    |C++20||

# 定数マクロ

- `#define マクロ名 置換文字列`

# 関数マクロ

- `#define マクロ名(引数) 置換文字列`

# 組み込みマクロ

- `__FILE__`
- `__LINE__`
- `__func__`
- `__VA_ARGS__`

# #演算子（文字列化演算子）

マクロ引数に`#`をつけると`"文字列"`（ダブルクォーテーションがついた状態）にすることができる.

```cpp {.line-numbers}
#include <iostream>

// #演算子（文字列化演算子）
// マクロ引数を文字列（ダブルクォーテーションをつけた状態）に変換する
#define FOO( x ) foo( #x )

void foo( const char* msg )
{
    std::cout << "foo: " << msg << std::endl;
}

int main()
{
    FOO( 1 );          // => foo( "1" )
    FOO( message );    // => foo( "message" )
    FOO( "message" );  // => foo( "\"message\"" )

    return 0;
}
```

# ##演算子（連結演算子）

マクロ引数は`##`で連結することができる.

```cpp {.line-numbers}
#include <iostream>

// ##演算子（トークン連結演算子）
// ##の左辺と右辺を連結する
#define FOO( x ) foo_ ## x()

void foo_1()
{
    std::cout << "foo_1" << std::endl;
}

void foo_2()
{
    std::cout << "foo_2" << std::endl;
}

int main()
{
    FOO( 1 );  // => foo_1()
    FOO( 2 );  // => foo_2()

    return 0;
}
```

# マクロ引数のマクロを展開する

`#演算子`や`##演算子`のマクロ引数がマクロの場合、`#演算子`や`##演算子`でマクロ引数のマクロは展開されてない。

この場合、関数マクロを2ステップにすることで、マクロ引数のマクロを展開することができる.

# マクロ展開結果を確認する

- VisualStudio
    - "/E"オプションで、マクロが展開されたソースコード（プリプロセッサの処理結果）を「ビルド」ウィンドウに出力することができる
    - "/P"オプションを追加することで、展開結果をファイルに出力されるようになる（拡張子"i"）
