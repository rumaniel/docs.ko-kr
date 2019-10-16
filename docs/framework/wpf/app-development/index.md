---
title: 애플리케이션 개발
ms.date: 01/26/2018
helpviewer_keywords:
- WPF [WPF], about application development
- application development [WPF], about
ms.assetid: 2996ce5e-81e9-49ae-881b-952db3dd1b7e
ms.openlocfilehash: 519ff6f40ea303b64864683db222b55c6e5a23aa
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964810"
---
# <a name="application-development"></a>애플리케이션 개발
<a name="introduction"></a>WPF (Windows Presentation Foundation)는 다음과 같은 종류의 응용 프로그램을 개발 하는 데 사용할 수 있는 프레젠테이션 프레임 워크입니다.  
  
- 독립 실행형 응용 프로그램 (클라이언트 컴퓨터에 설치 되 고 실행 되는 실행 가능 어셈블리로 빌드된 기존 스타일의 Windows 응용 프로그램).  
  
- [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)]실행 가능 어셈블리로 빌드되고 Microsoft Internet Explorer 또는 Mozilla Firefox와 같은 웹 브라우저에서 호스팅되는 탐색 페이지로 구성 된 응용 프로그램입니다.  
  
- 사용자 지정 컨트롤 라이브러리(재사용 가능한 컨트롤을 포함하는 실행 불가능한 어셈블리)  
  
- 클래스 라이브러리(재사용 가능한 클래스를 포함하는 실행 불가능한 어셈블리)  
  
> [!NOTE]
> Windows 서비스에서 WPF 유형을 사용해서는 안 됩니다. Windows 서비스에서 이러한 기능을 사용하려고 하면 예상대로 작동하지 않을 수 있습니다.  
  
 이 애플리케이션 집합을 빌드하려면 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에서 서비스 호스트를 구현합니다. 이 항목에서 이러한 서비스의 개요를 제공하며 자세한 정보를 찾을 수 있습니다.  

<a name="Application_Management"></a>   
## <a name="application-management"></a>애플리케이션 관리  
 실행 가능한 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 애플리케이션에는 일반적으로 다음을 포함하는 핵심 기능 집합이 필요합니다.  
  
- 일반적인 애플리케이션 인프라 만들기 및 관리(시스템 및 입력 메시지를 수신하는 Windows 메시지 루프 및 진입점 메서드 만들기 포함)  
  
- 애플리케이션의 수명 추적 및 상호 작용  
  
- 명령줄 매개 변수 검색 및 처리  
  
- 애플리케이션 범위 속성 및 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 리소스 공유  
  
- 처리되지 않은 예외 검색 및 처리  
  
- 종료 코드 반환  
  
- 독립 실행형 애플리케이션에서 창 관리  
  
- 탐색 창 및 프레임이 있는 독립 실행형 애플리케이션 및 [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)]에서 탐색 추적  
  
 이러한 기능은 *애플리케이션 정의*를 사용하여 애플리케이션에 추가되는 <xref:System.Windows.Application> 클래스에 의해 구현됩니다.  
  
 자세한 내용은 [애플리케이션 관리 개요](application-management-overview.md)를 참조하세요.  
  
<a name="WPF_Application_Resource__Content__and_Data_Files"></a>   
## <a name="wpf-application-resource-content-and-data-files"></a>WPF 애플리케이션 리소스, 콘텐츠 및 데이터 파일  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]는 포함 리소스에 대 한 Microsoft .NET 프레임 워크의 핵심 지원을 확장 하 여 세 가지 비실행 데이터 파일 (리소스, 콘텐츠 및 데이터)에 대 한 지원을 제공 합니다. 자세한 내용은 [WPF 애플리케이션 리소스, 콘텐츠 및 데이터 파일](wpf-application-resource-content-and-data-files.md)을 참조하세요.  
  
 WPF 실행 불가능 데이터 파일에 대한 지원의 핵심 구성 요소는 고유한 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]를 사용하여 이를 식별하고 로드하는 기능입니다. 자세한 내용은 [WPF의 Pack URI](pack-uris-in-wpf.md)를 참조하세요.  
  
<a name="Windows_and_Dialog_Boxes"></a>   
## <a name="windows-and-dialog-boxes"></a>창 및 대화 상자  
 사용자는 창을 통해 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 독립 실행형 애플리케이션과 상호 작용합니다. 창의 목적은 애플리케이션 콘텐츠를 호스트하고 일반적으로 사용자가 콘텐츠와 상호 작용할 수 있도록 애플리케이션 기능을 노출하는 것입니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에서 창은 다음을 지원하는 <xref:System.Windows.Window> 클래스에 의해 캡슐화됩니다.  
  
- 창 만들기 및 표시  
  
- 소유자/피소유자 창 관계 설정  
  
- 창 모양 구성(예: 크기, 위치, 아이콘, 제목 표시줄 텍스트, 테두리)  
  
- 창의 수명 추적 및 상호 작용  
  
 자세한 내용은 [WPF 창 개요](wpf-windows-overview.md)를 참조하세요.  
  
 <xref:System.Windows.Window>는 대화 상자로 알려진 특별한 유형의 창을 만드는 기능을 지원합니다. 모달 및 모덜리스 유형의 대화 상자를 모두 만들 수 있습니다.  
  
 편의를 위해 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 응용 프로그램에 대 한 재사용 및 일관적인 사용자 환경의 이점은, 및 <xref:System.Windows.Controls.PrintDialog>의 세 가지 일반적인 Windows 대화 <xref:Microsoft.Win32.OpenFileDialog>상자 <xref:Microsoft.Win32.SaveFileDialog>를 노출 합니다.  
  
 메시지 상자는 중요한 텍스트 정보를 보여 주고 간단한 예/아니요/확인/취소 질문을 묻는 특별한 유형의 대화 상자입니다. <xref:System.Windows.MessageBox> 클래스를 사용하여 메시지 상자를 만들고 표시합니다.  
  
 자세한 내용은 [대화 상자 개요](dialog-boxes-overview.md)를 참조하세요.  
  
<a name="Navigation"></a>   
## <a name="navigation"></a>탐색  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에서는 페이지(<xref:System.Windows.Controls.Page>) 및 하이퍼링크(<xref:System.Windows.Documents.Hyperlink>)를 통한 웹 스타일 탐색을 지원합니다. 다음을 포함한 다양한 방법으로 탐색을 구현할 수 있습니다.  
  
- 웹 브라우저에 호스트되는 독립 실행형 페이지  
  
- 웹 브라우저에 호스트되는 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]로 컴파일된 페이지  
  
- 독립 실행형 애플리케이션으로 컴파일되고 탐색 창(<xref:System.Windows.Navigation.NavigationWindow>)에서 호스트하는 페이지  
  
- 독립 실행형 페이지나 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 또는 독립 실행형 애플리케이션으로 컴파일된 페이지에서 호스트할 수 있는 프레임(<xref:System.Windows.Controls.Frame>)에서 호스트되는 페이지  
  
 탐색을 쉽게 하려면 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에서 다음을 구현합니다.  
  
- 응용 프로그램 내 탐색을 지원하기 위해 <xref:System.Windows.Controls.Frame>, <xref:System.Windows.Navigation.NavigationWindow>, [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)]에서 사용되는 탐색 요청을 처리하기 위한 공유 탐색 엔진 <xref:System.Windows.Navigation.NavigationService>  
  
- 탐색을 시작하는 탐색 메서드  
  
- 탐색 수명을 추적하고 상호 작용하는 탐색 이벤트  
  
- 저널을 사용하여 뒤로/앞으로 탐색 저장(검사하고 조작할 수도 있음)  
  
 자세한 내용은 [탐색 개요](navigation-overview.md)를 참조하세요.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]는 구조적 탐색이라고 알려진 특별한 유형의 탐색도 지원합니다. 구조적 탐색을 사용하여 호출 함수와 일치하는 구조적이고 예측 가능한 방식으로 데이터를 반환하는 하나 이상의 페이지를 호출할 수 있습니다. 이 기능은 <xref:System.Windows.Navigation.PageFunction%601> 클래스에 따라 달라지며 [구조적 탐색 개요](structured-navigation-overview.md)에 자세히 설명되어 있습니다. <xref:System.Windows.Navigation.PageFunction%601>은 복잡한 탐색 토폴로지 생성을 간소화하는 역할도 합니다. 이러한 탐색 토폴로지에 대한 설명은 [탐색 토폴로지 개요](navigation-topologies-overview.md)에 나와 있습니다.  
  
<a name="Hosting"></a>   
## <a name="hosting"></a>호스팅  
 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)]Microsoft Internet Explorer 또는 Firefox에서 호스팅될 수 있습니다. 각 호스팅 모델에는 [호스팅](hosting-wpf-applications.md)에서 다루는 고유한 고려 사항 및 제약 조건 집합이 있습니다.  
  
<a name="Build_and_Deploy"></a>   
## <a name="build-and-deploy"></a>빌드 및 배포  
 명령줄 컴파일러를 사용하여 명령 프롬프트에서 간단한 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 애플리케이션을 빌드할 수 있지만 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]와 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)]가 통합되어 개발 및 빌드 프로세스를 단순화한 추가 지원을 제공합니다. 자세한 내용은 [WPF 애플리케이션 빌드](building-a-wpf-application-wpf.md)를 참조하세요.  
  
 빌드하는 애플리케이션의 유형에 따라 선택할 수 있는 하나 이상의 배포 옵션이 있습니다. 자세한 내용은 [WPF 애플리케이션 배포](deploying-a-wpf-application-wpf.md)를 참조하세요.  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[애플리케이션 관리 개요](application-management-overview.md)|애플리케이션 수명, 창, 애플리케이션 리소스 및 탐색 관리를 비롯하여 <xref:System.Windows.Application> 클래스에 대해 개략적으로 설명합니다.|  
|[WPF의 창](windows-in-wpf-applications.md)|<xref:System.Windows.Window> 클래스 및 대화 상자의 사용 방법을 비롯하여 응용 프로그램의 창 관리에 대해 세부적으로 설명합니다.|  
|[탐색 개요](navigation-overview.md)|애플리케이션 페이지 간의 탐색 관리에 대해 개략적으로 설명합니다.|  
|[호스팅](hosting-wpf-applications.md)|[!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)]에 대한 개요를 설명합니다.|  
|[빌드 및 배포](building-and-deploying-wpf-applications.md)|WPF 애플리케이션을 빌드하고 배포하는 방법에 대해 설명합니다.|  
|[Visual Studio에서의 WPF 소개](../getting-started/introduction-to-wpf-in-vs.md)|WPF의 주요 기능에 대해 설명합니다.|  
|[연습: 내 첫 WPF 데스크톱 애플리케이션](../getting-started/walkthrough-my-first-wpf-desktop-application.md)|페이지 탐색, 레이아웃, 컨트롤, 이미지, 스타일 및 바인딩을 사용하여 WPF 애플리케이션을 만드는 방법을 보여 주는 연습입니다.|
