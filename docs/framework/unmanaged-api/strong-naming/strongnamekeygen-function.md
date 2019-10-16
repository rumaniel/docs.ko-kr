---
title: StrongNameKeyGen 함수
ms.date: 03/30/2017
api_name:
- StrongNameKeyGen
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameKeyGen
helpviewer_keywords:
- StrongNameKeyGen function [.NET Framework strong naming]
ms.assetid: 883e413a-ad2f-4f7f-b1b9-aeb8fe5b65f8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f062f47790136e8cd39c6751b7c75eef660c2b9a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70799145"
---
# <a name="strongnamekeygen-function"></a>StrongNameKeyGen 함수
강력한 이름 사용을 위한 새 퍼블릭/프라이빗 키 쌍을 만듭니다.  
  
 이 함수는 더 이상 사용 되지 않습니다. 대신 [ICLRStrongName:: StrongNameKeyGen](../hosting/iclrstrongname-strongnamekeygen-method.md) 메서드를 사용 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
BOOLEAN StrongNameKeyGen (  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  DWORD     dwFlags,  
    [out] BYTE      **ppbKeyBlob,  
    [out] ULONG     *pcbKeyBlob  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `wszKeyContainer`  
 진행 요청 된 키 컨테이너 이름입니다. `wszKeyContainer`임시 이름을 생성 하려면 비어 있지 않은 문자열 이거나 null 이어야 합니다.  
  
 `dwFlags`  
 진행 키를 등록 된 상태로 유지할지 여부를 지정 합니다. 다음 값이 지원 됩니다.  
  
- 0x00000000-임시 키 `wszKeyContainer` 컨테이너 이름을 생성 하기 위해가 null 일 때 사용 됩니다.  
  
- 0x00000001 (`SN_LEAVE_KEY`)-키를 등록 된 상태로 유지 하도록 지정 합니다.  
  
 `ppbKeyBlob`  
 제한이 반환 된 공개/개인 키 쌍입니다.  
  
 `pcbKeyBlob`  
 제한이 의 `ppbKeyBlob`크기 (바이트)입니다.  
  
## <a name="return-value"></a>반환 값  
 `true`성공적으로 완료 되 면 그렇지 않으면 `false`입니다.  
  
## <a name="remarks"></a>설명  
 함수 `StrongNameKeyGen` 는 1024 비트 키를 만듭니다. 키를 검색 한 후에는 [StrongNameFreeBuffer](strongnamefreebuffer-function.md) 함수를 호출 하 여 할당 된 메모리를 해제 해야 합니다.  
  
 `StrongNameKeyGen` 함수가 성공적으로 완료되지 않으면 [StrongNameErrorInfo](strongnameerrorinfo-function.md) 함수를 호출하여 마지막으로 생성된 오류를 검색합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** StrongName.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [StrongNameKeyGen 메서드](../hosting/iclrstrongname-strongnamekeygen-method.md)
- [StrongNameKeyGenEx 메서드](../hosting/iclrstrongname-strongnamekeygenex-method.md)
- [ICLRStrongName 인터페이스](../hosting/iclrstrongname-interface.md)
