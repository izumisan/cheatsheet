# C# Tips

# 逆引き名前空間

|クラス|名前空間|アセンブリ|
|---|---|---|
|INotifyPropertyChanged|System.ComponentModel||

## Rx関連

下記の4つusingしておけば、とりあえずは困らない。

```cs
using System.Reactive.Linq;
using System.Reactive.Disposable;
using Reactive.Bindings;
using Reactive.Bindings.Extensions;
```

# リソースの破棄

## Disposeパターン 

### 基底クラス

```cs {.line-numbers}
public class Base : IDisposable
{
    public Base()
    {
    }

    // ファイナライザ
    ~Base()
    {
        Dispose( false );
    }

    private bool _disposed = false;

    public void Dispose()
    {
        Dispose( true );
        GC.SuppressFinalize( this );
    }

    // Disposeメソッド
    //  true: Disposeメソッドからの呼び出し
    // false: ファイナライザからの呼び出し
    protected virtual void Dispose( bool disposing )
    {
        if ( !_disposed )
        {
            if ( disposing )
            {
                //@@@ マネージリソースの解放
            }

            //@@@ アンマネージリソースの解放

            _disposed = true;
        }
    }
}
```

### 派生クラス

```cs {.line-numbers}
public class Derived : Base
{
    public Derived()
        : base()
    {
    }

    // ファイナライザ
    ~Derived()
    {
        Dispose( false );
    }

    //@@@ 派生クラスでIDisposable.Dispose()は実装しない.

    private bool _disposed = false;

    // 基底クラスのDipose(bool)のオーバライド
    //  true: Disposeメソッドからの呼び出し
    // false: ファイナライザからの呼び出し
    protected override void Dispose( bool disposing )
    {
        if ( !_disposed )
        {
            if ( disposing )
            {
                //@@@ マネージリソースの解放
            }

            //@@@ アンマネージリソースの解放

            _disposed = true;

            // 基底クラスのDispose(bool)の呼び出し
            base.Dispose( disposing );
        }
    }
}
```

## CompositeDisposable

- System.Reactive.Disposables名前空間
- 要System.Reactive.Core
- 自身のDispose時、登録した要素のDispose()を呼び出す（一括破棄）
- 自身のDispose後は再利用不可
    - Dispose後に要素を追加すると、直後にDiposeされる？
- 要素のみDisposeするには、Clear()を使用する

# `IEnumerable<T>`の実装

```cs {.line-numbers}
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;

namespace IEnumerableSample
{
    public class Foo : IEnumerable<int>
    {
        public Foo()
        {
            var random = new Random();
            _data = Enumerable.Range( 0, 10 )
                              .Select( _ => random.Next() )
                              .ToList();
        }

        private List<int> _data = null;

        #region IEnumerable<T>の実装

        public IEnumerator<int> GetEnumerator()
        {
            return _data.GetEnumerator();
        }
        #endregion

        #region IEnumerableの実装

        IEnumerator IEnumerable.GetEnumerator()
        {
            return this.GetEnumerator();
        }
        #endregion
    }
}
```

# `IEquatable<T>`の実装

- `IEquatable<T>`を実装する
- `Object.Equal()`をオーバーライドする
- `Object.GetHashCode()`をオーバーライドする

基底クラス

```cs {.line-numbers}
public class Base : IEquatable<Base>
{
    public Base()
    {
    }

    public int Id { get; set; } = 0;

    public double Value { get; set; } = 0.0;

    public string Name { get; set; } = string.Empty;

    public override bool Equals( object rhs )
    {
        return this.Equals( rhs as Base );
    }

    public bool Equals( Base rhs )
    {
        if ( ReferenceEquals( rhs, null ) )
            return false;

        if ( ReferenceEquals( this, rhs ) )
            return true;

        if ( this.GetType() != rhs.GetType() )
            return false;

        return ( this.Id == rhs.Id ) &&
                ( this.Value == rhs.Value ) &&
                ( this.Name == rhs.Name );
    }

    public override int GetHashCode()
    {
        return this.Id.GetHashCode();
    }
}
```

派生クラス

```cs {.line-numbers}
public class Derived : Base, IEquatable<Derived>
{
    public Derived()
    {
    }

    public double DerivedValue { get; set; } = 0.0;

    public override bool Equals( object rhs )
    {
        return this.Equals( rhs as Derived );
    }

    public bool Equals( Derived rhs )
    {
        if ( ReferenceEquals( rhs, null ) )
            return false;

        if ( ReferenceEquals( this, rhs ) )
            return true;

        if ( this.GetType() != rhs.GetType() )
            return false;

        return ( base.Equals( rhs ) ) &&
                ( this.DerivedValue == rhs.DerivedValue );
    }

    public override int GetHashCode()
    {
        return base.GetHashCode();
    }
}
```

## `Object.GetHashCode()`のオーバーライド

戻り値（ハッシュ値）について
- オブジェクトが等しい場合（Equalsがtrueの場合）、同じハッシュ値を返す必要がある
- メソッド呼び出し等の操作により、ハッシュ値が変更されてはならない
- 異なるオブジェクトであっても、同じハッシュ値を返しても良い
    - この場合、検索効率が落ちる

一般的な実装方法
- 全ての不変フィールドに対してXORをとった値を返す


# 列挙型に対する操作

- 列挙型に指定した値が定義されているか否かを確認する
    ```cs
    Enum.IsDefined( typeof( Month ), 1 )  // => true
    Enum.IsDefined( typeof( Month ), 2 )  // => true
    Enum.IsDefined( typeof( Month ), 13 )  // => false
    ```
- 文字列を列挙型に変換する
    ```cs
    Enum.Parse( typeof( Month ), "January" )  // => Month.January
    ```
- 全ての要素を列挙する
    ```cs
    Enum.GetValues( typeof( Month ) ).Cast<Month>()  // => [ Month.January, ... , Month.December ]
    ```