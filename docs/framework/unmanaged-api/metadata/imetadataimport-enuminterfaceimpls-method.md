---
title: IMetaDataImport::EnumInterfaceImpls 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumInterfaceImpls
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumInterfaceImpls
helpviewer_keywords:
- IMetaDataImport::EnumInterfaceImpls method [.NET Framework metadata]
- EnumInterfaceImpls method [.NET Framework metadata]
ms.assetid: ba6e178f-128b-4e47-a13c-b4be73eb106c
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0d0f94949cdc82cdecd52f003f3400c43014fabf
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67780457"
---
# <a name="imetadataimportenuminterfaceimpls-method"></a>IMetaDataImport::EnumInterfaceImpls 메서드
지정 된 구현 하는 모든 인터페이스를 열거 `TypeDef`합니다. 
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT EnumInterfaceImpls (  
   [in, out]  HCORENUM       *phEnum,   
   [in]   mdTypeDef          td,  
   [out]  mdInterfaceImpl    rImpls[],   
   [in]   ULONG              cMax,  
   [out]  ULONG*             pcImpls  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `phEnum`  
 [out에서] 열거자에 대 한 포인터입니다.  
  
 `td`  
 [in] 토큰 인터페이스 구현을 나타내는 MethodDef 토큰 인 열거할는 TypeDef입니다.  
  
 `rImpls`  
 [out] MethodDef 토큰을 저장 하는 데 사용 되는 배열입니다.  
  
 `cMax`  
 [in] `rImpls` 배열의 최대 크기입니다.  
  
 `pcImpls`  
 [out] 반환 된 토큰의 실제 수 `rImpls`입니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|설명|  
|-------------|-----------------|  
|`S_OK`|`EnumInterfaceImpls` 성공적으로 반환 합니다.|  
|`S_FALSE`|열거할 MethodDef 토큰이 있습니다. 이런 경우 `pcImpls` 0으로 설정 됩니다.|  

## <a name="remarks"></a>설명

컬렉션을 반환 하는 열거형 `mdInterfaceImpl` 지정 된 구현 되는 각 인터페이스에 대 한 토큰 `TypeDef`합니다. 인터페이스 토큰 인터페이스를 지정 된 순서 대로 반환 됩니다 (통해 `DefineTypeDef` 또는 `SetTypeDefProps`). 반환 된 속성 `mdInterfaceImpl` 토큰을 사용 하 여 쿼리할 수 있습니다 [GetInterfaceImplProps](imetadataimport-getinterfaceimplprops-method.md)합니다.
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
