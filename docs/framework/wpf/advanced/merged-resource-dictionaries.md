---
title: 병합된 리소스 사전
ms.date: 03/30/2017
helpviewer_keywords:
- merged resource dictionaries [WPF]
- dictionaries [WPF], merged resources
ms.assetid: d159531f-05d4-49fd-b951-c332de51e5bc
ms.openlocfilehash: 466a18a58acfebf6d779a1d0eba3d2637743806e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69911721"
---
# <a name="merged-resource-dictionaries"></a>병합된 리소스 사전
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 리소스에서는 병합된 리소스 사전 기능을 지원합니다. 이 기능을 사용하면 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애플리케이션의 리소스 부분을 컴파일된 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 애플리케이션 외부에서 정의할 수 있습니다. 그런 다음 리소스를 애플리케이션 간에 공유하고 지역화를 위해 더욱 간편하게 격리할 수도 있습니다.  
  
## <a name="introducing-a-merged-resource-dictionary"></a>병합된 리소스 사전 도입  
 태그에서 다음 구문을 사용하여 병합된 리소스 사전을 페이지에 도입할 수 있습니다.  
  
 [!code-xaml[ResourceMergeDictionary#MergedXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/ResourceMergeDictionary/CS/default.xaml#mergedxaml)]  
  
 요소에 <xref:System.Windows.ResourceDictionary> 는 일반적으로 리소스 컬렉션의 모든 항목에 필요한 [x:Key 지시문](../../xaml-services/x-key-directive.md)이 없습니다. 그러나 <xref:System.Windows.ResourceDictionary> 컬렉션<xref:System.Windows.ResourceDictionary.MergedDictionaries%2A> 내의 다른 참조는이 병합 된 리소스 사전 시나리오에 대해 예약 된 특수 한 경우입니다. 병합 <xref:System.Windows.ResourceDictionary> 된 리소스 사전을 도입 하는에는 [x:Key 지시문](../../xaml-services/x-key-directive.md)을 사용할 수 없습니다. 일반적으로 <xref:System.Windows.ResourceDictionary.MergedDictionaries%2A> 컬렉션 <xref:System.Windows.ResourceDictionary> 내의 각는 특성을 <xref:System.Windows.ResourceDictionary.Source%2A> 지정 합니다. <xref:System.Windows.ResourceDictionary.Source%2A> 값[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 은 병합할 리소스 파일의 위치로 확인 되는입니다. 루트 요소로 사용 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 하는다른파일이어야하는의대상입니다.<xref:System.Windows.ResourceDictionary>  
  
> [!NOTE]
> 을 지정 <xref:System.Windows.ResourceDictionary> <xref:System.Windows.ResourceDictionary.Source%2A>하는 대신 또는 지정 된 원본에서 포함 되는 리소스 외에도 병합 된 사전으로 지정 된 내에서 리소스를 정의 하는 것은 유효 합니다. 그러나 이는 일반적인 시나리오가 아닙니다. 병합된 사전의 기본 시나리오는 외부 파일 위치에서 리소스를 병합하는 것입니다. 페이지의 태그 내에서 리소스를 지정 하려면 일반적으로 병합 된 사전이 아닌 주 <xref:System.Windows.ResourceDictionary> 에 이러한 리소스를 정의 해야 합니다.  
  
## <a name="merged-dictionary-behavior"></a>병합된 사전 동작  
 병합된 사전의 리소스는 리소스 조회 범위에서 이 사전이 병합된 주 리소스 사전의 범위 바로 뒤에 있는 위치에 있습니다. 개별 사전 내에서는 리소스 키가 고유해야 하지만 하나의 키가 병합된 사전 집합 내에서 여러 번 나올 수 있습니다. 이 경우 반환 되는 리소스는 <xref:System.Windows.ResourceDictionary.MergedDictionaries%2A> 컬렉션에서 순차적으로 찾은 마지막 사전에서 제공 됩니다. <xref:System.Windows.ResourceDictionary.MergedDictionaries%2A> 컬렉션이 에[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]정의 된 경우 컬렉션에 있는 병합 된 사전의 순서는 태그에서 제공 되는 요소의 순서입니다. 키를 기본 사전에서 정의하고 병합된 사전에서도 정의하는 경우 반환되는 리소스는 기본 사전에서 가져옵니다. 이러한 범위 지정 규칙은 정적 리소스 참조와 동적 리소스 참조 모두에 동일하게 적용됩니다.  
  
### <a name="merged-dictionaries-and-code"></a>병합된 사전 및 코드  
 병합된 사전을 코드를 통해 `Resources` 사전에 추가할 수 있습니다. 기본적으로 `Resources` 속성에 대해 <xref:System.Windows.ResourceDictionary> 존재 하는 기본적으로 비어 있는 기본값은 초기에 비어 <xref:System.Windows.ResourceDictionary.MergedDictionaries%2A> 있는 컬렉션 속성입니다. 코드를 통해 병합 된 사전을 <xref:System.Windows.ResourceDictionary>추가 하려면 원하는 주 복제본에 대 한 참조를 가져오고 해당 <xref:System.Windows.ResourceDictionary.MergedDictionaries%2A> 속성 값을 가져온 다음에 `Add` <xref:System.Windows.ResourceDictionary.MergedDictionaries%2A>포함 된 제네릭 `Collection` 에서를 호출 합니다. 추가 하는 개체는 새 <xref:System.Windows.ResourceDictionary>개체 여야 합니다. 코드에서는 <xref:System.Windows.ResourceDictionary.Source%2A> 속성을 설정 하지 않습니다. 대신 개체를 만들거나 로드 하 <xref:System.Windows.ResourceDictionary> 여 개체를 가져와야 합니다. <xref:System.Windows.ResourceDictionary> 기존를 로드 하 여 <xref:System.Windows.ResourceDictionary> 루트가 있는 기존 <xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=nameWithType> [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일 스트림에서 호출 하는 한 가지 방법은 <xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=nameWithType> 반환 값을로 <xref:System.Windows.ResourceDictionary>캐스팅 하는 것입니다.  
  
### <a name="merged-resource-dictionary-uris"></a>병합된 리소스 사전 URI  
 사용할 [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 형식으로 표시된 병합된 리소스 사전을 포함하기 위한 몇 가지 기술이 있습니다. 대체로 이러한 기술은 프로젝트의 일부로 컴파일된 리소스와 프로젝트의 일부로 컴파일되지 않은 리소스의 두 가지 범주로 나눌 수 있습니다.  
  
 프로젝트의 일부로 컴파일된 리소스의 경우 리소스 위치를 참조하는 상대 경로를 사용할 수 있습니다. 상대 경로는 컴파일하는 동안 평가됩니다. 리소스 빌드 작업을 통해 리소스를 프로젝트의 일부로 정의해야 합니다. 리소스 .xaml 파일을 프로젝트에 리소스로 포함하는 경우 리소스 파일을 출력 디렉터리로 복사할 필요가 없습니다. 리소스가 컴파일된 애플리케이션 내에 이미 포함되어 있습니다. 또한 콘텐츠 빌드 작업을 사용할 수도 있지만 이 경우 파일을 출력 디렉터리에 복사하는 것뿐만 아니라 실행 파일과의 동일한 경로 관계에 리소스 파일을 배포해야 합니다.  
  
> [!NOTE]
> 포함 리소스 빌드 작업은 사용하지 않습니다. 빌드 작업 자체는 응용 프로그램에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 대해 지원 되지만의 <xref:System.Windows.ResourceDictionary.Source%2A> 해결 방법은 통합 <xref:System.Resources.ResourceManager>되지 않으므로 개별 리소스를 스트림에서 분리할 수 없습니다. 리소스에 액세스 하는 데 사용 하는 <xref:System.Resources.ResourceManager> 경우에도 포함 리소스를 다른 용도로 사용할 수 있습니다.  
  
 관련 기술로는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일에 대한 Pack URI를 소스로 참조하는 방법이 있습니다. Pack URI를 사용하면 참조된 어셈블리 및 다른 기술의 구성 요소를 참조할 수 있습니다. Pack URI에 대한 자세한 내용은 [WPF 애플리케이션 리소스, 콘텐츠 및 데이터 파일](../app-development/wpf-application-resource-content-and-data-files.md)을 참조하세요.  
  
 프로젝트의 일부로 컴파일되지 않는 리소스의 경우 URI가 런타임에 평가됩니다. file: 또는 http:와 같은 일반 URI 전송을 사용하여 리소스 파일을 참조할 수 있습니다. 컴파일되지 않은 리소스 방법을 사용하는 경우 file: 액세스에 추가 배포 단계가 필요하고 http: 액세스에 인터넷 보안 영역이 수반된다는 단점이 있습니다.  
  
### <a name="reusing-merged-dictionaries"></a>병합된 사전 다시 사용  
 병합할 리소스 사전을 유효한 [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]를 통해 참조할 수 있으므로 병합된 리소스 사전을 여러 애플리케이션에서 공유하거나 다시 사용할 수 있습니다. 이렇게 하는 정확한 방법은 애플리케이션 배포 전략이나 사용하는 애플리케이션 모델에 따라 달라집니다. 앞서 설명한 Pack URI 전략에서는 배포하는 동안 어셈블리 참조를 공유하여 여러 프로젝트에서 병합된 리소스를 공통 소스로 지정할 수 있습니다. 이 시나리오에서는 리소스가 계속 클라이언트별로 배포되며 하나 이상의 애플리케이션에서 참조된 어셈블리를 배포해야 합니다. 또한 http 프로토콜을 사용하는 배포된 URI를 통해 병합된 리소스를 참조할 수도 있습니다.  
  
 병합된 사전을 로컬 애플리케이션 파일로 작성하거나 로컬 공유 저장소에 기록하는 것도 병합된 사전/애플리케이션 배포의 사용 가능한 시나리오입니다.  
  
### <a name="localization"></a>지역화  
 지역화해야 하는 리소스를 기본 사전에 병합된 사전으로 격리하고 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 사용 완화로 보관하는 경우 이러한 파일을 별도로 지역화할 수 있습니다. 이 기술은 위성 리소스 어셈블리를 지역화하는 것에 비해 간단합니다. 자세한 내용은 [WPF 세계화 및 지역화 개요](wpf-globalization-and-localization-overview.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.ResourceDictionary>
- [XAML 리소스](xaml-resources.md)
- [리소스 및 코드](resources-and-code.md)
- [WPF 응용 프로그램 리소스, 콘텐츠 및 데이터 파일](../app-development/wpf-application-resource-content-and-data-files.md)
