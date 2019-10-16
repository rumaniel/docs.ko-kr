---
title: ASP.NET 웹 서비스를 WCF로 마이그레이션
ms.date: 03/30/2017
ms.assetid: 1adbb931-f0b1-47f3-9caf-169e4edc9907
ms.openlocfilehash: 52e0e499b5338e20377c14b598c045a5173df7d3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965348"
---
# <a name="migrating-aspnet-web-services-to-wcf"></a>ASP.NET 웹 서비스를 WCF로 마이그레이션
ASP.NET은 .NET Framework 클래스 라이브러리 및 웹 서비스 빌드를 위한 도구뿐 아니라 인터넷 정보 서비스(IIS) 내 호스팅 서비스에 대한 기능도 제공합니다. WCF (Windows Communication Foundation)는 웹 서비스에서 사용 하는 프로토콜을 포함 하 여 소프트웨어 엔터티가 프로토콜을 사용 하 여 통신할 수 있도록 하는 .NET Framework 클래스 라이브러리, 도구 및 호스팅 기능을 제공 합니다.  ASP.NET 웹 서비스를 WCF로 마이그레이션하면 응용 프로그램에서 WCF에 고유한 새로운 기능 및 향상 된 기능을 활용할 수 있습니다.  
  
 WCF에는 ASP.NET 웹 서비스에 비해 몇 가지 중요 한 이점이 있습니다. ASP.NET 웹 서비스 도구는 웹 서비스를 구축 하는 데만 사용 되지만 WCF는 소프트웨어 엔터티가 서로 통신 해야 하는 경우 사용할 수 있는 도구를 제공 합니다. 따라서 여러 소프트웨어 통신 시나리오를 적용하는 데 개발자가 알아야 하는 기술의 수가 적어지기 때문에 결과적으로는 소프트웨어 개발 프로젝트를 완료하는 데 필요한 시간뿐 아니라 소프트웨어 개발 리소스 비용을 줄일 수 있습니다.  
  
 웹 서비스 개발 프로젝트의 경우에도 WCF는 ASP.NET 웹 서비스 지원 보다 더 많은 웹 서비스 프로토콜을 지원 합니다. 이러한 추가 프로토콜은 무엇보다도 신뢰할 수 있는 세션 및 트랜잭션이 사용되는 더욱 정교한 솔루션을 제공합니다.  
  
 WCF는 ASP.NET 웹 서비스 보다 더 많은 메시지 전송 프로토콜을 지원 합니다. ASP.NET 웹 서비스는 HTTP(Hypertext Transfer Protocol)를 사용하여 메시지 보내기만 지원합니다. WCF는 HTTP를 사용 하 여 메시지를 보낼 뿐만 아니라 TCP (전송 제어 프로토콜), 명명 된 파이프 및 MSMQ (Microsoft Message Queuing)를 지원 합니다. 더 중요 한 것은 추가 전송 프로토콜을 지원 하도록 WCF를 확장 하는 것입니다. 따라서 WCF를 사용 하 여 개발 된 소프트웨어는 다양 한 다른 소프트웨어와 함께 작동 하도록 조정 될 수 있으므로 투자 수익을 높일 수 있습니다.  
  
 WCF는 ASP.NET 웹 서비스에서 제공 하는 것 보다 훨씬 다양 한 응용 프로그램 배포 및 관리 기능을 제공 합니다. ASP.NET도 포함 하는 구성 시스템 외에도 WCF는 구성 편집기, 보낸 사람에서 받는 사람으로의 활동 추적, 모든 수의 중개자, 추적 뷰어, 메시지 로깅, 방대한 수의 성능 카운터를 제공 합니다. WMI(Windows Management Instrumentation)에 대 한 지원.  
  
 ASP.NET 웹 서비스를 기준으로 WCF의 이러한 잠재적 이점을 고려 하 여를 사용 하거나 ASP.NET 웹 서비스를 사용 하려는 경우 다음과 같은 몇 가지 옵션을 사용할 수 있습니다.  
  
- ASP.NET 웹 서비스를 계속 사용 하 고 WCF에서 제공 되 혜택을 하지 않게.  
  
- 나중에 WCF를 채택 하는 의도로 ASP.NET 웹 서비스를 계속 사용 합니다. 이 섹션의 항목에서는 향후 WCF 응용 프로그램과 함께 새로운 ASP.NET 웹 서비스 응용 프로그램을 사용할 수 있는 잠재 고객을 최대화 하는 방법을 설명 합니다. 이 단원의 항목에서는 새 ASP.NET 웹 서비스를 WCF로 쉽게 마이그레이션할 수 있도록 새 서비스를 빌드하는 방법에 대해서도 설명 합니다. 그러나 서비스 보안이 중요 하거나, 신뢰성 또는 트랜잭션 보증이 필요 하거나, 사용자 지정 관리 기능을 생성 해야 하는 경우 WCF를 채택 하는 것이 더 좋은 옵션입니다. WCF는 정확히 그러한 시나리오를 위해 설계 되었습니다.  
  
- 기존 ASP.NET 웹 서비스 응용 프로그램을 계속 유지 하면서 새 개발을 위해 WCF를 채택 합니다. 이 선택이 최선의 선택일 가능성이 큽니다. 이를 통해 WCF의 이점을 얻을 수 있으며,이를 통해 기존 응용 프로그램을 수정 하는 데 드는 비용이 절약. 이 시나리오에서는 새로운 WCF 응용 프로그램이 기존 ASP.NET 응용 프로그램과 공존할 수 있습니다. 새 WCF 응용 프로그램은 기존 ASP.NET 웹 서비스를 사용할 수 있으며 wcf ASP.NET 호환 모드를 사용 하 여 기존 ASP.NET 응용 프로그램에 새 운영 기능을 프로그래밍 하는 데 사용할 수 있습니다.  
  
- WCF를 채택 하 고 기존 ASP.NET 웹 서비스 응용 프로그램을 WCF로 마이그레이션합니다. 이 옵션을 선택 하면 WCF에서 제공 하는 기능을 사용 하 여 기존 응용 프로그램을 개선 하거나 새롭고 더욱 강력한 WCF 응용 프로그램 내에서 기존 ASP.NET 웹 서비스의 기능을 재현할 수 있습니다.  
  
> [!NOTE]
> WCF 서비스가 IIS 5.x에서 호스트 되 고 ASP.NET이 제거 되는 경우 주의 해야 합니다. WCF 서비스를 IIS 5.x에서 호스트 하는 경우 ASP.NET을 제거 하면 서비스에 대 한 코드를 요청할 수 있습니다. IIS 5.x를 실행 하는 운영 체제에서 ASP.NET이 제거 되 고 WCF가 제거 되 면 확장명이 .svc 인 파일이 텍스트 파일로 간주 되 고 소스 코드를 비롯 한 내용이 요청자에 게 반환 됩니다.  
  
 이 섹션에서는 이러한 옵션에 대해 자세히 설명 하 고, ASP.NET 웹 서비스를 WCF와 비교 하 고, ASP.NET 웹 서비스 코드를 WCF로 마이그레이션하는 방법에 대 한 지침을 제공 합니다.  
  
## <a name="see-also"></a>참고자료

- [Windows Communication Foundation 채택 예상: 향후 마이그레이션 간소화](../../../../docs/framework/wcf/feature-details/anticipating-adopting-wcf-migration.md)
- [Windows Communication Foundation 채택 예상: 향후 통합 감속](../../../../docs/framework/wcf/feature-details/anticipating-adopting-the-wcf-easing-future-integration.md)
- [Windows Communication Foundation 채택](../../../../docs/framework/wcf/feature-details/adopting-wcf.md)
- [용도와 사용되는 표준을 기반으로 ASP.NET 웹 서비스와 WCF 비교](../../../../docs/framework/wcf/feature-details/comparing-aspnet-web-services-to-wcf-based-on-purpose-and-standards-used.md)
- [개발을 기반으로 ASP.NET 웹 서비스와 WCF 비교](../../../../docs/framework/wcf/feature-details/comparing-aspnet-web-services-to-wcf-based-on-development.md)
