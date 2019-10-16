---
title: IValidator::FormatEventInfo 메서드
ms.date: 03/30/2017
api_name:
- IValidator.FormatEventInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- FormatEventInfo
helpviewer_keywords:
- IValidator::FormatEventInfo method [.NET Framework hosting]
- FormatEventInfo method, IValidator interface [.NET Framework hosting]
ms.assetid: 4c0c7477-05ba-461b-b21b-cbfba95f1db1
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 31329a8674a9991a3f306eeff44ee3437ad64a5c
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67779440"
---
# <a name="ivalidatorformateventinfo-method"></a>IValidator::FormatEventInfo 메서드
지정 된 유효성 검사 오류에 해당 하는 오류 메시지를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT FormatEventInfo(  
    [in] HRESULT            hVECode,  
    [in] VEContext          Context,  
    [in, out] LPWSTR        msg,  
    [in] unsigned long      ulMaxLength,  
    [in] SAFEARRAY(VARIANT) psa  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `hVECode`  
 [in] 유효성 검사 오류 처리기로 전달 된 HRESULT 값입니다.  
  
 `Context`  
 [in] `VEContext` 유효성 검사 오류에 대 한 컨텍스트 정보를 포함 하는 인스턴스.  
  
 `msg`  
 [out에서] 반환 된 오류 메시지를 포함 하는 문자열입니다.  
  
 `ulMaxLength`  
 [in] 오류 메시지의 최대 길이입니다.  
  
 `psa`  
 [in] 오류를 설명 하는 추가 매개 변수를 포함 하는 안전 배열입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** IValidator.idl, IValidator.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
