---
title: StrongNameGetPublicKey 함수
ms.date: 03/30/2017
api_name:
- StrongNameGetPublicKey
api_location:
- mscoree.dll
- mscorsn.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameGetPublicKey
helpviewer_keywords:
- StrongNameGetPublicKey function [.NET Framework strong naming]
ms.assetid: 5b58c87f-3f72-40df-9b9a-291076931cc3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ae87ebd0b8225f14ca029fac80528d47f5a866cf
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70799065"
---
# <a name="strongnamegetpublickey-function"></a>StrongNameGetPublicKey 함수
퍼블릭/퍼블릭 키 쌍에서 퍼블릭 키를 가져옵니다. 키 쌍은 CSP (암호화 서비스 공급자) 내에서 키 컨테이너 이름으로 제공 되거나 원시 바이트 컬렉션으로 제공 될 수 있습니다.  
  
 이 함수는 더 이상 사용 되지 않습니다. 대신 [ICLRStrongName:: StrongNameGetPublicKey](../hosting/iclrstrongname-strongnamegetpublickey-method.md) 메서드를 사용 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
BOOLEAN StrongNameGetPublicKey (   
    [in]  LPCWSTR   szKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbPublicKeyBlob,  
    [out] ULONG     *pcbPublicKeyBlob  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `szKeyContainer`  
 진행 공개/개인 키 쌍을 포함 하는 키 컨테이너의 이름입니다. `pbKeyBlob` 가`szKeyContainer` null 인 경우는 CSP 내에서 유효한 컨테이너를 지정 해야 합니다. 이 경우 `StrongNameGetPublicKey` 는 컨테이너에 저장 된 키 쌍에서 공개 키를 추출 합니다.  
  
 가 `pbKeyBlob` null이 아닌 경우 키 쌍은 키 BLOB (binary large object)에 포함 된 것으로 간주 됩니다.  
  
 키는 1024 비트 RSA (Rivest Rivest-shamir-adleman Rivest-shamir-adleman) 서명 키 여야 합니다. 지금은 다른 유형의 키를 지원 하지 않습니다.  
  
 `pbKeyBlob`  
 진행 공개/개인 키 쌍에 대 한 포인터입니다. 이 쌍은 Win32 `CryptExportKey` 함수에서 만든 형식입니다. 가 `pbKeyBlob` null 인 경우에 `szKeyContainer` 지정 된 키 컨테이너는 키 쌍을 포함 하는 것으로 간주 됩니다.  
  
 `cbKeyBlob`  
 진행 의 `pbKeyBlob`크기 (바이트)입니다.  
  
 `ppbPublicKeyBlob`  
 제한이 반환 된 공개 키 BLOB입니다. 매개 `ppbPublicKeyBlob` 변수는 공용 언어 런타임에 의해 할당 되 고 호출자에 게 반환 됩니다. 호출자는 [StrongNameFreeBuffer](strongnamefreebuffer-function.md) 함수를 사용 하 여 메모리를 해제 해야 합니다.  
  
 `pcbPublicKeyBlob`  
 제한이 반환 된 공개 키 BLOB의 크기입니다.  
  
## <a name="return-value"></a>반환 값  
 `true`성공적으로 완료 되 면 그렇지 않으면 `false`입니다.  
  
## <a name="remarks"></a>설명  
 공개 키가 [PublicKeyBlob](publickeyblob-structure.md) 구조에 포함 되어 있습니다.  
  
 `StrongNameGetPublicKey`함수가 성공적으로 완료되지 않으면 [StrongNameErrorInfo](strongnameerrorinfo-function.md) 함수를 호출하여 마지막으로 생성된 오류를 검색합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** StrongName.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [StrongNameGetPublicKey 메서드](../hosting/iclrstrongname-strongnamegetpublickey-method.md)
- [StrongNameTokenFromPublicKey 메서드](../hosting/iclrstrongname-strongnametokenfrompublickey-method.md)
- [ICLRStrongName 인터페이스](../hosting/iclrstrongname-interface.md)
- [PublicKeyBlob 구조체](publickeyblob-structure.md)
