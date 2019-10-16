---
title: BlessIWbemServices 함수 (관리 되지 않는 API 참조)
description: BlessIWbemServices 함수는 사용자 자격 증명이 IWbemServices 클래스에 대 한 액세스를 허용 하는지 여부를 나타냅니다.
ms.date: 11/06/2017
api_name:
- BlessIWbemServices
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BlessIWbemServices
helpviewer_keywords:
- BlessIWbemServices function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e00197b72ca7fc8941475ae51159351d53da12d3
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855963"
---
# <a name="blessiwbemservices-function"></a>BlessIWbemServices 함수
사용자 자격 증명이 지정 된 [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) 클래스에 대 한 액세스를 허용 하는지 여부를 나타냅니다.   
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>구문  
  
```cpp
HRESULT BlessIWbemServices (
   [in] IWbemServices* pIWbemServices,
   [in] BSTR strUser, 
   [in] BSTR strPassword, 
   [in] BSTR strAuthority, 
   [in] DWORD impLevel, 
   [in] DWORD authnLevel
);
```  

## <a name="parameters"></a>매개 변수

`pIWbemServices`\
진행 사용 권한이 필요한 [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) 개체에 대 한 포인터입니다.

`strUser`\
진행 사용자 이름입니다.

`strPassword`\
진행 와 `strUser`연결 된 암호입니다.

`strAuthority`\
진행 사용자의 도메인 이름입니다. 자세한 내용은 [Connectserverwmi](connectserverwmi.md) 함수를 참조 하세요.

`impLevel`\
진행 가장 수준입니다.

`authnLevel`\
진행 권한 수준입니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *winerror.h* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
| `E_INVALIDARG` | 0x80070057 | 하나 이상의 인수가 잘못 되었습니다. |
| `E_POINTER` | 0x80004003 | `pIWbemServices`가 `null`인 경우 | 
| `E_FAIL` | 0x80000008 | 지정 되지 않은 오류가 발생 했습니다. |
| `E_OUTOFMEMORY` | 0x80000002 | 작업을 수행 하는 데 사용할 수 있는 메모리가 부족 합니다. | 
| `S_OK` | 0 | 함수 호출에 성공 했습니다. | 

## <a name="requirements"></a>요구 사항  

 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** WMINet_Utils.idl  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
