---
title: IMapToken::Map 메서드
ms.date: 03/30/2017
api_name:
- IMapToken.Map
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMapToken::Map
helpviewer_keywords:
- IMapToken::Map method [.NET Framework metadata]
- Map method [.NET Framework metadata]
ms.assetid: b9b4bf2f-1098-43d6-9619-a99b4bda1940
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8ac12d5b6bc2911e3bd879285a9a12f65c426f0d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67745862"
---
# <a name="imaptokenmap-method"></a>IMapToken::Map 메서드
메타 데이터 서명을 사용 하 여 어셈블리 간에 관계를 매핑합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT Map (  
    [in]  mdToken tkImp,   
    [in]  mdToken tkEmit  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `tkImp`  
 [in] 가져온된 코드 개체를 나타내는 메타 데이터 토큰입니다.  
  
 `tkEmit`  
 [in] 내보낸된 코드가 개체를 나타내는 메타 데이터 토큰입니다.  
  
## <a name="remarks"></a>설명  
 토큰 다시 매핑하는 경우 병합 하는 동안 가져온된 (원본) 메타 데이터 범위에서 사용 하는 원래 토큰에서 범위를 지정 하 고 내보낸된 (대상) 메타 데이터 범위에서 사용 하는 새 토큰에서 범위를 지정 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMapToken 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imaptoken-interface.md)
