---
title: IMetaDataAssemblyImport::GetAssemblyRefProps 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.GetAssemblyRefProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::GetAssemblyRefProps
helpviewer_keywords:
- IMetaDataAssemblyImport::GetAssemblyRefProps method [.NET Framework metadata]
- GetAssemblyRefProps method [.NET Framework metadata]
ms.assetid: 5c6b7fb4-cbca-4479-b650-ab9a99732ea0
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: aa633d554652050af51065e11221f898b34d5c63
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67772676"
---
# <a name="imetadataassemblyimportgetassemblyrefprops-method"></a>IMetaDataAssemblyImport::GetAssemblyRefProps 메서드
지정 된 메타 데이터 서명 사용 하 여 어셈블리 참조에 대 한 속성 집합을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetAssemblyRefProps (  
    [in]  mdAssemblyRef        mdar,   
    [out] const void          **ppbPublicKeyOrToken,   
    [out] ULONG                *pcbPublicKeyOrToken,   
    [out] LPWSTR               szName,   
    [in]  ULONG                cchName,   
    [out] ULONG                *pchName,   
    [out] ASSEMBLYMETADATA     *pMetaData,   
    [out] const void           **ppbHashValue,   
    [out] ULONG                *pcbHashValue,   
    [out] DWORD                *pdwAssemblyRefFlags  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `mdar`  
 [in] `mdAssemblyRef` 메타 데이터 토큰을 가져올 속성에 대 한 어셈블리 참조를 나타내는입니다.  
  
 `ppbPublicKeyOrToken`  
 [out] 공개 키 또는 메타 데이터 토큰에 대 한 포인터입니다.  
  
 `pcbPublicKeyOrToken`  
 [out] 반환 된 공개 키 또는 토큰의 바이트 수입니다.  
  
 `szName`  
 [out] 어셈블리의 단순한 이름입니다.  
  
 `cchName`  
 [in] 와이드 문자에서 크기의 `szName`합니다.  
  
 `pchName`  
 [out] 에 실제로 반환 된 와이드 문자 수에 대 한 포인터 `szName`합니다.  
  
 `pMetaData`  
 [out] 어셈블리 메타 데이터를 포함 하는 ASSEMBLYMETADATA 구조체에 대 한 포인터입니다.  
  
 `ppbHashValue`  
 [out] 해시 값에 대 한 포인터입니다. Sha-1 알고리즘을 사용 하는 해시입니다를 `PublicKey` 의 플래그는 arfFullOriginator 하지 않으면 참조 되는 어셈블리의 속성을 [AssemblyRefFlags](../../../../docs/framework/unmanaged-api/metadata/assemblyrefflags-enumeration.md) 열거형 설정 됩니다.  
  
 `pcbHashValue`  
 [out] 반환 된 해시 값에 와이드 문자 수입니다.  
  
 `pdwAssemblyRefFlags`  
 [out] 어셈블리에 적용 하는 메타 데이터를 설명 하는 플래그에 대 한 포인터입니다. 플래그 값은 하나 이상의 조합 [CorAssemblyFlags](../../../../docs/framework/unmanaged-api/metadata/corassemblyflags-enumeration.md) 값입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드가 반환 되 고 성공 하면 s_ok이 고 그렇지 않은 경우 Winerror.h 헤더 파일에 정의 된 오류 코드 중 하나 반환 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataAssemblyImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyimport-interface.md)
