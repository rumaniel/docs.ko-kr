---
title: 배포 아키텍처
ms.date: 03/30/2017
ms.assetid: ed4ca86e-e3d8-4acb-87aa-1921fbc353be
ms.openlocfilehash: 5f93c7a11ed37e411fc584c8de16f141336c7f43
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69952639"
---
# <a name="architecture-of-syndication"></a>배포 아키텍처
배포 API는 네트워크에서 배포된 콘텐츠를 다양한 형식으로 작성할 수 있는 형식 중립적 프로그래밍 모델을 제공하기 위해 디자인되었습니다. 추상 데이터 모델은 다음 클래스로 구성됩니다.  
  
- <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
- <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
- <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
- <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
- <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
 이러한 클래스는 이름이 다른 경우도 일부 있지만 Atom 1.0 사양에 정의된 구문에 밀접하게 매핑됩니다.  
  
 WCF (Windows Communication Foundation)에서 배포 피드는 다른 유형의 서비스 작업으로 모델링 됩니다. 즉, 반환 형식이의 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter>파생 클래스 중 하나인 경우에 한 합니다. 피드의 검색은 요청-회신 메시지 교환으로 모델링됩니다. 클라이언트는 서비스에 대한 요청 및 서비스 응답을 보냅니다. 요청 메시지는 원시 HTTP와 같은 인프라 프로토콜을 통해 설정되며, 응답 메시지에는 일반적으로 인식되는 배포 형식(RSS 2.0 또는 Atom 1.0)으로 구성되는 페이로드가 포함됩니다. 이러한 메시지 교환을 구현하는 서비스를 배포 서비스라고 합니다.  
  
 배포 서비스 계약은 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> 클래스의 인스턴스를 반환하는 작업 집합으로 구성됩니다. 다음 예제에서는 배포 서비스에 대한 인터페이스 선언을 보여 줍니다.  
  
 [!code-csharp[S_UE_SyndicationBoth#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ue_syndicationboth/cs/service.cs#0)]  
  
 배포 지원은에서 피드를 서비스로 사용할 수 있도록와 <xref:System.ServiceModel.WebHttpBinding> <xref:System.ServiceModel.Description.WebHttpBehavior> 함께 사용 되는 바인딩을 정의 하는 WCF REST 프로그래밍 모델을 기반으로 빌드됩니다. WCF REST 프로그래밍 모델에 대 한 자세한 내용은 [Wcf 웹 HTTP 프로그래밍 모델 개요](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)를 참조 하세요.  
  
> [!NOTE]
> Atom 1.0 사양에 따라 날짜 구문에 소수로 표시된 초를 지정할 수 있습니다. WCF 구현을 serialize 및 deserialize 할 때 소수 자릿수 초를 무시 합니다.  
  
## <a name="object-model"></a>개체 모델  
 배포의 개체 모델은 다음 표의 클래스 그룹으로 구성됩니다.  
  
 클래스 형식 지정:  
  
|클래스|Description|  
|-----------|-----------------|  
|<xref:System.ServiceModel.Syndication.Atom10FeedFormatter>|<xref:System.ServiceModel.Syndication.SyndicationFeed> 인스턴스를 Atom 1.0 형식으로 serialize하는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.Atom10FeedFormatter%601>|<xref:System.ServiceModel.Syndication.SyndicationFeed> 파생 클래스를 Atom 1.0 형식으로 serialize하는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.Atom10ItemFormatter>|<xref:System.ServiceModel.Syndication.SyndicationItem> 인스턴스를 Atom 1.0 형식으로 serialize하는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.Atom10ItemFormatter%601>|<xref:System.ServiceModel.Syndication.SyndicationItem> 파생 클래스를 Atom 1.0 형식으로 serialize하는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.Rss20FeedFormatter>|<xref:System.ServiceModel.Syndication.SyndicationFeed> 인스턴스를 RSS 2.0 형식으로 serialize하는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.Rss20FeedFormatter%601>|<xref:System.ServiceModel.Syndication.SyndicationFeed> 파생 클래스를 RSS 2.0 형식으로 serialize하는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.Rss20ItemFormatter>|<xref:System.ServiceModel.Syndication.SyndicationItem> 인스턴스를 RSS 2.0 형식으로 serialize하는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.Rss20ItemFormatter%601>|<xref:System.ServiceModel.Syndication.SyndicationItem> 파생 클래스를 RSS 2.0 형식으로 serialize하는 클래스입니다.|  
  
 개체 모델 클래스:  
  
|클래스|Description|  
|-----------|-----------------|  
|<xref:System.ServiceModel.Syndication.SyndicationCategory>|배포 피드의 범주를 나타내는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.SyndicationContent>|배포 콘텐츠를 나타내는 기본 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.SyndicationElementExtension>|배포 요소 확장을 나타내는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.SyndicationElementExtensionCollection>|<xref:System.ServiceModel.Syndication.SyndicationElementExtension> 개체의 컬렉션입니다.|  
|<xref:System.ServiceModel.Syndication.SyndicationFeed>|최상위 수준 피드 개체를 나타내는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.SyndicationItem>|피드 항목을 나타내는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.SyndicationLink>|배포 피드 또는 항목 내에서 링크를 나타내는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.SyndicationPerson>|Atom Person 구문을 나타내는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.SyndicationVersions>|지원되는 배포 프로토콜 버전을 나타내는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.TextSyndicationContent>|최종 사용자에게 표시되는 <xref:System.ServiceModel.Syndication.SyndicationItem> 콘텐츠를 나타내는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.TextSyndicationContentKind>|지원되는 다른 형식의 텍스트 배포 콘텐츠를 나타내는 열거형입니다.|  
|<xref:System.ServiceModel.Syndication.UrlSyndicationContent>|다른 리소스에 대한 URL로 구성된 배포 콘텐츠를 나타내는 클래스입니다.|  
|<xref:System.ServiceModel.Syndication.XmlSyndicationContent>|브라우저에 표시되지 않는 배포 콘텐츠를 나타내는 클래스입니다.|  
  
 개체 모델의 핵심 데이터 추상화는 <xref:System.ServiceModel.Syndication.SyndicationFeed> 및 <xref:System.ServiceModel.Syndication.SyndicationItem> 클래스에 해당하는 Feed 및 Item입니다. Feed는 제목, 설명 및 만든 이와 같은 피드 수준의 일부 메타데이터, 알 수 없는 확장을 저장하는 위치 및 나머지 피드 정보 콘텐츠를 구성하는 항목 집합을 노출합니다. Item은 제목, 요약 및 게시 날짜와 같은 항목 수준의 일부 메타데이터, 알 수 없는 확장을 저장하는 위치 및 나머지 항목 정보 콘텐츠를 포함하는 콘텐츠 요소를 사용 가능하게 만듭니다. Atom 1.0 및 RSS 사양에 참조되어 있는 일반 데이터 구문을 나타내는 추가 클래스에서는 Feed 및 Item의 핵심 추상화를 지원합니다.  
  
 Feed 인스턴스에 포함되어 있는 정보는 다양한 XML 형식으로 변환할 수 있습니다. XML에서 변환하거나 XML로 변환하는 프로세스는 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> 클래스에서 관리합니다. 이 클래스는 추상 클래스입니다. 구체적인 구현은 Atom 1.0 및 RSS 2.0, <xref:System.ServiceModel.Syndication.Atom10FeedFormatter> 및 <xref:System.ServiceModel.Syndication.Rss20FeedFormatter>를 위해 제공됩니다. 파생 Feed 클래스를 사용하려면 <xref:System.ServiceModel.Syndication.Atom10FeedFormatter%601> 또는 <xref:System.ServiceModel.Syndication.Rss20FeedFormatter%601> 중 하나를 사용합니다. 그러면 파생 Feed 클래스를 지정할 수 있습니다. 파생 Item 클래스를 사용하려면 <xref:System.ServiceModel.Syndication.Atom10ItemFormatter%601> 또는 <xref:System.ServiceModel.Syndication.Rss20ItemFormatter%601> 중 하나를 사용합니다. 그러면 파생 Item 클래스를 지정할 수 있습니다. 타사에서는 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter>의 자체 구현을 파생하여 다른 배포 형식을 지원할 수 있습니다.  
  
## <a name="extensibility"></a>확장성  
  
- 배포 프로토콜의 주요 기능은 확장성입니다. Atom 1.0 및 RSS 2.0에서는 사양에 정의되지 않은 배포 피드에 특성 및 요소를 추가할 수 있습니다. WCF 배포 프로그래밍 모델은 사용자 지정 특성 및 확장을 사용 하는 두 가지 방법, 즉 새 클래스 파생 및 느슨하게 형식화 된 액세스를 제공 합니다. 자세한 내용은 [배포 확장성](../../../../docs/framework/wcf/feature-details/syndication-extensibility.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [WCF 배포 개요](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md)
- [WCF 배포 개체 모델을 Atom 및 RSS로 매핑하는 방법](../../../../docs/framework/wcf/feature-details/how-the-wcf-syndication-object-model-maps-to-atom-and-rss.md)
- [WCF 웹 HTTP 프로그래밍 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
