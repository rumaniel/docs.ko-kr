---
title: QualifierSet_Next 함수 (관리 되지 않는 API 참조)
description: QualifierSet_Next 함수는 열거형의 다음 한정자를 검색 합니다.
ms.date: 11/06/2017
api_name:
- QualifierSet_Next
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_Next
helpviewer_keywords:
- QualifierSet_Next function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f97a19f236b87a7f4c5b2014aca6ee4abd338c63
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798277"
---
# <a name="qualifierset_next-function"></a>QualifierSet_Next 함수
[QualifierSet_BeginEnumeration](qualifierset-beginenumeration.md) 함수를 호출하여 시작된 열거형의 다음 한정자를 검색합니다.   

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT QualifierSet_Next (
   [in] int                  vFunc, 
   [in] IWbemQualifierSet*   ptr, 
   [in] LONG                 lFlags,
   [out] BSTR*               pstrName,        
   [out] VARIANT*            pVal,
   [out] LONG*               plFlavor                 
); 
```  

## <a name="parameters"></a>매개 변수

`vFunc`   
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`   
진행 [IWbemQualifierSet](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset) 인스턴스에 대 한 포인터입니다.

`lFlags`   
[in] 예약되어 있습니다. 이 매개 변수는 0 이어야 합니다.

`pstrName`   
제한이 한정자의 이름입니다. 이면 `null`이 매개 변수는 무시 되 고, `pstrName` 그렇지 않으면 유효한 `BSTR` 를 가리키지 않거나 메모리 누수가 발생 하지 않습니다. Null이 아닌 경우 함수는 반환 `BSTR` `WBEM_S_NO_ERROR`될 때 항상 새를 할당 합니다.

`pVal`   
제한이 성공 하면 한정자의 값입니다. 함수가 실패 `VARIANT` 하면에서 가리키는가 `pVal` 수정 되지 않습니다. 이 매개 변수가 `null`이면 매개 변수는 무시 됩니다.

`plFlavor`   
제한이 한정자 버전을 받는 LONG에 대 한 포인터입니다. 버전 정보를 원하지 않는 경우이 매개 변수는 일 `null`수 있습니다. 

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
|`WBEM_E_UNEXPECTED` | 0x8004101d | 호출자가 [QualifierSet_BeginEnumeration](qualifierset-beginenumeration.md)를 호출 하지 않았습니다. |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 새 열거를 시작할 수 없습니다. |
| `WBEM_S_NO_MORE_DATA` | 0x40005 | 더 이상 한정자가 열거에 남아 있지 않습니다. |
|`WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |
  
## <a name="remarks"></a>설명

이 함수는 [IWbemQualifierSet:: Next](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemqualifierset-next) 메서드에 대 한 호출을 래핑합니다.

함수가 반환 `QualifierSet_Next` `WBEM_S_NO_MORE_DATA`될 때까지 함수를 반복적으로 호출 하 여 모든 한정자를 열거 합니다. 열거를 조기에 종료 하려면 [QualifierSet_EndEnumeration](qualifierset-endenumeration.md) 함수를 호출 합니다.

열거 하는 동안 반환 되는 한정자의 순서는 정의 되지 않습니다.

## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** WMINet_Utils.idl  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
