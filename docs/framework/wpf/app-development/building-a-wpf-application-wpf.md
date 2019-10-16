---
title: WPF 애플리케이션 빌드(WPF)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WPF application [WPF], building
ms.assetid: a58696fd-bdad-4b55-9759-136dfdf8b91c
ms.openlocfilehash: a5254de07029e53dd6b72bd2c096c38525a661b6
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69958718"
---
# <a name="building-a-wpf-application-wpf"></a>WPF 애플리케이션 빌드(WPF)

WPF (Windows Presentation Foundation) 응용 프로그램은 .NET Framework 실행 파일 (.exe), 라이브러리 (.dll) 또는 두 어셈블리 형식의 조합으로 빌드할 수 있습니다. 이 항목에서는 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 애플리케이션을 빌드하는 방법과 빌드 프로세스의 주요 단계에 대해 설명합니다.

<a name="Building_a_WPF_Application_using_Command_Line"></a>

## <a name="building-a-wpf-application"></a>WPF 애플리케이션 빌드

다음과 같은 방법으로 WPF 애플리케이션을 컴파일할 수 있습니다.

- 명령줄. 애플리케이션에 코드(XAML 없음)와 애플리케이션 정의 파일만 포함되어야 합니다. 자세한 내용은 [csc.exe를 사용한 명령줄 빌드](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md) 또는 [명령줄에서 빌드(Visual Basic)](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)를 참조하세요.

- MSBuild(Microsoft Build Engine). 애플리케이션에 코드 및 XAML 파일 외에 MSBuild 프로젝트 파일이 포함되어야 합니다. 자세한 내용은 "MSBuild"를 참조하세요.

- Visual Studio. Visual Studio는 MSBuild를 사용하여 WPF 애플리케이션을 컴파일하고 UI를 만들기 위한 비주얼 디자이너를 포함하는 통합 개발 환경입니다. 자세한 내용은 visual Studio를 [사용 하 여 코드 작성 및 관리](/visualstudio/ide/index-writing-code) 및 [VISUAL Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)을 참조 하세요.

<a name="The_Windows_Presentation_Foundation_Build_Pipeline"></a>

## <a name="wpf-build-pipeline"></a>WPF 빌드 파이프라인

[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 프로젝트를 빌드할 때 언어별 및 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]별 대상 조합이 호출됩니다. 이러한 대상을 실행 중인 프로세스를 빌드 파이프라인이라고 하며 주요 단계는 다음 그림에서와 같이 설명됩니다.

![WPF 빌드 프로세스](./media/wpfbuildsystem-figure1.png "WPFBuildSystem_Figure1")

<a name="Pre_Build_Initializations"></a>

### <a name="pre-build-initializations"></a>빌드 전 초기화

빌드하기 전에 MSBuild는 다음을 포함 하 여 중요 한 도구 및 라이브러리의 위치를 결정 합니다.

- .NET Framework입니다.

- [!INCLUDE[TLA2#tla_wcsdk](../../../../includes/tla2sharptla-wcsdk-md.md)] 디렉터리

- [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 참조 어셈블리 위치

- 어셈블리 검색 경로의 속성

MSBuild에서 어셈블리를 검색 하는 첫 번째 위치는 참조 어셈블리 디렉터리 (%ProgramFiles%\Reference\\Assemblies\Microsoft\Framework\v3.0)입니다. 이 단계에서 빌드 프로세스는 다양한 속성 및 항목 그룹을 초기화하고 필요한 정리 작업을 수행합니다.

<a name="Resolving_references"></a>

### <a name="resolving-references"></a>참조 확인

빌드 프로세스는 애플리케이션 프로젝트를 빌드하는 데 필요한 어셈블리를 찾아서 바인딩합니다. 이 논리는 `ResolveAssemblyReference` 작업에 포함되어 있습니다. 프로젝트 파일에서 `Reference`로 선언된 모든 어셈블리는 시스템에 이미 설치된 어셈블리의 메타데이터 및 검색 경로에 대한 정보와 함께 작업에 제공됩니다. 이 작업은 어셈블리를 찾고 설치된 어셈블리의 메타데이터를 사용하여 출력 매니페스트에 표시할 필요 없는 이러한 코어 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 어셈블리를 필터링합니다. 이 작업의 목적은 ClickOnce 매니페스트에서 중복되는 정보를 방지하는 것입니다. 예를 들어, PresentationFramework는 및에 대해 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 빌드된 응용 프로그램을 대표 하는 것으로 간주 될 수 있으므로 모든 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 어셈블리가 .NET Framework 있는 모든 컴퓨터의 동일한 위치에 존재 하기 때문입니다. 설치 된 모든 .NET Framework 참조 어셈블리에 대 한 모든 정보를 매니페스트에 포함할 필요가 없습니다.

<a name="Markup_Compilation___Pass_1"></a>

### <a name="markup-compilationpass-1"></a>태그 컴파일 - 패스 1

이 단계에서는 런타임 시 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]을 구문 분석하고 속성 값을 검증하는 데 시간을 소비하지 않도록 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일을 구문 분석 및 컴파일합니다. 컴파일된 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일은 사전 토큰화되어 있으므로 런타임 시 이 파일을 로드하면 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일을 로드하는 것보다 훨씬 속도가 빨라집니다.

이 단계에서 다음 작업은 `Page` 빌드 항목인 모든 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일에 대해 수행됩니다.

1. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일은 태그 컴파일러에 의해 구문 분석됩니다.

2. 컴파일된 표현은 해당 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에 대해 만들어져서 obj\Release 폴더에 복사됩니다.

3. 새 partial 클래스의 CodeDOM 표현이 만들어져서 obj\Release 폴더에 복사됩니다.

또한 모든 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일에 대해 언어별 코드 파일이 생성됩니다. 예를 들어 Visual Basic 프로젝트의 페이지 1. x x x. x x x. x x x. x x x. C# 프로젝트의 Page1.g.cs 페이지에 대해,이 생성 됩니다. 파일 이름에 ".g"가 있으면 파일이 태그 파일(예: `Page` 또는 `Window`)의 최상위 수준 요소에 대한 partial 클래스 선언을 포함하여 생성된 코드라는 의미입니다. 클래스는 ( `partial` C# `Extends` Visual Basic)에서 한정자를 사용 하 여 선언 되며,이는 다른 곳에서 클래스에 대 한 다른 선언이 있음을 나타내기 위해 일반적으로 코드 Page1.xaml.cs 파일에 있습니다.

Partial 클래스는 적절 한 기본 클래스 (예: 페이지) <xref:System.Windows.Controls.Page> 에서 확장 되 고 인터페이스를 <xref:System.Windows.Markup.IComponentConnector?displayProperty=nameWithType> 구현 합니다. 인터페이스 <xref:System.Windows.Markup.IComponentConnector> 에는 구성 요소를 초기화 하 고 해당 콘텐츠의 요소에 대해 이름 및 이벤트를 연결 하는 메서드가 있습니다. 결과적으로 생성된 코드 파일에는 다음과 같은 메서드 구현이 있습니다.

```csharp
public void InitializeComponent() {
    if (_contentLoaded) {
        return;
    }
    _contentLoaded = true;
    System.Uri resourceLocater =
        new System.Uri(
            "window1.xaml",
            System.UriKind.RelativeOrAbsolute);
    System.Windows.Application.LoadComponent(this, resourceLocater);
}
```

```vb
Public Sub InitializeComponent() _

    If _contentLoaded Then
        Return
    End If

    _contentLoaded = True
    Dim resourceLocater As System.Uri = _
        New System.Uri("mainwindow.xaml", System.UriKind.Relative)

    System.Windows.Application.LoadComponent(Me, resourceLocater)

End Sub
```

기본적으로 태그 컴파일은 MSBuild 엔진과 동일 <xref:System.AppDomain> 하 게 실행 됩니다. 따라서 성능이 크게 향상됩니다. 이 동작은 `AlwaysCompileMarkupFilesInSeparateDomain` 속성을 통해 전환할 수 있습니다. 이렇게 하면 별도 <xref:System.AppDomain>의를 언로드하여 모든 참조 어셈블리를 언로드할 때 이점이 있습니다.

<a name="Pass_2_of_Markup_Compilation"></a>

### <a name="markup-compilationpass-2"></a>태그 컴파일 - 패스 2

일부 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 페이지는 태그 컴파일의 패스 1에서 컴파일됩니다. 이때 로컬로 정의된 형식 참조(동일한 프로젝트의 코드에서 정의된 형식에 대한 참조)가 있는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일은 컴파일에서 제외됩니다. 이는 로컬로 정의된 형식이 소스에만 있어 아직 컴파일되지 않았기 때문입니다. 이를 확인하기 위해 파서는 추론을 사용하여 태그 파일에서 `x:Name`과 같은 항목을 찾습니다. 이러한 인스턴스를 찾은 경우 코드 파일이 컴파일될 때까지 해당 태그 파일의 컴파일이 연기되며 나중에 두 번째 태그 컴파일 패스가 이러한 파일을 처리합니다.

<a name="File_Classification"></a>

### <a name="file-classification"></a>파일 분류

빌드 프로세스는 출력 파일을 배치할 애플리케이션 어셈블리를 기반으로 다른 리소스 그룹에 출력 파일을 배치합니다. 일반적으로 지역화되지 않은 애플리케이션에서 `Resource`로 표시된 모든 데이터 파일은 주 어셈블리(실행 파일 또는 라이브러리)에 배치됩니다. 프로젝트에서 `UICulture`가 설정된 경우 컴파일된 모든 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일 및 해당 리소스(특히 언어별로 표시된 리소스)가 위성 리소스 어셈블리에 배치됩니다. 또한 모든 언어 중립 리소스는 주 어셈블리에 배치됩니다. 빌드 프로세스의 이 단계에서 해당 사항이 결정됩니다.

프로젝트 파일의 `ApplicationDefinition`, `Page` 및 `Resource` 빌드 작업은 `Localizable` 메타데이터(허용 가능한 값은 `true` 및 `false`)를 통해 보강할 수 있으며 이는 파일이 언어와 관련되었는지 또는 언어 중립적인지 지정합니다.

<a name="Core_Compilation"></a>

### <a name="core-compilation"></a>핵심 컴파일

핵심 컴파일 단계에서는 코드 파일을 컴파일합니다. 이 작업은 언어별 대상 파일 Microsoft.CSharp.targets 및 Microsoft.VisualBasic.targets의 논리에 의해 오케스트레이션됩니다. 추론을 통해 태그 컴파일러의 단일 패스로 충분하다고 판단된 경우 주 어셈블리가 생성됩니다. 그러나 프로젝트에서 하나 이상의 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일에 로컬로 정의된 형식에 대한 참조가 있는 경우 태그 컴파일의 두 번째 패스가 완료된 후 최종 애플리케이션 어셈블리가 만들어질 수 있도록 임시 .dll 파일이 생성됩니다.

<a name="Manifest_generation"></a>

### <a name="manifest-generation"></a>매니페스트 생성

빌드 프로세스가 끝날 때 응용 프로그램 어셈블리와 콘텐츠 파일이 모두 준비 되 면 응용 프로그램에 대 한 ClickOnce 매니페스트가 생성 됩니다.

배포 매니페스트 파일은 배포 모델, 즉 현재 버전, 업데이트 동작 및 게시자 ID를 디지털 시그니처와 함께 설명합니다. 이 매니페스트는 배포를 처리하는 관리자가 작성합니다. 파일 확장명은 .xbap([!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)])이며 설치된 애플리케이션의 경우 .application입니다. .xbap는 `HostInBrowser` 프로젝트 속성에 의해 지정되며 그 결과 매니페스트는 애플리케이션이 브라우저에 호스트되는 것으로 식별합니다.

애플리케이션 매니페스트(.exe.manifest 파일)는 애플리케이션 어셈블리 및 종속 라이브러리를 설명하고 애플리케이션에 필요한 사용 권한을 나열합니다. 이 파일은 애플리케이션 개발자가 작성합니다. ClickOnce 응용 프로그램을 시작 하기 위해 사용자는 응용 프로그램의 배포 매니페스트 파일을 엽니다.

이러한 매니페스트 파일은 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)]에 대해 항상 만들어집니다. 설치된 애플리케이션의 경우 프로젝트 파일에서 `GenerateManifests` 속성 값이 `true`로 지정되지 않는 한 만들어지지 않습니다.

[!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)]일반적인 인터넷 영역 응용 프로그램에 할당 된 권한 이상의 두 가지 추가 권한 ( <xref:System.Security.Permissions.WebBrowserPermission> 및 <xref:System.Security.Permissions.MediaPermission>)을 가져옵니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 빌드 시스템은 응용 프로그램 매니페스트에서 이러한 사용 권한을 선언합니다.

<a name="Incremental_Build_Support"></a>

## <a name="incremental-build-support"></a>증분 빌드 지원

[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 빌드 시스템은 증분 빌드에 대한 지원을 제공합니다. 태그 또는 코드에 대한 변경 사항을 지능적으로 검색하고 변경 사항의 영향을 받는 아티팩트만 컴파일합니다. 증분 빌드 메커니즘은 다음 파일을 사용합니다.

- 현재 컴파일러 상태를 유지 관리하는 $(*AssemblyName*)_MarkupCompiler.Cache 파일

- 로컬로 정의된 형식에 대한 참조가 있는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일을 캐시하는 $(*AssemblyName*) _MarkupCompiler.lref 파일

다음은 증분 빌드를 제어하는 규칙 집합입니다.

- 파일은 빌드 시스템이 변경을 검색하는 가장 작은 단위입니다. 따라서 코드 파일의 경우 빌드 시스템에서 형식이 변경되었는지 또는 코드가 추가되었는지 확인할 수 없습니다. 이는 프로젝트 파일도 마찬가지입니다.

- 증분 빌드 메커니즘은 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 페이지가 클래스를 정의하거나 다른 클래스를 사용한다는 것을 인식해야 합니다.

- `Reference` 항목이 변경된 경우 모든 페이지를 다시 컴파일합니다.

- 코드 파일이 변경되면 로컬로 정의된 형식 참조가 있는 모든 페이지를 다시 컴파일합니다.

- [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일이 변경된 경우:

  - 프로젝트에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]이 `Page`로 선언된 경우: [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에 로컬로 정의된 형식 참조가 없는 경우 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 및 모든 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 페이지를 로컬 참조와 함께 다시 컴파일합니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에 로컬 참조가 있는 경우 모든 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 페이지를 로컬 참조와 함께 다시 컴파일합니다.

  - 프로젝트 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 에서가로 `ApplicationDefinition` 선언 된 경우: 모든 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 페이지를 다시 컴파일합니다 <xref:System.Windows.Application> (원인 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] : 각각이 변경 되었을 수 있는 형식에 대 한 참조).

- 프로젝트 파일에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일 대신 애플리케이션 정의로 코드 파일을 선언한 경우:

  - 프로젝트 파일의 `ApplicationClassName` 값이 변경되었는지(새로운 애플리케이션 형식이 있는지) 확인합니다. 변경된 경우 전체 애플리케이션을 다시 컴파일합니다.

  - 변경되지 않은 경우 모든 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 페이지를 로컬 참조와 함께 다시 컴파일합니다.

- 프로젝트 파일이 변경된 경우: 앞에서 설명한 규칙을 모두 적용하고 다시 컴파일해야 할 항목을 확인합니다. `AssemblyName`, `IntermediateOutputPath`, `RootNamespace` 및 `HostInBrowser` 속성이 변경되면 전체 다시 컴파일됩니다.

다시 컴파일 작업은 다음과 같은 시나리오로 수행될 수 있습니다.

- 전체 애플리케이션이 다시 컴파일됩니다.

- 로컬로 정의된 형식 참조가 있는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일만 다시 컴파일됩니다.

- 모든 항목이 다시 컴파일되지 않습니다(프로젝트의 모든 항목이 변경되지 않음).

## <a name="see-also"></a>참고자료

- [WPF 응용 프로그램 배포](deploying-a-wpf-application-wpf.md)
- [WPF MSBuild 참조](/visualstudio/msbuild/wpf-msbuild-reference)
- [WPF의 Pack URI](pack-uris-in-wpf.md)
- [WPF 응용 프로그램 리소스, 콘텐츠 및 데이터 파일](wpf-application-resource-content-and-data-files.md)
