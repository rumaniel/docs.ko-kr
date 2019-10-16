---
title: 검색 프록시 구현
ms.date: 03/30/2017
ms.assetid: dda20e79-8df3-438e-a281-69d779d978ec
ms.openlocfilehash: 5d9296d8ba70d4c9e8d8339fa3a032d9c4c62826
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62047063"
---
# <a name="implementing-a-discovery-proxy"></a>검색 프록시 구현
이 단원에서는 검색 프록시를 구현하는 데 필요한 단계에 대해 설명합니다. 검색 프록시는 서비스의 리포지토리를 포함하는 독립 실행형 서비스입니다. 클라이언트는 검색 프록시를 쿼리하여 해당 검색 프록시가 인식하는 검색 가능한 서비스를 찾을 수 있습니다. 프록시를 서비스로 채우는 방식은 구현자의 재량에 따라 결정됩니다. 예를 들어 검색 프록시가 기존 서비스 리포지토리에 연결하여 해당 정보를 검색 가능하게 만들거나, 관리자가 관리 API를 사용하여 프록시에 검색 가능한 서비스를 추가하거나, 검색 프록시가 알림 기능을 사용하여 해당 내부 캐시를 업데이트할 수 있습니다.  
  
 WCF 구현은 프록시를 손쉽게 바인딩할 수 있는 기본 클래스를 제공합니다. 이러한 API를 사용하면 기존 리포지토리 위에 검색 프록시 헤드를 빌드할 수 있습니다.  
  
 여기서 구현된 검색 프록시도 다른 WCF 서비스와 마찬가지로 검색 가능하게 만들어 클라이언트가 해당 검색 프록시의 엔드포인트를 찾을 수 있도록 할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [방법: 검색 프록시 구현](../../../../docs/framework/wcf/feature-details/how-to-implement-a-discovery-proxy.md)  
 검색 프록시를 구현하는 방법에 대해 설명합니다.  
  
 [방법: 검색 프록시에 등록할 검색 가능한 서비스를 구현 합니다.](../../../../docs/framework/wcf/feature-details/discoverable-service-that-registers-with-the-discovery-proxy.md)  
 검색 프록시에 등록할 검색 가능한 WCF 서비스를 구현 하는 방법에 설명 합니다.  
  
 [방법: 검색 프록시를 사용 하 여 서비스를 검색 하는 클라이언트 응용 프로그램 구현](../../../../docs/framework/wcf/feature-details/client-app-discovery-proxy-to-find-a-service.md)  
 서비스에 대 한 검색 하려면 검색 프록시를 사용 하는 WCF 클라이언트 응용 프로그램을 구현 하는 방법에 설명 합니다.  
  
 [방법: 검색 프록시 테스트](../../../../docs/framework/wcf/feature-details/how-to-test-the-discovery-proxy.md)  
 이전 세 항목에서 작성한 코드를 테스트하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [WCF 검색](../../../../docs/framework/wcf/feature-details/wcf-discovery.md)
- [방법: 프로그래밍 방식으로 WCF 서비스 및 클라이언트에 검색 기능 추가](../../../../docs/framework/wcf/feature-details/how-to-programmatically-add-discoverability-to-a-wcf-service-and-client.md)
