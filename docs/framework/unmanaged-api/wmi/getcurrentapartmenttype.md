---
title: GetCurrentApartmentType 함수 (관리 되지 않는 API 참조)
description: GetCurrentApartmentType 함수는 호출자가 실행 중인 아파트의 유형을 검색 합니다.
ms.date: 11/06/2017
api_name:
- GetCurrentApartmentType
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetCurrentApartmentType
helpviewer_keywords:
- GetCurrentApartmentType function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ff64be47802a46979818ab54cc3efb4112dd05e0
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798619"
---
# <a name="getcurrentapartmenttype-function"></a>GetCurrentApartmentType 함수
호출자가 실행 중인 아파트의 유형을 검색합니다.   
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetCurrentApartmentType (
   [in] int                   vFunc, 
   [in] IComThreadingInfo*    ptr, 
   [out] APTTYPE*             aptType
); 
```  

## <a name="parameters"></a>매개 변수

`vFunc`  
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`  
진행 [IComThreadingInfo](/windows/desktop/api/objidlbase/nn-objidlbase-icomthreadinginfo) 인스턴스에 대 한 포인터입니다.

`aptType`  
제한이 호출자의 아파트를 나타내는 [Apttype](/windows/win32/api/objidlbase/ne-objidlbase-apttype) 열거형 값에 대 한 포인터입니다.

## <a name="return-value"></a>반환 값

|상수  |값  |설명  |
|---------|---------|---------|
| `S_OK` | 0 | 함수가 성공적으로 완료 되었습니다. |
| `E_FAIL` | 0x80000008 | 호출자가 아파트에서 실행 되 고 있지 않습니다. |
  
## <a name="remarks"></a>설명

이 함수는 [IComThreadingInfo:: GetCurrentApartmentType](/windows/desktop/api/objidlbase/nf-objidlbase-icomthreadinginfo-getcurrentapartmenttype) 메서드에 대 한 호출을 래핑합니다.

## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** WMINet_Utils.idl  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
