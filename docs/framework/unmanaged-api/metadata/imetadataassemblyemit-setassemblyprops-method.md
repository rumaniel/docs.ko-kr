---
title: IMetaDataAssemblyEmit::SetAssemblyProps 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyEmit.SetAssemblyProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyEmit::SetAssemblyProps
helpviewer_keywords:
- SetAssemblyProps method [.NET Framework metadata]
- IMetaDataAssemblyEmit::SetAssemblyProps method [.NET Framework metadata]
ms.assetid: 91b633d7-9e75-43c3-a8d2-2144984e5f9e
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 34335321207e98a518ff3e0fdb5ea1dc3ac68b75
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67776256"
---
# <a name="imetadataassemblyemitsetassemblyprops-method"></a>IMetaDataAssemblyEmit::SetAssemblyProps 메서드
지정된 `Assembly` 메타데이터 구조를 수정합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetAssemblyProps (  
    [in] mdAssembly               pma,  
    [in] const void               *pbPublicKey,  
    [in] ULONG                    cbPublicKey,  
    [in] ULONG                    ulHashAlgId,  
    [in] LPCWSTR                  szName,  
    [in] const ASSEMBLYMETADATA   *pMetaData,  
    [in] DWORD                    dwAssemblyFlags  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pma`  
 [in] 지정 된 메타 데이터 토큰을 `Assembly` 수정할 메타 데이터 구조입니다.  
  
 `pbPublicKey`  
 [in] 어셈블리의 게시자의 공개 키에 대 한 포인터입니다.  
  
 `cbPublicKey`  
 [in] 크기 (바이트) `pbPublicKey`합니다.  
  
 `ulHashAlgId`  
 [in] 어셈블리 파일을 해시 하는 데 사용 하는 해시 알고리즘의 식별자입니다.  
  
 `szName`  
 [in] 어셈블리의 사람이 읽을 수 있는 텍스트 이름입니다.  
  
 `pMetaData`  
 [in] ASSEMBLYMETADATA 어셈블리의 버전, 플랫폼 및 로캘 정보를 포함 하는 포인터입니다.  
  
 `dwAssemblyFlags`  
 [in] 비트 조합 [AssemblyFlags](../../../../docs/framework/unmanaged-api/metadata/assemblyflags-enumeration.md) 어셈블리의 다양 한 특성을 지정 하는 값입니다.  
  
## <a name="remarks"></a>설명  
 만들려는 `Assembly` 메타 데이터 구조를 사용 합니다 [imetadataassemblyemit:: Defineassembly](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-defineassembly-method.md) 메서드.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataAssemblyEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md)
