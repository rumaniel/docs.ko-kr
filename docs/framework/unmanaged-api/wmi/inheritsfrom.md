---
title: InheritsFrom 함수 (관리 되지 않는 API 참조)
description: InheritsFrom 함수는 클래스 또는 인스턴스가 특정 부모 클래스에서 파생 되는지 여부를 확인 합니다.
ms.date: 11/06/2017
api_name:
- InheritsFrom
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- InheritsFrom
helpviewer_keywords:
- InheritsFrom function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0c32c54ec56ea0fe4f4039ca6438a91338edbadb
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798454"
---
# <a name="inheritsfrom-function"></a>InheritsFrom 함수
현재 클래스 또는 인스턴스가 지정된 부모 클래스에서 파생되는지 여부를 결정합니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
    
## <a name="syntax"></a>구문  
  
```cpp
HRESULT InheritsFrom (
   [in] int               vFunc, 
   [in] IWbemClassObject* ptr, 
   [in] LPCWSTR           wszAncestor 
); 
```  

## <a name="parameters"></a>매개 변수

`vFunc`  
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`  
진행 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스에 대 한 포인터입니다.

`wszAncestor`  
진행 클래스의 이름입니다. `wszAncestor`는 유효한 `LPCWSTR`을 가리켜야 합니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |설명  |
|---------|---------|---------|
| `WBEM_S_NO_ERROR` | 0 | 현재 개체는에서 `wszAncestor`상속 됩니다.  |
| `WBEM_S_FALSE` | 1 | 현재 개체가에서 `wszAncestor`상속 되지 않는 경우 |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | `wszAncestor`가 `null`인 경우 |
  
## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: InheritsFrom](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-inheritsfrom) 메서드에 대 한 호출을 래핑합니다.

## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** WMINet_Utils.idl  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
