---
title: '방법: 검색 프록시 테스트'
ms.date: 03/30/2017
ms.assetid: d96e3fa2-3c42-4e5d-8244-2694081bdc32
ms.openlocfilehash: 856b86241299585b80d58c6d37582463736a5935
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61972915"
---
# <a name="how-to-test-the-discovery-proxy"></a>방법: 검색 프록시 테스트
이 항목은 검색 프록시를 구현하는 방법에 대해 설명하는 네 항목 중 네 번째 항목입니다. 이전 항목인 [방법: 검색 프록시를 사용 하 여 서비스를 검색 하는 클라이언트 응용 프로그램을 구현](../../../../docs/framework/wcf/feature-details/client-app-discovery-proxy-to-find-a-service.md), 검색 프록시를 사용 하 여 서비스를 찾으려면 다음 서비스를 호출 하는 WCF 클라이언트 응용 프로그램을 구현 합니다. 이 항목에서는 검색 프록시, 서비스 및 클라이언트 애플리케이션이 올바로 작동하는지 확인하는 방법에 대해 설명합니다.  
  
### <a name="run-the-discovery-proxy"></a>검색 프록시 실행  
  
1. 관리자 권한으로 명령 프롬프트를 엽니다.  
  
2. 라는 대화 상자가 표시 될 수 있습니다. Windows 방화벽에는이 프로그램의 일부 기능이 차단 했습니다. 이 메시지가 나타나면 클릭 합니다 **차단 해제** 단추입니다.  
  
3. 명령 프롬프트 내에서 검색 프록시인 DiscoveryProxy.exe를 실행합니다.  
  
4. DiscoveryProxy.exe에 다음 텍스트가 표시됩니다. `Proxy started. Hit Enter to exit`  
  
### <a name="run-the-discoverable-service"></a>검색 가능한 서비스 실행  
  
1. 관리자 권한으로 명령 프롬프트를 엽니다.  
  
2. 명령 프롬프트 내에서 검색 가능한 서비스인 Service.exe를 실행합니다.  
  
3. DiscoveryProxy.exe에 다음 텍스트가 표시 됩니다: `******* Adding the following service: ** [Service Contract Name] ** [Service Endpoint Addr] 3.******* Done *******` 합니다.  
  
### <a name="run-the-client-application"></a>클라이언트 애플리케이션 실행  
  
1. 명령 프롬프트를 엽니다.  
  
2. 명령 프롬프트 내에서 클라이언트 애플리케이션인 client.exe를 실행합니다.  
  
3. 몇 초 후 클라이언트 응용 프로그램에는 다음 텍스트를 표시합니다. [Service-endpoint]에 연결합니다.  
  
4. Service.exe 다음 텍스트를 표시 한 다음 되어야 합니다. 요청을 받음 인사말, 필자는 응답 합니다.  
  
5. Client.exe를 다음 텍스트를 표시 한 다음 되어야 합니다. Hello Client!  
  
### <a name="shut-down-the-applications"></a>애플리케이션 종료  
  
1. 클라이언트 애플리케이션을 종료합니다.  
  
2. 서비스를 종료합니다. 검색 프록시에 다음 텍스트가 표시됩니다. `******* Removing the following service: ** [Service Contract Name] ** [Service Endpoint Addr] 2.3.******* Done *******`  
  
3. 검색 프록시를 종료합니다.  
  
## <a name="see-also"></a>참고자료

- [WCF 검색 개요](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md)
- [방법: 검색 프록시 구현](../../../../docs/framework/wcf/feature-details/how-to-implement-a-discovery-proxy.md)
- [방법: 검색 프록시에 등록할 검색 가능한 서비스를 구현 합니다.](../../../../docs/framework/wcf/feature-details/discoverable-service-that-registers-with-the-discovery-proxy.md)
- [방법: 검색 프록시를 사용 하 여 서비스를 검색 하는 클라이언트 응용 프로그램 구현](../../../../docs/framework/wcf/feature-details/client-app-discovery-proxy-to-find-a-service.md)
