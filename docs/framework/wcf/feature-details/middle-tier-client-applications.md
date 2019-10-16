---
title: 중간 계층 클라이언트 애플리케이션
ms.date: 03/30/2017
ms.assetid: f9714a64-d0ae-4a98-bca0-5d370fdbd631
ms.openlocfilehash: 1b1ba177c365bb6913679ed2a217e66d7a0d522b
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65877464"
---
# <a name="middle-tier-client-applications"></a>중간 계층 클라이언트 애플리케이션
이 항목에서는 Windows Communication Foundation (WCF)를 사용 하는 중간 계층 클라이언트 응용 프로그램에 관련 된 다양 한 문제를 설명 합니다.  
  
## <a name="increasing-middle-tier-client-performance"></a>중간 계층 클라이언트 성능 향상  
 ASP.NET을 사용 하 여 웹 서비스와 같은 이전 통신 기술과 비교 WCF 클라이언트 인스턴스를 생성 하는 WCF의 다양 한 기능 집합으로 인해 더 복잡할 수 있습니다. 예를 들어, <xref:System.ServiceModel.ChannelFactory%601> 개체가 열릴 때 클라이언트 인스턴스에 대한 시작 시간을 늘리는 절차인 서비스를 사용하여 보안 세션을 설정할 수 있습니다. 일반적으로 이러한 추가 기능이 영향을 주지 않습니다 클라이언트 응용 프로그램 크게 WCF 클라이언트는 여러 개의 호출 하 고 닫습니다.  
  
 그러나 중간 계층 클라이언트 응용 프로그램 수 많은 WCF 클라이언트 개체 신속 하 게 만들고, 결과적으로, 초기화 요구 사항이 향상 합니다. 서비스를 호출할 때 중간 계층 애플리케이션의 성능을 향상시키는 두 가지 기본적인 방법이 있습니다.  
  
- WCF 클라이언트 개체를 캐시 하 고 가능한 경우 후속 호출에 대 한 재사용 합니다.  
  
- 만들기는 <xref:System.ServiceModel.ChannelFactory%601> 개체 및 해당 개체를 사용 하 여 새 WCF 클라이언트 채널 개체를 호출할 때마다 만들 합니다.  
  
 이러한 방법을 사용할 때 고려해야 할 문제는 다음과 같습니다.  
  
- 서비스는 클라이언트별 상태를 유지 하는 세션을 사용 하 여, 경우 서비스의 상태를 중간 계층 클라이언트에 연결 되기 때문에 다중 클라이언트 계층 요청을 사용 하 여 중간 계층 WCF 클라이언트를 재사용할 수 없습니다.  
  
- 때문에 중간 계층 WCF 클라이언트 (또는 WCF 클라이언트 채널 개체)를 다시 사용 하지 않고 중간 계층에서 들어오는 각 요청에 대 한 새 클라이언트를 만들어야 서비스 클라이언트 단위로 인증을 수행 해야 하는 경우 중간 계층의 클라이언트 자격 증명 WCF 클라이언트 후 수정할 수 없습니다 (또는 <xref:System.ServiceModel.ChannelFactory%601>) 만들었습니다.  
  
- 채널과 채널에서 만든 클라이언트는 스레드로부터 안전하므로 네트워크에서 동시에 여러 메시지 쓰기를 지원하지 않을 수 있습니다. 큰 메시지를 보낼 경우, 특히 스트리밍할 경우에는 다른 보내기 작업이 완료되는 동안 보내기 작업이 차단될 수 있습니다. 따라서 채널을 재사용하여 제어의 흐름이 서비스로 반환될 경우 즉, 코드 경로에서 공유 클라이언트에 대한 콜백을 생성하는 서비스를 공유 클라이언트가 호출할 경우 동시성 결여 및 교착 상태의 두 가지 문제가 발생할 수 있습니다. 다시 사용 하는 WCF 클라이언트의 유형에 관계 없이 마찬가지입니다.  
  
- 채널을 공유하는지 여부에 관계없이 오류가 발생한 채널을 처리해야 합니다. 그러나 채널을 다시 사용할 경우 오류 채널에서 대기 중인 여러 요청 또는 보내기를 종료할 수 있습니다.  
  
 여러 요청에 대 한 클라이언트를 재사용 하는 것에 대 한 모범 사례를 보여 주는 예제를 보려면 [ASP.NET 클라이언트에서 데이터 바인딩](../../../../docs/framework/wcf/samples/data-binding-in-an-aspnet-client.md)합니다.  
  
 또한 <xref:System.Xml.Serialization.XmlSerializer>를 사용하여 serialize할 수 있는 데이터 형식을 사용하는 클라이언트가 런타임에 해당 데이터 형식에 대한 serialization 코드를 생성하고 컴파일할 때 시작 성능이 저하될 수 있습니다. 이 시작 성능을 향상시킬 수 있습니다. 합니다 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 응용 프로그램에 대 한 컴파일된 어셈블리 로부터 필요한 serialization 코드를 생성 하 여 이러한 응용 프로그램의 시작 성능을 향상 시킬 수 있습니다. 자세한 내용은 [방법: 시작 시간의 WCF 클라이언트 응용 프로그램 개선 XmlSerializer를 사용 하 여](../../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)입니다.  
  
## <a name="see-also"></a>참고자료

- [WCF 클라이언트를 사용하여 서비스 액세스](../../../../docs/framework/wcf/feature-details/accessing-services-using-a-client.md)
