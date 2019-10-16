---
title: '방법: 서비스 계약에서 오류 선언'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e8da98e7-d22f-4f60-ac82-3fb0928a353f
ms.openlocfilehash: 2de14a76fd2ce8ad656c2b64f5f9e5b17d81eebc
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216869"
---
# <a name="how-to-declare-faults-in-service-contracts"></a>방법: 서비스 계약에서 오류 선언

관리 코드에서 오류 조건이 발생하면 예외가 throw됩니다. 그러나 WCF (Windows Communication Foundation) 응용 프로그램에서 서비스 계약은 서비스 계약에서 SOAP 오류를 선언 하 여 클라이언트에 반환 되는 오류 정보를 지정 합니다. 예외와 오류 간의 관계에 대 한 개요는 [계약 및 서비스에서 오류 지정 및 처리](specifying-and-handling-faults-in-contracts-and-services.md)를 참조 하세요.

## <a name="create-a-service-contract-that-specifies-a-soap-fault"></a>SOAP 오류를 지정하는 서비스 계약 만들기

1. 작업을 하나 이상 포함하는 서비스 계약을 만듭니다. 예는 [방법: 서비스 계약](how-to-define-a-wcf-service-contract.md)을 정의 합니다.

2. 클라이언트가 알림을 받을 수 있는 오류 조건을 지정할 수 있는 작업을 선택합니다. 클라이언트에 SOAP 오류를 반환 하는 오류 조건을 결정 하려면 [계약 및 서비스에서 오류 지정 및 처리](specifying-and-handling-faults-in-contracts-and-services.md)를 참조 하세요.

3. 선택한 작업에 <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType>를 적용하고 serialize할 수 있는 오류 형식을 생성자에 전달합니다. Serialize 할 수 있는 형식을 만들고 사용 하는 방법에 대 한 자세한 내용은 [서비스 계약에서 데이터 전송 지정](./feature-details/specifying-data-transfer-in-service-contracts.md)을 참조 하세요. 다음 예제에서는 `SampleMethod` 작업으로 인해 `GreetingFault`가 발생하도록 지정하는 방법을 보여 줍니다.

     [!code-csharp[FaultContractAttribute#4](~/samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#4)]
     [!code-vb[FaultContractAttribute#4](~/samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#4)]

4. 오류 조건을 클라이언트에 전달하는 계약의 모든 작업에 대해 2단계와 3단계를 반복합니다.

## <a name="implementing-an-operation-to-return-a-specified-soap-fault"></a>지정한 SOAP 오류를 반환하는 작업 구현
 앞의 절차와 같이 특정 SOAP 오류를 반환하여 오류 조건을 호출 애플리케이션에 전달할 수 있도록 작업에서 지정하고 나면 다음 단계로 해당 사양을 구현합니다.

### <a name="throw-the-specified-soap-fault-in-the-operation"></a>작업에서 지정한 SOAP 오류 throw

1. <xref:System.ServiceModel.FaultContractAttribute>에 지정된 오류 조건이 작업에서 발생하면 지정한 SOAP 오류가 형식 매개 변수인 새 <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType>을 throw합니다. 다음 예제에서는 앞의 절차와 다음 코드 섹션에 표시된 `GreetingFault`에서 `SampleMethod`를 throw하는 방법을 보여 줍니다.

     [!code-csharp[FaultContractAttribute#5](~/samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#5)]
     [!code-vb[FaultContractAttribute#5](~/samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#5)]

## <a name="example"></a>예제

다음 코드 예제에서는 `GreetingFault` 작업에 대해 `SampleMethod`를 지정하는 단일 작업 구현을 보여 줍니다.

[!code-csharp[FaultContractAttribute#1](~/samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#1)]
[!code-vb[FaultContractAttribute#1](~/samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#1)]

## <a name="see-also"></a>참고 항목

- <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType>
