---
title: IMetaDataEmit::DefineProperty 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineProperty
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineProperty
helpviewer_keywords:
- IMetaDataEmit::DefineProperty method [.NET Framework metadata]
- DefineProperty method [.NET Framework metadata]
ms.assetid: 5c4c1dc2-d40d-4173-bbe6-7058fb21c98f
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 69b398fa003abc0dba00ee89a9bb911a8c2dd6df
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67777508"
---
# <a name="imetadataemitdefineproperty-method"></a>IMetaDataEmit::DefineProperty 메서드
지정 된 지정된 된 형식에 대 한 속성 정의 만듭니다 `get` 및 `set` 메서드 접근자는 속성 정의에 대 한 토큰을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT DefineProperty (   
    [in]  mdTypeDef          td,   
    [in]  LPCWSTR            szProperty,   
    [in]  DWORD              dwPropFlags,   
    [in]  PCCOR_SIGNATURE    pvSig,   
    [in]  ULONG              cbSig,   
    [in]  DWORD              dwCPlusTypeFlag,   
    [in]  void const         *pValue,   
    [in]  ULONG              cchValue,   
    [in]  mdMethodDef        mdSetter,   
    [in]  mdMethodDef        mdGetter,   
    [in]  mdMethodDef        rmdOtherMethods[],   
    [out] mdProperty         *pmdProp   
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `td`  
 [in] 클래스 또는 속성이 정의 되는 인터페이스에 대 한 토큰입니다.  
  
 `szProperty`  
 [in] 속성의 이름입니다.  
  
 `dwPropFlags`  
 [in] 속성 플래그입니다.  
  
 `pvSig`  
 [in] 속성 서명입니다.  
  
 `cbSig`  
 [in] 바이트 수가 `pvSig`합니다.  
  
 `dwCPlusTypeFlag`  
 [in] 형식 속성의 기본값입니다.  
  
 `pValue`  
 [in] 속성에 대 한 기본 값입니다.  
  
 `cchValue`  
 [in] \(유니코드) 수의 문자 `pValue`합니다.  
  
 `mdSetter`  
 [in] 속성 값을 설정 하는 메서드.  
  
 `mdGetter`  
 [in] 속성 값을 가져오는 메서드.  
  
 `rmdOtherMethods[]`  
 [in] 속성과 연결 된 다른 메서드는 배열입니다. 배열 종료는 `mdTokenNil`합니다.  
  
 `pmdProp`  
 [out] `mdProperty` 할당 된 토큰입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MSCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
