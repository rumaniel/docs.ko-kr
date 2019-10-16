---
title: 계약
ms.date: 03/30/2017
ms.assetid: aa00f6b3-7e1f-4213-841a-206463fca20b
ms.openlocfilehash: e4a21e95a6f1f1860ed36c968d17bb8ac8465dce
ms.sourcegitcommit: 9ee6cd851b6e176a5811ea28ed0d5935c71950f9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68868438"
---
# <a name="contract"></a>계약
계약  
  
## <a name="syntax"></a>구문  
  
```csharp
class Contract  
{  
  sint32 AppDomainId;  
  Behavior Behaviors[];  
  string Name;  
  string Namespace;  
  Operation Operations[];  
  sint32 ProcessId;  
  Contract ref;  
  string SessionMode;  
  string Type;  
};  
```  
  
## <a name="methods"></a>메서드  
 Contract 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 Contract 클래스에는 다음 속성이 있습니다.  
  
### <a name="appdomainid"></a>AppDomainId  
 데이터 형식: sint32  
  
 액세스 유형: 읽기 전용  
  
 계약을 호스팅하는 appdomain의 appdomain ID입니다.  
  
### <a name="behaviors"></a>동작  
 데이터 형식: 동작 배열  
  
 액세스 유형: 읽기 전용  
  
 이 계약과 연결된 동작입니다.  
  
### <a name="name"></a>이름  
 데이터 형식: string  
  
 액세스 유형: 읽기 전용  
  
 WSDL에 있는 계약의 이름입니다.  
  
### <a name="namespace"></a>네임스페이스  
 데이터 형식: string  
  
 액세스 유형: 읽기 전용  
  
 WSDL에 있는 `portType` 요소의 네임스페이스입니다.  
  
### <a name="operations"></a>작업  
 데이터 형식: 작업 배열  
  
 액세스 유형: 읽기 전용  
  
 이 계약의 작업입니다.  
  
### <a name="processid"></a>ProcessId  
 데이터 형식: sint32  
  
 액세스 유형: 읽기 전용  
  
 계약을 호스팅하는 프로세스의 프로세스 ID입니다.  
  
### <a name="ref"></a>ref  
 데이터 형식: 계약  
  
 액세스 유형: 읽기 전용  
  
 계약이 이중 계약인 경우 콜백의 형식입니다.  
  
### <a name="sessionmode"></a>SessionMode  
 데이터 형식: string  
  
 액세스 유형: 읽기 전용  
  
 계약에서 채널 세션을 사용하기 위해 이 계약과 연결된 바인딩이 필요한지 여부를 나타냅니다.  
  
### <a name="type"></a>형식  
 데이터 형식: string  
  
 액세스 유형: 읽기 전용  
  
 계약의 형식입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Description.ContractDescription>
