---
title: GetPublicKeyToken 메서드
ms.date: 03/30/2017
api_name:
- IALink2.GetPublicKeyToken
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- GetPublicKeyToken
helpviewer_keywords:
- GetPublicKeyToken method
ms.assetid: 4a16374c-94b0-47b0-9fed-88c2b0cdccd4
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 158ecc036d56e2ad9a3fa650677c04ebcbfd7696
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70777216"
---
# <a name="getpublickeytoken-method"></a>GetPublicKeyToken 메서드
지정 된 keyfile 또는 키 컨테이너에 대 한 공개 키 토큰을 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetPublicKeyToken(  
    LPCWSTR pszKeyFile,  
    LPCWSTR pszKeyContainer,  
    void* pvPublicKeyToken,  
    DWORD* pcbPublicKeyToken  
) PURE;  
```  
  
## <a name="parameters"></a>매개 변수  
 `pszKeyFile`  
 키의 파일 이름입니다.  
  
 `pszKeyContainer`  
 키 컨테이너의 이름입니다.  
  
 `pvPublicKeyToken`  
 키 토큰을 저장할 주소입니다.  
  
 `pcbPublicKeyToken`  
 로 `pvPublicKeyToken`표시 되는 버퍼의 크기 (바이트)를 지정 합니다. 반환 시 실제 사용 된 바이트 수를 포함 합니다.  
  
## <a name="return-value"></a>반환 값  
 메서드가 성공 하면 S_OK를 반환 합니다.  
  
## <a name="requirements"></a>요구 사항  
 Alink가 필요 합니다.  
  
## <a name="see-also"></a>참고자료

- [IALink2 인터페이스](ialink2-interface.md)
- [IALink 인터페이스](ialink-interface.md)
- [ALink API](index.md)
