---
title: IMetaDataImport::FindField 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindField
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindField
helpviewer_keywords:
- IMetaDataImport::FindField method [.NET Framework metadata]
- FindField method [.NET Framework metadata]
ms.assetid: 38cd4e16-fbb2-471c-aa73-ac51a1931ad2
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1baee71b5b8575f51eb54fbc8a037a5dddd24500
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782533"
---
# <a name="imetadataimportfindfield-method"></a>IMetaDataImport::FindField 메서드
에 포인터를 가져옵니다 FieldDef 토큰 포함 되는 필드에 대 한 지정 된 <xref:System.Type> 지정 된 이름 및 메타 데이터 서명을 하 고 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT FindField (  
   [in]  mdTypeDef         td,  
   [in]  LPCWSTR           szName,  
   [in]  PCCOR_SIGNATURE   pvSigBlob,  
   [in]  ULONG             cbSigBlob,  
   [out] mdFieldDef        *pmb  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `td`  
 [in] 클래스 또는 검색할 필드를 포함 하는 인터페이스에 대 한 TypeDef 토큰입니다. 이 값이 `mdTokenNil`, 전역 변수에 대 한 조회가 수행 됩니다.  
  
 `szName`  
 [in] 검색할 필드의 이름입니다.  
  
 `pvSigBlob`  
 [in] 필드의 이진 메타 데이터 서명에 대 한 포인터입니다.  
  
 `cbSigBlob`  
 [in] 크기 (바이트) `pvSigBlob`합니다.  
  
 `pmb`  
 [out] 일치 하는 FieldDef 토큰에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 바깥쪽 클래스 또는 인터페이스를 사용 하 여 필드를 지정 했습니다 (`td`), 해당 이름 (`szName`), 및 해당 서명 필요에 따라 (`pvSigBlob`).  
  
 에 전달 된 서명을 `FindField` 시그니처는 특정 범위에 바인딩되므로 현재 범위에서 생성 해야 합니다. 시그니처는 바깥쪽 클래스 또는 값 형식을 식별 하는 토큰을 포함할 수 있습니다. (토큰은 로컬 TypeDef 테이블에 인덱스). 현재 범위의 컨텍스트 외부 런타임 시그니처를 한에 대 한 입력으로 사용할 수는 없습니다 `FindField`합니다.  
  
 `FindField` 클래스 또는 인터페이스에서 직접 정의 된 필드만을 찾습니다. 상속 된 필드는 찾지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
