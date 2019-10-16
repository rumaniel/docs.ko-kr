---
title: 애플리케이션 관리 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application management [WPF]
ms.assetid: 32b1c054-5aca-423b-b4b5-ed8dc4dc637d
ms.openlocfilehash: d0e3ecbfd42d14ea468adf8a99be0f525c5eb39d
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70040966"
---
# <a name="application-management-overview"></a>애플리케이션 관리 개요

모든 애플리케이션은 애플리케이션 구현 및 관리에 적용하는 일반적인 기능 집합을 공유하는 경향이 있습니다. 이 항목에서는 응용 프로그램을 만들고 관리 하기 위한 <xref:System.Windows.Application> 클래스의 기능에 대해 간략하게 설명 합니다.

## <a name="the-application-class"></a>Application 클래스

WPF에서 일반적인 응용 프로그램 범위 기능은 <xref:System.Windows.Application> 클래스에 캡슐화 됩니다. 클래스 <xref:System.Windows.Application> 에는 다음과 같은 기능이 포함 되어 있습니다.

- 애플리케이션 수명 추적 및 상호 작용

- 명령줄 매개 변수 검색 및 처리

- 처리되지 않은 예외의 검색 및 응답

- 애플리케이션 범위 속성 및 리소스 공유

- 독립 실행형 애플리케이션에서 창 관리

- 탐색 추적 및 관리

<a name="The_Application_Class"></a>

## <a name="how-to-perform-common-tasks-using-the-application-class"></a>Application 클래스를 사용하여 일반적인 작업을 수행하는 방법

<xref:System.Windows.Application> 클래스의 모든 세부 정보에 관심이 없는 경우 다음 표에서는에 대 한 <xref:System.Windows.Application> 몇 가지 일반적인 작업과 이러한 작업을 수행 하는 방법을 보여 줍니다. 관련 API 및 항목을 확인하여 추가 정보 및 샘플 코드를 찾을 수 있습니다.

|작업|방식|
|----------|--------------|
|현재 애플리케이션을 나타내는 개체 가져오기|<xref:System.Windows.Application.Current%2A?displayProperty=nameWithType> 속성을 사용합니다.|
|애플리케이션에 시작 화면 추가|[WPF 응용 프로그램에 시작 화면 추가](how-to-add-a-splash-screen-to-a-wpf-application.md)를 참조 하세요.|
|애플리케이션 시작|<xref:System.Windows.Application.Run%2A?displayProperty=nameWithType> 메서드를 사용하세요.|
|애플리케이션 중지|개체의 메서드를 <xref:System.Windows.Application.Shutdown%2A> 사용 합니다. <xref:System.Windows.Application.Current%2A?displayProperty=nameWithType>|
|명령줄에서 인수 가져오기|이벤트를 <xref:System.Windows.Application.Startup?displayProperty=nameWithType> 처리 하 고 속성 <xref:System.Windows.StartupEventArgs.Args%2A?displayProperty=nameWithType> 을 사용 합니다. 예제는 <xref:System.Windows.Application.Startup?displayProperty=nameWithType> 이벤트를 참조 하세요.|
|애플리케이션 종료 코드 가져오기 및 설정|이벤트 처리기 <xref:System.Windows.Application.Shutdown%2A> <xref:System.Windows.ExitEventArgs.ApplicationExitCode%2A?displayProperty=nameWithType> <xref:System.Windows.Application.Exit?displayProperty=nameWithType> 에서 속성을 설정 하거나 메서드를 호출 하 고 정수를 전달 합니다.|
|처리되지 않은 예외의 검색 및 응답|처리는 <xref:System.Windows.Application.DispatcherUnhandledException> 이벤트입니다.|
|애플리케이션 범위 리소스 가져오기 및 설정|<xref:System.Windows.Application.Resources%2A?displayProperty=nameWithType> 속성을 사용합니다.|
|애플리케이션 범위 리소스 사전 사용|[응용 프로그램 범위 리소스 사전 사용](how-to-use-an-application-scope-resource-dictionary.md)을 참조 하세요.|
|애플리케이션 범위 속성 가져오기 및 설정|<xref:System.Windows.Application.Properties%2A?displayProperty=nameWithType> 속성을 사용합니다.|
|애플리케이션 상태 가져오기 및 저장|응용 프로그램 [세션 간에 응용 프로그램 범위 속성 유지 및 복원](persist-and-restore-application-scope-properties.md)을 참조 하세요.|
|리소스 파일, 콘텐츠 파일 및 원본 사이트 파일을 포함하여 비코드 데이터 파일 관리|[WPF 응용 프로그램 리소스, 콘텐츠 및 데이터 파일](wpf-application-resource-content-and-data-files.md)을 참조 하세요.|
|독립 실행형 애플리케이션의 창 관리|[WPF 창 개요](wpf-windows-overview.md)를 참조하세요.|
|탐색 추적 및 관리|[탐색 개요](navigation-overview.md)를 참조 하세요.|

<a name="The_Application_Definition"></a>

## <a name="the-application-definition"></a>애플리케이션 정의

<xref:System.Windows.Application> 클래스의 기능을 활용 하려면 응용 프로그램 정의를 구현 해야 합니다. WPF 응용 프로그램 정의는에서 <xref:System.Windows.Application> 파생 되 고 특수 MSBuild 설정을 사용 하 여 구성 되는 클래스입니다.

### <a name="implementing-an-application-definition"></a>애플리케이션 정의 구현

일반적인 WPF 응용 프로그램 정의는 태그와 코드 숨김으로 모두 사용 하 여 구현 됩니다. 따라서 코드 숨김에서 애플리케이션별 동작을 구현하고 이벤트를 처리하는 동시에 태그를 사용하여 애플리케이션 속성과 리소스를 선언적으로 설정하고 이벤트를 등록할 수 있습니다.

다음 예제에서는 태그 및 코드 숨김을 모두 사용하여 애플리케이션 정의를 구현하는 방법을 보여 줍니다.

[!code-xaml[ApplicationSnippets#ApplicationXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationSnippets/CSharp/App.xaml#applicationxaml)]

[!code-csharp[ApplicationSnippets#ApplicationCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationSnippets/CSharp/App.xaml.cs#applicationcodebehind)]
[!code-vb[ApplicationSnippets#ApplicationCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationSnippets/visualbasic/application.xaml.vb#applicationcodebehind)]

태그 파일과 코드 숨김 파일이 함께 작동하도록 하려면 다음이 필요합니다.

- 태그에서 요소는 `Application` `x:Class` 특성을 포함 해야 합니다. 응용 프로그램을 빌드할 때 `x:Class` 태그 파일에가 있으면 MSBuild가에서 <xref:System.Windows.Application> 파생 되 고 `x:Class` 특성으로 `partial` 지정 된 이름을 가진 클래스를 만듭니다. 이렇게 하려면 XAML 스키마 (`xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`)에 대 한 XML 네임 스페이스 선언을 추가 해야 합니다.

- 코드를 사용할 `partial` 때 클래스는 태그의 `x:Class` 특성으로 지정 되는 동일한 이름의 클래스 여야 하며에서 <xref:System.Windows.Application>파생 되어야 합니다. 이렇게 하면 응용 프로그램을 빌드할 때 태그 파일에 대해 생성 `partial` 되는 클래스와 코드 숨김이 연결 될 수 있습니다 ( [WPF 응용 프로그램 빌드](building-a-wpf-application-wpf.md)참조).

> [!NOTE]
> Visual Studio를 사용 하 여 새 WPF 응용 프로그램 프로젝트 또는 WPF 브라우저 응용 프로그램 프로젝트를 만드는 경우 응용 프로그램 정의는 기본적으로 포함 되며 태그와 코드 숨김으로 모두 사용 하 여 정의 됩니다.

이 코드는 애플리케이션 정의를 구현하는 데 필요한 최소한의 코드이지만, 그러나 응용 프로그램을 빌드하고 실행 하기 전에 응용 프로그램 정의에 대 한 추가 MSBuild 구성을 설정 해야 합니다.

### <a name="configuring-the-application-definition-for-msbuild"></a>MSBuild용 애플리케이션 정의 구성

독립 실행형 응용 프로그램 및 Xbap (XAML 브라우저 응용 프로그램)는 특정 수준의 인프라를 구현 해야 실행할 수 있습니다. 이 인프라의 가장 중요한 부분은 진입점입니다. 사용자가 애플리케이션을 시작하면 운영 체제에서는 잘 알려진 애플리케이션 시작 함수인 진입점을 호출합니다.

일반적으로는 기술에 따라 개발자가 직접 이 코드 일부나 전체를 작성해야 합니다. 그러나 다음 msbuild 프로젝트 파일에 표시 된 것 처럼 응용 프로그램 정의의 태그 파일이 msbuild `ApplicationDefinition` 항목으로 구성 된 경우 WPF는이 코드를 생성 합니다.

```xml
<Project
  DefaultTargets="Build"
                        xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  ...
  <ApplicationDefinition Include="App.xaml" />
  <Compile Include="App.xaml.cs" />
  ...
</Project>
```

코드를 포함 하는 코드는 정상적인 코드를 포함 하기 때문에 MSBuild `Compile` 항목으로 표시 됩니다.

응용 프로그램 정의의 태그 및 코드 숨김으로 이러한 MSBuild 구성을 적용 하면 MSBuild에서 다음과 같은 코드를 생성 합니다.

[!code-csharp[auto-generated-code](~/samples/snippets/csharp/VS_Snippets_Wpf/AppDefAugSnippets/CSharp/App.cs)]
[!code-vb[auto-generated-code](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AppDefAugSnippets/VisualBasic/App.vb)]

결과 코드는 진입점 메서드 `Main`를 포함 하는 추가 인프라 코드를 사용 하 여 응용 프로그램 정의를 보강 합니다. 특성 <xref:System.STAThreadAttribute> 은 wpf 응용 프로그램의 `Main` 주 UI 스레드가 wpf 응용 프로그램에 필요한 STA 스레드 임을 나타내기 위해 메서드에 적용 됩니다. 호출 `Main` 될 때 메서드를 `InitializeComponent` 호출 하 여 `App` 이벤트를 등록 하 고 태그에 구현 된 속성을 설정 하기 전에의 새 인스턴스를 만듭니다. 는 `InitializeComponent` 사용자를 위해 생성 되므로 및 <xref:System.Windows.Window> 구현에 대해 <xref:System.Windows.Controls.Page> 수행 하 `InitializeComponent` 는 것 처럼 응용 프로그램 정의에서 명시적으로 호출할 필요가 없습니다. 마지막으로, <xref:System.Windows.Application.Run%2A> 메서드를 호출 하 여 응용 프로그램을 시작 합니다.

<a name="Getting_the_Current_Application"></a>

## <a name="getting-the-current-application"></a>현재 애플리케이션 가져오기

<xref:System.Windows.Application> 클래스의 기능은 응용 프로그램에서 공유 되므로 당 <xref:System.Windows.Application> <xref:System.AppDomain>클래스의 인스턴스는 하나만 있을 수 있습니다. 이를 적용 하기 위해 <xref:System.Windows.Application> 클래스는 singleton 클래스로 [ C# ](https://go.microsoft.com/fwlink/?LinkId=100567)구현 됩니다. 즉,의 단일 인스턴스를 만들고 <xref:System.Windows.Application.Current%2A> 속성을 사용 `static` 하 여이에 대 한 공유 액세스를 제공 합니다.

다음 코드에서는 현재 <xref:System.Windows.Application> <xref:System.AppDomain>의 개체에 대 한 참조를 가져오는 방법을 보여 줍니다.

[!code-csharp[ApplicationManagementOverviewSnippets#GetCurrentAppCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/CSharp/MainWindow.xaml.cs#getcurrentappcode)]
[!code-vb[ApplicationManagementOverviewSnippets#GetCurrentAppCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/VisualBasic/MainWindow.xaml.vb#getcurrentappcode)]

<xref:System.Windows.Application.Current%2A><xref:System.Windows.Application> 클래스의 인스턴스에 대 한 참조를 반환 합니다. <xref:System.Windows.Application> 파생 된 클래스에 대 한 참조를 원하는 경우 다음 예제와 같이 <xref:System.Windows.Application.Current%2A> 속성의 값을 캐스팅 해야 합니다.

[!code-csharp[ApplicationManagementOverviewSnippets#GetSTCurrentAppCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/CSharp/MainWindow.xaml.cs#getstcurrentappcode)]
[!code-vb[ApplicationManagementOverviewSnippets#GetSTCurrentAppCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/VisualBasic/MainWindow.xaml.vb#getstcurrentappcode)]

개체<xref:System.Windows.Application> 수명의 임의 지점에서의 <xref:System.Windows.Application.Current%2A> 값을 검사할 수 있습니다. 하지만 이러한 검사를 수행할 때는 주의해야 합니다. 클래스가 인스턴스화된 후에는 <xref:System.Windows.Application> 개체의 상태가 일치 하지 않는 기간이 발생 합니다. <xref:System.Windows.Application> 이 기간 <xref:System.Windows.Application> 동안는 응용 프로그램 인프라를 설정 하 고, 속성을 설정 하 고, 이벤트를 등록 하는 등 코드를 실행 하는 데 필요한 다양 한 초기화 작업을 수행 합니다. 이 기간 동안 <xref:System.Windows.Application> 개체를 사용 하려고 하면 코드에서 예기치 않은 결과가 발생할 수 있으며,이는 설정 되는 다양 한 <xref:System.Windows.Application> 속성에 따라 달라 지는 경우에 특히 그렇습니다.

에서 <xref:System.Windows.Application> 초기화 작업을 완료 하면 수명이 실제로 시작 됩니다.

<a name="Application_Lifetime"></a>

## <a name="application-lifetime"></a>애플리케이션 수명

WPF 응용 프로그램의 수명은에서 <xref:System.Windows.Application> 발생 하는 몇 가지 이벤트로 표시 됩니다 .이 이벤트는 응용 프로그램이 시작 되 고, 활성화 및 비활성화 되 고, 종료 된 시기를 알려 주는 데 사용 됩니다.

<a name="Splash_Screen"></a>

### <a name="splash-screen"></a>시작 화면

.NET Framework 3.5 s p 1 부터는 시작 창 또는 *시작 화면*에서 사용할 이미지를 지정할 수 있습니다. 클래스 <xref:System.Windows.SplashScreen> 를 사용 하면 응용 프로그램을 로드 하는 동안 시작 창을 쉽게 표시할 수 있습니다. 가 호출 되기 전에 <xref:System.Windows.Application.Run%2A> 창이만들어지고표시됩니다.<xref:System.Windows.SplashScreen> 자세한 내용은 [응용 프로그램 시작 시간](../advanced/application-startup-time.md) 및 [WPF 응용 프로그램에 시작 화면 추가](how-to-add-a-splash-screen-to-a-wpf-application.md)를 참조 하세요.

<a name="Starting_an_Application"></a>

### <a name="starting-an-application"></a>애플리케이션 시작

가 <xref:System.Windows.Application.Run%2A> 호출 되 고 응용 프로그램이 초기화 된 후 응용 프로그램을 실행할 준비가 된 것입니다. 이 순간은 <xref:System.Windows.Application.Startup> 이벤트가 발생할 때 표시 됩니다.

[!code-csharp[Startup-event](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationStartupSnippets/CSharp/App.xaml.cs?range=3-11,31-33)]
[!code-vb[Startup-event](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationStartupSnippets/visualbasic/application.xaml.vb?range=5-11,30-32)]

응용 프로그램 수명의이 시점에서 가장 일반적인 작업은 UI를 표시 하는 것입니다.

<a name="Showing_a_User_Interface"></a>

### <a name="showing-a-user-interface"></a>사용자 인터페이스 표시

대부분의 독립 실행형 Windows 응용 <xref:System.Windows.Window> 프로그램은 실행을 시작할 때를 엽니다. <xref:System.Windows.Application.Startup> 이벤트 처리기는 다음 코드에서 보여 주는 것 처럼이 작업을 수행할 수 있는 한 위치입니다.

[!code-xaml[AppShowWindowHardSnippets#StartupEventMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/AppShowWindowHardSnippets/CSharp/App.xaml#startupeventmarkup)]

[!code-csharp[AppShowWindowHardSnippets#StartupEventCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/AppShowWindowHardSnippets/CSharp/App.xaml.cs#startupeventcodebehind)]
[!code-vb[AppShowWindowHardSnippets#StartupEventCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AppShowWindowHardSnippets/VisualBasic/Application.xaml.vb#startupeventcodebehind)]

> [!NOTE]
> 독립 실행형 <xref:System.Windows.Window> 응용 프로그램에서 인스턴스화될 첫 번째는 기본적으로 주 응용 프로그램 창이 됩니다. 이 <xref:System.Windows.Window> 개체는 <xref:System.Windows.Application.MainWindow%2A?displayProperty=nameWithType> 속성에서 참조 됩니다. 처음 인스턴스화되 <xref:System.Windows.Application.MainWindow%2A> <xref:System.Windows.Window> 는 것과 다른 창이 주 창인 경우 속성 값을 프로그래밍 방식으로 변경할 수 있습니다.

처음으로 XBAP를 시작 하면로 <xref:System.Windows.Controls.Page>이동 하는 경우가 많습니다. 다음 코드에서 이를 확인할 수 있습니다.

[!code-xaml[XBAPAppStartupSnippets#StartupXBAPMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/XBAPAppStartupSnippets/CSharp/App.xaml#startupxbapmarkup)]

[!code-csharp[XBAPAppStartupSnippets#StartupXBAPCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/XBAPAppStartupSnippets/CSharp/App.xaml.cs#startupxbapcodebehind)]
[!code-vb[XBAPAppStartupSnippets#StartupXBAPCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XBAPAppStartupSnippets/VisualBasic/Application.xaml.vb#startupxbapcodebehind)]

만을 `StartupUri` 열거나로 <xref:System.Windows.Application.Startup> <xref:System.Windows.Window> <xref:System.Windows.Controls.Page>이동 하는 경우에는 태그에 특성을 대신 설정할 수 있습니다.

다음 예제에서는 독립 실행형 응용 프로그램 <xref:System.Windows.Application.StartupUri%2A> 에서를 사용 하 여을 <xref:System.Windows.Window>여는 방법을 보여 줍니다.

[!code-xaml[ApplicationManagementOverviewSnippets#OverviewStartupUriMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/CSharp/App.xaml#overviewstartupurimarkup)]

다음 예제에서는 XBAP에서를 사용 <xref:System.Windows.Application.StartupUri%2A> 하 여 <xref:System.Windows.Controls.Page>로 이동 하는 방법을 보여 줍니다.

[!code-xaml[PageSnippets#XBAPStartupUriMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/PageSnippets/CSharp/App.xaml#xbapstartupurimarkup)]

이 태그는 창을 여는 이전 코드와 같은 효과를 갖습니다.

> [!NOTE]
> 탐색에 대 한 자세한 내용은 [탐색 개요](navigation-overview.md)를 참조 하세요.

매개 변수가 없는 생성자를 <xref:System.Windows.Application.Startup> 사용 하 여 인스턴스화해야 <xref:System.Windows.Window> 하거나 해당 속성을 설정 하거나 표시 하기 전에 해당 이벤트를 구독 하거나 명령줄 인수를 처리 해야 하는 경우 이벤트를 처리 하 여를 열어야 합니다. 응용 프로그램이 시작 될 때 제공 된입니다.

<a name="Processing_Command_Line_Arguments"></a>

### <a name="processing-command-line-arguments"></a>명령줄 인수 처리

Windows에서 독립 실행형 응용 프로그램은 명령 프롬프트 또는 바탕 화면에서 실행할 수 있습니다. 두 경우 모두 명령줄 인수를 애플리케이션으로 전달할 수 있습니다. 다음 예제에서는 단일 명령줄 인수 "/StartMinimized"를 사용하여 시작되는 애플리케이션을 보여 줍니다.

`wpfapplication.exe /StartMinimized`

응용 프로그램을 초기화 하는 동안 WPF는 운영 체제에서 명령줄 인수를 검색 하 여 <xref:System.Windows.Application.Startup> <xref:System.Windows.StartupEventArgs> 매개 변수의 <xref:System.Windows.StartupEventArgs.Args%2A> 속성을 통해 이벤트 처리기에 전달 합니다. 다음과 같은 코드를 사용하여 명령줄 인수를 검색하고 저장할 수 있습니다.

[!code-xaml[ApplicationStartupSnippets#HandleStartupXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationStartupSnippets/CSharp/App.xaml#handlestartupxaml)]

[!code-csharp[ApplicationStartupSnippets#HandleStartupCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationStartupSnippets/CSharp/App.xaml.cs#handlestartupcodebehind)]
[!code-vb[ApplicationStartupSnippets#HandleStartupCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationStartupSnippets/visualbasic/application.xaml.vb#handlestartupcodebehind)]

코드는 **/start최소화** 된 명령줄 인수가 제공 되었는지 여부를 확인 하기 위해를 처리 <xref:System.Windows.WindowState> <xref:System.Windows.Application.Startup> 하 고, 그럴 경우를 사용 하 여 주 <xref:System.Windows.WindowState.Minimized>창을 엽니다. <xref:System.Windows.Window.WindowState%2A> 속성을 프로그래밍 방식으로 설정 해야 하므로 main <xref:System.Windows.Window> 은 코드에서 명시적으로 열어야 합니다.

Xbap는 ClickOnce 배포를 사용 하 여 시작 되기 때문에 명령줄 인수를 검색 하 고 처리할 수 없습니다 ( [WPF 응용 프로그램 배포](deploying-a-wpf-application-wpf.md)참조). 그러나 XBAP를 시작하는 데 사용되는 URL에서 쿼리 문자열 매개 변수를 검색하고 처리할 수 있습니다.

<a name="Application_Activation_and_Deactivation"></a>

### <a name="application-activation-and-deactivation"></a>애플리케이션 활성화 및 비활성화

Windows에서는 사용자가 응용 프로그램 간에 전환할 수 있습니다. 가장 일반적인 방법은 ALT+TAB 키 조합을 사용하는 것입니다. 응용 프로그램은 사용자가 선택할 수 있는 것으로 표시 <xref:System.Windows.Window> 된 경우에만 전환할 수 있습니다. 현재 선택 <xref:System.Windows.Window> 된는 *활성 창* ( *전경* <xref:System.Windows.Window> 창이 라고도 함) 이며 사용자 입력을 받는입니다. 활성 창이 있는 응용 프로그램은 *활성 응용 프로그램* (또는 *포그라운드 응용 프로그램*)입니다. 다음과 같은 경우에 애플리케이션이 활성 애플리케이션이 됩니다.

- 시작 되 고가 표시 <xref:System.Windows.Window>됩니다.

- 사용자는 응용 프로그램에서를 <xref:System.Windows.Window> 선택 하 여 다른 응용 프로그램에서 전환 합니다.

이벤트를 <xref:System.Windows.Application.Activated?displayProperty=nameWithType> 처리 하 여 응용 프로그램이 활성화 되는 시기를 감지할 수 있습니다.

마찬가지로 다음과 같은 경우에는 애플리케이션이 비활성화됩니다.

- 사용자가 현재 애플리케이션에서 다른 애플리케이션으로 전환하는 경우

- 애플리케이션이 종료되는 경우

이벤트를 <xref:System.Windows.Application.Deactivated?displayProperty=nameWithType> 처리 하 여 응용 프로그램이 비활성 상태가 되는 경우를 감지할 수 있습니다.

다음 코드에서는 <xref:System.Windows.Application.Activated> 및 <xref:System.Windows.Application.Deactivated> 이벤트를 처리 하 여 응용 프로그램이 활성 상태 인지 여부를 확인 하는 방법을 보여 줍니다.

[!code-xaml[ApplicationActivationSnippets#DetectActivationStateXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationActivationSnippets/CSharp/App.xaml#detectactivationstatexaml)]

[!code-csharp[ApplicationActivationSnippets#DetectActivationStateCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationActivationSnippets/CSharp/App.xaml.cs#detectactivationstatecodebehind)]
[!code-vb[ApplicationActivationSnippets#DetectActivationStateCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationActivationSnippets/visualbasic/application.xaml.vb#detectactivationstatecodebehind)]

을 <xref:System.Windows.Window> 활성화 하 고 비활성화할 수도 있습니다. 자세한 내용은 <xref:System.Windows.Window.Activated?displayProperty=nameWithType> 및 <xref:System.Windows.Window.Deactivated?displayProperty=nameWithType>를 참조하세요.

> [!NOTE]
> Xbap에 <xref:System.Windows.Application.Deactivated?displayProperty=nameWithType> 대해서 도발생하지않습니다.<xref:System.Windows.Application.Activated?displayProperty=nameWithType>

<a name="Application_Shutdown"></a>

### <a name="application-shutdown"></a>애플리케이션 종료

다음과 같은 이유로 애플리케이션이 종료되면 애플리케이션 수명이 끝납니다.

- 사용자가 모든 <xref:System.Windows.Window>를 닫습니다.

- 사용자가 주 <xref:System.Windows.Window>를 닫습니다.

- 사용자가 로그 오프 하거나 종료 하 여 Windows 세션을 종료 합니다.

- 애플리케이션별 조건이 충족된 경우

응용 <xref:System.Windows.Application> 프로그램 종료를 관리 하는 데 도움이 <xref:System.Windows.Application.Shutdown%2A> 되도록는 메서드 <xref:System.Windows.Application.ShutdownMode%2A> , 속성 및 <xref:System.Windows.Application.SessionEnding> 및 <xref:System.Windows.Application.Exit> 이벤트를 제공 합니다.

> [!NOTE]
> <xref:System.Windows.Application.Shutdown%2A>가 <xref:System.Security.Permissions.UIPermission>있는 응용 프로그램 에서만를 호출할 수 있습니다. 독립 실행형 WPF 응용 프로그램에는 항상이 권한이 있습니다. 그러나 인터넷 영역 부분 신뢰 보안 샌드박스에서 실행 되는 Xbap는 그렇지 않습니다.

#### <a name="shutdown-mode"></a>종료 모드

대부분의 애플리케이션은 모든 창을 닫거나 주 창을 닫으면 종료됩니다. 하지만 다른 애플리케이션과 관련된 조건이 특정 애플리케이션의 종료 시점을 결정하는 경우가 있습니다. <xref:System.Windows.Application.ShutdownMode%2A> 다음<xref:System.Windows.ShutdownMode> 열거형 값 중 하나를 사용 하 여를 설정 하 여 응용 프로그램을 종료 하는 조건을 지정할 수 있습니다.

- <xref:System.Windows.ShutdownMode.OnLastWindowClose>

- <xref:System.Windows.ShutdownMode.OnMainWindowClose>

- <xref:System.Windows.ShutdownMode.OnExplicitShutdown>

의 <xref:System.Windows.Application.ShutdownMode%2A> 기본값은입니다 <xref:System.Windows.ShutdownMode.OnLastWindowClose>. 즉, 사용자가 응용 프로그램의 마지막 창을 닫을 때 응용 프로그램이 자동으로 종료 됩니다. 그러나 주 창이 닫힐 때 응용 프로그램을 종료 해야 하는 경우 WPF는를로 <xref:System.Windows.Application.ShutdownMode%2A> <xref:System.Windows.ShutdownMode.OnMainWindowClose>설정 하면 자동으로이를 수행 합니다. 이는 다음 예에서 확인할 수 있습니다.

[!code-xaml[ApplicationShutdownModeSnippets#OnMainWindowCloseMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationShutdownModeSnippets/CS/Page1.xaml#onmainwindowclosemarkup)]

응용 프로그램별 종료 조건이 있는 경우를로 <xref:System.Windows.Application.ShutdownMode%2A> <xref:System.Windows.ShutdownMode.OnExplicitShutdown>설정 합니다. 이 경우 명시적으로 메서드를 <xref:System.Windows.Application.Shutdown%2A> 호출 하 여 응용 프로그램을 종료 하는 것은 사용자의 책임입니다. 그렇지 않으면 모든 창이 닫힌 경우에도 응용 프로그램이 계속 실행 됩니다. <xref:System.Windows.Application.ShutdownMode%2A> 가 또는 일<xref:System.Windows.ShutdownMode.OnMainWindowClose>경우 <xref:System.Windows.Application.Shutdown%2A>를암시적으로호출 합니다<xref:System.Windows.ShutdownMode.OnLastWindowClose> .

> [!NOTE]
> <xref:System.Windows.Application.ShutdownMode%2A>는 XBAP에서 설정할 수 있지만 무시 됩니다. XBAP는 브라우저에서 벗어나거나 XBAP를 호스트 하는 브라우저가 닫히면 항상 종료 됩니다. 자세한 내용은 [탐색 개요](navigation-overview.md)를 참조하세요.

#### <a name="session-ending"></a>세션 종료

<xref:System.Windows.Application.ShutdownMode%2A> 속성에서 설명 하는 종료 조건은 응용 프로그램에만 적용 됩니다. 하지만 외부 조건에 따라 애플리케이션이 종료되는 경우도 있습니다. 가장 일반적인 외부 조건은 사용자가 다음 작업을 통해 Windows 세션을 종료할 때 발생 합니다.

- 로그오프

- 종료

- 다시 시작

- 최대 절전 모드

Windows 세션이 종료 되는 시기를 검색 하기 위해 다음 예제 <xref:System.Windows.Application.SessionEnding> 와 같이 이벤트를 처리할 수 있습니다.

[!code-xaml[ApplicationSessionEndingSnippets#HandlingSessionEndingXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationSessionEndingSnippets/CSharp/App.xaml#handlingsessionendingxaml)]

[!code-csharp[ApplicationSessionEndingSnippets#HandlingSessionEndingCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationSessionEndingSnippets/CSharp/App.xaml.cs#handlingsessionendingcodebehind)]
[!code-vb[ApplicationSessionEndingSnippets#HandlingSessionEndingCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationSessionEndingSnippets/visualbasic/application.xaml.vb#handlingsessionendingcodebehind)]

이 예제에서 코드는 <xref:System.Windows.SessionEndingCancelEventArgs.ReasonSessionEnding%2A> 속성을 검사 하 여 Windows 세션이 종료 되는 방법을 확인 합니다. 또한 이 값을 사용하여 사용자에게 확인 메시지를 표시합니다. 사용자가 세션을 종료 하지 않으려는 경우 코드는를로 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> `true` 설정 하 여 Windows 세션의 종료를 방지 합니다.

> [!NOTE]
> <xref:System.Windows.Application.SessionEnding>는 Xbap에 대해 발생 하지 않습니다.

#### <a name="exit"></a>종료

애플리케이션이 종료될 때 애플리케이션 상태 유지와 같은 몇 가지 최종 처리를 수행해야 할 경우가 있습니다. 이러한 상황에서는 이벤트 처리기가 다음 예제 <xref:System.Windows.Application.Exit> 에서 수행 하는 `App_Exit` 것 처럼 이벤트를 처리할 수 있습니다. 이 클래스는 *app.xaml* 파일에서 이벤트 처리기로 정의 됩니다. 해당 구현은 *App.xaml.cs* 및 *응용 프로그램 .xaml* 파일에서 강조 표시 됩니다.

[!code-xaml[Defining-the-Exit-event-handler](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml?highlight=1-7)]

[!code-csharp[Handling-the-Exit-event](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml.cs?highlight=42-55)]
[!code-vb[Handling-the-Exit-event](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/visualbasic/application.xaml.vb?highlight=34-45)]

전체 예제는 [응용 프로그램 세션 간에 응용 프로그램 범위 속성 유지 및 복원](persist-and-restore-application-scope-properties.md)을 참조 하세요.

<xref:System.Windows.Application.Exit>는 독립 실행형 응용 프로그램과 Xbap 모두에서 처리할 수 있습니다. Xbap의 경우 <xref:System.Windows.Application.Exit> 다음과 같은 상황에서이 발생 합니다.

- 에서 XBAP를 탐색 합니다.

- Internet Explorer에서 XBAP를 호스트 하는 탭이 닫혀 있는 경우

- 브라우저가 닫힌 경우

#### <a name="exit-code"></a>종료 코드

대부분의 경우 애플리케이션은 운영 체제에서 사용자 요청에 대한 응답으로 시작하게 됩니다. 하지만 다른 애플리케이션에서 일부 특정 작업을 수행하기 위해 애플리케이션을 시작할 수도 있습니다. 시작된 애플리케이션이 종료될 경우 시작하는 애플리케이션에서 시작된 애플리케이션이 종료되는 조건을 알고 싶을 수 있습니다. 이러한 상황에서 Windows는 응용 프로그램이 종료 될 때 응용 프로그램 종료 코드를 반환할 수 있도록 허용 합니다. 기본적으로 WPF 응용 프로그램은 종료 코드 값 0을 반환 합니다.

> [!NOTE]
> Visual Studio에서 디버그할 때 응용 프로그램이 종료 되 면 **출력** 창에 다음과 같은 메시지에서 응용 프로그램 종료 코드가 표시 됩니다.
>
> `The program '[5340] AWPFApp.vshost.exe: Managed' has exited with code 0 (0x0).`
>
> **보기** 메뉴에서 **출력** 을 클릭 하 여 **출력** 창을 엽니다.

종료 코드를 변경 하기 위해 정수 인수를 허용 <xref:System.Windows.Application.Shutdown%28System.Int32%29> 하는 오버 로드를 호출 하 여 종료 코드를 사용할 수 있습니다.

[!code-csharp[ApplicationExitSnippets#AppExitCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationExitSnippets/CSharp/MainWindow.xaml.cs#appexitcode)]
[!code-vb[ApplicationExitSnippets#AppExitCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationExitSnippets/visualbasic/mainwindow.xaml.vb#appexitcode)]

<xref:System.Windows.Application.Exit> 이벤트를 처리 하 여 종료 코드의 값을 검색 하 고 변경할 수 있습니다. 이벤트 처리기는 <xref:System.Windows.ExitEventArgs.ApplicationExitCode%2A> 속성을 사용 <xref:System.Windows.ExitEventArgs> 하 여 종료 코드에 대 한 액세스를 제공 하는를 전달 합니다. <xref:System.Windows.Application.Exit> 자세한 내용은 <xref:System.Windows.Application.Exit>을 참조하세요.

> [!NOTE]
> 독립 실행형 응용 프로그램과 Xbap 모두에서 종료 코드를 설정할 수 있습니다. 그러나 Xbap의 종료 코드 값은 무시 됩니다.

<a name="Unhandled_Exceptions"></a>

### <a name="unhandled-exceptions"></a>처리되지 않은 예외

원하지 않는 예외를 throw하는 경우와 같이 애플리케이션이 비정상적인 상황에서 종료되는 경우가 있습니다. 이런 경우에는 애플리케이션에 예외를 검색하고 처리할 코드가 없을 수 있습니다. 이런 형식의 예외가 처리되지 않은 예외이며, 애플리케이션이 닫히기 전에 다음 그림에 표시된 것과 비슷한 알림으로 표시됩니다.

![처리 되지 않은 예외 알림을 보여 주는 스크린샷](./media/application-management-overview/unhandled-exception-notification.png)

사용자 환경의 관점에서는 애플리케이션에서 다음과 같은 작업의 일부 또는 전부를 수행하여 이러한 기본 동작을 방지하는 것이 바람직합니다.

- 사용자에게 친숙한 정보 표시

- 애플리케이션을 실행 상태로 유지

- Windows 이벤트 로그에 자세한 개발자에 게 친숙 한 예외 정보를 기록 합니다.

이러한 지원을 구현 하는 것은 <xref:System.Windows.Application.DispatcherUnhandledException> 이벤트가 발생 하는 처리 되지 않은 예외를 검색할 수 있는지 여부에 따라 달라 집니다.

[!code-xaml[detecting-unhandled-exceptions](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationDispatcherUnhandledExceptionSnippets/CSharp/App.xaml#handledispatcherunhandledexceptionxaml)]

[!code-csharp[code-to-detect-unhandled-exceptions](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationDispatcherUnhandledExceptionSnippets/CSharp/App.xaml.cs)]
[!code-vb[code-to-detect-unhandled-exceptions](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationDispatcherUnhandledExceptionSnippets/visualbasic/application.xaml.vb)]

이벤트 처리기는 예외 자체 ( <xref:System.Windows.Threading.DispatcherUnhandledExceptionEventArgs> <xref:System.Windows.Threading.DispatcherUnhandledExceptionEventArgs.Exception%2A?displayProperty=nameWithType>)를 포함 하 여 처리 되지 않은 예외와 관련 된 컨텍스트 정보를 포함 하는 매개 변수를 전달 합니다. <xref:System.Windows.Application.DispatcherUnhandledException> 이 정보를 사용하여 예외를 처리하는 방법을 결정할 수 있습니다.

을 처리 <xref:System.Windows.Application.DispatcherUnhandledException>하는 경우에는 <xref:System.Windows.Threading.DispatcherUnhandledExceptionEventArgs.Handled%2A?displayProperty=nameWithType> 속성을로 `true`설정 해야 합니다. 그렇지 않으면 WPF는 예외를 아직 처리 되지 않은 것으로 간주 하 고 앞에서 설명한 기본 동작으로 되돌립니다. 처리 되지 않은 예외가 발생 하 고 <xref:System.Windows.Application.DispatcherUnhandledException> 이벤트가 처리 되지 않거나 이벤트가 처리 되 고 <xref:System.Windows.Threading.DispatcherUnhandledExceptionEventArgs.Handled%2A> 가로 `false`설정 된 경우 응용 프로그램이 즉시 종료 됩니다. 또한 다른 <xref:System.Windows.Application> 이벤트가 발생 하지 않습니다. 따라서 응용 프로그램이 종료 되기 전에 <xref:System.Windows.Application.DispatcherUnhandledException> 실행 해야 하는 코드가 응용 프로그램에 있는 경우를 처리 해야 합니다.

처리되지 않은 예외의 결과로 애플리케이션이 종료될 수는 있지만 애플리케이션은 대개 다음 섹션에서 설명하는 것처럼 사용자 요청에 대한 응답으로 종료됩니다.

<a name="Application_Lifetime_Events"></a>

### <a name="application-lifetime-events"></a>애플리케이션 수명 이벤트

독립 실행형 응용 프로그램 및 Xbap는 정확히 동일한 수명이 아닙니다. 다음 그림에서는 독립 실행형 애플리케이션 수명에서의 주요 이벤트와 이러한 이벤트가 발생하는 순서를 보여 줍니다.

![독립 실행형 응용 프로그램 &#45; 응용 프로그램 개체 이벤트](./media/applicationmodeloverview-applicationobjectevents.png "ApplicationModelOverview_ApplicationObjectEvents")

마찬가지로, 다음 그림은 XBAP의 수명에서 키 이벤트를 보여 주고이 이벤트가 발생 하는 순서를 보여 줍니다.

![XBAP &#45; 응용 프로그램 개체 이벤트](./media/applicationmodeloverview-applicationobjectevents-xbap.png "ApplicationModelOverview_ApplicationObjectEvents_xbap")

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Application>
- [WPF 창 개요](wpf-windows-overview.md)
- [탐색 개요](navigation-overview.md)
- [WPF 응용 프로그램 리소스, 콘텐츠 및 데이터 파일](wpf-application-resource-content-and-data-files.md)
- [WPF의 Pack URI](pack-uris-in-wpf.md)
- [응용 프로그램 모델: 방법 도움말 항목](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms749013(v=vs.100))
- [응용 프로그램 개발](index.md)
