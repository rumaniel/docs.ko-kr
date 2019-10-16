---
title: NextMethod 함수 (관리 되지 않는 API 참조)
description: NextMethod 함수는 열거형에서 다음 메서드를 검색 합니다.
ms.date: 11/06/2017
api_name:
- NextMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- NextMethod
helpviewer_keywords:
- NextMethod function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ee743a4499824bea723043d5a2c7d57d7cbd7106
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798426"
---
# <a name="nextmethod-function"></a>NextMethod 함수
[Beginmethodenumeration](beginmethodenumeration.md)호출로 시작 하는 열거형의 다음 메서드를 검색 합니다.  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT NextMethod (
   [in] int                 vFunc, 
   [in] IWbemClassObject*   ptr, 
   [in] LONG                lFlags,
   [out] BSTR*              pName,
   [out] IWbemClassObject** ppInSignature,
   [out] IWbemClassObject** ppOutSignature   
); 
```  

## <a name="parameters"></a>매개 변수

`vFunc`  
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`  
진행 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스에 대 한 포인터입니다.

`lFlags`  
[in] 예약되어 있습니다. 이 매개 변수는 0 이어야 합니다.

`pName`  
제한이 호출 이전을 `null` 가리키는 포인터입니다. 함수가 반환 될 때 메서드 이름이 포함 된 새 `BSTR` 의 주소입니다. 

`ppSignatureIn`  
제한이 메서드에 대 한 `in` 매개 변수를 포함 하는 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 에 대 한 포인터를 받는 포인터입니다. 

`ppSignatureOut`  
제한이 메서드에 대 한 `out` 매개 변수를 포함 하는 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 에 대 한 포인터를 받는 포인터입니다. 

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |설명  |
|---------|---------|---------|
| `WBEM_E_UNEXPECTED` | 0x8004101d | [`BeginEnumeration`](beginenumeration.md) 함수를 호출 하지 않았습니다. |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |
| `WBEM_S_NO_MORE_DATA` | 0x40005 | 열거형에 속성이 더 이상 없습니다. |
  
## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: NextMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod) 메서드에 대 한 호출을 래핑합니다.

호출자는 [Beginmethodenumeration](beginmethodenumeration.md) 함수를 호출 하 여 열거형 시퀀스를 시작한 다음 함수가 반환 `WBEM_S_NO_MORE_DATA`될 때까지 [nextmethod] 함수를 호출 합니다. 필요에 따라 호출자는 [Endmethodenumeration](endmethodenumeration.md)을 호출 하 여 시퀀스를 완료 합니다. 호출자는 언제 든 지 [Endmethodenumeration](endmethodenumeration.md) 을 호출 하 여 열거형을 일찍 종료할 수 있습니다.

## <a name="example"></a>예제

C++ 예제를 보려면 [IWbemClassObject:: nextmethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod) 메서드를 참조 하세요.

## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** WMINet_Utils.idl  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
