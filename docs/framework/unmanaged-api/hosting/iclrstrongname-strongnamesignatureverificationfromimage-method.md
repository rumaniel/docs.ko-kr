---
title: ICLRStrongName::StrongNameSignatureVerificationFromImage 메서드
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameSignatureVerificationFromImage
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameSignatureVerificationFromImage
helpviewer_keywords:
- ICLRStrongName::StrongNameSignatureVerificationFromImage method [.NET Framework hosting]
- StrongNameSignatureVerificationFromImage method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: da91c138-ee30-4fd4-a040-464d97d7e41a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 21aeceff72ea6222992cb6f3d055ed6f71cda9bf
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67759246"
---
# <a name="iclrstrongnamestrongnamesignatureverificationfromimage-method"></a>ICLRStrongName::StrongNameSignatureVerificationFromImage 메서드
메모리에 이미 매핑된 어셈블리가 연결된 공개 키에 유효한지 확인합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT StrongNameSignatureVerificationFromImage (  
    [in]  BYTE    *pbBase,  
    [in]  DWORD   dwLength,  
    [in]  DWORD   dwInFlags,  
    [out] DWORD   *pdwOutFlags  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pbBase`  
 [in] 매핑된 어셈블리 매니페스트의 상대 가상 주소입니다.  
  
 `dwLength`  
 [in] 매핑된 이미지의 바이트 크기입니다.  
  
 `dwInFlags`  
 [in] 확인 동작에 영향을 주는 플래그입니다. 다음 값이 지원 됩니다.  
  
- `SN_INFLAG_FORCE_VER` (0x00000001)-레지스트리 설정을 재정의 해야 하는 경우에 확인이 수행 합니다.  
  
- `SN_INFLAG_INSTALL` (0x00000002)-이 이미지에서 수행 된 첫 번째 확인 작업 임을 지정 합니다.  
  
- `SN_INFLAG_ADMIN_ACCESS` (0x00000004)-캐시는 관리 권한이 있는 사용자만 액세스할 수 있도록 지정 합니다.  
  
- `SN_INFLAG_USER_ACCESS` (0x00000008)-어셈블리는 현재 사용자만 액세스할 수 있도록 지정 합니다.  
  
- `SN_INFLAG_ALL_ACCESS` (0x00000010)-캐시의 액세스 제한이 않음을 지정 합니다.  
  
- `SN_INFLAG_RUNTIME` (0x80000000)-내부 디버깅을 위해 예약 되어 있습니다.  
  
 `pdwOutFlags`  
 [out] 출력 추가 정보에 대 한 플래그입니다. 다음 값을 사용할 수 있습니다.  
  
- `SN_OUTFLAG_WAS_VERIFIED` (0x00000001)-이 값 설정할지 `false` 레지스트리 설정으로 인해 확인이 성공 했는지를 지정 합니다.  
  
## <a name="return-value"></a>반환 값  
 `S_OK` 메서드가 성공적으로 완료 하는 경우 그렇지 않으면 실패를 나타내는 HRESULT 값을 (참조 [일반적인 HRESULT 값](https://go.microsoft.com/fwlink/?LinkId=213878) 목록에 대 한).  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MetaHost.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRStrongName 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
