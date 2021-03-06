---
title: サポートされている .NET 実装 - EF Core
author: rowanmiller
ms.date: 08/30/2017
uid: core/platforms/index
ms.openlocfilehash: 8fc25f4a35794162c92fd292990c24e977d1bf1b
ms.sourcegitcommit: 5e11125c9b838ce356d673ef5504aec477321724
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2018
ms.locfileid: "50022263"
---
# <a name="net-implementations-supported-by-ef-core"></a>EF Core でサポートされている .NET 実装

Microsoft は .NET コードを記述できるあらゆる場所で EF Core を使えるようにすることを目指しており、その目標に向かって現在も取り組んでいます。 EF Core の .NET Core および .NET Framework でのサポートは、自動テストによってカバーされており、多くのアプリケーションがそれを正常に使用していることがわかっていますが、Mono、Xamarin、UWP にはいくつか問題があります。

## <a name="overview"></a>概要

.NET 実装のガイダンスを下の表にまとめました。

| .NET 実装                                                                                                  | Status                                                             | EF Core 1.x の要件                                                                                | EF Core 2.x の要件 <sup>(1)</sup>                                                                 |
|:---------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------|
| **.NET Core** ([ASP.NET Core](../get-started/aspnetcore/index.md)、[コンソール](../get-started/netcore/index.md)など) | 完全サポート/推奨                                    | [.NET Core SDK 1.x](https://www.microsoft.com/net/core/)                                                | [.NET Core SDK 2.x](https://www.microsoft.com/net/core/)                                                |
| **.NET Framework** (WinForms、WPF、ASP.NET、[コンソール](../get-started/full-dotnet/index.md)など)                    | 完全サポート/推奨 EF6 も使用できます <sup>(2)</sup> | .NET Framework 4.5.1                                                                                    | .NET Framework 4.6.1                                                                                    |
| **Mono & Xamarin**                                                                                                   | 進行中 <sup>(3)</sup>                                         | Mono 4.6 <br/> Xamarin.iOS 10 <br/> Xamarin.Mac 3 <br/> Xamarin.Android 7                               | Mono 5.4 <br/> Xamarin.iOS 10.14 <br/> Xamarin.Mac 3.8 <br/> Xamarin.Android 7.5                        |
| [**ユニバーサル Windows プラットフォーム**](../get-started/uwp/index.md)                                                        | EF Core 2.0.1 を推奨 <sup>(4)</sup>                           | [.NET Core UWP 5.x パッケージ](https://www.nuget.org/packages/Microsoft.NETCore.UniversalWindowsPlatform/) | [.NET Core UWP 6.x パッケージ](https://www.nuget.org/packages/Microsoft.NETCore.UniversalWindowsPlatform/) |

<sup>(1)</sup> EF Core 2.0 は、[.NET Standard 2.0](https://docs.microsoft.com/dotnet/standard/net-standard) をサポートする .NET の実装を対象とし、そのためこれを必要とします。

<sup>(2)</sup> 適切なテクノロジを選択するには、「[Compare EF Core & EF6](../../efcore-and-ef6/index.md)」(EF Core と EF6 を比較する) を参照してください。

<sup>(3)</sup> Xamarin には問題と既知の制限があり、そのために、EF Core 2.0 で開発された一部のアプリケーションが正しく動作しない可能性があります。 回避策については、[アクティブな懸案事項](https://github.com/aspnet/entityframeworkCore/issues?q=is%3Aopen+is%3Aissue+label%3Aarea-xamarin)の一覧を確認してください。

<sup>(4)</sup> この記事の「[ユニバーサル Windows プラットフォーム](#universal-windows-platform)」セクションをご覧ください。

## <a name="universal-windows-platform"></a>ユニバーサル Windows プラットフォーム

EF Core と .NET UWP の以前のバージョンには、多数の互換性の問題があり、特に .NET ネイティブ ツールチェーンでコンパイルされたアプリケーションの場合に顕著でした。 新しい .NET UWP バージョンでは、.NET Standard 2.0 のサポートが追加され、.NET Native 2.0 が含まれています。これにより、以前に報告されているほとんどの互換性の問題が解決されています。 EF Core 2.0.1 は、UWP でより完全にテストされていますが、テストは自動化されていません。

UWP で EF Core を使用する場合:

* クエリのパフォーマンスを最適化するには、LINQ クエリで匿名型を回避します。 UWP アプリケーションをアプリ ストアに配置するには、アプリケーションを .NET ネイティブでコンパイルする必要があります。 匿名型のクエリは、.NET ネイティブではパフォーマンスが低下します。

* `SaveChanges()` のパフォーマンスを最適化するには、[ChangeTrackingStrategy.ChangingAndChangedNotifications](/dotnet/api/microsoft.entityframeworkcore.changetrackingstrategy) を使用し、エンティティ型で [INotifyPropertyChanged](https://msdn.microsoft.com/library/system.componentmodel.inotifypropertychanged.aspx)、[INotifyPropertyChanging](https://msdn.microsoft.com/library/system.componentmodel.inotifypropertychanging.aspx)、[INotifyCollectionChanged](https://msdn.microsoft.com/library/system.collections.specialized.inotifycollectionchanged.aspx) を実装します。

## <a name="report-issues"></a>問題のレポート

予想どおりに機能しない組み合わせについては、[EF Core 問題追跡ツール](https://github.com/aspnet/entityframeworkcore/issues/new)で新しい問題を登録することが推奨されています。 Xamarin 関連の問題については、 [Xamarin.Android](https://github.com/xamarin/xamarin-android/issues/new) または [Xamarin.iOS](https://github.com/xamarin/xamarin-macios/issues/new) の問題追跡ツールをご利用ください。
