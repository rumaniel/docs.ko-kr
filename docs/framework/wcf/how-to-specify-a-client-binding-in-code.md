---
title: '방법: 코드에서 클라이언트 바인딩 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6bee5da4-adf7-42e6-8f78-63a9e5c6dbad
ms.openlocfilehash: 37769a84ca623e2f7f246d36180aa17537e90bfa
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70990227"
---
# <a name="how-to-specify-a-client-binding-in-code"></a>방법: 코드에서 클라이언트 바인딩 지정
이 예제에서는 계산기 서비스를 사용할 클라이언트를 만들고 해당 클라이언트에 대한 바인딩을 코드를 사용하여 명령적으로 지정합니다. 클라이언트는 `CalculatorService` 인터페이스를 구현하는 `ICalculator`에 액세스하고, 서비스 및 클라이언트 모두 <xref:System.ServiceModel.BasicHttpBinding> 클래스를 사용합니다.  
  
 이 절차에서는 계산기 서비스를 실행 중인 것으로 가정합니다. 서비스 빌드에 대 한 자세한 내용은 [방법: 구성](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)에서 서비스 바인딩을 지정 합니다. 또한 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)WINDOWS COMMUNICATION FOUNDATION (WCF)를 사용 하 여 클라이언트 구성 요소를 자동으로 생성 합니다. 이 도구는 서비스에 액세스하기 위한 클라이언트 코드를 생성합니다.  
  
 클라이언트는 두 가지 부분에 빌드됩니다. Svcutil.exe는 `ClientCalculator` 인터페이스를 구현하는 `ICalculator`를 생성합니다. 그런 다음 `ClientCalculator`의 인스턴스를 구성한 후 코드를 사용하여 서비스에 대한 주소와 바인딩을 지정하여 이 클라이언트 애플리케이션을 구성합니다.  
  
 이 예제의 소스 복사에 대해서는 [Basicbinding](../../../docs/framework/wcf/samples/basicbinding.md) 샘플을 참조 하세요.  
  
### <a name="to-specify-a-custom-binding-in-code"></a>코드에서 사용자 지정 바인딩을 지정하려면  
  
1. 명령줄에서 Svcutil.exe를 사용하여 서비스 메타데이터에서 코드를 생성합니다.  
  
    ```console  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2. 생성된 클라이언트에는 클라이언트 구현에서 충족해야 하는 서비스 계약을 정의하는 `ICalculator` 인터페이스가 포함되어 있습니다.  
  
     [!code-csharp[C_HowTo_CodeClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#1)]
     [!code-vb[C_HowTo_CodeClientBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#1)]  
  
3. 또한 생성된 클라이언트에는 `ClientCalculator`의 구현이 포함되어 있습니다.  
  
     [!code-csharp[C_HowTo_CodeClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#2)]
     [!code-vb[C_HowTo_CodeClientBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#2)]  
  
4. 클라이언트 애플리케이션에서 `ClientCalculator` 클래스를 사용하는 <xref:System.ServiceModel.BasicHttpBinding>의 인스턴스를 만든 다음 지정된 주소에서 서비스 작업을 호출합니다.  
  
     [!code-csharp[C_HowTo_CodeClientBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#3)]
     [!code-vb[C_HowTo_CodeClientBinding#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#3)]  
  
5. 클라이언트를 컴파일하고 실행합니다.  
  
## <a name="see-also"></a>참고자료

- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
