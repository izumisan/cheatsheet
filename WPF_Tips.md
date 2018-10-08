# WPF Tips

# 依存関係プロパティ・添付プロパティ

## 依存関係プロパティ（Dependency Property）

- WPF用に拡張されたWPFプロパティシステム
- XAMLからのアクセス、データバインディング等が可能となる
- DependencyObjectを継承したクラスで定義が可能

### 依存関係プロパティの実装

- `DependencyObject(System.Windows名前空間)`を継承したクラスで定義可能
- 依存関係プロパティの名称は、末尾が"Property"である必要がある
    - ex) FooProperty, BarProperty
- `DependencyProperty.Registerメソッド`で依存関係プロパティを登録する
- 依存関係プロパティへのアクセスは、`GetValueメソッド`, `SetValueメソッド`を利用する
    - GetValueメソッド, SetValueメソッドはDependencyObjectのメソッド
    - 通常、CLR形式のラッパープロパティを定義する
        - ここで定義するラッパープロパティにロジックを定義してはならない


以下に、`DependencyObject`を継承した`Fooクラス`に対し`Name依存関係プロパティ`を実装したサンプルコードを示す

```cs
// 依存関係プロパティの名称は、"～Property"である必要がある
// 依存関係プロパティは、DependencyProperty.Registerメソッドで登録する
public static readonly DependencyProperty NameProperty =
    DependencyProperty.Register( "Name",
                                 typeof( string ),
                                 typeof( Foo ),
                                 new PropertyMetadata( default( string ) ) );

// 依存関係プロパティへのアクセスは、GetValueメソッド、SetValueメソッドを使用する
// 一般的に、下記のようなCLR形式のラッパープロパティを定義し、Fooクラス等のC#コードからは
// このプロパティ経由で依存関係プロパティにアクセスする
public string Name
{
    get { return (string)GetValue( NameProperty ); }
    set { SetValue( NameProperty, value ); }
}
```

## 添付プロパティ（Attached Property）

- 依存関係プロパティの一種（特殊化）
- 任意のオブジェクト（クラス）に対し、任意のプロパティを設定することができる
- `Grid.Row`, `Grid.Column`や`DockPanel.Dock`等がこの添付プロパティにあたる

### 添付プロパティの実装

- 添付プロパティを**定義**するクラスは、任意のクラスで可能
    - DependencyObjectのサブクラスである必要はない
- 添付プロパティを**設定**するクラスは、DependencyObjectのサブクラスであること
- `DependencyProperty.RegisterAttachedメソッド`で添付プロパティを登録する
- 添付プロパティには、静的なアクセッサー（Getterメソッド、Setterメソッド）を定義する必要がある
    - アクセッサー名は、GetXXXX(), SetXXXX()とする必要がある
    - Hoge添付プロパティの場合
        - GetHoge( DependencyObject obj )
        - SetHoge( DependencyObject obj, object value )

## その他

- [依存関係プロパティの概要 - Microsoft Docs](https://docs.microsoft.com/ja-jp/dotnet/framework/wpf/advanced/dependency-properties-overview)
- [添付プロパティの概要 - Microsoft Docs](https://docs.microsoft.com/ja-jp/dotnet/framework/wpf/advanced/attached-properties-overview)
- [Dependency Properties - WPF Tutorial.net](http://www.wpftutorial.net/DependencyProperties.html)


# 参考

- [WPF4.5入門 - かずきのBlog@hatena](https://blog.okazuki.jp/entry/2014/12/27/200015)
- [WPFアーキテクチャ - Microsoft Docs](https://docs.microsoft.com/ja-jp/dotnet/framework/wpf/advanced/wpf-architecture)
- [WPF Tutorial.net](http://www.wpftutorial.net/Home.html)
