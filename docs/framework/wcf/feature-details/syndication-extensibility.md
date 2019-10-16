---
title: 배포 확장성
ms.date: 03/30/2017
ms.assetid: 4d941175-74a2-4b15-81b3-086e8a95d25f
ms.openlocfilehash: 688b31f3c87b7c9ad4842cfe6834b0dbc9e5b85b
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64585947"
---
# <a name="syndication-extensibility"></a>배포 확장성
배포 API는 네트워크에 배포된 콘텐츠를 다양한 형식으로 작성할 수 있는 형식 중립적 프로그래밍 모델을 제공하기 위해 디자인되었습니다. 추상 데이터 모델은 다음 클래스로 구성됩니다.  
  
- <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
- <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
- <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
- <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
- <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
 이러한 클래스는 이름이 다른 경우도 일부 있지만 Atom 1.0 사양에 정의된 구문에 밀접하게 매핑됩니다.  
  
 배포 프로토콜의 주요 기능은 확장성입니다. Atom 1.0 및 RSS 2.0에서는 사양에 정의되지 않은 배포 피드에 특성 및 요소를 추가합니다. Windows Communication Foundation (WCF) 배포 프로그래밍 모델에는 사용자 지정 특성 및 확장에 대 한 자유로운 형식의 액세스를 사용 하 여 작업 하 고 새 클래스를 파생의 다음과 같은 방법으로 제공 합니다.  
  
## <a name="loosely-typed-access"></a>자유로운 형식의 액세스  
 새 클래스를 파생하여 확장을 추가하려면 추가 코드를 작성해야 합니다. 다른 옵션은 자유로운 형식으로 확장에 액세스합니다. 배포 추상 데이터 모델에 정의된 모든 형식에는 `AttributeExtensions` 및 `ElementExtensions`라는 속성이 포함되어 있지만 한 가지 예외가 있습니다. 즉, <xref:System.ServiceModel.Syndication.SyndicationContent>에는 `AttributeExtensions` 속성이 있지만 `ElementExtensions` 속성은 없습니다. 이러한 속성은 각각 `TryParseAttribute` 및 `TryParseElement` 메서드에서 처리하지 않은 확장 컬렉션입니다. <xref:System.ServiceModel.Syndication.SyndicationElementExtensionCollection.ReadElementExtensions%2A?displayProperty=nameWithType>, `ElementExtensions`, <xref:System.ServiceModel.Syndication.SyndicationFeed>, <xref:System.ServiceModel.Syndication.SyndicationItem> 및 <xref:System.ServiceModel.Syndication.SyndicationLink>의 <xref:System.ServiceModel.Syndication.SyndicationPerson> 속성에서 <xref:System.ServiceModel.Syndication.SyndicationCategory>을 호출하여 처리되지 않은 이러한 확장에 액세스할 수 있습니다. 이러한 메서드 집합은 지정된 이름과 네임스페이스가 있는 확장명을 모두 찾고, `TExtension`의 인스턴스에 개별적으로 deserialize한 다음 `TExtension` 개체의 컬렉션으로 반환합니다.  
  
## <a name="deriving-a-new-class"></a>새 클래스 파생  
 기존의 추상 데이터 모델 클래스에서 새 클래스를 파생시킬 수 있습니다. 작업하는 대부분의 피드에 특정 확장이 있는 애플리케이션을 구현할 때 이 작업을 수행합니다. 이 항목에서는 프로그램에서 사용하는 대부분의 피드에 `MyExtension` 확장이 포함되어 있습니다. 향상된 프로그래밍 환경을 제공하려면 다음 단계를 수행합니다.  
  
- 확장명 데이터를 보관할 클래스를 만듭니다. 이 경우 MyExtension이라고 하는 클래스를 만듭니다.  
  
- 프로그래밍을 위해 MyExtension 형식의 속성을 노출하려면 <xref:System.ServiceModel.Syndication.SyndicationItem>에서 MyExtensionItem이라고 하는 클래스를 파생시킵니다.  
  
- MyExtension을 읽을 때 새 MyExtension 인스턴스를 인스턴스화하려면 MyExtensionItem 클래스의 <xref:System.ServiceModel.Syndication.SyndicationItem.TryParseElement%28System.Xml.XmlReader%2CSystem.String%29>를 재정의합니다.  
  
- MyExtension 속성의 내용을 XML 작성기에 쓰려면 MyExtensionItem 클래스의 <xref:System.ServiceModel.Syndication.SyndicationItem.WriteElementExtensions%28System.Xml.XmlWriter%2CSystem.String%29>를 재정의합니다.  
  
- <xref:System.ServiceModel.Syndication.SyndicationFeed>에서 MyExtensionFeed라는 클래스를 파생시킵니다.  
  
- 기본 <xref:System.ServiceModel.Syndication.SyndicationFeed.CreateItem> 대신 MyExtensionItem을 인스턴스화하려면 MyExtensionFeed 클래스의 <xref:System.ServiceModel.Syndication.SyndicationItem>을 재정의합니다. 일련의 메서드가 <xref:System.ServiceModel.Syndication.SyndicationFeed>, <xref:System.ServiceModel.Syndication.SyndicationItem> 및 <xref:System.ServiceModel.Syndication.SyndicationLink> 개체(예: <xref:System.ServiceModel.Syndication.SyndicationCategory>, <xref:System.ServiceModel.Syndication.SyndicationPerson>, <xref:System.ServiceModel.Syndication.SyndicationFeed.CreateLink>)를 만들 수 있는 <xref:System.ServiceModel.Syndication.SyndicationFeed.CreateCategory> 및 <xref:System.ServiceModel.Syndication.SyndicationFeed.CreatePerson>에 정의되어 있습니다. 이러한 메서드를 모두 재정의하여 사용자 지정 파생 클래스를 만들 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [WCF 배포 개요](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md)
- [배포 아키텍처](../../../../docs/framework/wcf/feature-details/architecture-of-syndication.md)
