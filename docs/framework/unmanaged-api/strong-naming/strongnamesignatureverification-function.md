---
title: StrongNameSignatureVerification 함수
ms.date: 03/30/2017
api_name:
- StrongNameSignatureVerification
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameSignatureVerification
helpviewer_keywords:
- StrongNameSignatureVerification function [.NET Framework strong naming]
ms.assetid: 933758dd-231e-4382-8819-242c0a13a4b7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8943df861b1bff2b28c68d0233fc336d1b5d4579
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798942"
---
# <a name="strongnamesignatureverification-function"></a>StrongNameSignatureVerification 함수
제공된 경로의 어셈블리 매니페스트에 지정된 플래그에 따라 확인되는 강력한 이름 서명이 포함되는지 여부를 나타내는 값을 가져옵니다.  
  
 이 함수는 더 이상 사용 되지 않습니다. 대신 [ICLRStrongName:: StrongNameSignatureVerification](../hosting/iclrstrongname-strongnamesignatureverification-method.md) 메서드를 사용 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
BOOLEAN StrongNameSignatureVerification (  
    [in]  LPCWSTR   wszFilePath,  
    [in]  DWORD     dwInFlags,  
    [out] DWORD     *pdwOutFlags  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `wszFilePath`  
 진행 어셈블리에서 확인할 이식 가능한 실행 파일 (.dll 또는 .exe)의 경로입니다.  
  
 `dwInFlags`  
 진행 확인 동작을 수정 하는 플래그입니다. 다음 값이 지원 됩니다.  
  
- `SN_INFLAG_FORCE_VER`(0x00000001)-레지스트리 설정을 재정의 해야 하는 경우에도 강제로 확인 합니다.  
  
- `SN_INFLAG_INSTALL`(0x00000002)-매니페스트를 처음 확인 하는 것을 지정 합니다.  
  
- `SN_INFLAG_ADMIN_ACCESS`(0x00000004)-캐시가 관리 권한이 있는 사용자 에게만 액세스를 허용 하도록 지정 합니다.  
  
- `SN_INFLAG_USER_ACCESS`(0x00000008)-현재 사용자만 어셈블리에 액세스할 수 있도록 지정 합니다.  
  
- `SN_INFLAG_ALL_ACCESS`(0x00000010)-캐시가 액세스 제한에 대 한 보장을 제공 하지 않도록 지정 합니다.  
  
- `SN_INFLAG_RUNTIME`(0x80000000)-내부 디버깅용으로 예약 되어 있습니다.  
  
 `pdwOutFlags`  
 제한이 강력한 이름 서명을 확인 했는지 여부를 나타내는 플래그입니다. 지원 되는 값은 다음과 같습니다.  
  
- `SN_OUTFLAG_WAS_VERIFIED`(0x00000001)-이 값은 레지스트리 설정 `false` 으로 인해 확인이 성공 하도록 지정 하기 위해로 설정 됩니다.  
  
## <a name="return-value"></a>반환 값  
 `true`확인에 성공 했으면이 고, 그렇지 않으면입니다. 그렇지 않으면 `false`입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** StrongName.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [StrongNameSignatureVerification 메서드](../hosting/iclrstrongname-strongnamesignatureverification-method.md)
- [StrongNameSignatureVerificationEx 메서드](../hosting/iclrstrongname-strongnamesignatureverificationex-method.md)
- [ICLRStrongName 인터페이스](../hosting/iclrstrongname-interface.md)
