---
title: IMetaDataImport::GetPropertyProps 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetPropertyProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetPropertyProps
helpviewer_keywords:
- GetPropertyProps method [.NET Framework metadata]
- IMetaDataImport::GetPropertyProps method [.NET Framework metadata]
ms.assetid: dc0ff3e6-7e7d-4f6c-948d-52b28f5cb78c
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e83afcf6c872927e614fce33ca96e93f0da4f497
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67778879"
---
# <a name="imetadataimportgetpropertyprops-method"></a>IMetaDataImport::GetPropertyProps 메서드
지정 된 토큰에 의해 표현 되는 속성에 대 한 메타 데이터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetPropertyProps (  
   [in]  mdProperty        prop,  
   [out] mdTypeDef         *pClass,   
   [out] LPCWSTR           szProperty,   
   [in]  ULONG             cchProperty,   
   [out] ULONG             *pchProperty,   
   [out] DWORD             *pdwPropFlags,   
   [out] PCCOR_SIGNATURE   *ppvSig,   
   [out] ULONG             *pbSig,   
   [out] DWORD             *pdwCPlusTypeFlag,   
   [out] UVCP_CONSTANT     *ppDefaultValue,  
   [out] ULONG             *pcchDefaultValue,  
   [out] mdMethodDef       *pmdSetter,   
   [out] mdMethodDef       *pmdGetter,   
   [out] mdMethodDef       rmdOtherMethod[],  
   [in]  ULONG             cMax,   
   [out] ULONG             *pcOtherMethod   
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `prop`  
 [in] 에 대 한 메타 데이터를 반환할 속성을 나타내는 토큰입니다.  
  
 `pClass`  
 [out] 속성을 구현 하는 형식을 나타내는 TypeDef 토큰에 대 한 포인터입니다.  
  
 `szProperty`  
 [out] 속성 이름을 저장할 버퍼입니다.  
  
 `cchProperty`  
 [in] 와이드 문자에서 크기 `szProperty`합니다.  
  
 `pchProperty`  
 [out] 반환 하는 와이드 문자 수가 `szProperty`합니다.  
  
 `pdwPropFlags`  
 [out] 속성에 적용할 특성 플래그에 대 한 포인터입니다. 이 값은의 비트 마스크를 [CorPropertyAttr](../../../../docs/framework/unmanaged-api/metadata/corpropertyattr-enumeration.md) 열거형입니다.  
  
 `ppvSig`  
 [out] 속성의 메타 데이터 서명에 대 한 포인터입니다.  
  
 `pbSig`  
 [out] 반환 된 바이트 수가 `ppvSig`합니다.  
  
 `pdwCPlusTypeFlag`  
 [out] 속성의 기본값은 상수의 형식을 지정 하는 플래그입니다. CorElementType 열거형에서이 값은입니다.  
  
 `ppDefaultValue`  
 [out] 이 속성의 기본값을 저장 하는 바이트에 대 한 포인터입니다.  
  
 `pcchDefaultValue`  
 [out] 와이드 문자에서 크기 `ppDefaultValue`이면 `pdwCPlusTypeFlag` ELEMENT_TYPE_STRING;은 그렇지 않은 경우이 값은 관계가 없습니다. 이런 경우, 길이의 `ppDefaultValue` 에 지정 된 형식에서 유추 됩니다 `pdwCPlusTypeFlag`합니다.  
  
 `pmdSetter`  
 [out] 속성에 대 한 set 접근자 메서드를 나타내는 MethodDef 토큰에 대 한 포인터입니다.  
  
 `pmdGetter`  
 [out] 속성의 get 접근자 메서드를 나타내는 MethodDef 토큰에 대 한 포인터입니다.  
  
 `rmdOtherMethod`  
 [out] 배열 속성에 연결 된 다른 메서드를 나타내는 MethodDef 토큰입니다.  
  
 `cMax`  
 [in] `rmdOtherMethod` 배열의 최대 크기입니다. 모든 메서드를 포함할 수 있는 크기 배열의 얻을 수 없는 경우 경고 없이 건너뜁니다.  
  
 `pcOtherMethod`  
 [out] MethodDef 토큰에서 반환 된 수가 `rmdOtherMethod`합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
