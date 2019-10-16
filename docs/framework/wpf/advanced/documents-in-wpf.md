---
title: WPF의 문서
ms.date: 03/30/2017
helpviewer_keywords:
- documents [WPF], packaging
- documents [WPF], text layout
- documents [WPF], XPS
- 'XPS documents [WPF], , '
- documents [WPF], controls
- documents [WPF], types of
- documents [WPF], browser-viewable
ms.assetid: 6e8db7bc-050a-4070-aa72-bb8c46e87ff8
ms.openlocfilehash: e21abca4dd02a849d0240888f831125ab96aa8f1
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393283"
---
# <a name="documents-in-wpf"></a>WPF의 문서
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]은 이전 세대의 Windows에서 보다 쉽게 액세스 하 고 읽을 수 있도록 설계 된 고화질 콘텐츠를 만들 수 있는 다양 한 문서 기능을 제공 합니다. 고급 기능 및 품질 외에도 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 문서 표시, 패키징 및 보안을 위한 통합 서비스도 제공합니다. 이 항목에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 문서 형식 및 문서 패키징을 소개합니다.  

<a name="types_of_documents"></a>   
## <a name="types-of-documents"></a>문서 종류  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 용도에 따라 문서를 두 개의 광범위한 범주로 구분합니다. 이러한 문서 범주를 “고정 문서”와 “유동 문서”라고 합니다.  
  
 고정 문서는 사용된 디스플레이 또는 프린터 하드웨어와 무관하게 정확한 [!INCLUDE[TLA#tla_wys](../../../../includes/tlasharptla-wys-md.md)] 프레젠테이션이 필요한 애플리케이션용으로 설계되었습니다. 일반적으로 고정 문서는 데스크톱 출판, 워드 프로세싱 및 양식 레이아웃에 사용되며, 이 경우 원래 페이지 디자인을 고수하는 것이 중요합니다. 고정 문서에서는 사용 중인 디스플레이나 인쇄 디바이스와 무관하게 콘텐츠 요소의 정확한 위치를 레이아웃의 일부로 유지합니다. 예를 들어, 96dpi 디스플레이에 보이는 고정 문서 페이지는 600dpi 레이저 프린터로 출력할 때와 4800dpi 사진 식자기로 출력할 때 모두 똑같이 표시됩니다. 어느 경우에든 페이지 레이아웃은 동일하며, 문서 품질은 각 디바이스의 기능에 따라 최대화됩니다.  
  
 이에 비해 유동 문서는 보기와 가독성을 최적화하도록 설계되어 있으며, 문서 이용 시 용이한 가독성이 주된 요인인 시나리오에서 최적으로 활용할 수 있습니다. 유동 문서는 미리 정의된 하나의 레이아웃으로 설정되는 것이 아니라, 창 크기, 디바이스 해상도 및 선택적 사용자 기본 설정 등의 런타임 변수에 따라 동적으로 콘텐츠를 조정하고 리플로우합니다. 웹 페이지는 페이지 콘텐츠를 현재 창에 맞게 동적으로 형식화하는 유동 문서의 간단한 예입니다. 유동 문서는 런타임 환경을 기반으로 사용자의 보기 및 읽기 환경을 최적화합니다. 예를 들어, 동일한 유동 문서가 고해상도 19인치 디스플레이나 소형 2x3인치 PDA 화면에서 최적의 가독성을 제공하기 위해 동적으로 서식을 다시 지정합니다. 또한 유동 문서에는 검색, 가독성을 최적화하는 보기 모드 및 글꼴의 모양과 크기를 변경하는 기능 등의 여러 기본 제공 기능이 포함되어 있습니다.  플로우 문서에 대한 그림, 예제 및 자세한 정보는 [유동 문서 개요](flow-document-overview.md)를 참조하세요.  
  
<a name="document_viewer"></a>   
## <a name="document-controls-and-text-layout"></a>문서 컨트롤 및 텍스트 레이아웃  
 .NET Framework는 응용 프로그램 내에서 고정 된 문서, 유동 문서 및 일반 텍스트를 사용 하 여 간소화 하는 미리 빌드된 컨트롤 집합을 제공 합니다.  @No__t-0 컨트롤을 사용 하 여 고정 문서 콘텐츠의 표시를 지원 합니다.  유동 문서 콘텐츠 표시는 다른 사용자 시나리오에 매핑되는 <xref:System.Windows.Controls.FlowDocumentReader>, <xref:System.Windows.Controls.FlowDocumentPageViewer>, <xref:System.Windows.Controls.FlowDocumentScrollViewer>의 세 가지 컨트롤로 지원 됩니다 (아래 섹션 참조).  기타 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤에서는 일반 텍스트 사용을 지원하는 간소화된 레이아웃을 제공합니다(아래 [사용자 인터페이스의 텍스트](#text_in_the_user_interface) 참조).  
  
### <a name="fixed-document-control---documentviewer"></a>고정 문서 컨트롤 - DocumentViewer  
 @No__t-0 컨트롤은 @no__t 1 콘텐츠를 표시 하도록 디자인 되었습니다. @No__t-0 컨트롤은 인쇄 출력, 클립보드에 복사, 확대/축소 및 텍스트 검색 기능을 비롯 한 일반적인 작업에 대 한 기본 제공 지원을 제공 하는 직관적인 사용자 인터페이스를 제공 합니다. 컨트롤에서는 친숙한 스크롤링 메커니즘을 통해 콘텐츠 페이지에 액세스하는 권한을 제공합니다. 모든 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤과 마찬가지로 <xref:System.Windows.Controls.DocumentViewer>은 완전 하거나 부분 스타일을 지원 하 여 컨트롤이 거의 모든 응용 프로그램 또는 환경에 시각적으로 통합 될 수 있도록 합니다.  
  
 <xref:System.Windows.Controls.DocumentViewer>은 읽기 전용 방식으로 콘텐츠를 표시 하도록 설계 되었습니다. 콘텐츠 편집 또는 수정을 사용할 수 없으며 지원 되지 않습니다.  
  
<a name="flow_document"></a>   
### <a name="flow-document-controls"></a>유동 문서 컨트롤  

> [!NOTE]
> 유동 문서 기능 및 이러한 기능을 만드는 방법에 대 한 자세한 내용은 [유동 문서 개요](flow-document-overview.md)를 참조 하세요.  
  
 유동 문서 콘텐츠 표시는 <xref:System.Windows.Controls.FlowDocumentReader>, <xref:System.Windows.Controls.FlowDocumentPageViewer> 및 <xref:System.Windows.Controls.FlowDocumentScrollViewer>의 세 가지 컨트롤에서 지원 됩니다.  
  
#### <a name="flowdocumentreader"></a>FlowDocumentReader  
 <xref:System.Windows.Controls.FlowDocumentReader> 사용자가 단일 페이지 (페이지-에-) 보기 모드를 한 번에 두 페이지 (책 읽기 형식) 보기 모드 및 연속 스크롤 (바닥이 없음) 보기 모드를 비롯 한 다양 한 보기 모드를 동적으로 선택할 수 있도록 하는 기능이 포함 되어 있습니다.  이러한 표시 모드에 대 한 자세한 내용은을 <xref:System.Windows.Controls.FlowDocumentReaderViewingMode>참조 하십시오.  여러 보기 모드를 <xref:System.Windows.Controls.FlowDocumentPageViewer> <xref:System.Windows.Controls.FlowDocumentScrollViewer> 동적으로 전환 하는 기능이 필요 하지 않은 경우에는 특정 보기 모드에서 수정 되는 더 간단한 유동 콘텐츠 뷰어를 제공 합니다.  
  
#### <a name="flowdocumentpageviewer-and-flowdocumentscrollviewer"></a>FlowDocumentPageViewer 및 FlowDocumentScrollViewer  
 <xref:System.Windows.Controls.FlowDocumentPageViewer>콘텐츠를 실시간 보기 모드로 표시 하지만는 <xref:System.Windows.Controls.FlowDocumentScrollViewer> 연속 스크롤 모드에서 콘텐츠를 표시 합니다.  둘 다 <xref:System.Windows.Controls.FlowDocumentPageViewer> 고 <xref:System.Windows.Controls.FlowDocumentScrollViewer> 특정 보기 모드로 고정 됩니다. 와 비교 합니다. 여기에는 사용자가 <xref:System.Windows.Controls.FlowDocumentReaderViewingMode> 열거형에서 제공 하는 다양 한 보기 모드를 동적으로 선택할 수 있는 기능이 포함 되며, 또는 <xref:System.Windows.Controls.FlowDocumentScrollViewer>보다 <xref:System.Windows.Controls.FlowDocumentPageViewer> 많은 리소스를 사용 하는 비용이 듭니다. <xref:System.Windows.Controls.FlowDocumentReader>  
  
 기본적으로 세로 스크롤 막대는 항상 표시되며 가로 스크롤 막대는 필요한 경우 표시됩니다. 기본값 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 에 대 한 <xref:System.Windows.Controls.FlowDocumentScrollViewer> 도구 모음을 다루지 않습니다 하지만 <xref:System.Windows.Controls.FlowDocumentScrollViewer.IsToolBarVisible%2A> 기본 제공 도구 모음을 사용 하도록 설정 하려면 속성을 사용할 수 있습니다.  
  
<a name="text_in_the_user_interface"></a>   
### <a name="text-in-the-user-interface"></a>사용자 인터페이스의 텍스트  
 문서에 텍스트를 추가하는 외에도 양식과 같은 애플리케이션 UI에서 명확하게 텍스트를 사용할 수 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 화면에 텍스트를 그리는 데 사용하는 여러 컨트롤이 포함되어 있습니다. 각 컨트롤은 다른 시나리오를 대상으로 하며 고유 기능 및 제한 사항 목록을 가지고 있습니다. 일반적으로 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]의 간단한 문장과 같이 제한 된 텍스트 지원이 필요한 경우 <xref:System.Windows.Controls.TextBlock> 요소를 사용 해야 합니다. 최소 텍스트 지원이 필요한 경우 <xref:System.Windows.Controls.Label>을 사용할 수 있습니다. 자세한 내용은 [TextBlock 개요](../controls/textblock-overview.md)를 참조하세요.  
  
<a name="packaging"></a>   
## <a name="document-packaging"></a>문서 패키징  
 @No__t-0 Api는 응용 프로그램 데이터, 문서 콘텐츠 및 관련 리소스를 간편 하 게 액세스 하 고, 이식 가능 하며, 쉽게 배포할 수 있는 단일 컨테이너에 구성 하는 효율적인 방법을 제공 합니다. ZIP 파일은 여러 개체를 단일 단위로 보관할 수 있는 @no__t 0 형식의 예입니다. 패키징 Api는 XML 및 ZIP 파일 아키텍처에서 개방형 패키징 규칙 표준을 사용 하 여 설계 된 기본 <xref:System.IO.Packaging.ZipPackage> 구현을 제공 합니다. @No__t-0 패키징 Api를 사용 하면 패키지를 간단 하 게 만들고 그 안에 개체를 저장 하 고 액세스할 수 있습니다. @No__t-0에 저장 된 개체를 <xref:System.IO.Packaging.PackagePart> ("part") 이라고 합니다. 패키지에는 파트의 작성기를 식별하고 패키지의 콘텐츠가 수정되지 않았는지 유효성을 검사하는 데 사용할 수 있는 서명된 디지털 인증서도 포함될 수 있습니다.  또한 패키지에는 추가 정보를 패키지에 추가 하거나 기존 파트의 콘텐츠를 실제로 수정 하지 않고 특정 부분과 연결 하는 <xref:System.IO.Packaging.PackageRelationship> 기능이 포함 되어 있습니다.  패키지 서비스는 Microsoft Windows Rights Management (RM)도 지원 합니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 패키지 아키텍처는 다음과 같은 여러 주요 기술의 기반 역할을 합니다.  
  
- Xps 문서는 XPS (XML Paper Specification)를 준수 합니다.  
  
- Microsoft Office “12” Open XML 형식 문서(.docx).  
  
- 고유 애플리케이션 디자인에 맞는 사용자 지정 스토리지 형식.  
  
 패키징 Api에 따라 <xref:System.Windows.Xps.Packaging.XpsDocument>은 @no__t 1 고정 콘텐츠 문서를 저장 하기 위해 특별히 설계 되었습니다. @No__t-0은 뷰어에서 열거나, @no__t 1 컨트롤에 표시 하거나, 인쇄 스풀로 라우팅하거나, XPS 호환 프린터로 직접 출력할 수 있는 자체 포함 문서입니다.  
  
 다음 섹션에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]와 함께 제공 되는 <xref:System.IO.Packaging.Package> 및 <xref:System.Windows.Xps.Packaging.XpsDocument> Api에 대 한 추가 정보를 제공 합니다.  
  
<a name="packages"></a>   
### <a name="package-components"></a>패키지 구성 요소  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 패키징 API를 사용하면 애플리케이션 데이터와 문서를 이식 가능한 단일 단위로 구성할 수 있습니다. ZIP 파일은 가장 일반적인 패키지 유형 중 하나이고, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 제공하는 기본 패키지 유형입니다.  <xref:System.IO.Packaging.Package>은 개방형 표준 XML 및 ZIP 파일 아키텍처를 사용 하 여 <xref:System.IO.Packaging.ZipPackage>을 구현 하는 추상 클래스입니다.  @No__t-0 메서드는 <xref:System.IO.Packaging.ZipPackage>을 사용 하 여 기본적으로 ZIP 파일을 만들고 사용 합니다. 패키지에는 다음과 같은 세 가지 기본 유형의 항목이 포함될 수 있습니다.  
  
|||  
|-|-|  
|<xref:System.IO.Packaging.PackagePart>|애플리케이션 콘텐츠, 데이터, 문서 및 리소스 파일.|  
|<xref:System.IO.Packaging.PackageDigitalSignature>|ID, 인증 및 유효성 검사용 [X.509 인증서].|  
|<xref:System.IO.Packaging.PackageRelationship>|패키지 또는 특정 파트와 관련된 추가 정보.|  
  
<a name="PackageParts"></a>   
#### <a name="packageparts"></a>PackageParts  
 @No__t-0 ("part")은 <xref:System.IO.Packaging.Package>에 저장 된 개체를 참조 하는 추상 클래스입니다. ZIP 파일에서 패키지 파트는 ZIP 파일에 저장된 개별 파일에 해당합니다.  <xref:System.IO.Packaging.ZipPackagePart>은 <xref:System.IO.Packaging.ZipPackage>에 저장 된 직렬화 가능 개체에 대 한 기본 구현을 제공 합니다.  파일 시스템과 마찬가지로 패키지에 포함된 파트는 계층 구조 디렉터리 또는 “폴더 스타일” 조직에 저장됩니다.  @No__t-0 패키징 Api를 사용 하 여 응용 프로그램은 단일 ZIP 파일 컨테이너를 사용 하 여 여러 <xref:System.IO.Packaging.PackagePart> 개체를 작성, 저장 및 읽을 수 있습니다.  
  
<a name="PackageDigitalSignatures"></a>   
#### <a name="packagedigitalsignatures"></a>PackageDigitalSignatures  
 보안을 위해 <xref:System.IO.Packaging.PackageDigitalSignature> ("디지털 서명")을 패키지 내의 파트와 연결할 수 있습니다. @No__t-0은 다음 두 가지 기능을 제공 하는 [509]를 통합 합니다.  
  
1. 파트의 작성기를 식별하고 인증합니다.  
  
2. 파트가 수정되지 않았는지 유효성을 검사합니다.  
  
 디지털 시그니처는 파트를 수정하지 못하게 하지는 않지만, 파트를 임의 방식으로 변경하면 디지털 시그니처의 유효성 검사 확인이 실패합니다. 그러면 애플리케이션에서 파트 열기를 차단하거나 사용자에게 파트가 수정되어 안전하지 않음을 알리는 등의 적절한 조치를 수행할 수 있습니다.  
  
<a name="PackageRelationships"></a>   
#### <a name="packagerelationships"></a>PackageRelationships  
 @No__t-0 ("관계")은 패키지 또는 패키지 내의 파트와 추가 정보를 연결 하는 메커니즘을 제공 합니다. 관계는 실제 파트 콘텐츠를 수정하지 않고 파트와 추가 정보를 연결할 수 있는 패키지 수준 기능입니다. 대부분의 경우 새 데이터를 파트 콘텐츠에 직접 삽입하는 것은 실용적이지 않습니다.  
  
- 파트의 실제 형식 및 해당 콘텐츠 스키마는 알 수 없습니다.  
  
- 알려진 경우에도 콘텐츠 스키마에서는 새 정보를 추가하는 방법을 제공하지 않습니다.  
  
- 파트는 디지털 방식으로 서명되거나 암호화될 수 있으며, 수정은 불가능합니다.  
  
 패키지 관계에서는 자세한 정보를 추가하여 개별 파트 또는 전체 패키지와 연결하는 검색 가능한 방법을 제공합니다. 패키지 관계는 다음 두 개의 주요 기능에 사용합니다.  
  
1. 파트 간 종속성 관계 정의.  
  
2. 메모 또는 파트와 관련된 다른 데이터를 추가하는 정보 관계 정의.  
  
 @No__t-0은 종속성을 정의 하 고 패키지 또는 패키지의 일부에 연결 된 다른 정보를 추가 하는 빠른 검색 가능 수단을 제공 합니다.  
  
<a name="Dependency_Relationships"></a>   
##### <a name="dependency-relationships"></a>종속성 관계  
 종속성 관계는 한 파트가 다른 파트에 지정하는 종속성을 설명하는 데 사용됩니다. 예를 들어, 패키지에는 하나 이상의 \<img> 이미지 태그를 포함하는 HTML 파트가 포함될 수 있습니다. 이미지 태그는 패키지 내부의 다른 파트 또는 패키지 외부의 다른 파트(예: 인터넷을 통해 액세스 가능)로 있는 이미지를 참조합니다. HTML 파일과 연결 된 <xref:System.IO.Packaging.PackageRelationship>을 만들면 종속 리소스를 빠르고 쉽게 검색 하 고 액세스할 수 있습니다. 브라우저 또는 뷰어 애플리케이션에서 파트 관계에 직접 액세스하고 스키마를 모르거나 문서를 구문 분석하지 않아도 종속 리소스의 어셈블링을 즉시 시작할 수 있습니다.  
  
<a name="Information_Relationships"></a>   
##### <a name="information-relationships"></a>정보 관계  
 메모 또는 주석과 마찬가지로, <xref:System.IO.Packaging.PackageRelationship>은 파트 콘텐츠 자체를 실제로 수정 하지 않고도 파트와 연결 될 다른 유형의 정보를 저장 하는 데도 사용할 수 있습니다.  
  
<a name="XPS_Documents"></a>   
## <a name="xps-documents"></a>XPS 문서  
 XPS (XML Paper Specification) 문서는 렌더링에 필요한 모든 리소스 및 정보와 함께 하나 이상의 수정 된 문서를 포함 하는 패키지입니다.  XPS는 네이티브 [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)] 인쇄 스풀 파일 형식 이기도 합니다.  @No__t-0은 표준 ZIP 데이터 집합에 저장 되 고 XML 및 이진 구성 요소 (예: 이미지 및 글꼴 파일)의 조합을 포함할 수 있습니다. [PackageRelationships](#PackageRelationships)는 문서를 완전하게 렌더링하는 데 필요한 리소스와 콘텐츠 사이의 종속성을 정의하는 데 사용합니다.  @No__t-0 디자인은 여러 사용을 지 원하는 고품질의 단일 문서 솔루션을 제공 합니다.  
  
- 고정 문서 콘텐츠와 리소스를 읽고 쓰며, 이식 가능하고 배포하기 쉬운 단일 파일로 저장.  
  
- XPS 뷰어 응용 프로그램을 사용 하 여 문서 표시  
  
- [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)]의 기본 인쇄 스풀 출력 형식으로 문서 출력.  
  
- 문서를 XPS 호환 프린터로 직접 라우팅합니다.  
  
## <a name="see-also"></a>참조

- <xref:System.Windows.Documents.FixedDocument>
- <xref:System.Windows.Documents.FlowDocument>
- <xref:System.Windows.Xps.Packaging.XpsDocument>
- <xref:System.IO.Packaging.ZipPackage>
- <xref:System.IO.Packaging.ZipPackagePart>
- <xref:System.IO.Packaging.PackageRelationship>
- <xref:System.Windows.Controls.DocumentViewer>
- [텍스트 모드](optimizing-performance-text.md)
- [유동 문서 개요](flow-document-overview.md)
- [인쇄 개요](printing-overview.md)
- [문서 serialization 및 스토리지](document-serialization-and-storage.md)
