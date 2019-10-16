---
title: StrongNameGetPublicKeyEx 메서드
ms.date: 03/30/2017
api_name:
- ICLRStrongName2.StrongNameGetPublicKeyEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- StrongNameGetPublicKeyEx
helpviewer_keywords:
- StrongNameGetPublicKeyEx method, ICLRStrongName2 interface [.NET Framework hosting]
- ICLRStrongName2::StrongNameGetPublicKeyEx method [.NET Framework hosting]
ms.assetid: 63d8260c-fb32-4f8f-a357-768afd570f68
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 36ff06b4bbe916e7038840d9bf3cbc455f161b70
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67768306"
---
# <a name="strongnamegetpublickeyex-method"></a>StrongNameGetPublicKeyEx 메서드
공개/개인 키 쌍에서 공개 키를 가져옵니다 하 고 해시 알고리즘 및 서명 알고리즘을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT StrongNameGetPublicKey (   
    [in]  LPCWSTR   pwzKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbPublicKeyBlob,  
    [out] ULONG     *pcbPublicKeyBlob  
    [in]  ULONG     uHashAlgId,  
    [in]  ULONG     uReserved,  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pwzKeyContainer`  
 [in] 공개/개인 키 쌍을 포함 하는 키 컨테이너의 이름입니다. 하는 경우 `pbKeyBlob` 이 null 이면 `szKeyContainer` 암호화 서비스 공급자 (CSP) 내에서 유효한 컨테이너를 지정 해야 합니다. 이 경우에 `StrongNameGetPublicKeyEx` 메서드 컨테이너에 저장 된 키 쌍에서 공개 키를 추출 합니다.  
  
 경우 `pbKeyBlob` null이 아니면 키 쌍 가정 키 binary large object (BLOB)에 포함 되어야 합니다.  
  
 키에는 1024 비트 adleman의 Rivest-Shamir (RSA) 키를 서명 해야 합니다. 다른 종류의 키이 이번에 지원 됩니다.  
  
 `pbKeyBlob`  
 [in] 공개/개인 키 쌍에 대 한 포인터입니다. 이 쌍이 win32 만들어진 형식을 `CryptExportKey` 함수입니다. 하는 경우 `pbKeyBlob` 가 null 이면 지정 된 키 컨테이너 `szKeyContainer` 키 쌍을 포함 하도록 간주 됩니다.  
  
 `cbKeyBlob`  
 [in] 크기 (바이트)의 `pbKeyBlob`합니다.  
  
 `ppbPublicKeyBlob`  
 [out] 반환 된 공개 키 BLOB입니다. `ppbPublicKeyBlob` 매개 변수는 공용 언어 런타임에 의해 할당 되 고 호출자에 게 반환 합니다. 호출자에 게 사용 하 여 메모리를 해제 해야 합니다 [iclrstrongname:: Strongnamefreebuffer](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamefreebuffer-method.md) 메서드.  
  
 `pcbPublicKeyBlob`  
 [out] 반환 된 공개 키 BLOB의 크기입니다.  
  
 `uHashAlgId`  
 [in] 어셈블리 해시 알고리즘입니다. 허용 되는 값의 목록은 설명 섹션을 참조 하세요.  
  
 `uReserved`  
 [in] 사용 하도록 예약 됩니다. 기본값은 null입니다.  
  
## <a name="return-value"></a>반환 값  
 `S_OK` 메서드가 성공적으로 완료 하는 경우 그렇지 않으면 실패를 나타내는 HRESULT 값을 (참조 [일반적인 HRESULT 값](https://go.microsoft.com/fwlink/?LinkId=213878) 목록에 대 한).  
  
## <a name="remarks"></a>설명  
 공개 키에 포함 된 [PublicKeyBlob](../../../../docs/framework/unmanaged-api/strong-naming/publickeyblob-structure.md) 구조입니다.  
  
## <a name="remarks"></a>설명  
 다음 테이블에 대 한 허용 되는 값 집합을 보여 줍니다.는 `uHashAlgId` 매개 변수입니다.  
  
|이름|값|  
|----------|-----------|  
|없음|0|  
|SHA-1|0x8004|  
|SHA-256|0x800c|  
|SHA-384|0x800d|  
|SHA-512|0x800e|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MetaHost.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [StrongNameTokenFromPublicKey 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnametokenfrompublickey-method.md)
- [PublicKeyBlob 구조체](../../../../docs/framework/unmanaged-api/strong-naming/publickeyblob-structure.md)
- [ICLRStrongName 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
- [StrongNameGetPublicKey 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamegetpublickey-method.md)
