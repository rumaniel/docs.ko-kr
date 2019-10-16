---
title: 클라이언트 런타임 동작 지정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- behaviors [WCF], system-provided client
ms.assetid: d16d3405-be70-4edb-8f62-b5f614ddeca5
ms.openlocfilehash: 738aadf93b726569eb59fc281cca2e482bace0bc
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645179"
---
# <a name="specifying-client-run-time-behavior"></a>클라이언트 런타임 동작 지정
클라이언트 응용 프로그램에 맞게 런타임 동작을 수정 하려면 Windows Communication Foundation (WCF) 서비스와 마찬가지로 Windows Communication Foundation (WCF) 클라이언트를 구성할 수 있습니다. 세 가지 특성을 사용하여 클라이언트 런타임 동작을 지정할 수 있습니다. 이중 클라이언트 콜백 개체는 <xref:System.ServiceModel.CallbackBehaviorAttribute> 및 <xref:System.ServiceModel.Description.CallbackDebugBehavior> 특성을 사용하여 런타임 동작을 수정할 수 있습니다. 다른 특성인 <xref:System.ServiceModel.Description.ClientViaBehavior>는 논리 대상과 직접 네트워크 대상을 구분하는 데 사용할 수 있습니다. 또한 이중 클라이언트 콜백 형식은 서비스측 동작 중 일부를 사용할 수 있습니다. 자세한 내용은 [서비스 런타임 동작 지정](../../../docs/framework/wcf/specifying-service-run-time-behavior.md)합니다.  
  
## <a name="using-the-callbackbehaviorattribute"></a>CallbackBehaviorAttribute 사용  
 <xref:System.ServiceModel.CallbackBehaviorAttribute> 클래스를 사용하여 클라이언트 애플리케이션에서 콜백 계약 구현의 실행 동작을 구성하거나 확장할 수 있습니다. 이 특성은 인스턴스 동작과 트랜잭션 설정을 제외하고 <xref:System.ServiceModel.ServiceBehaviorAttribute> 클래스와 유사한 기능을 콜백 클래스에 대해 수행합니다.  
  
 <xref:System.ServiceModel.CallbackBehaviorAttribute> 클래스는 콜백 계약을 구현하는 클래스에 적용해야 합니다. 비이중 계약 구현에 적용하면 런타임에 <xref:System.InvalidOperationException> 예외가 throw됩니다. 다음 코드 예제에서는 <xref:System.ServiceModel.CallbackBehaviorAttribute> 개체를 사용하여 마샬링할 스레드를 확인하고, <xref:System.Threading.SynchronizationContext> 속성을 사용하여 메시지 유효성 검사를 적용하고, <xref:System.ServiceModel.CallbackBehaviorAttribute.ValidateMustUnderstand%2A> 속성을 사용하여 디버깅 목적으로 서비스에 대한 <xref:System.ServiceModel.CallbackBehaviorAttribute.IncludeExceptionDetailInFaults%2A> 개체로 예외를 반환하는 콜백 개체의 <xref:System.ServiceModel.FaultException> 클래스를 보여 줍니다.  
  
 [!code-csharp[CallbackBehaviorAttribute#3](../../../samples/snippets/csharp/VS_Snippets_CFX/callbackbehaviorattribute/cs/client.cs#3)]
 [!code-vb[CallbackBehaviorAttribute#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/callbackbehaviorattribute/vb/client.vb#3)]  
  
## <a name="using-callbackdebugbehavior-to-enable-the-flow-of-managed-exception-information"></a>CallbackDebugBehavior를 사용하여 관리되는 예외 정보의 흐름 활성화  
 프로그래밍 방식으로 또는 애플리케이션 구성 파일에서 <xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A> 속성을 `true`로 설정하여 디버깅 목적으로 클라이언트 콜백 개체에 있는 관리되는 예외 정보 흐름을 다시 서비스로 이동되게 할 수 있습니다.  
  
 관리되는 예외 정보를 서비스로 이동하면 예외 정보가 내부 클라이언트 구현 정보를 노출하여 권한이 없는 서비스에서 사용할 수 있으므로 보안상 위험할 수 있습니다. 또한 프로그래밍 방식으로 <xref:System.ServiceModel.Description.CallbackDebugBehavior> 속성을 설정할 수도 있지만 배포 시 <xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A> 비활성화를 잊기 쉬울 수 있습니다.  
  
 보안 문제와 관련이 있으므로 다음 작업을 수행하는 것이 좋습니다.  
  
- 애플리케이션 구성 파일을 사용하여 <xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A> 속성 값을 `true`로 설정합니다.  
  
- 제어된 디버깅 시나리오에서만 이 작업을 수행합니다.  
  
 다음 코드 예제에서는 클라이언트를 관리 되는 예외 정보에서에서 반환할 클라이언트 콜백 개체가 SOAP 메시지의 WCF에 지시 하는 구성 파일을 보여 줍니다.  
  
 [!code-xml[SCA.CallbackContract#4](../../../samples/snippets/csharp/VS_Snippets_CFX/sca.callbackcontract/cs/client.exe.config#4)]  
 
## <a name="using-the-clientviabehavior-behavior"></a>ClientViaBehavior 동작 사용  
 <xref:System.ServiceModel.Description.ClientViaBehavior> 동작을 사용하여 전송 채널을 만들어야 하는 Uniform Resource Identifier를 지정할 수 있습니다. 직접 네트워크 대상이 메시지의 의도된 프로세서가 아닌 경우 이 동작을 사용합니다. 이 경우 호출 애플리케이션에서 최종 대상을 알 필요가 없거나 대상 `Via` 헤더가 주소가 아닌 경우에 다중 홉 대화가 가능합니다.  
  
## <a name="see-also"></a>참고자료

- [서비스 런타임 동작 지정](../../../docs/framework/wcf/specifying-service-run-time-behavior.md)
