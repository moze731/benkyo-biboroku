# WPF

## WPFとは

.NETのUIフレームワークの一つ。.NETのUIフレームワークはWPF以外に以下のようなものがある。

| UIフレームワーク | 説明 |
|:------|:------|
| Windows Forms App | 最も利用されているUIフレームワーク。.NETの初期から存在しており、古くはなっているもののシェアはダントツ。 |
| MAUI | Xamarinの後継のクロスプラットフォームUIフレームワーク。現在プレビュー版 |
| WinUI | UWP用のUIフレームワークが、WinUI3.0から、Win32とUWP共通で使えるUIフレームワークになった。2.0でもXaml Islandにより、Win32から利用可能ではあった。 |

## WPFの概念

- WPFはViewとModelの分割を概念として取り入れているフレームワーク
  - MVVVMを目指したフレームワークだが、UIフレームワークとしての機能としては、ViewとModelの分割と連携までという印象。
  - 気を付けて使うことで、MVVMでの実装も十分できるが、UIフレームワークにMVVMを強瀬する機能はない
- MVVNMを強制するフレームワークとして、WPF上で動くPrismというフレームワークがある

## 名前空間

- 標準ライブラリ
  - WPFのコア機能
    - [System.Windows](https://docs.microsoft.com/ja-jp/dotnet/api/system.windows?view=net-5.0)
      - WPFの基本クラスが属する名前空間
    - System.Windows.Controls
    - [System.Windows.Data](https://docs.microsoft.com/ja-jp/dotnet/api/system.windows.data?view=net-5.0)
      - CollectionをBindingする際に使う型等が属する名前空間
    - [System.Windows.Threading](https://docs.microsoft.com/ja-jp/dotnet/api/system.windows.threading?view=net-5.0)
      - すべてのコントロールの軽装元になる、`DispatcherObject`が属する名前空間。WPFのスレッド処理に関する機能。
  - WPFアプリ実装に使える.NET他機能
    - [System.ComponentModel](https://docs.microsoft.com/ja-jp/dotnet/api/system.componentmodel?view=net-5.0)
      - UIElement等が、想定している各種Event等が属する名前空間
      - MVVMでアプリケーション開発する際に、必須で使用する、ViewへのViewModelクラスのPropertyの変更通知用interfaceの`INotifyPropertyChanged`が属する名前空間
    - [System.Runtime.CompilerServices](https://docs.microsoft.com/ja-jp/dotnet/api/system.runtime.compilerservices?view=net-5.0)
      - イベント処理等で、Property名のメタ情報`[CallerMemberName]`が属する名前空間
    - [System.Collection.ObjectModel](https://docs.microsoft.com/ja-jp/dotnet/api/system.collections.objectmodel?view=net-5.0)
      - `ObservableCollection<T>` が属する名前空間
- NuGetライブラリ
  - [Microsoft.Xaml.Behavior.Wpf](https://www.nuget.org/packages/Microsoft.Xaml.Behaviors.Wpf/)
    - Blendの機能である、Behavior、Trigger、Actionを統合したライブラリ

## 構成要素の体系（個人的なとりまとめ）

- View
  - XAML  
    ViewはXAMLという言語で、記載する。XAMLもC#と同じく、CLI言語。XMLベースなので、タグを使ったマークアップ方式で記載する。記載に内容は、C#でいうところのインスタンス作成。インスタンスは画面項目（ボタンとかテキストボックスとか）がメインになる。要は、コントロールの宣言をC#で全部書くより、マークアップ言語の方が書きやすいよねということだと思う。

## WPF Projectの構成

- App.xamlがエントリポイント
  - 最初に表示するViewをStartupUri属性で指定している
  - App.xamlは、アプリケーション全体で使うリソースの定義などでも使う。
  - App.xaml.cs、エントリポイントでC#で何かしたい時に使う