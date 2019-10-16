---
title: IMetaDataAssemblyEmit::DefineManifestResource 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyEmit.DefineManifestResource
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyEmit::DefineManifestResource
helpviewer_keywords:
- DefineManifestResource method [.NET Framework metadata]
- IMetaDataAssemblyEmit::DefineManifestResource method [.NET Framework metadata]
ms.assetid: 27f6d295-0fe9-4cda-b77e-6e7d5c53df09
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 781953fe5bf209f195ef4887dff45e1902741f0c
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67775313"
---
# <a name="imetadataassemblyemitdefinemanifestresource-method"></a>IMetaDataAssemblyEmit::DefineManifestResource 메서드
지정된 매니페스트 리소스에 대한 메타데이터를 포함하는 `ManifestResource` 구조를 만들고 연결된 메타데이터 토큰을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT DefineManifestResource (  
    [in] LPCWSTR                szName,   
    [in] mdToken                tkImplementation,   
    [in] DWORD                  dwOffset,   
    [in] DWORD                  dwResourceFlags,  
    [out] mdManifestResource    *pmdmr  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `szName`  
 [in] 리소스의 이름입니다.  
  
 `tkImplementation`  
 [in] 형식의 메타 데이터 토큰이 `mdtFile` 또는 `mdtAssemblyRef` 리소스 공급자에 매핑되는 합니다. NULL 값을 메타 데이터는 포함 된 리소스 공급자 임을 나타냅니다.  
  
 `dwOffset`  
 [in] 파일 내에서 리소스의 시작 오프셋입니다. 독립 실행형 파일에서 리소스에 대 한이 값은 항상 0입니다. PE (이식 가능한 실행) 파일에 포함 된 리소스, 리소스 cor.h 헤더 파일에 지정 된 위치에서 시작 하는 BLOB의 오프셋입니다.  
  
 `dwResourceFlags`  
 [in] 리소스 정의 대 한 속성 설정을 지정 하는 플래그 값의 비트 조합입니다.  
  
 `pmdmr`  
 [out] 반환 된 메타 데이터 토큰에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 하나의 `ManifestResource` 각 어셈블리의 파일에서 구현 되는 각 리소스에 대 한 메타 데이터 구조를 정의 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataAssemblyEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md)
