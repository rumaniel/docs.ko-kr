---
title: StrongNameSignatureVerificationEx 함수
ms.date: 03/30/2017
api_name:
- StrongNameSignatureVerificationEx
api_location:
- mscoree.dll
- mscorwks.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameSignatureVerificationEx
helpviewer_keywords:
- StrongNameSignatureVerificationEx function [.NET Framework strong naming]
ms.assetid: cfe4b634-18bf-44b8-9773-d94fb7e8a480
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 08247c1ec5b868055e4836b3c0fb520a536374e8
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798921"
---
# <a name="strongnamesignatureverificationex-function"></a>StrongNameSignatureVerificationEx 함수
제공된 경로의 어셈블리 매니페스트에 강력한 이름 서명이 포함되는지 여부를 나타내는 값을 가져옵니다.  
  
 이 함수는 더 이상 사용 되지 않습니다. 대신 [ICLRStrongName:: StrongNameSignatureVerificationEx](../hosting/iclrstrongname-strongnamesignatureverificationex-method.md) 메서드를 사용 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
BOOLEAN StrongNameSignatureVerificationEx (  
    [in]  LPCWSTR   wszFilePath,  
    [in]  BOOLEAN   fForceVerification,  
    [out] BOOLEAN   *pfWasVerified  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `wszFilePath`  
 진행 확인할 어셈블리의 이식 가능한 실행 파일 (.exe 또는 .dll) 파일에 대 한 경로입니다.  
  
 `fForceVerification`  
 진행 레지스트리 설정을 재정의 해야 하는 경우에도 유효성 검사를 수행 하려면이 고 `false`, 그렇지 않으면입니다. `true`  
  
 `pfWasVerified`  
 제한이 강력한 이름 서명을 확인 했으면이 고, `false`그렇지 않으면입니다. `true` `pfWasVerified`레지스트리 설정으로 인해 `false` 확인이 성공적으로 수행 된 경우에도로 설정 됩니다.  
  
## <a name="return-value"></a>반환 값  
 `true`확인에 성공 했으면이 고, 그렇지 않으면입니다. 그렇지 않으면 `false`입니다.  
  
## <a name="remarks"></a>설명  
 `StrongNameSignatureVerificationEx`[StrongNameSignatureVerification](strongnamesignatureverification-function.md) 함수와 비슷한 기능을 제공 합니다. 그러나에 대 한 `StrongNameSignatureVerificationEx` 두 번째 입력 매개 변수 및 출력 매개 변수는 대신 `DWORD`형식 `BOOLEAN` 입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** StrongName.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [StrongNameSignatureVerificationEx 메서드](../hosting/iclrstrongname-strongnamesignatureverificationex-method.md)
- [StrongNameSignatureVerification 메서드](../hosting/iclrstrongname-strongnamesignatureverification-method.md)
- [ICLRStrongName 인터페이스](../hosting/iclrstrongname-interface.md)
