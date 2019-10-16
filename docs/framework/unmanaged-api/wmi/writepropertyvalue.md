---
title: WritePropertyValue 함수 (관리 되지 않는 API 참조)
description: WritePropertyValue 함수는 속성에 바이트를 씁니다.
ms.date: 11/06/2017
api_name:
- WritePropertyValue
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- WritePropertyValue
helpviewer_keywords:
- WritePropertyValue function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a3c42129835f9b30bed493a0992d49d7e2a458e2
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798177"
---
# <a name="writepropertyvalue-function"></a>WritePropertyValue 함수
지정된 수의 바이트를 속성 핸들로 식별되는 속성에 씁니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
    
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT WritePropertyValue (
   [in] int                  vFunc, 
   [in] IWbemObjectAccess*   ptr, 
   [in] long                 lHandle,
   [in] long                 lNumBytes,
   [in] byte*                aData
); 
```  

## <a name="parameters"></a>매개 변수

`vFunc`  
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`  
진행 [IWbemObjectAccess](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemobjectaccess) 인스턴스에 대 한 포인터입니다.

`lHandle`  
진행 이 속성을 식별 하는 핸들을 포함 하는 정수입니다. [Getpropertyhandle](getpropertyhandle.md) 함수를 호출 하 여 핸들을 검색할 수 있습니다.   

`lNumBytes`  
진행 속성에 기록 되는 바이트 수입니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요.

`pHandle`   
제한이 데이터를 포함 하는 바이트 배열에 대 한 포인터입니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |설명  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
|`WBEM_E_TYPE_MISMATCH` | 0x80041005 | 형식 불일치가 발생 했습니다. |
|`WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |
  
## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: WritePropertyValue](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemobjectaccess-writepropertyvalue) 메서드에 대 한 호출을 래핑합니다.

이 함수를 사용 하 여 문자열 및 기타`DWORD` `QWORD` 이외의 모든 데이터를 설정 합니다.

문자열이 아닌 속성 값의 `lNumBytes` 경우는 지정 된 속성 형식의 올바른 데이터 크기 여야 합니다. 문자열 속성 값의 경우 `lNumBytes` 는 지정 된 문자열의 길이 (바이트) 여야 하 고 문자열 자체는 짝수 길이 (바이트) 여야 하 고 null 종료 문자를 따라야 합니다.

## <a name="requirements"></a>요구 사항  
**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** WMINet_Utils.idl  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
