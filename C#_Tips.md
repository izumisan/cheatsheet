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

# Dispose関連

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
