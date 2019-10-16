---
title: IMetaDataEmit::DefineParam 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineParam
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineParam
helpviewer_keywords:
- IMetaDataEmit::DefineParam method [.NET Framework metadata]
- DefineParam method [.NET Framework metadata]
ms.assetid: d86a3d14-4796-4909-9591-dfafe3de5ce4
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9d64a1ef21cd4fa4224609c7cd415c1611313769
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67777553"
---
# <a name="imetadataemitdefineparam-method"></a>IMetaDataEmit::DefineParam 메서드
지정한 시그니처를 지정된 된 토큰에서 참조 하는 메서드를 사용 하 여 매개 변수 정의 만들고 해당 매개 변수 정의 대 한 토큰을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT DefineParam (  
    [in]  mdMethodDef md,   
    [in]  ULONG       ulParamSeq,   
    [in]  LPCWSTR     szName,   
    [in]  DWORD       dwParamFlags,   
    [in]  DWORD       dwCPlusTypeFlag,   
    [in]  void const  *pValue,  
    [in]  ULONG       cchValue,   
    [out] mdParamDef  *ppd   
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `md`  
 [in] 매개 변수를 정의 하는 메서드에 대 한 토큰입니다.  
  
 `ulParamSeq`  
 [in] 매개 변수 시퀀스 번호입니다.  
  
 `szName`  
 [in] 유니코드에서 매개 변수의 이름입니다.  
  
 `dwParamFlags`  
 [in] 플래그 매개 변수입니다. 이 비트 마스크의 `CorParamAttr` 값입니다.  
  
 `dwCPlusTypeFlag`  
 [in] `ELEMENT_TYPE_` *\** 상수 값에 대 한 합니다.  
  
 `pValue`  
 [in] 매개 변수에 상수 값입니다.  
  
 `cchValue`  
 [in] 유니코드 문자에서 크기의 `pValue`합니다.  
  
 `ppd`  
 [out] `mdParamDef` 할당 된 토큰입니다.  
  
## <a name="remarks"></a>설명  
 시퀀스 값 `ulParamSeq` 매개 변수에 대 한 1부터 시작 합니다. 반환 값에 0의 시퀀스 번호가 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MSCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
