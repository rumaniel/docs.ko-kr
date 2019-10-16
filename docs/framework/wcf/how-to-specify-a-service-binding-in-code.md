---
title: '방법: 코드에서 서비스 바인딩 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 67ab5dd8-79c1-4e62-aa75-828ea918a53a
ms.openlocfilehash: 9f3320b031141246a394191a1924509204707dc1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61928806"
---
# <a name="how-to-specify-a-service-binding-in-code"></a>방법: 코드에서 서비스 바인딩 지정
이 예제에서는 계산기 서비스에 대해 `ICalculator` 계약을 정의하고, `CalculatorService` 클래스에서 서비스를 구현한 다음 코드로 엔드포인트를 정의합니다. 이 때 서비스가 <xref:System.ServiceModel.BasicHttpBinding> 클래스를 사용하도록 지정합니다.  
  
 일반적으로 바인딩 및 주소 정보를 코드에서 명령적으로 지정하지 않고 구성에서 선언적으로 지정하는 것이 좋습니다. 일반적으로 배포된 서비스의 바인딩과 주소가 서비스를 배포할 때 사용된 바인딩 및 주소와 다르기 때문에 코드로 엔드포인트를 정의하는 것은 효과적이지 않습니다. 일반적으로 바인딩 및 주소 지정 정보를 코드와 구분하면 애플리케이션을 다시 컴파일하거나 다시 배포할 필요 없이 해당 정보를 변경할 수 있습니다.  
  
 코드 대신 구성 요소를 사용 하 여이 서비스를 구성 하는 방법에 대 한 참조 [방법: 구성에서 서비스 바인딩 지정](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)합니다.  
  
### <a name="to-specify-in-code-to-use-the-basichttpbinding-for-the-service"></a>코드에서 서비스에 BasicHttpBinding을 사용하도록 지정하려면  
  
1. 서비스 유형에 대한 서비스 계약을 정의합니다.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#1)]
     [!code-vb[C_HowTo_CodeServiceBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#1)]  
  
2. 서비스 클래스에 서비스 계약을 구현합니다.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#2)]
     [!code-vb[C_HowTo_CodeServiceBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#2)]  
  
3. 호스팅 애플리케이션에서 서비스에 사용할 바인딩 및 서비스에 대한 기본 주소를 만듭니다.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#3)]
     [!code-vb[C_HowTo_CodeServiceBinding#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#3)]  
  
4. 서비스에 대한 호스트를 만들고 엔드포인트를 추가한 다음 호스트를 엽니다.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#4)]
     [!code-vb[C_HowTo_CodeServiceBinding#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#4)]  
  
### <a name="to-modify-the-default-values-of-the-binding-properties"></a>바인딩 속성의 기본값을 수정하려면  
  
1. <xref:System.ServiceModel.BasicHttpBinding> 클래스의 기본 속성 값 중 하나를 수정하려면 호스트를 만들기 전에 바인딩의 속성 값을 새 값으로 설정합니다. 예를 들어, 기본 열기 및 닫기 시간 제한 값을 1분에서 2분으로 변경하려면 다음을 사용합니다.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#5)]
     [!code-vb[C_HowTo_CodeServiceBinding#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#5)]  
  
## <a name="see-also"></a>참고자료

- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
- [엔드포인트 주소 지정](../../../docs/framework/wcf/specifying-an-endpoint-address.md)
