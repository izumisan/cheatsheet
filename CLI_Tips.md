# C++/CLI

- `ref class Foo`で.NETの参照型クラス（マネージドクラス）を定義
- 参照型クラスのインスタンス生成には、`gcnew`を使う
- 参照型インスタンス変数には、ポインタ`*`ではなくハンドル`^`を使う
- ハンドルへの参照（追跡参照）は、`%`を使う
- .NETクラスライブラリを使用する場合は、`#using "foo.dll"`のようにusingディレクティブを使用する（要usingパス設定）

```cpp {.line-numbers}
#pragma once
#include <string>
using namespace System;

namespace clisample
{

public ref class Foo
{
public:
    /*!
        コンストラクタ
    */
    Foo()
        : m_value( 0 )
        , m_unmanagedString( new std::string( "unmanaged-string" ) )
        , m_managedString( "managed-string" )
    {
    }

    /*!
        デストラクタ
    */
    ~Foo()
    {
        // マネージリソースの破棄


        // ファイナライザの呼び出し
        this->!Foo();
    }

    /*!
        ファイナライザ
    */
    !Foo()
    {
        // アンマネージリソースの破棄
        delete m_unmanagedString;
        m_unmanagedString = nullptr;
    }

public:
    /*!
        Valueプロパティ
    */
    property int Value
    {
        int get()
        {
            return m_value;
        }

        void set( const int value )
        {
            m_value = value;
        }
    }

    /*!
        UnmanagedStringプロパティ
    */
    property std::string UnmanagedString
    {
        std::string get()
        {
            return *m_unmanagedString;
        }
    }

    /*!
        ManagedStringプロパティ
    */
    property String^ ManagedString
    {
        String^ get()
        {
            return m_managedString;
        }
    }

private:
    int m_value;
    std::string* m_unmanagedString;
    String^ m_managedString;
};

} // namespace clisample

```
