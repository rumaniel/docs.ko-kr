---
title: WPF 추가 기능 개요
ms.date: 03/30/2017
helpviewer_keywords:
- add-ins and XAML browser applications [WPF]
- add-ins overview [WPF]
- add-ins [WPF], performance
- add-ins [WPF], benefits
- .NET Framework add-in model [WPF]
- add-ins [WPF], user interface
- add-ins and the user interface [WPF]
- add-ins [WPF], architecture
- add-ins [WPF], limitations
ms.assetid: 00b4c776-29a8-4dba-b603-280a0cdc2ade
ms.openlocfilehash: a146f15a1c2755f254e198d471a42ca9ec29b072
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182537"
---
# <a name="wpf-add-ins-overview"></a>WPF 추가 기능 개요

<a name="Introduction"></a>.NET Framework는 개발자가 추가 기능 확장성을 지 원하는 응용 프로그램을 만드는 데 사용할 수 있는 추가 기능 모델을 포함 합니다. 이 추가 기능 모델을 사용하면 애플리케이션 기능과 통합하고 이 기능을 확장하는 추가 기능을 만들 수 있습니다. 일부 시나리오에서는 응용 프로그램에서 추가 기능을 통해 제공 되는 사용자 인터페이스를 표시 해야 합니다. 이 항목에서는 WPF가 .NET Framework 추가 기능 모델을 보강 하 여 이러한 시나리오, it의 아키텍처, 이점 및 제한 사항을 사용 하도록 설정 하는 방법을 보여 줍니다.

<a name="Requirements"></a>

## <a name="prerequisites"></a>전제 조건

.NET Framework 추가 기능 모델에 대해 잘 알고 있어야 합니다. 자세한 내용은 [추가 기능 및 확장성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))을 참조하세요.

<a name="AddInsOverview"></a>

## <a name="add-ins-overview"></a>추가 기능 개요

애플리케이션에서는 새 기능을 통합하기 위해 애플리케이션을 다시 컴파일하여 배포하는 복잡한 작업을 방지하도록 확장성 메커니즘을 구현하여 개발자(자사 및 타사)가 새 기능을 통합하는 다른 애플리케이션을 만들 수 있도록 합니다. 이러한 형식의 확장성을 지원하는 가장 일반적인 방법은 추가 기능(“추가 기능” 및 “플러그 인”이라고도 함)을 사용하는 것입니다. 추가 기능으로 확장성을 노출하는 실제 애플리케이션의 예에는 다음이 있습니다.

- Internet Explorer 추가 기능.

- Windows Media Player 플러그 인.

- Visual Studio 추가 기능.

예를 들어, Windows Media Player 추가 기능 모델을 사용하면 타사 개발자가 다양한 방식으로 Windows Media Player를 확장하는 “플러그 인”을 구현할 수 있습니다. 이러한 방식에는 Windows Media Player에서 기본적으로 지원하지 않는 미디어 형식(예: DVD, MP3)의 디코더와 인코더, 오디오 효과 및 스킨이 포함됩니다. 모든 추가 기능 모델에 공통인 동작과 엔터티가 여러 개 있지만, 각 추가 기능 모델은 애플리케이션에 고유한 기능을 노출하도록 빌드되어 있습니다.

일반적인 추가 기능 확장성 솔루션의 세 가지 기본 엔터티는 *계약*, *추가 기능* 및 *호스트 애플리케이션*입니다. 계약은 추가 기능이 다음 두 방법으로 호스트 애플리케이션과 통합하는 방법을 정의합니다.

- 추가 기능은 호스트 애플리케이션으로 구현된 기능과 통합됩니다.

- 호스트 애플리케이션에서 추가 기능과 통합될 기능을 노출합니다.

추가 기능을 사용하려면 호스트 애플리케이션에서 해당 기능을 찾아 런타임 시 로드해야 합니다. 따라서 추가 기능을 지원하는 애플리케이션에서는 다음과 같은 추가 작업을 담당합니다.

- **검색**: 호스트 응용 프로그램에서 지 원하는 계약을 준수 하는 추가 기능 찾기

- **활성화**: 추가 기능과의 통신 로드, 실행 및 설정

- **격리**: 응용 프로그램 도메인 또는 프로세스를 사용 하 여 추가 기능에 대 한 잠재적인 보안 및 실행 문제 로부터 응용 프로그램을 보호 하는 격리 경계를 설정 합니다.

- **통신**: 메서드를 호출 하 고 데이터를 전달 하 여 추가 기능과 호스트 응용 프로그램이 격리 경계에서 서로 통신할 수 있도록 합니다.

- **수명 관리**: 응용 프로그램 도메인 및 프로세스를 명확 하 고 예측 가능한 방식으로 로드 및 언로드 ( [응용 프로그램 도메인](../../app-domains/application-domains.md)참조).

- **버전 관리**: 새 버전이 생성 될 때 호스트 응용 프로그램과 추가 기능이 계속 통신할 수 있도록 합니다.

근본적으로, 강력한 추가 기능 모델을 개발하는 것은 쉬운 작업이 아닙니다. 이러한 이유로 .NET Framework는 추가 기능 모델을 빌드하기 위한 인프라를 제공 합니다.

> [!NOTE]
> 추가 기능에 대한 자세한 내용은 [추가 기능 및 확장성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))을 참조하세요.

<a name="NETFrameworkAddInModelOverview"></a>

## <a name="net-framework-add-in-model-overview"></a>.NET Framework 추가 기능 모델 개요

<xref:System.AddIn> 네임 스페이스에 있는 .NET Framework 추가 기능 모델에는 추가 기능 확장성의 개발을 간소화 하기 위해 설계 된 형식 집합이 포함 되어 있습니다. .NET Framework 추가 기능 모델의 기본 단위는 호스트 응용 프로그램과 추가 기능이 서로 통신 하는 방법을 정의 하는 *계약*입니다. 계약은 계약의 호스트-애플리케이션별 *보기*를 사용하여 호스트 애플리케이션에 노출됩니다. 마찬가지로 계약의 추가 기능별 *보기*가 추가 기능에 노출됩니다. 호스트 애플리케이션과 추가 기능이 계약의 각 보기 간에 통신할 수 있도록 *어댑터*가 사용됩니다. 계약, 보기 및 어댑터를 세그먼트라고 하며, 관련 세그먼트 집합이 *파이프라인*을 구성합니다. 파이프라인은 .NET Framework 추가 기능 모델이 검색, 활성화, 보안 격리, 실행 격리 (응용 프로그램 도메인 및 프로세스 사용), 통신, 수명 관리 및 버전 관리를 지 원하는 기반이 됩니다.

개발자는 이러한 지원을 모두 활용하여 호스트 애플리케이션의 기능과 통합하는 추가 기능을 빌드할 수 있습니다. 그러나 일부 시나리오에서는 호스트 응용 프로그램이 추가 기능에서 제공 하는 사용자 인터페이스를 표시 해야 합니다. .NET Framework의 각 프레젠테이션 기술에는 사용자 인터페이스를 구현 하는 자체 모델이 있으므로 .NET Framework 추가 기능 모델은 특정 프레젠테이션 기술을 지원 하지 않습니다. 대신 WPF는 추가 기능에 대 한 UI 지원으로 .NET Framework 추가 기능 모델을 확장 합니다.

<a name="WPFAddInModel"></a>

## <a name="wpf-add-ins"></a>WPF 추가 기능

WPF를 .NET Framework 추가 기능 모델과 함께 사용 하면 호스트 응용 프로그램이 추가 기능에서 사용자 인터페이스를 표시 해야 하는 다양 한 시나리오를 해결할 수 있습니다. 특히 이러한 시나리오는 다음과 같은 두 가지 프로그래밍 모델을 사용 하 여 WPF에서 해결 됩니다.

1. **추가 기능이 UI를 반환함**. 추가 기능에서 계약에 정의 된 대로 메서드 호출을 통해 호스트 응용 프로그램에 대 한 UI를 반환 합니다. 이 시나리오는 다음과 같은 경우에 사용됩니다.

    - 추가 기능에서 반환 되는 UI의 모양은 동적으로 생성 된 보고서와 같이 런타임에만 존재 하는 데이터 또는 조건에 따라 달라 집니다.

    - 추가 기능에서 제공 하는 서비스에 대 한 UI는 추가 기능을 사용할 수 있는 호스트 응용 프로그램의 UI와 다릅니다.

    - 이 추가 기능은 주로 호스트 응용 프로그램에 대 한 서비스를 수행 하 고 UI를 사용 하 여 호스트 응용 프로그램에 상태를 보고 합니다.

2. **추가 기능이 UI임**. 추가 기능은 계약에 정의 된 대로 UI입니다. 이 시나리오는 다음과 같은 경우에 사용됩니다.

    - 추가 기능에서 광고와 같이 표시되고 있지 않은 서비스를 제공하지 않는 경우.

    - 추가 기능에서 제공 하는 서비스에 대 한 UI는 계산기 또는 색 선택기와 같이 해당 추가 기능을 사용할 수 있는 모든 호스트 응용 프로그램에 공통적입니다.

이러한 시나리오에서는 호스트 응용 프로그램과 추가 기능 응용 프로그램 도메인 간에 UI 개체를 전달할 수 있어야 합니다. .NET Framework 추가 기능 모델은 원격 기능을 사용 하 여 응용 프로그램 도메인 간에 통신 하므로 응용 프로그램 간에 전달 되는 개체를 원격으로 사용할 수 있어야 합니다.

원격으로 사용 가능한 개체는 다음 중 하나 이상을 수행하는 클래스의 인스턴스입니다.

- 파생 되는 <xref:System.MarshalByRefObject> 클래스입니다.

- <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현합니다.

- 에 <xref:System.SerializableAttribute> 특성을 적용 합니다.

> [!NOTE]
> 원격으로 사용할 .NET Framework 개체 만들기에 대 한 자세한 내용은 [개체를 원격](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/wcf3swha(v=vs.100))으로 만들기를 참조 하세요.

WPF UI 형식은 원격으로 사용할 수 없습니다. 문제를 해결 하기 위해 WPF는 .NET Framework 추가 기능 모델을 확장 하 여 추가 기능으로 만든 WPF UI를 호스트 응용 프로그램에서 표시할 수 있도록 합니다. 이 지원은 <xref:System.AddIn.Contract.INativeHandleContract> 인터페이스와 <xref:System.AddIn.Pipeline.FrameworkElementAdapters> 클래스 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> 에서 구현 하는 두 개의 정적 메서드인 및와 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>같은 두 가지 형식으로 WPF에서 제공 됩니다. 상위 수준에서는 대략적으로 이러한 형식과 메서드가 다음과 같은 방식으로 사용됩니다.

1. WPF는 추가 기능에서 제공 하는 사용자 인터페이스가 셰이프, 컨트롤, 사용자 컨트롤, 레이아웃 <xref:System.Windows.FrameworkElement>패널 및 페이지와 같이에서 직접 또는 간접적으로 파생 되는 클래스 여야 합니다.

2. 계약이 추가 기능과 호스트 응용 프로그램 간에 전달 되는 UI를 선언 하는 모든 경우에는가 <xref:System.AddIn.Contract.INativeHandleContract> <xref:System.Windows.FrameworkElement>아닌로 선언 해야 합니다. <xref:System.AddIn.Contract.INativeHandleContract> 는 격리 경계를 넘어 전달 될 수 있는 추가 기능 UI를 원격으로 표현한 것입니다.

3. 추가 기능의 응용 프로그램 도메인에서 전달 되기 전에는를 <xref:System.Windows.FrameworkElement> 호출 <xref:System.AddIn.Contract.INativeHandleContract> <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>하 여로 패키지 됩니다.

4. 호스트 응용 프로그램의 응용 프로그램 도메인 <xref:System.AddIn.Contract.INativeHandleContract> 에 전달 된 후에는를 호출 <xref:System.Windows.FrameworkElement> <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>하 여로 다시 패키지 해야 합니다.

, <xref:System.AddIn.Contract.INativeHandleContract> 및를<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> 사용 하는 방법은 특정 시나리오에 따라 달라 집니다. <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> 다음 섹션에서는 각 프로그래밍 모델의 자세한 내용을 제공합니다.

<a name="ReturnUIFromAddInContract"></a>

## <a name="add-in-returns-a-user-interface"></a>추가 기능이 사용자 인터페이스를 반환함

UI를 호스트 응용 프로그램에 반환 하는 추가 기능에는 다음이 필요 합니다.

1. .NET Framework [추가 기능 및 확장성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100)) 설명서에 설명 된 대로 호스트 응용 프로그램, 추가 기능 및 파이프라인을 만들어야 합니다.

2. 계약은를 구현 <xref:System.AddIn.Contract.IContract> 해야 하며 UI를 반환 하려면 계약에서 형식의 <xref:System.AddIn.Contract.INativeHandleContract>반환 값을 사용 하 여 메서드를 선언 해야 합니다.

3. 추가 기능과 호스트 응용 프로그램 간에 전달 되는 UI는에서 <xref:System.Windows.FrameworkElement>직접 또는 간접적으로 파생 되어야 합니다.

4. 추가 기능에서 반환 되는 UI는 격리 경계를 통과 <xref:System.Windows.FrameworkElement> <xref:System.AddIn.Contract.INativeHandleContract> 하기 전에에서로 변환 해야 합니다.

5. 반환 되는 UI는 격리 경계를 넘는 <xref:System.AddIn.Contract.INativeHandleContract> <xref:System.Windows.FrameworkElement> 후에서로 변환 되어야 합니다.

6. 호스트 응용 프로그램에서 반환 <xref:System.Windows.FrameworkElement>된를 표시 합니다.

UI를 반환 하는 추가 기능을 구현 하는 방법을 보여 주는 예제는 UI를 [반환 하는 추가 기능 만들기](how-to-create-an-add-in-that-returns-a-ui.md)를 참조 하세요.

<a name="AddInIsAUI"></a>

## <a name="add-in-is-a-user-interface"></a>추가 기능이 사용자 인터페이스임

추가 기능이 UI 인 경우 다음이 필요 합니다.

1. .NET Framework [추가 기능 및 확장성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100)) 설명서에 설명 된 대로 호스트 응용 프로그램, 추가 기능 및 파이프라인을 만들어야 합니다.

2. 추가 기능에 대 한 계약 인터페이스는를 구현 <xref:System.AddIn.Contract.INativeHandleContract>해야 합니다.

3. 호스트 응용 프로그램에 전달 되는 추가 기능은에서 <xref:System.Windows.FrameworkElement>직접 또는 간접적으로 파생 되어야 합니다.

4. 격리 경계를 통과 <xref:System.Windows.FrameworkElement> <xref:System.AddIn.Contract.INativeHandleContract> 하려면 먼저 추가 기능을에서로 변환 해야 합니다.

5. 격리 경계를 넘는 <xref:System.AddIn.Contract.INativeHandleContract> <xref:System.Windows.FrameworkElement> 후에는 추가 기능을에서로 변환 해야 합니다.

6. 호스트 응용 프로그램에서 반환 <xref:System.Windows.FrameworkElement>된를 표시 합니다.

UI 인 추가 기능을 구현 하는 방법을 보여 주는 예제는 [Ui 인 추가 기능 만들기](how-to-create-an-add-in-that-is-a-ui.md)를 참조 하세요.

<a name="ReturningMultipleUIsFromAnAddIn"></a>

## <a name="returning-multiple-uis-from-an-add-in"></a>추가 기능에서 여러 UI 반환

추가 기능은 호스트 응용 프로그램에서 표시할 여러 사용자 인터페이스를 제공 하는 경우가 많습니다. 예를 들어 ui 인 호스트 응용 프로그램에도 상태 정보를 제공 하는 UI 인 추가 기능을 고려해 보세요. 이와 같은 추가 기능은 [추가 기능이 사용자 인터페이스를 반환함](#ReturnUIFromAddInContract) 및 [추가 기능이 사용자 인터페이스임](#AddInIsAUI) 모델의 기술을 조합하여 구현할 수 있습니다.

<a name="AddInsAndXBAPs"></a>

## <a name="add-ins-and-xaml-browser-applications"></a>추가 기능 및 XAML 브라우저 애플리케이션

지금까지의 예에서는 호스트 애플리케이션이 독립형 애플리케이션으로 설치되었습니다. 다음과 같은 추가 빌드 및 구현 요구 사항이 있긴 하지만 [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)]에서도 추가 기능을 호스팅할 수 있습니다.

- 응용 프로그램 매니페스트는 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]와 동일한 폴더에 있는 클라이언트 컴퓨터의 ClickOnce 응용 프로그램 캐시에 파이프라인 (폴더 및 어셈블리) 및 추가 기능 어셈블리를 다운로드 하도록 특별히 구성 해야 합니다. [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]

- 추가 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 기능을 검색 하 고 로드 하는 코드는에 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 대 한 ClickOnce 응용 프로그램 캐시를 파이프라인 및 추가 기능 위치로 사용 해야 합니다.

- 추가 기능이 원본 사이트에 있는 느슨한 파일을 참조하는 경우 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]는 특수 보안 컨텍스트에 추가 기능을 로드해야 합니다. 추가 기능이 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)]에서 호스팅된 경우 이러한 추가 기능은 호스트 애플리케이션의 원본 사이트에 있는 느슨한 파일만 참조할 수 있습니다.

이러한 작업은 다음 하위 섹션에 자세히 설명되어 있습니다.

### <a name="configuring-the-pipeline-and-add-in-for-clickonce-deployment"></a>ClickOnce 배포를 위한 파이프라인 및 추가 기능 구성

[!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)]는 ClickOnce 배포 캐시의 안전한 폴더에 다운로드 되어 실행 됩니다. [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]가 추가 기능을 호스트하려면 파이프라인과 추가 기능 어셈블리도 안전한 폴더에 다운로드해야 합니다. 이 작업을 수행하려면 다운로드할 파이프라인과 추가 기능 어셈블리를 모두 포함하도록 애플리케이션 매니페스트를 구성해야 합니다. [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]에서 파이프라인 어셈블리를 검색하려면 파이프라인과 추가 기능 어셈블리가 호스트 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 프로젝트의 루트 폴더에 있어야 하지만, 이 작업은 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]에서 가장 쉽게 수행됩니다.

결과적으로 첫 번째 단계에서는 각 파이프라인 어셈블리의 빌드 출력과 추가 기능 어셈블리 프로젝트를 설정하여 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 프로젝트의 루트에 파이프라인 및 추가 기능 어셈블리를 빌드합니다. 다음 표에서는 호스트 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 프로젝트와 동일한 솔루션 및 루트 폴더에 있는 파이프라인 어셈블리 프로젝트와 추가 기능 어셈블리 프로젝트의 빌드 출력 경로를 보여줍니다.

표 1: XBAP에서 호스트 되는 파이프라인 어셈블리의 출력 경로를 빌드합니다.

|파이프라인 어셈블리 프로젝트|빌드 출력 경로|
|-------------------------------|-----------------------|
|계약|`..\HostXBAP\Contracts\`|
|추가 기능 뷰|`..\HostXBAP\AddInViews\`|
|추가 기능측 어댑터|`..\HostXBAP\AddInSideAdapters\`|
|호스트측 어댑터|`..\HostXBAP\HostSideAdapters\`|
|추가 기능|`..\HostXBAP\AddIns\WPFAddIn1`|

다음 단계에서는 다음을 수행하여 파이프라인 어셈블리와 추가 기능 어셈블리를 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]의 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 콘텐츠 파일로 지정합니다.

1. 솔루션 탐색기에서 각 파이프라인 폴더를 마우스 오른쪽 단추로 클릭하고 **프로젝트에 포함**을 선택하여 프로젝트에 파이프라인 및 추가 기능 어셈블리 포함.

2. **속성** 창에서 각 파이프라인 어셈블리 및 추가 기능 어셈블리의 **빌드 작업**을 **콘텐츠**로 설정.

마지막 단계에서는 다운로드할 파이프라인 어셈블리 파일과 추가 기능 어셈블리 파일을 포함하도록 애플리케이션 매니페스트를 구성합니다. 파일은 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 응용 프로그램이 차지 하는 ClickOnce 캐시에 있는 폴더의 루트에 있는 폴더에 있어야 합니다. 구성은 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]에서 다음을 수행하여 구현할 수 있습니다.

1. [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 프로젝트를 마우스 오른쪽 단추로 클릭하고, **속성**, **게시** 순으로 클릭한 다음 **애플리케이션 파일** 단추를 클릭합니다.

2. **애플리케이션 파일** 대화 상자에서 각 파이프라인과 추가 기능 DLL의 **게시 상태**를 **포함(자동)** 으로 설정하고 각 파이프라인과 추가 기능 DLL에 대해 **그룹 다운로드**을 **(필수)** 로 설정합니다.

### <a name="using-the-pipeline-and-add-in-from-the-application-base"></a>애플리케이션 기준 위치에서 파이프라인과 추가 기능 사용

파이프라인 및 추가 기능이 ClickOnce 배포에 대해 구성 된 경우와 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]동일한 clickonce 캐시 폴더에 다운로드 됩니다. [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]의 파이프라인과 추가 기능을 사용하려면 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 코드를 통해 애플리케이션 기준 위치에서 가져와야 합니다. 파이프라인 및 추가 기능을 사용 하기 위한 .NET Framework 추가 기능 모델의 다양 한 형식 및 멤버는이 시나리오에 대 한 특별 한 지원을 제공 합니다. 먼저 경로는 <xref:System.AddIn.Hosting.PipelineStoreLocation.ApplicationBase> 열거형 값으로 식별 됩니다. 다음을 포함하는 파이프라인을 사용하기 위해 관련 추가 기능 멤버의 오버로드와 함께 이 값을 사용합니다.

- <xref:System.AddIn.Hosting.AddInStore.FindAddIns%28System.Type%2CSystem.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=nameWithType>

- <xref:System.AddIn.Hosting.AddInStore.FindAddIns%28System.Type%2CSystem.AddIn.Hosting.PipelineStoreLocation%2CSystem.String%5B%5D%29?displayProperty=nameWithType>

- <xref:System.AddIn.Hosting.AddInStore.Rebuild%28System.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=nameWithType>

- <xref:System.AddIn.Hosting.AddInStore.Update%28System.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=nameWithType>

### <a name="accessing-the-hosts-site-of-origin"></a>호스트의 원본 사이트에 액세스

추가 기능이 원본 사이트의 파일을 참조할 수 있도록 호스트 애플리케이션과 동일한 수준의 보안 격리로 추가 기능을 로드해야 합니다. 이 보안 수준은 <xref:System.AddIn.Hosting.AddInSecurityLevel.Host?displayProperty=nameWithType> 열거형 값으로 식별 되며 추가 기능이 활성화 될 때 <xref:System.AddIn.Hosting.AddInToken.Activate%2A> 메서드로 전달 됩니다.

<a name="WPFAddInModelArchitecture"></a>

## <a name="wpf-add-in-architecture"></a>WPF 추가 기능 아키텍처

가장 높은 수준에서 볼 수 있듯이 WPF는 <xref:System.Windows.FrameworkElement>, 및 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>를 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> 사용 하 여 <xref:System.AddIn.Contract.INativeHandleContract>.NET Framework 추가 기능을 통해 직접 또는 간접적으로 파생 되는 사용자 인터페이스를 구현할 수 있습니다. 그 결과 호스트 응용 프로그램이 호스트 응용 프로그램의 UI <xref:System.Windows.FrameworkElement> 에서 표시 되는을 반환 합니다.

간단한 UI 추가 기능 시나리오의 경우 개발자에 게 필요한 만큼 자세히 설명 합니다. 더 복잡 한 시나리오의 경우, 특히 레이아웃, 리소스 및 데이터 바인딩과 같은 추가 WPF 서비스를 활용 하려는 경우에는 WPF가 UI를 지 원하는 .NET Framework 추가 기능 모델을 확장 하는 방법에 대 한 자세한 내용은 장점을 이해 하는 데 필요 합니다. 및 제한 사항입니다.

기본적으로 WPF는 추가 기능에서 호스트 응용 프로그램으로 UI를 전달 하지 않습니다. 대신 wpf는 WPF 상호 운용성을 사용 하 여 UI에 대 한 Win32 창 핸들을 전달 합니다. 따라서 추가 기능에서 UI가 호스트 응용 프로그램에 전달 되 면 다음 작업이 수행 됩니다.

- 추가 기능 쪽에서 WPF는 호스트 응용 프로그램에 의해 표시 되는 UI에 대 한 창 핸들을 가져옵니다. 창 핸들은에서 <xref:System.Windows.Interop.HwndSource> 파생 되 고을 구현 <xref:System.AddIn.Contract.INativeHandleContract>하는 내부 WPF 클래스에 의해 캡슐화 됩니다. 이 클래스의 인스턴스는에 의해 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> 반환 되며 추가 기능의 응용 프로그램 도메인에서 호스트 응용 프로그램 도메인으로 마샬링됩니다.

- 호스트 응용 프로그램 쪽에서 wpf는를에서 <xref:System.Windows.Interop.HwndSource> <xref:System.Windows.Interop.HwndHost> 파생 되 고 <xref:System.AddIn.Contract.INativeHandleContract>를 사용 하는 내부 WPF 클래스로 통해 합니다. 이 클래스의 인스턴스는에서 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> 호스트 응용 프로그램에 반환 됩니다.

<xref:System.Windows.Interop.HwndHost>WPF 사용자 인터페이스에서 창 핸들로 식별 되는 사용자 인터페이스를 표시 하기 위해 존재 합니다. 자세한 내용은 [WPF 및 Win32 상호 운용성](../advanced/wpf-and-win32-interoperation.md)을 참조하세요.

<xref:System.AddIn.Contract.INativeHandleContract>요약 하자면 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>,, 및 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> 는 WPF UI에 대 한 창 핸들을 추가 기능에서 호스트 응용 프로그램으로 전달할 수 있도록 합니다. 여기서는 <xref:System.Windows.Interop.HwndHost> 에 의해 캡슐화 되 고 호스트 응용 프로그램의 UI를 표시 합니다.

> [!NOTE]
> 호스트 응용 프로그램이 <xref:System.Windows.Interop.HwndHost>를 가져오기 때문에 호스트 응용 프로그램은에서 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> 반환 하는 개체를 추가 기능 <xref:System.Windows.Controls.UserControl>(예:)에서 구현 된 형식으로 변환할 수 없습니다.

기본적으로에 <xref:System.Windows.Interop.HwndHost> 는 호스트 응용 프로그램에서 사용할 수 있는 방법에 영향을 주는 특정 제한 사항이 있습니다. 그러나 WPF는 추가 <xref:System.Windows.Interop.HwndHost> 기능 시나리오에 대 한 몇 가지 기능으로 확장 됩니다. 이러한 이점과 한계는 아래에 설명되어 있습니다.

<a name="WPFAddInModelBenefits"></a>

## <a name="wpf-add-in-benefits"></a>WPF 추가 기능의 이점

Wpf 추가 기능 사용자 인터페이스는에서 <xref:System.Windows.Interop.HwndHost>파생 되는 내부 클래스를 사용 하 여 호스트 응용 프로그램에서 표시 되기 때문에 이러한 사용자 인터페이스는 레이아웃 같은 WPF UI 서비스와 관련 하 여의 <xref:System.Windows.Interop.HwndHost> 기능에 의해 제한 됩니다. 렌더링, 데이터 바인딩, 스타일, 템플릿 및 리소스입니다. 그러나 WPF는 다음을 포함 <xref:System.Windows.Interop.HwndHost> 하는 추가 기능을 사용 하 여 내부 하위 클래스를 보강 합니다.

- 호스트 응용 프로그램의 UI와 추가 기능의 UI 사이를 이동 합니다. "추가 기능은 UI입니다." 프로그래밍 모델을 사용 하려면 추가 기능이 완전히 신뢰할 수 있거나 부분적으로 신뢰할 수 있는지 <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> 에 관계 없이 탭 이동이 가능 하도록 추가 기능 측 어댑터가를 재정의 해야 합니다.

- 호스트 응용 프로그램 사용자 인터페이스에서 표시 되는 추가 기능 사용자 인터페이스에 대 한 내게 필요한 옵션 요구 사항

- 여러 응용 프로그램 도메인 시나리오에서 WPF 응용 프로그램을 안전 하 게 실행할 수 있도록 합니다.

- 보안 격리 (부분 신뢰 보안 샌드박스)를 사용 하 여 추가 기능을 실행할 때 추가 기능 UI 창 핸들에 대 한 잘못 된 액세스를 방지 합니다. 를 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> 호출 하면 다음과 같은 보안이 보장 됩니다.

  - "추가 기능에서 UI를 반환" 프로그래밍 모델을 사용할 경우 격리 경계를 넘어 추가 기능 UI에 대 한 창 핸들을 전달 하는 유일한 방법은를 호출 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>하는 것입니다.

  - "추가 기능은 UI" 프로그래밍 모델의 경우 추가 기능 측 어댑터에서 <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> 재정의 하 고 앞의 예제와 같이를 호출 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> 하는 것이 필요 합니다 .이는에서 추가 기능 측 어댑터의 `QueryContract` 구현을 호출 하는 것과 같습니다. 호스트 측 어댑터.

- 여러 애플리케이션 도메인 실행 보호 제공. 애플리케이션 도메인의 한계로 인해 추가 기능 애플리케이션 도메인에서 throw된 처리되지 않은 예외가 발생하면 격리 경계가 있는 경우에도 전체 애플리케이션이 중단됩니다. 그러나 WPF 및 .NET Framework 추가 기능 모델을 사용 하면이 문제를 해결 하 고 응용 프로그램의 안정성을 향상 시킬 수 있는 간단한 방법을 제공 합니다. UI를 표시 하는 wpf 추가 기능은 호스트 응용 프로그램이 <xref:System.Windows.Threading.Dispatcher> WPF 응용 프로그램 인 경우 응용 프로그램 도메인이 실행 되는 스레드에 대 한를 만듭니다. WPF 추가 <xref:System.Windows.Threading.Dispatcher.UnhandledException> <xref:System.Windows.Threading.Dispatcher>기능의 이벤트를 처리 하 여 응용 프로그램 도메인에서 발생 하는 처리 되지 않은 모든 예외를 검색할 수 있습니다. 속성에서를 <xref:System.Windows.Threading.Dispatcher> 가져올 수 있습니다. <xref:System.Windows.Threading.Dispatcher.CurrentDispatcher%2A>

<a name="WPFAddInModelLimitations"></a>

## <a name="wpf-add-in-limitations"></a>WPF 추가 기능 한계

WPF가, <xref:System.Windows.Interop.HwndSource> <xref:System.Windows.Interop.HwndHost>및 창 핸들에서 제공 하는 기본 동작에 추가 하는 이점 외에도 호스트 응용 프로그램에서 표시 되는 추가 기능 사용자 인터페이스에 대 한 제한 사항이 있습니다.

- 호스트 응용 프로그램에서 표시 되는 추가 기능 사용자 인터페이스는 호스트 응용 프로그램의 클리핑 동작을 고려 하지 않습니다.

- 상호 운용성 시나리오의 *에어스페이스* 개념도 추가 기능에 적용됩니다([기술 영역 개요](../advanced/technology-regions-overview.md) 참조).

- 리소스 상속, 데이터 바인딩 및 명령과 같은 호스트 응용 프로그램의 UI 서비스는 추가 기능 사용자 인터페이스에서 자동으로 사용할 수 없습니다. 추가 기능에 이러한 서비스를 제공하려면 파이프라인을 업데이트해야 합니다.

- 추가 기능 UI는 회전, 크기 조정, 기울이기 또는 변환의 영향을 받을 수 없습니다 ( [변환 개요](../graphics-multimedia/transforms-overview.md)참조).

- <xref:System.Drawing> 네임 스페이스에서 그리기 작업을 통해 렌더링 되는 추가 기능 사용자 인터페이스 내의 콘텐츠는 알파 혼합을 포함할 수 있습니다. 그러나 추가 기능 UI와이 UI를 포함 하는 호스트 응용 프로그램 UI는 모두 100% 불투명 해야 합니다. 즉, `Opacity` 둘 다의 속성을 1로 설정 해야 합니다.

- 추가 기능 UI를 포함 하는 호스트 응용 프로그램의 창 `true` 속성이로설정되어있으면추가기능이표시되지않습니다.<xref:System.Windows.Window.AllowsTransparency%2A> 이는 추가 기능 UI가 100% 불투명 (즉, `Opacity` 속성 값이 1 임) 인 경우에도 마찬가지입니다.

- 추가 기능 UI는 동일한 최상위 창의 다른 WPF 요소 위에 표시 되어야 합니다.

- 을 <xref:System.Windows.Media.VisualBrush>사용 하 여 추가 기능의 UI 부분을 렌더링할 수 없습니다. 대신, 추가 기능이 생성 된 UI의 스냅숏을 생성 하 여 계약에서 정의한 메서드를 사용 하 여 호스트 응용 프로그램에 전달할 수 있는 비트맵을 만들 수 있습니다.

- 추가 기능 UI의에서 미디어 파일 <xref:System.Windows.Controls.MediaElement> 을 재생할 수 없습니다.

- 추가 기능 ui에 대해 생성 된 마우스 이벤트는 호스트 응용 프로그램 `IsMouseOver` 에서 받아서 발생 하지 않으며 호스트 응용 프로그램 ui의 속성 `false`값은입니다.

- 추가 기능 UI `GotFocus` 의 컨트롤 간에 포커스가 이동 하면 호스트 응용 프로그램에서 및 `LostFocus` 이벤트를 받거나 발생 하지 않습니다.

- 추가 기능 UI를 포함 하는 호스트 응용 프로그램의 부분은 인쇄 시 흰색으로 표시 됩니다.

- 호스트 응용 프로그램에서 <xref:System.Windows.Threading.Dispatcher>실행을 계속 하는 경우 소유자 추가 기능이 언로드되기 전에 추가 기능 UI에서 만든 모든 디스패처 (참조)를 수동으로 종료 해야 합니다. 계약은 추가 기능이 언로드되기 전에 호스트 응용 프로그램이 추가 기능에 신호를 보낼 수 있도록 하는 메서드를 구현할 수 있으므로 추가 기능 UI에서 해당 디스패처를 종료할 수 있습니다.

- 추가 기능 UI가 <xref:System.Windows.Controls.InkCanvas> 이거나를 <xref:System.Windows.Controls.InkCanvas>포함 하는 경우에는 추가 기능을 언로드할 수 없습니다.

<a name="PerformanceOptimization"></a>

## <a name="performance-optimization"></a>성능 최적화

기본적으로 여러 응용 프로그램 도메인을 사용 하는 경우 각 응용 프로그램에 필요한 다양 한 .NET Framework 어셈블리가 모두 해당 응용 프로그램의 도메인에 로드 됩니다. 결과적으로 새 애플리케이션 도메인을 만들고 이 도메인의 애플리케이션을 시작하는 데 필요한 시간이 성능에 영향을 미칠 수 있습니다. 그러나 .NET Framework는 응용 프로그램이 이미 로드 된 경우 응용 프로그램 도메인 간에 어셈블리를 공유 하도록 응용 프로그램에 지시 하 여 시작 시간을 줄일 수 있는 방법을 제공 합니다. 진입점 메서드 (`Main`)에 적용 <xref:System.LoaderOptimizationAttribute> 해야 하는 특성을 사용 하 여이 작업을 수행 합니다. 이 경우, 애플리케이션 정의를 구현하는 코드만 사용해야 합니다([애플리케이션 관리 개요](application-management-overview.md) 참조).

## <a name="see-also"></a>참고 항목

- <xref:System.LoaderOptimizationAttribute>
- [추가 기능 및 확장성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))
- [애플리케이션 도메인](../../app-domains/application-domains.md)
- [.NET Framework 원격 기능 개요](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/kwdt6w2k(v=vs.100))
- [개체를 원격으로 만들기](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/wcf3swha(v=vs.100))
- [방법 항목](how-to-topics.md)
