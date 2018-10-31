---
title: GetPropertyHandle 함수 (관리 되지 않는 API 참조)
description: GetPropertyHandle 함수는 고유 핸들을 해당 identies 속성을 반환합니다.
ms.date: 11/06/2017
api_name:
- GetPropertyHandle
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetPropertyHandle
helpviewer_keywords:
- GetPropertyHandle function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2383003012ce1f6adffe0ad78ab614323840496f
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200417"
---
# <a name="getpropertyhandle-function"></a>GetPropertyHandle 함수
속성을 식별하는 고유한 핸들을 반환합니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
    
## <a name="syntax"></a>구문  
  
```  
HRESULT GetPropertyHandle (
   [in] int                  vFunc, 
   [in] IWbemObjectAccess*   ptr, 
   [in] LPCWSTR              wszPropertyName,
   [out] CIMTYPE*            pType,
   [out] long*               pHandle
); 
```  

## <a name="parameters"></a>매개 변수

`vFunc`  
[in] 이 매개 변수 사용 되지 않습니다.

`ptr`  
[in] 에 대 한 포인터를 [IWbemObjectAccess](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemobjectaccess) 인스턴스.

`wszPropertyName`  
[in] 속성 이름을 포함 하는 UTF16 인코딩 characaters의 null 종료 문자열입니다.   

`pType`  
[out] 에 대 한 포인터를 [ `CIMTYPE` ](/windows/desktop/api/wbemcli/ne-wbemcli-tag_cimtype_enumeration) 속성의 CIM 형식을 나타내는 열거형 멤버입니다.

`pHandle`   
[out] 속성 핸들을 포함 하는 정수에 대 한 포인터입니다.

## <a name="return-value"></a>반환 값

이 함수에 의해 반환 되는 다음 값에 정의 된 합니다 *WbemCli.h* 헤더 파일에서 정의할 수 상수로 코드:

|상수  |값  |설명  |
|---------|---------|---------|
|`WBEM_E_NOT_FOUND` | 0x80041002 | 지정된 된 속성 이름을 찾을 수 없습니다. |
|`WBEM_E_INVALID_PARAMETER` | '(0x80041008 | 매개 변수가 잘못 되었습니다. |
|`WBEM_E_NOT_SUPPORTED` | 0x8004100c | 요청 된 속성이 형식의 됩니다 `CIM_OBJECT` 또는 `CIM_ARRAY`합니다. |
|`WBEM_S_NO_ERROR` | 0 | 함수 호출이 성공 했습니다.  |
  
## <a name="remarks"></a>설명

이 함수에 대 한 호출을 래핑하는 [IWbemClassObject::GetPropertyHandle](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemobjectaccess-getpropertyhandle) 메서드.

이 핸들을 사용 하 여 속성을 사용 하는 경우 식별 [IWbemObjectAccess](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemobjectaccess) 읽기 또는 쓰기 속성 값에 대 한 방법입니다.

이외의 모든 데이터 형식의 속성에 대 한 검색할 수 핸들 `CIM_OBJECT` 고 `CIM_ARRAY`입니다. 클래스의 모든 인스턴스에서 처리 작업을 반환 합니다.

## <a name="requirements"></a>요구 사항  
**플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** WMINet_Utils.idl  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>참고자료  
[WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
