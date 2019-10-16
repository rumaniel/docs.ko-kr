---
title: IMetaDataEmit::DefineTypeRefByName 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineTypeRefByName
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineTypeRefByName
helpviewer_keywords:
- DefineTypeRefByName method [.NET Framework metadata]
- IMetaDataEmit::DefineTypeRefByName method [.NET Framework metadata]
ms.assetid: c30a4ce3-2d3e-411a-98df-e62ac4a5dd50
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f005ee9d3d9d4b8977cd6a1838fe46015e604df5
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67777474"
---
# <a name="imetadataemitdefinetyperefbyname-method"></a>IMetaDataEmit::DefineTypeRefByName 메서드
현재 범위 외부에 지정된 된 범위에 정의 된 형식에 대 한 메타 데이터를 토큰을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT DefineTypeRefByName (   
    [in]  mdToken     tkResolutionScope,   
    [in]  LPCWSTR     szName,   
    [out] mdTypeRef   *ptr   
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `tkResolutionScope`  
 [in] 결정 범위를 지정 하는 토큰입니다. 유효한 토큰 형식은 같습니다.  
  
- `mdModuleRef`호출자가 정의 된 동일한 어셈블리에서 형식 정의 된 경우.  
  
- `mdAssemblyRef`호출자가 정의 된 것 이외의 어셈블리에서 형식 정의 된 경우.  
  
- `mdTypeRef`에 형식이 중첩된 형식이 면 합니다.  
  
- `mdModule`호출자가 정의 된 동일한 모듈에는 형식이 정의 된 경우.  
  
- 전역적으로 정의 된 경우 null입니다.  
  
 `szName`  
 [in] 유니코드에 대상 형식의 이름입니다.  
  
 `ptr`  
 [out] 에 대 한 포인터를 `mdTypeRef` 형식에 할당 되는 토큰입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MSCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
