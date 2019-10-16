---
title: 엔드포인트
ms.date: 03/30/2017
ms.assetid: fe63370d-81a1-40f3-97c2-59cb357c78d2
ms.openlocfilehash: 03c401358839671d750985b95b1aada599931aad
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795901"
---
# <a name="endpoint"></a>엔드포인트
엔드포인트  
  
## <a name="syntax"></a>구문  
  
```csharp
class Endpoint  
{  
  string Address;  
  string AddressHeaders[];  
  string AddressIdentity;  
  sint32 AppDomainId;  
  Behavior Behaviors[];  
  Binding Binding;  
  string ContractName;  
  string CounterInstanceName;  
  string ListenUri;  
  string Name;  
  sint32 ProcessId;  
  Contract ref;  
};  
```  
  
## <a name="methods"></a>메서드  
 Endpoint 클래스는 다음과 같은 메서드를 정의합니다.  
  
|메서드|Description|  
|------------|-----------------|  
|[GetOperationCounterInstanceName](getoperationcounterinstancename.md)|작업 성능 카운터 인스턴스 이름을 검색합니다.|  
  
## <a name="properties"></a>속성  
 Endpoint 클래스에는 다음 속성이 있습니다.  
  
### <a name="address"></a>주소  
 데이터 형식: string  
  
 액세스 유형: 읽기 전용  
  
 엔드포인트의 주소를 포함하는 URI입니다.  
  
### <a name="addressheaders"></a>AddressHeaders  
 데이터 형식: string array  
  
 액세스 유형: 읽기 전용  
  
 이 엔드포인트에 연결된 주소 헤더의 컬렉션입니다.  
  
### <a name="addressidentity"></a>AddressIdentity  
 데이터 형식: string  
  
 액세스 유형: 읽기 전용  
  
 엔드포인트의 ID입니다.  
  
### <a name="appdomainid"></a>AppDomainId  
 데이터 형식: sint32  
  
 액세스 유형: 읽기 전용  
  
 엔드포인트를 호스트하는 appdomain의 appdomain ID입니다.  
  
### <a name="behaviors"></a>동작  
 데이터 형식: 동작 배열  
  
 액세스 유형: 읽기 전용  
  
 이 엔드포인트에서 구현된 동작의 컬렉션입니다.  
  
### <a name="binding"></a>바인딩  
 데이터 형식: 바인딩  
  
 액세스 유형: 읽기 전용  
  
 이 엔드포인트에서 사용하는 바인딩입니다.  
  
### <a name="contractname"></a>ContractName  
 데이터 형식: string  
  
 액세스 유형: 읽기 전용  
  
 이 엔드포인트가 공개하는 계약을 지정하는 문자열입니다.  
  
### <a name="counterinstancename"></a>CounterInstanceName  
 데이터 형식: string  
  
 액세스 유형: 읽기 전용  
  
 엔드포인트의 성능 카운터 인스턴스 이름입니다.  
  
### <a name="listenuri"></a>ListenUri  
 데이터 형식: string  
  
 액세스 유형: 읽기 전용  
  
 엔드포인트가 수신하는 URI입니다.  
  
### <a name="name"></a>이름  
 데이터 형식: string  
  
 액세스 유형: 읽기 전용  
  
 이 엔드포인트의 고유한 이름입니다.  
  
### <a name="processid"></a>ProcessId  
 데이터 형식: sint32  
  
 액세스 유형: 읽기 전용  
  
 엔드포인트를 호스트하는 프로세스의 프로세스 ID입니다.  
  
### <a name="ref"></a>ref  
 데이터 형식: 계약  
  
 액세스 유형: 읽기 전용  
  
 이 엔드포인트가 공개하는 계약입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|
