---
title: 기본 프로그래밍 수명 주기
ms.date: 03/30/2017
helpviewer_keywords:
- service creation [WCF]
ms.assetid: 7cf21bfe-23bd-46aa-8033-609f851dbf76
ms.openlocfilehash: 6d9ea3b877e7c735cf789039b2a6956037372888
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61782410"
---
# <a name="basic-programming-lifecycle"></a>기본 프로그래밍 수명 주기
Windows Communication Foundation (WCF) 응용 프로그램이 다른 응용 프로그램 플랫폼 또는 인터넷을 통해 컴퓨터의 동일한 지 여부를 통신할 수 있습니다. 이 항목에서는 WCF 응용 프로그램을 빌드하는 데 필요한 작업을 간략하게 설명 합니다. 작업 샘플 응용 프로그램을 참조 하세요 [초보자를 위한 자습서](../../../docs/framework/wcf/getting-started-tutorial.md)합니다.  
  
## <a name="the-basic-tasks"></a>기본 작업  
 수행할 기본 작업 순서는 다음과 같습니다.  
  
1. 서비스 계약을 정의합니다. 서비스 계약은 서비스 서명, 서비스 교환 날짜 및 계약에 필요한 기타 데이터를 지정합니다. 자세한 내용은 [Designing Service Contracts](../../../docs/framework/wcf/designing-service-contracts.md)합니다.  
  
2. 계약을 구현합니다. 서비스 계약을 구현하려면 계약을 구현하는 클래스를 만들고 런타임에 필요한 사용자 지정 동작을 지정합니다. 자세한 내용은 [Implementing Service Contracts](../../../docs/framework/wcf/implementing-service-contracts.md)합니다.  
  
3. 엔드포인트 및 기타 동작 정보를 지정하여 서비스를 구성합니다. 자세한 내용은 [서비스 구성](../../../docs/framework/wcf/configuring-services.md)합니다.  
  
4. 서비스를 호스트합니다. 자세한 내용은 [호스팅 서비스](../../../docs/framework/wcf/hosting-services.md)합니다.  
  
5. 클라이언트 애플리케이션을 빌드합니다. 자세한 내용은 [클라이언트 빌드](../../../docs/framework/wcf/building-clients.md)합니다.  
  
 이 단원의 항목은 이 순서를 따르지만 일부 시나리오에서는 첫 번째 단계부터 시작하지 않는 경우도 있습니다. 예를 들어 기존 서비스에 대한 클라이언트를 빌드하려면 5단계에서 시작합니다. 다른 사용자가 사용할 서비스를 빌드하는 경우 5단계를 건너뜁니다.  
  
 서비스 계약 개발에 익숙한 控 制 참조할 수 있습니다 [확장성 소개](../../../docs/framework/wcf/introduction-to-extensibility.md)합니다. 서비스에 문제가 있으면 확인 [WCF 문제 해결 퀵 스타트](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md) 다른 같은 문제나 비슷한 문제가 있는지 확인 합니다.  
  
## <a name="see-also"></a>참고자료

- [서비스 계약 구현](../../../docs/framework/wcf/implementing-service-contracts.md)
