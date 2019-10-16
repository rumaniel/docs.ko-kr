---
title: WPF 부분 신뢰 보안
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- partial trust security [WPF]
- detecting permissions [WPF]
- security settings for Internet Explorer [WPF]
- partial trust applications [WPF], debugging
- permissions [WPF], managing
- debugging partial trust applications [WPF]
- permissions [WPF], detecting
- feature security requirements [WPF]
- managing permissions [WPF]
ms.assetid: ef2c0810-1dbf-4511-babd-1fab95b523b5
ms.openlocfilehash: c3ec6ca6feba975517a9f982bb58e4b061516a61
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962810"
---
# <a name="wpf-partial-trust-security"></a>WPF 부분 신뢰 보안
<a name="introduction"></a> 일반적으로 악의적인 손상을 방지하기 위해 중요한 시스템 리소스에 직접 액세스하지 않도록 인터넷 응용 프로그램을 제한해야 합니다. 기본적으로 HTML 및 클라이언트 쪽 스크립팅 언어는 중요 한 시스템 리소스에 액세스할 수 없습니다. WPF (Windows Presentation Foundation) 브라우저에서 호스팅되는 응용 프로그램은 브라우저에서 실행할 수 있기 때문에 유사한 제한 사항을 준수 해야 합니다. 이러한 제한을 적용 하기 위해 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 는 CAS (코드 액세스 보안) 및 ClickOnce를 모두 사용 합니다 ( [WPF 보안 전략-플랫폼 보안](wpf-security-strategy-platform-security.md)참조). 기본적으로 브라우저에서 호스트 된 응용 프로그램은 인터넷, 로컬 인트라넷 또는 로컬 컴퓨터에서 시작 되었는지 여부에 관계 없이 인터넷 영역 CA 사용 권한 집합을 요청 합니다. 전체 권한 집합보다 적은 권한으로 실행하는 애플리케이션은 부분 신뢰로 실행된다고 할 수 있습니다.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]는 가능한 많은 기능을 부분 신뢰에서 안전 하 게 사용할 수 있도록 하는 다양 한 지원을 제공 하며, CA와 함께 부분 신뢰 프로그래밍에 대 한 추가 지원을 제공 합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
- [WPF 기능 부분 신뢰 지원](#WPF_Feature_Partial_Trust_Support)  
  
- [부분 신뢰 프로그래밍](#Partial_Trust_Programming)  
  
- [권한 관리](#Managing_Permissions)  
  
<a name="WPF_Feature_Partial_Trust_Support"></a>   
## <a name="wpf-feature-partial-trust-support"></a>WPF 기능 부분 신뢰 지원  
 다음 표에서는 인터넷 영역 권한 집합의 한도 내에서 사용 하기에 안전 하 게 사용 되는 Windows Presentation Foundation (WPF)의 상위 수준 기능을 보여 줍니다.  
  
 표 1: 부분 신뢰에서 안전 하 게 보호 되는 WPF 기능  
  
|기능 영역|기능|  
|------------------|-------------|  
|일반|브라우저 창<br /><br /> 원 사이트 액세스<br /><br /> IsolatedStorage(512KB 제한)<br /><br /> UIAutomation 공급자<br /><br /> 명령<br /><br /> IME(입력기)<br /><br /> 태블릿 스타일러스 및 잉크<br /><br /> 마우스 캡처 및 이동 이벤트를 사용하여 시뮬레이션된 끌어서 놓기<br /><br /> OpenFileDialog<br /><br /> XamlReader.Load를 통한 XAML Deserialization|  
|웹 통합|브라우저 다운로드 대화 상자<br /><br /> 사용자가 시작한 최상위 탐색<br /><br /> mailto:links<br /><br /> URI(Uniform Resource Identifier) 매개 변수<br /><br /> HTTPWebRequest<br /><br /> IFRAME에 호스팅되는 WPF 콘텐츠<br /><br /> 프레임을 사용하여 동일한 사이트 HTML 페이지 호스팅<br /><br /> WebBrowser를 사용하여 동일한 사이트 HTML 페이지 호스팅<br /><br /> 웹 서비스(ASMX)<br /><br /> 웹 서비스(Windows Communication Foundation 사용)<br /><br /> 스크립팅<br /><br /> 문서 개체 모델|  
|시각 효과|2D 및 3D<br /><br /> 애니메이션<br /><br /> 미디어(원본 사이트 및 도메인 간)<br /><br /> 이미지/오디오/비디오|  
|읽기|FlowDocuments<br /><br /> XPS 문서<br /><br /> 포함된 시스템 글꼴<br /><br /> CFF & 트루타입 글꼴|  
|편집|맞춤법 검사<br /><br /> RichTextBox<br /><br /> 일반 텍스트 및 잉크 클립보드 지원<br /><br /> 사용자가 시작한 붙여넣기<br /><br /> 선택한 콘텐츠 복사|  
|컨트롤|일반 컨트롤|  
  
 이 표에서는 높은 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 수준의 기능을 설명 합니다. 자세한 내용은 Windows SDK에서 각 멤버 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]에 필요한 사용 권한을 설명 합니다. 또한 다음 기능에는 특별한 고려 사항을 포함하는 부분 신뢰 실행에 대한 자세한 정보가 있습니다.  
  
- [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)][XAML 개요 (WPF)](./advanced/xaml-overview-wpf.md)를 참조 하세요.  
  
- 돌출 (참조 <xref:System.Windows.Controls.Primitives.Popup?displayProperty=nameWithType>).  
  
- 끌어서 놓기 ( [끌어서 놓기 개요](./advanced/drag-and-drop-overview.md)참조).  
  
- 클립보드 (참조 <xref:System.Windows.Clipboard?displayProperty=nameWithType>).  
  
- 이미징 (참조 <xref:System.Windows.Controls.Image?displayProperty=nameWithType>).  
  
- Serialization (참조 <xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=nameWithType> <xref:System.Windows.Markup.XamlWriter.Save%2A?displayProperty=nameWithType>).  
  
- 파일 열기 대화 상자 (참조 <xref:Microsoft.Win32.OpenFileDialog?displayProperty=nameWithType>).  
  
 다음 표에서는 인터넷 영역 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 권한 집합의 한도 내에서 실행 하기에 안전 하지 않은 기능을 간략하게 설명 합니다.  
  
 표 2: 부분 신뢰로 안전 하지 않은 WPF 기능  
  
|기능 영역|기능|  
|------------------|-------------|  
|일반|창(애플리케이션 정의 창 및 대화 상자)<br /><br /> SaveFileDialog<br /><br /> 파일 시스템<br /><br /> 레지스트리 액세스<br /><br /> 끌어서 놓기<br /><br /> XamlWriter.Save를 통한 XAML 직렬화<br /><br /> UIAutomation 클라이언트<br /><br /> 소스 창 액세스(HwndHost)<br /><br /> 완전한 음성 지원<br /><br /> Windows Forms 상호 운용성|  
|시각적 개체|비트맵 효과<br /><br /> 이미지 인코딩|  
|편집|RTF(서식 있는 텍스트) 클립보드<br /><br /> 전체 XAML 지원|  
  
<a name="Partial_Trust_Programming"></a>   
## <a name="partial-trust-programming"></a>부분 신뢰 프로그래밍  
 응용 [!INCLUDE[TLA2#tla_xbap](../../../includes/tla2sharptla-xbap-md.md)] 프로그램의 경우 기본 권한 집합을 초과 하는 코드는 보안 영역에 따라 다르게 동작 합니다. 일부 경우에는 사용자가 설치를 시도할 때 경고를 받게 됩니다. 사용자는 설치를 계속하거나 취소하도록 선택할 수 있습니다. 다음 표에서 각 보안 영역의 동작 및 애플리케이션이 완전 신뢰를 받기 위해 수행해야 하는 작업을 설명합니다.  
  
|보안 영역|동작|완전 신뢰 얻기|  
|-------------------|--------------|------------------------|  
|로컬 컴퓨터|자동 완전 신뢰|아무 동작도 필요하지 않습니다.|  
|인트라넷 및 신뢰할 수 있는 사이트|완전 신뢰 확인|사용자가 프롬프트에서 소스를 볼 수 있도록 인증서로 XBAP에 로그인합니다.|  
|인터넷|"신뢰할 수 없음"과 함께 실패|인증서로 XBAP에 로그인합니다.|  
  
> [!NOTE]
> 위의 표에 설명된 동작은 ClickOnce 신뢰 배포 모델을 따르지 않는 완전 신뢰 XBAP에 대한 것입니다.  
  
 일반적으로 허용되는 권한을 초과하는 코드는, 독립 실행형 애플리케이션과 브라우저에서 호스트된 애플리케이션 간에 공유되는 일반적인 코드일 수 있습니다. CAS 및 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 에서는이 시나리오를 관리 하기 위한 몇 가지 방법을 제공 합니다.  
  
<a name="Detecting_Permissions_using_CAS"></a>   
### <a name="detecting-permissions-using-cas"></a>CAS를 사용하여 권한 검색  
 경우에 따라 독립 실행형 응용 프로그램 및 [!INCLUDE[TLA2#tla_xbap#plural](../../../includes/tla2sharptla-xbapsharpplural-md.md)]모두에서 라이브러리 어셈블리의 공유 코드를 사용할 수 있습니다. 이러한 경우 코드는 애플리케이션에서 얻은 권한 집합이 허용하는 것보다 많은 권한이 필요할 수 있는 기능을 실행할 수 있습니다. 응용 프로그램은 Microsoft .NET Framework 보안을 사용 하 여 특정 권한이 있는지 여부를 검색할 수 있습니다. 특히, 원하는 권한의 인스턴스에서 메서드를 <xref:System.Security.CodeAccessPermission.Demand%2A> 호출 하 여 특정 권한이 있는지 여부를 테스트할 수 있습니다. 다음 예제는 로컬 디스크에 파일을 저장하는 기능이 있는지 여부에 대해 쿼리하는 코드입니다.  
  
 [!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsCODE1](~/samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandling.cs#detectpermscode1)]
 [!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsCODE1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandling.vb#detectpermscode1)]  
[!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsCODE2](~/samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandling.cs#detectpermscode2)]
[!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsCODE2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandling.vb#detectpermscode2)]  
  
 응용 프로그램에 필요한 사용 권한이 없는 경우를 <xref:System.Security.CodeAccessPermission.Demand%2A> 호출 하면 보안 예외가 throw 됩니다. 그렇지 않은 경우 사용 권한이 부여됩니다. `IsPermissionGranted`이 동작을 캡슐화 하 `true` 고 `false` 또는를 적절 하 게 반환 합니다.  
  
<a name="Graceful_Degradation_of_Functionality"></a>   
### <a name="graceful-degradation-of-functionality"></a>점진적인 기능 저하  
 코드에 필요한 작업을 수행할 권한이 있는지 확인하는 것은 다른 영역에서 실행될 수 있는 코드와 관련되어 있습니다. 영역 검색이 하나의 방법이지만, 가능한 경우 사용자를 위한 대안을 제공하는 것이 좋습니다. 예를 들어 부분 신뢰 애플리케이션은 격리된 저장소에만 파일을 만들 수 있지만, 일반적으로 완전 신뢰 애플리케이션은 사용자가 원하는 모든 곳에 파일을 만들 수가 있습니다. 파일을 만드는 코드가 완전 신뢰(독립 실행형) 애플리케이션과 부분 신뢰(브라우저에서 호스트된) 애플리케이션에서 공유되는 어셈블리에 존재하고 두 애플리케이션에서 사용자가 파일을 만들도록 하는 경우, 공유 코드는 해당 위치에 파일을 만들기 전에 부분 또는 완전 신뢰에서 실행 중인지 감지해야 합니다. 다음 코드는 두 사항을 모두 보여줍니다.  
  
 [!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE1](~/samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandlingGraceful.cs#detectpermsgracefulcode1)]
 [!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandlingGraceful.vb#detectpermsgracefulcode1)]  
[!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE2](~/samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandlingGraceful.cs#detectpermsgracefulcode2)]
[!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandlingGraceful.vb#detectpermsgracefulcode2)]  
  
 대부분의 경우, 부분 신뢰 대체 항목을 찾을 수 있어야 됩니다.  
  
 인트라넷과 같은 제어 되는 환경에서 사용자 지정 관리 프레임 워크는 클라이언트 기반 전체에 GAC (전역 어셈블리 캐시)에 설치할 수 있습니다. 이러한 라이브러리는 완전 신뢰가 필요한 코드를 실행 하 고를 사용 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 하 여 부분 신뢰를 허용 하는 응용 프로그램에서 참조 될 수 있습니다. 자세한 내용은 [보안](security-wpf.md) 및 [WPF 보안 전략-플랫폼 보안](wpf-security-strategy-platform-security.md)을 참조 하세요.  
  
<a name="Browser_Host_Detection"></a>   
### <a name="browser-host-detection"></a>브라우저 호스트 검색  
 CA를 사용 하 여 사용 권한을 확인 하는 것은 권한 별로 확인 해야 하는 경우에 적합 한 기술입니다. 이 기술은 일반적인 프로세스의 일부인 예외 감지에 영향을 받으며, 일반적으로 권장되지 않고 성능 문제를 일으킬 수 있습니다. 대신이 인터넷 영역 [!INCLUDE[TLA#tla_xbap](../../../includes/tlasharptla-xbap-md.md)] 샌드박스 내 에서만 실행 되는 경우에 대해 [!INCLUDE[TLA#tla_xbap#plural](../../../includes/tlasharptla-xbapsharpplural-md.md)]true를 반환 <xref:System.Windows.Interop.BrowserInteropHelper.IsBrowserHosted%2A?displayProperty=nameWithType> 하는 속성을 사용할 수 있습니다.  
  
> [!NOTE]
> <xref:System.Windows.Interop.BrowserInteropHelper.IsBrowserHosted%2A>응용 프로그램을 실행 하는 데 사용 되는 권한 집합이 아니라 브라우저에서 응용 프로그램을 실행 하 고 있는지만 구분 합니다.  
  
<a name="Managing_Permissions"></a>   
## <a name="managing-permissions"></a>권한 관리  
 기본적으로 부분 [!INCLUDE[TLA2#tla_xbap#plural](../../../includes/tla2sharptla-xbapsharpplural-md.md)] 신뢰 (기본 인터넷 영역 권한 집합)를 사용 하 여 실행 합니다. 그러나 애플리케이션의 요구에 따라 기본값에서 권한 집합을 변경할 수 있습니다. 예를 들어 [!INCLUDE[TLA2#tla_xbap#plural](../../../includes/tla2sharptla-xbapsharpplural-md.md)] 가 로컬 인트라넷에서 시작 되는 경우 다음 표에 표시 된 권한 집합을 활용할 수 있습니다.  
  
 표 3: LocalIntranet 및 인터넷 권한  
  
|사용 권한|특성|LocalIntranet|인터넷|  
|----------------|---------------|-------------------|--------------|  
|DNS|DNS 서버 액세스|예|아니요|  
|환경 변수|읽기|예|아니요|  
|파일 대화 상자|열기|예|예|  
|파일 대화 상자|제한 없음|예|아니요|  
|격리된 스토리지|사용자가 어셈블리 격리|예|아니요|  
|격리된 스토리지|알 수 없는 격리|예|예|  
|격리된 스토리지|무제한 사용자 할당량|예|아니요|  
|미디어|안전한 오디오, 비디오 및 이미지|예|예|  
|인쇄|기본 인쇄|예|아니요|  
|인쇄|안전 인쇄|예|예|  
|반사|내보내기|예|아니요|  
|보안|관리되는 코드 실행|예|예|  
|보안|부여된 권한 어셜션|예|아니요|  
|사용자 인터페이스|제한 없음|예|아니요|  
|사용자 인터페이스|안전한 최상위 창|예|예|  
|사용자 인터페이스|소유 클립보드|예|예|  
|웹 브라우저|HTML 안전 프레임 탐색|예|예|  
  
> [!NOTE]
> 잘라내기 및 붙여넣기는 사용자가 시작한 경우 부분 신뢰에서만 허용됩니다.  
  
 권한을 높이는 경우 프로젝트 설정 및 ClickOnce 애플리케이션 매니페스트를 변경해야 합니다. 자세한 내용은 [WPF XAML 브라우저 애플리케이션 개요](./app-development/wpf-xaml-browser-applications-overview.md)를 참조하세요. 다음 문서도 유용할 수 있습니다.  
  
- [Mage.exe(매니페스트 생성 및 편집 도구)](../tools/mage-exe-manifest-generation-and-editing-tool.md).  
  
- [MageUI.exe(매니페스트 생성 및 편집 도구, 그래픽 클라이언트)](../tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client.md).  
  
- [ClickOnce 응용 프로그램 보안](/visualstudio/deployment/securing-clickonce-applications).  
  
 에 [!INCLUDE[TLA2#tla_xbap](../../../includes/tla2sharptla-xbap-md.md)] 완전 신뢰가 필요한 경우 동일한 도구를 사용 하 여 요청 된 사용 권한을 늘릴 수 있습니다. 는 [!INCLUDE[TLA2#tla_xbap](../../../includes/tla2sharptla-xbap-md.md)] 로컬 컴퓨터, 인트라넷 또는 브라우저의 신뢰할 수 있는 사이트 또는 허용 된 사이트에 나열 된 URL에서 설치 및 시작 하는 경우에만 완전 신뢰를 받습니다. 인트라넷 또는 신뢰할 수 있는 사이트에서 애플리케이션이 설치되면, 사용자는 상승된 권한을 알리는 표준 ClickOnce 프롬프트를 받습니다. 사용자는 설치를 계속하거나 취소하도록 선택할 수 있습니다.  
  
 또는 모든 보안 영역에서 완전 신뢰 배포를 위한 ClickOnce 신뢰 배포 모델을 사용할 수 있습니다. 자세한 내용은 [신뢰할 수 있는 응용 프로그램 배포 개요](/visualstudio/deployment/trusted-application-deployment-overview) 및 [보안](security-wpf.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [보안](security-wpf.md)
- [WPF 보안 전략 - 플랫폼 보안](wpf-security-strategy-platform-security.md)
- [WPF 보안 전략 - 보안 엔지니어링](wpf-security-strategy-security-engineering.md)
