---
title: '방법: 신뢰할 수 있는 세션 내에서 메시지 교환'
ms.date: 03/30/2017
ms.assetid: 87cd0e75-dd2c-44c1-8da0-7b494bbdeaea
ms.openlocfilehash: aad4eae870e3ba603c56a28a620fe8bc0e31ceb6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61778367"
---
# <a name="how-to-exchange-messages-within-a-reliable-session"></a>방법: 신뢰할 수 있는 세션 내에서 메시지 교환

이 항목에서는 기본적이지는 않지만 신뢰할 수 있는 세션을 지원하는 시스템 제공 바인딩 중 하나를 사용하여 이러한 세션을 사용하도록 설정하는 데 필요한 단계에 대해 간략하게 설명합니다. 명령적 코드를 사용 하 여 신뢰할 수 있는 세션을 사용 하도록 설정 하거나 구성 파일에서 선언적으로 합니다. 이 절차는 신뢰할 수 있는 세션을 사용 하도록 설정 하는 메시지를 전송 된 동일한 순서로 도착 하는 규정 클라이언트와 서비스 구성 파일을 사용 합니다.

이 절차의 핵심은 끝점 구성 요소를 포함 하는 `bindingConfiguration` 이라는 바인딩 구성을 참조 하는 특성 `Binding1`합니다. 합니다 [  **\<바인딩 >** ](../../../../docs/framework/misc/binding.md) 설정 하 여 신뢰할 수 있는 세션을 사용 하도록 설정 하려면이 이름을 참조 하는 구성 요소를 `enabled` 특성을 [  **\<reliableSession >** ](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731302(v=vs.100)) 요소를 `true`입니다. `ordered` 특성을 `true`로 설정하여 신뢰할 수 있는 세션에 대해 순서가 지정된 배달 보증을 지정합니다.

이 예제의 소스 복사에 대해서 [WS 신뢰할 수 있는 세션](../../../../docs/framework/wcf/samples/ws-reliable-session.md)합니다.

### <a name="configure-the-service-with-a-wshttpbinding-to-use-a-reliable-session"></a>신뢰할 수 있는 세션을 사용 하도록 WSHttpBinding으로 서비스 구성

1. 서비스 유형에 대한 서비스 계약을 정의합니다.

   [!code-csharp[c_HowTo_UseReliableSession#1121](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/service.cs#1121)]

1. 서비스 클래스에 서비스 계약을 구현합니다. 서비스 구현 내 주소 또는 바인딩 정보는 지정 되지 note 합니다. 구성 파일에서 주소 또는 바인딩 정보를 검색 하는 코드를 작성 하는 데 필요한 아닙니다.

   [!code-csharp[c_HowTo_UseReliableSession#1122](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/service.cs#1122)]

1. 만들기는 *Web.config* 파일에 대 한 끝점을 구성 하는 `CalculatorService` 를 사용 하는 <xref:System.ServiceModel.WSHttpBinding> 신뢰할 수 있는 세션이 활성화 되어 있고 필요한 메시지의 순차적 전달을 사용 하 여 합니다.

   [!code-xml[c_HowTo_UseReliableSession#2111](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/common/web.config#2111)]

1. 만들기는 *Service.svc* 줄이 포함 된 파일:

   ```
   <%@ServiceHost language=c# Service="CalculatorService" %>
   ```

1. 위치는 *Service.svc* 인터넷 정보 서비스 (IIS) 가상 디렉터리의 파일에에서 있습니다.

### <a name="configure-the-client-with-a-wshttpbinding-to-use-a-reliable-session"></a>신뢰할 수 있는 세션을 사용 하도록 WSHttpBinding으로 클라이언트를 구성

1. 사용 된 [ServiceModel Metadata 유틸리티 도구 (*Svcutil.exe*)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 서비스 메타 데이터에서 코드를 생성 하려면 명령줄에서:

   ```console
   Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>
   ```

1. 생성된 된 클라이언트를 포함 합니다 `ICalculator` 클라이언트 구현에서 충족 해야 하는 서비스 계약을 정의 하는 인터페이스입니다.

   [!code-csharp[C_HowTo_UseReliableSession#1221](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/client.cs#1221)]

1. 또한 생성된 클라이언트 애플리케이션에는 `ClientCalculator`의 구현이 포함되어 있습니다. 참고 서비스 구현 내에 주소 및 바인딩 정보를 어디서 나 지정 되지 않습니다. 구성 파일에서 주소 또는 바인딩 정보를 검색 하는 코드를 작성 하는 데 필요한 아닙니다.

   [!code-csharp[C_HowTo_UseReliableSession#1222](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/client.cs#1222)]

1. *Svcutil.exe* 를 사용 하는 클라이언트의 구성도 생성 합니다 <xref:System.ServiceModel.WSHttpBinding> 클래스입니다. 구성 파일의 이름을 *App.config* Visual Studio를 사용 하는 경우.

   [!code-xml[C_HowTo_UseReliableSession#2211](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/common/app.config#2211)]

1. 인스턴스를 만듭니다는 `ClientCalculator` 응용 프로그램에서 서비스 작업을 호출 합니다.

   [!code-csharp[C_HowTo_UseReliableSession#1223](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/client.cs#1223)]

1. 클라이언트를 컴파일하고 실행합니다.

## <a name="example"></a>예제

기본적으로 여러 시스템 제공 바인딩은 신뢰할 수 있는 세션을 지원합니다. 여기에는 다음이 포함됩니다.

- <xref:System.ServiceModel.WSDualHttpBinding>

- <xref:System.ServiceModel.NetNamedPipeBinding>

- <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>

신뢰할 수 있는 세션을 지 원하는 사용자 지정 바인딩을 만드는 방법의 예제를 참조 하세요. [방법: HTTPS를 사용 하 여 사용자 지정 신뢰할 수 있는 세션 바인딩 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-reliable-session-binding-with-https.md)합니다.

## <a name="see-also"></a>참고자료

- [신뢰할 수 있는 세션](../../../../docs/framework/wcf/feature-details/reliable-sessions.md)
