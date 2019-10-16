---
title: IMetaDataAssemblyEmit::DefineAssemblyRef 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyEmit.DefineAssemblyRef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyEmit::DefineAssemblyRef
helpviewer_keywords:
- DefineAssemblyRef method [.NET Framework metadata]
- IMetaDataAssemblyEmit::DefineAssemblyRef method [.NET Framework metadata]
ms.assetid: 0b284b18-0084-4b3a-912a-5ebe9f29c88b
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c150f4bda901627fc21ed54926c3cf959bb829a3
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67776298"
---
# <a name="imetadataassemblyemitdefineassemblyref-method"></a>IMetaDataAssemblyEmit::DefineAssemblyRef 메서드
이 어셈블리가 참조하는 어셈블리에 대한 메타데이터를 포함하는 `AssemblyRef` 구조를 만들고 연결된 메타데이터 토큰을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT DefineAssemblyRef (  
    [in]  void                *pbPublicKeyOrToken,  
    [in]  ULONG               cbPublicKeyOrToken,  
    [in]  LPCWSTR             szName,  
    [in]  ASSEMBLYMETADATA    pMetaData,  
    [in]  void                *pbHashValue,  
    [in]  ULONG               cbHashValue,  
    [in]  DWORD               dwAssemblyRefFlags,  
    [out] mdAssemblyRef       *pmdar  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pbPublicKeyOrToken`  
 [in] 참조 된 어셈블리의 게시자의 공개 키입니다. 도우미 함수 [StrongNameTokenFromAssembly](../../../../docs/framework/unmanaged-api/strong-naming/strongnametokenfromassembly-function.md) 이 매개 변수로 전달 하는 공개 키의 해시를 가져오는 데 사용할 수 있습니다.  
  
 `cbPublicKeyOrToken`  
 [in] 크기 (바이트) `pbPublicKeyOrToken`합니다.  
  
 `szName`  
 [in] 어셈블리의 사람이 읽을 수 있는 텍스트 이름입니다. 이 값은 1024 자를 초과할 수 없습니다.  
  
 `pMetaData`  
 [in] 참조 된 어셈블리의 버전, 플랫폼 및 로캘 정보를 포함 하는 ASSEMBLYMETADATA 인스턴스.  
  
 `pbHashValue`  
 [in] 참조 된 어셈블리와 연결 된 해시 데이터입니다. 선택 사항입니다.  
  
 `cbHashValue`  
 [in] 크기 (바이트) `pbHashValue`합니다.  
  
 `dwAssemblyRefFlags`  
 [in] 비트 조합 [CorAssemblyFlags](../../../../docs/framework/unmanaged-api/metadata/corassemblyflags-enumeration.md) 실행 엔진의 동작에 영향을 주는 값입니다.  
  
 `pmdar`  
 [out] 반환 된 포인터 `AssemblyRef` 메타 데이터 토큰입니다.  
  
## <a name="remarks"></a>설명  
 하나의 `AssemblyRef` 이 어셈블리가 참조 하는 각 어셈블리에 대 한 메타 데이터 구조를 정의 해야 합니다.  
  
 런타임 시 참조 된 어셈블리의 세부 정보는 "있는 그대로" 작성"정보를 나타내는 표시를 사용 하 여 어셈블리 확인자에 전달 됩니다. 어셈블리 확인자는 다음 정책을 적용합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataAssemblyEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md)
