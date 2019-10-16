---
title: SetSecurity 함수 (관리 되지 않는 API 참조)
description: SetSecurity 함수는 현재 스레드의 가장 토큰을 검색 합니다.
ms.date: 11/06/2017
api_name:
- SetSecurity
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- SetSecurity
helpviewer_keywords:
- SetSecurity function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 94c76213acb66116105d181e9961a33976047ee7
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798242"
---
# <a name="setsecurity-function"></a>SetSecurity 함수

현재 스레드와 연결된 가장 토큰을 검색합니다. 

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT SetSecurity (
   [out] boolean* pNeedToReset, 
   [out] HANDLE* pCurrentThreadToken
); 
```

## <a name="parameters"></a>매개 변수

`pNeedToReset`\
제한이 함수가 반환 될 때 [resetsecurity](resetsecurity.md) 함수를 호출 하 `boolean` 여 토큰을 다시 설정 해야 하는지 여부를 나타내는에 대 한 포인터를 포함 합니다.

`token`\
제한이 함수가 반환 될 때 현재 스레드와 연결 된 가장 토큰의 핸들에 대 한 포인터를 포함 합니다. 현재 스레드와 연결 된 `null` 토큰이 없는 경우 값은이 될 수 있습니다. 

## <a name="return-value"></a>반환 값

함수가 성공 하면 반환 값 `S_OK` 은 (0)입니다.

함수가 실패 하면 반환 값은 0이 아닌 오류 코드입니다. 확장 오류 정보를 가져오려면 [Geterrorinfo](geterrorinfo.md) 함수를 호출 합니다.

## <a name="requirements"></a>요구 사항

 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

 **헤더:** WMINet_Utils.idl

 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
