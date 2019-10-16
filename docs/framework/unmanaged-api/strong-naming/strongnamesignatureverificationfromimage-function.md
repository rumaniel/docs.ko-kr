---
title: StrongNameSignatureVerificationFromImage 함수
ms.date: 03/30/2017
api_name:
- StrongNameSignatureVerificationFromImage
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameSignatureVerificationFromImage
helpviewer_keywords:
- StrongnameSignatureVerificationFromImage function [.NET Framework strong naming]
ms.assetid: 9fb144d2-07e0-4a0e-8e05-907bbb6c9e03
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c22339b7d48e89f99d1500cfdda53f00f1234b80
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70799071"
---
# <a name="strongnamesignatureverificationfromimage-function"></a>StrongNameSignatureVerificationFromImage 함수
메모리에 이미 매핑된 어셈블리가 연결된 공개 키에 유효한지 확인합니다.  
  
 이 함수는 더 이상 사용 되지 않습니다. 대신 [ICLRStrongName:: StrongNameVerificationFromImage](../hosting/iclrstrongname-strongnamesignatureverificationfromimage-method.md) 메서드를 사용 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
BOOLEAN StrongNameSignatureVerificationFromImage (  
    [in]  BYTE    *pbBase,  
    [in]  DWORD   dwLength,  
    [in]  DWORD   dwInFlags,  
    [out] DWORD   *pdwOutFlags  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pbBase`  
 진행 매핑된 어셈블리 매니페스트의 상대 가상 주소입니다.  
  
 `dwLength`  
 진행 매핑된 이미지의 크기 (바이트)입니다.  
  
 `dwInFlags`  
 진행 확인 동작에 영향을 주는 플래그입니다. 다음 값이 지원 됩니다.  
  
- `SN_INFLAG_FORCE_VER`(0x00000001)-레지스트리 설정을 재정의 해야 하는 경우에도 강제로 확인 합니다.  
  
- `SN_INFLAG_INSTALL`(0x00000002)-이 이미지에서 수행 되는 첫 번째 확인을 지정 합니다.  
  
- `SN_INFLAG_ADMIN_ACCESS`(0x00000004)-캐시가 관리 권한이 있는 사용자 에게만 액세스를 허용 하도록 지정 합니다.  
  
- `SN_INFLAG_USER_ACCESS`(0x00000008)-현재 사용자만 어셈블리에 액세스할 수 있도록 지정 합니다.  
  
- `SN_INFLAG_ALL_ACCESS`(0x00000010)-캐시가 액세스 제한에 대 한 보장을 제공 하지 않도록 지정 합니다.  
  
- `SN_INFLAG_RUNTIME`(0x80000000)-내부 디버깅용으로 예약 되어 있습니다.  
  
 `pdwOutFlags`  
 제한이 추가 출력 정보에 대 한 플래그입니다. 지원 되는 값은 다음과 같습니다.  
  
- `SN_OUTFLAG_WAS_VERIFIED`(0x00000001)-이 값은 레지스트리 설정 `false` 으로 인해 확인이 성공 하도록 지정 하기 위해로 설정 됩니다.  
  
## <a name="return-value"></a>반환 값  
 `true`성공적으로 완료 되 면 그렇지 않으면 `false`입니다.  
  
## <a name="remarks"></a>설명  
 `StrongNameSignatureVerificationFromImage` 함수가 성공적으로 완료되지 않으면 [StrongNameErrorInfo](strongnameerrorinfo-function.md) 함수를 호출하여 마지막으로 생성된 오류를 검색합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** StrongName.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [StrongNameSignatureVerificationFromImage 메서드](../hosting/iclrstrongname-strongnamesignatureverificationfromimage-method.md)
- [ICLRStrongName 인터페이스](../hosting/iclrstrongname-interface.md)
