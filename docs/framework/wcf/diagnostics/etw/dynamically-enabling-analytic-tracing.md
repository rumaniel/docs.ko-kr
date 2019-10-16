---
title: 동적으로 분석 추적을 사용하도록 설정
ms.date: 03/30/2017
ms.assetid: 58b63cfc-307a-427d-b69d-9917ff9f44ac
ms.openlocfilehash: bea64ac9a9312d17b7f47e72a46d876552e20a12
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798102"
---
# <a name="dynamically-enabling-analytic-tracing"></a>동적으로 분석 추적을 사용하도록 설정
Windows 운영 체제에 포함된 도구와 함께 ETW(Event Tracing for Windows)를 사용하여 추적을 동적으로 사용하거나 사용하지 않도록 설정할 수 있습니다. 모든 [!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)] WCF (Windows Communication Foundation) 서비스의 경우 응용 프로그램의 web.config 파일을 수정 하거나 서비스를 다시 시작 하지 않고도 분석 추적을 동적으로 사용 하거나 사용 하지 않도록 설정할 수 있습니다. 그러면 애플리케이션을 중지하지 않고도 추적 이벤트를 내보낼 수 있습니다.  
  
 WCF 추적 옵션을 비슷한 방법으로 구성할 수 있습니다. 예를 들어 애플리케이션을 중지하지 않고도 심각도 수준을 **Error** 에서 **Information** 으로 변경할 수 있습니다. 이 작업은 다음과 같은 도구를 사용하여 수행할 수 있습니다.  
  
- **Logman** – 추적 데이터를 구성, 제어 및 쿼리하기 위한 명령줄 도구입니다. 자세한 내용은 [Logman Create trace](https://go.microsoft.com/fwlink/?LinkId=165426) And [Logman Update trace](https://go.microsoft.com/fwlink/?LinkId=165427)를 참조 하십시오.  
  
- **EventViewer** - 추적 결과를 보기 위한 Windows 그래픽 관리 도구입니다. 자세한 내용은 [WCF 서비스 및 ETW(Windows용 이벤트 추적)](../../samples/wcf-services-and-event-tracing-for-windows.md) 및 [이벤트 뷰어](https://go.microsoft.com/fwlink/?LinkId=165428)를 참조 하세요.  
  
- **Perfmon** – 카운터를 사용하여 추적이 시스템 성능에 미치는 영향과 추적 카운터를 모니터링하는 Windows 그래픽 관리 도구입니다. 자세한 내용은 [수동으로 데이터 수집기 집합 만들기](https://go.microsoft.com/fwlink/?LinkId=165429)를 참조 하세요.  
  
### <a name="keywords"></a>키워드  
 일반적으로 <xref:System.ServiceModel.Activation.Configuration.ServiceModelActivationSectionGroup.Diagnostics%2A> 클래스를 사용하는 경우 .NET Framework 추적 메시지가 심각도 수준(예: Error, Warning 및 Information)을 기준으로 필터링됩니다. ETW는 이러한 심각도 수준 개념을 지원할 뿐 아니라 키워드를 사용하는 새롭고 유연한 필터 메커니즘도 지원합니다. 키워드는 추적 이벤트를 통해 각 이벤트가 무엇을 의미하는지에 대한 추가 컨텍스트를 제공하는 데 사용할 수 있는 임의의 텍스트 값입니다.  
  
 WCF 분석 추적의 경우 각 추적 이벤트에 두 가지 유형의 키워드가 있습니다. 첫 번째는 각 이벤트에 하나 이상 있는 시나리오 키워드입니다. 이러한 키워드는 각 이벤트가 지원하는 시나리오를 나타냅니다. 시나리오 키워드는 세 가지가 있는데, 각 키워드는 다음 표와 같이 고유한 용도로 설계되었습니다. 키워드를 사용한 필터링은 WCF 서비스를 방해 하지 않고 동적으로 변경할 수 있습니다. 즉, 현재 추적 시나리오와 수집되는 추적 정보의 양을 동적으로 변경할 수 있습니다. 예를 들어 `HealthMonitoring` 을 `Troubleshooting` 으로 변경하고 추적 이벤트 세분성을 높일 수 있습니다.  
  
|키워드|설명|  
|-------------|-----------------|  
|`HealthMonitoring`|서비스의 작업을 모니터링할 수 있는 매우 간단한 최소한의 추적입니다.|  
|`EndToEndMonitoring`|메시지 흐름 추적을 지원하는 데 사용되는 이벤트입니다.|  
|`Troubleshooting`|WCF의 확장성 지점과 관련 된 보다 세부적인 이벤트입니다.|  
  
 키워드의 두 번째 그룹은 이벤트를 내보낼 .NET Framework의 구성 요소를 정의 합니다.  
  
|키워드|설명|  
|-------------|-----------------|  
|`UserEvents`|.NET Framework 아닌 사용자 코드에서 내보내는 이벤트입니다.|  
|`ServiceModel`|WCF 런타임에서 내보내는 이벤트입니다.|  
|`ServiceHost`|서비스 호스트에서 내보내는 이벤트입니다.|  
|`WCFMessageLogging`|WCF 메시지 로깅 이벤트입니다.|  
  
## <a name="see-also"></a>참고자료

- [WCF 서비스 및 Windows용 이벤트 추적](../../samples/wcf-services-and-event-tracing-for-windows.md)
