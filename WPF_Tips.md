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

# ルーティングイベント

- トンネルイベント
    - **ルート要素から**イベント発生要素までイベントが処理されるまで子要素に伝搬していく
    - Preview～の命名規則で実装されている
- バブルイベント
    - イベント発生要素からイベントが処理されるまで親要素に伝搬していく
    - トンネルイベント後にバブルイベントが発行される

# バインディングモード

|モード|説明|
|---|---|
|OneWay|ソースからターゲットへの一方通行の同期|
|TwoWay|双方向の同期|
|OneWayToSource|ターゲットからソースへの一方通行の同期|
|OneTime|ソースからターゲットへの初回のみ同期|

-  ソース？ターゲット？
    - `<Label Content={Binding Name}/>`の場合
        - ソース：　Nameプロパティ
        - ターゲット：　LabelのContentプロパティ

## UpdateSourceTriggerプロパティ

`TwoWay`又は`OneWayToSource`の時、`UpdateSourceTrigger`で**ソース側に通知するタイミング**を指定できる

|値|説明|
|---|---|
|Default||
|PropertyChanged|プロパティが変更したタイミングで、ソース側に通知（変更）される|
|LostFocus|フォーカスが外れたタイミングで、ソース側に通知（更新）される|
|Explicit|UpdateSourceメソッドで、明示的にソースの更新を指示した場合に更新される|


# Trigger, DataTrigger, EventTrigger

## `<Trigger>`

- プロパティ（Dependency Property）変更時、指定したセッターを実行する

## `<DataTrigger>`

- プロパティ変更時、指定したセッターを実行する
- `Trigger`と異なり、DependencyProperty以外にも指定できる

## `<EventTrigger>`

- 指定したイベント発行時、指定したアクションを実行する
- ストリーボードを開始（`BeginStoryboard`）するのによく利用される

## その他

- MultiTrigger
- MultiDataTrigger


## 参考

- [WPF Tutorial.net](https://www.wpf-tutorial.com/styles/trigger-datatrigger-event-trigger/)

# Blend付属トリガー・アクション・ビヘイビア

- Blend for VisualStudioに含まれているトリガー・アクション・ビヘイビア
- WPF標準（FrameworkElement）ではないが、Blend自体は標準で同梱されるので、実質、標準的に利用可能
- 標準のものより高機能
- 標準と同名のものもあるため注意
- 使用の際、下記を追加する
    ```
    xmlns:i="http://schemas.microsoft.com/expression/2010/interactivity"
    ```
    ```
    xmlns:ei="http://schemas.microsoft.com/expression/2010/interactions"
    ```
    - `Microsoft.Expression.Interactions`を参照追加すること
    - `Microsoft.Expression.Interactions.dll`は、VS2017から個別コンポートネントにある`Blend for Visual Studio SDK`を選択してインストールする必要がある


## トリガー

- DataTrigger
- EventTrigger
- KeyTrigger
- TimerTrigger
- PropertyChangedEventTrigger
- StoryboardCompletedTrigger

## アクション

- InvokeCommandAction
- CallMethodAction
- ChangePropertyAction
- ControlStoryboardAction
- LaunchUriOrFileAction
- GoToStateAction
    - ビジュアル・ステート（外観状態）を変化させるアクション

## ビヘイビア

- FluidMoveBehavior 
- MouseDragElementBehavior 
- TranslateZoomRotateBehavior 


# Microsoft.Xaml.Behaviors.Wpf

- Blendのトリガー・アクション・ビヘイビアがOSS化され、nugetパッケージ（`Microsoft.Xaml.Behaviors.Wpf`）として提供されるようになったので、今後はこちらを利用した方が良い
- Blend付属のものと名前空間が異なるので、`Microsoft.Xaml.Behaviors.Wpf`への置き換えにはある程度の変更が必要となる
- 主な変更例
    ```
    # xaml
    xmlns:i ="http://schemas.microsoft.com/expression/2010/interactivity"
    xmlns:ei="http://schemas.microsoft.com/expression/2010/interactions"
    
    # namespace
    System.Windows.Input
    ```
    ↓
    ```
    # xaml
    xmlns:i="http://schemas.microsoft.com/xaml/behaviors"
    xmlns:ei="http://schemas.microsoft.com/xaml/behaviors"

    # namespace
    Microsoft.Xaml.Behaviors
    ```

# 参考

- [WPF4.5入門 - かずきのBlog@hatena](https://blog.okazuki.jp/entry/2014/12/27/200015)
- [WPFアーキテクチャ - Microsoft Docs](https://docs.microsoft.com/ja-jp/dotnet/framework/wpf/advanced/wpf-architecture)
- [WPF Tutorial.net](http://www.wpftutorial.net/Home.html)
    - [Learn WPF in one Week - WPF Tutorial.net](http://www.wpftutorial.net/LearnWPFin14Days.html)
