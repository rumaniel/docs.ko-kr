---
title: WCF 배포 개요
ms.date: 03/30/2017
ms.assetid: af6d4c39-e5e8-4099-aee6-5261feff9107
ms.openlocfilehash: ef62c4460ff5dd4890de174afda671facee97f2e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61768565"
---
# <a name="wcf-syndication-overview"></a>WCF 배포 개요
Windows Communication Foundation (WCF) WCF 서비스에서 배포 피드를 노출 하는 것에 대 한 지원을 제공 합니다. 배포는 서버가 피드라고 하는 상호 운용 가능한 형식의 일부 애플리케이션 데이터를 노출하는 애플리케이션 통합 메커니즘입니다. 피드는 일부 피드 수준 메타데이터(제목, 만든 이, URL 및 기타 메타데이터)와 일련의 피드 항목으로 구성된 애플리케이션 데이터 컬렉션입니다. 피드 내에서 피드 항목은 일반적으로 역순으로 시간 순서가 지정됩니다. 피드 항목은 표준 항목 수준 메타데이터 세트(제목 URL, 작성일, 범주 및 기타 항목 수준 메타데이터)과 임의 크기의 애플리케이션별 데이터로 구성됩니다. 가장 일반적인 두 가지 유형의 배포 피드 신디케이션 RSS (Really Simple) 2.0 및 Atom 1.0으로 WCF에서 지원 되는 됩니다.  
  
## <a name="object-model"></a>개체 모델  
 WCF에는 피드, 피드 항목 및 관련된 메타 데이터를 형식 독립적 방법으로 작업할 수 있는 배포 관련 클래스 집합을 정의: <xref:System.ServiceModel.Syndication.SyndicationFeed>, <xref:System.ServiceModel.Syndication.SyndicationItem>를 <xref:System.ServiceModel.Syndication.SyndicationPerson>, <xref:System.ServiceModel.Syndication.SyndicationLink>, 및 기타 배포 관련 클래스입니다. WCF에는 또한 비롯 한 배포 지원을 제공 WCF REST 프로그래밍 모델에 빌드한 인프라 클래스를 정의 합니다. <xref:System.ServiceModel.Syndication.Atom10FeedFormatter>, 및 <xref:System.ServiceModel.Syndication.Rss20FeedFormatter>합니다. 피드 포맷터 클래스는 RSS 2.0 및 Atom 1.0과의 개체 모델 serialize를 지원합니다.  
  
## <a name="scenarios"></a>시나리오  
 오늘날 가장 일반적인 배포 사용 방법은 블로깅이며 블로그 작성자는 주기적으로 일부 유형의 정보를 게시합니다. 이러한 정보는 텍스트, 이미지, 오디오 또는 기타 유형의 정보일 수 있습니다. 또한 많은 신문 및 잡지에서도 배포를 사용하여 새로운 소식이나 기사를 게시합니다. 사용자가 이러한 피드를 구독하면 해당 사이트에서 제공하는 모든 새로운 정보를 최신 상태로 유지할 수 있습니다. 가장 일반적으로 배포가 블로그 및 게시자와 연결되지만 배포 피드를 사용하여 노출하려는 버그 데이터베이스와 같은 정보 컬렉션을 노출하는 모든 애플리케이션에 배포를 사용할 수 있습니다. 호출 작업을 노출 하는 WCF 서비스를 만들 수 있습니다 `CodeDefects`합니다. 이 작업에서 버그를 검색하려는 사용자의 전자 메일 주소를 지정하는 매개 변수를 가져올 수 있습니다. 클라이언트 작업 호출에 다음 URL을 사용할 수 있습니다: `http://someserver/bugDatabase/CodeDefects?user=johndoe`합니다.  
  
## <a name="syndication-formats"></a>배포 형식  
 WCF 배포 플랫폼은 RSS 2.0 및 Atom 1.0을 지원 합니다.  
  
## <a name="see-also"></a>참고자료

- [WCF 웹 HTTP 프로그래밍 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
