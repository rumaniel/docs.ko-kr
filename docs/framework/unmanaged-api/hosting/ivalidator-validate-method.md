---
title: IValidator::Validate 메서드
ms.date: 03/30/2017
api_name:
- IValidator.Validate
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- Validate
helpviewer_keywords:
- IValidator::Validate method [.NET Framework hosting]
- Validate method, IValidator interface [.NET Framework hosting]
ms.assetid: 7d68666a-fb73-4455-bebd-908d49a16abc
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 840a3779ca5692787c2c352db60a29d6a4d4ba4f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67768594"
---
# <a name="ivalidatorvalidate-method"></a>IValidator::Validate 메서드
지정 된 pe (이식 가능) 또는 Microsoft MSIL (intermediate language) 파일의 유효성을 검사 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT Validate (  
    [in] IVEHandler            *veh,  
    [in] IUnknown              *pAppDomain,  
    [in] unsigned long          ulFlags,  
    [in] unsigned long          ulMaxError,  
    [in] unsigned long          token,  
    [in] LPWSTR                 fileName,  
    [in, size_is(ulSize)] BYTE *pe,  
    [in] unsigned long          ulSize  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `veh`  
 [in] 에 대 한 포인터는 `IVEHandler` 유효성 검사 오류를 처리 하는 인스턴스.  
  
 `pAppDomain`  
 [in] 파일이 로드 되는 응용 프로그램 도메인에 대 한 포인터입니다.  
  
 `ulFlags`  
 [in] 비트 조합 [ValidatorFlags](../../../../docs/framework/unmanaged-api/hosting/validatorflags-enumeration.md) 수행 해야 하는 유효성 검사를 나타내는 값입니다.  
  
 `ulMaxError`  
 [in] 유효성 검사를 종료 하기 전까지 허용 오류의 최대 수입니다.  
  
 `token`  
 [in] 사용 되지 않습니다.  
  
 `fileName`  
 [in] 유효성을 검사할 파일의 이름을 지정 하는 문자열입니다.  
  
 `pe`  
 [in] 파일 저장 되는 메모리 버퍼에 대 한 포인터입니다.  
  
 `ulSize`  
 [in] 유효성을 검사할 파일의 바이트 크기입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** IValidator.idl, IValidator.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
