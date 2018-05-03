# C# Tips

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