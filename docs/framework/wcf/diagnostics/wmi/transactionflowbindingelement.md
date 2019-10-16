---
title: TransactionFlowBindingElement
ms.date: 03/30/2017
ms.assetid: 0a9656fe-2400-45ca-ad79-92715c8cf190
ms.openlocfilehash: a58d5620abbb636480ceea3020552246ae284842
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61641686"
---
# <a name="transactionflowbindingelement"></a>TransactionFlowBindingElement
TransactionFlowBindingElement  
  
## <a name="syntax"></a>구문  
  
```csharp
class TransactionFlowBindingElement : BindingElement  
{  
  string IssuedTokens;  
  string TransactionProtocol;  
  boolean Transactions;  
};  
```  
  
## <a name="methods"></a>메서드  
 TransactionFlowBindingElement 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 TransactionFlowBindingElement 클래스에는 다음과 같은 속성이 있습니다.  
  
### <a name="issuedtokens"></a>IssuedTokens  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 발급된 보안 토큰 헤더(WS-Trust의 IssuedTokens)의 요구 사항을 지정합니다.  
  
### <a name="transactionprotocol"></a>TransactionProtocol  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 서비스에서 트랜잭션을 이동하는 데 사용하는 트랜잭션 프로토콜입니다.  
  
### <a name="transactions"></a>트랜잭션  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 들어오는 트랜잭션이 지원되는지 여부를 나타냅니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels.TransactionFlowBindingElement>
