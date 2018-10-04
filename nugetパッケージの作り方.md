# nugetパッケージの作り方

# 手順

1. nuspecファイルを作成する
    - VisualStudioプロジェクトからひな形を生成する
        - プロジェクトファイルがある場所で下記コマンドを実行する  
          `> nuget.exe spec`
    - DLLからnusupecファイルのひな形を生成する
        - `> nuget.exe spec xxx.dll`
1. nuspecファイルを編集する
1. nugetパッケージを作成する
    - VisualStudioプロジェクトからnugetパッケージを作成する
        - `> nuget.exe pack -Properties Configuration=Release xxx.csproj`
    - nuspecファイルからnugetパッケージを作成する
        - `> nuget.exe pack xxx.nuspec`

- nugetコマンドラインツールは以下から入手できる
    - https://www.nuget.org/downloads

# nuspecファイル

## `metadata`

- id [必須]
  - パッケージID。パッケージの名前空間を設定しておけばよい。
- version [必須]
  - パッケージのバージョン
- description [必須]
  - パッケージの説明文
- authors [必須]
  - パッケージ作成者一覧。カンマ区切り。
- title
  - パッケージタイトル。省略した場合はパッケージIDが使用される。

## Replacementトークン

`<metadata>`ノード内`$`で区切られたトークンは、`pack`コマンドの`-properties`スイッチで指定した値に置き換えることができる。

`> nuget pack -properties <name>=<value>;<name>=<value>`

|トークン|値|
|---|---|
|`$id$`|AssemblyName|
|`$version$`|AssemblyInformationalVersion or AssemblyVersion|
|`$author$`|AssemblyCompany|
|`$title$`|AssemblyTitle|
|`$description$`|AssemblyDescription|
|`$copyright$`|AssemblyCopyright|

## 依存パッケージ

`<dependencies>`要素の`<dependency>`で依存パッケージを指定する

## `file`

パッケージに含めるファイルを`<file>`で指定する。

- src
  - パッケージに含めるファイルパス。nuspecファイルからの相対パス。
- target
  - インストール先のパス。`lib`, `content`, `build`, `tools`のいずれかから始まっている必要がある
    - `lib`
      - 参照として追加される
    - `content`
      - プロジェクトに追加される
- exclude
  - `src`から除外するファイルorファイルパターン

## ターゲットフレーム

- net40
- net45
- net46
- net461
- net462
- net47
- net471
- net472
- netcore
- netcore45
- netcore451
- netcore50
- netstandard1.6
- netstandard2.0

https://docs.microsoft.com/ja-jp/nuget/reference/target-frameworks


# nuspecファイル例

## Fooパッケージ

![](images/foonupkg.png)

```xml
<?xml version="1.0"?>
<package >
  <metadata>
    <id>$id$</id>
    <version>$version$</version>
    <title>$title$</title>
    <authors>$author$</authors>
    <owners>$author$</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>$description$</description>
    <releaseNotes>Creating nuget package.</releaseNotes>
    <copyright>Copyright 2018</copyright>
  </metadata>
  <files>
    <file src="bin/Release/Foo.dll" target="lib/net461"/>
  </files>
</package>
```

## Barパッケージ

![](images/barnupkg.png)

```xml
<?xml version="1.0"?>
<package >
  <metadata>
    <id>Bar</id>
    <version>$version$</version>
    <title>$title$</title>
    <authors>$author$</authors>
    <owners>$author$</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>$description$</description>
    <releaseNotes>Creating nuget package.</releaseNotes>
    <copyright>Copyright 2018</copyright>
    <dependencies>
      <!-- 依存パッケージ -->
      <dependency id="Qux" version="1.0.0"/>
    </dependencies>
  </metadata>
  <files>
    <!-- 参照に追加 -->
    <file src="bin/Release/Bar.dll" target="lib/net461"/>
    <file src="bin/Release/Baz.dll" target="lib/net461"/>
    <!-- プロジェクトに追加 -->
    <file src="README.md" target="content/Bar"/>
  </files>
</package>
```

# リンク

- [NuGet パッケージの作成 - Microsoft](https://docs.microsoft.com/ja-jp/nuget/create-packages/creating-a-package)
- [.nuspecリファレンス - Microsoft](https://docs.microsoft.com/ja-jp/nuget/reference/nuspec)
- [プライベートなnugetパッケージを作る - Qiita](https://qiita.com/Temarin/items/f8847bf787c161e874e6)
