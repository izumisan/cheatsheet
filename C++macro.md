# C++ マクロ

# 定数マクロ

# 関数マクロ

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
