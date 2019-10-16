---
title: IMetaDataImport::FindMethod 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindMethod
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindMethod
helpviewer_keywords:
- FindMethod method [.NET Framework metadata]
- IMetaDataImport::FindMethod method [.NET Framework metadata]
ms.assetid: 0f9bde1d-e306-438d-941b-d0925b322304
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4225794740b7786c6f758c9a0953d323c31a1081
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782484"
---
# <a name="imetadataimportfindmethod-method"></a>IMetaDataImport::FindMethod 메서드
토큰을 가져옵니다 methoddef 묶여 있는 메서드에 대 한 지정 된 <xref:System.Type> 지정 된 이름 및 메타 데이터 서명을 하 고 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT FindMethod (  
   [in]  mdTypeDef          td,  
   [in]  LPCWSTR            szName,   
   [in]  PCCOR_SIGNATURE    pvSigBlob,   
   [in]  ULONG              cbSigBlob,   
   [out] mdMethodDef        *pmb  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `td`  
 [in] `mdTypeDef` 검색할 멤버를 포함 하는 형식 (클래스 또는 인터페이스)에 대 한 토큰입니다. 이 값이 `mdTokenNil`, 다음 전역 함수에 대 한 조회가 수행 됩니다.  
  
 `szName`  
 [in] 검색할 메서드의 이름입니다.  
  
 `pvSigBlob`  
 [in] 메서드 서명의 이진 메타 데이터에 대 한 포인터입니다.  
  
 `cbSigBlob`  
 [in] 크기 (바이트) `pvSigBlob`합니다.  
  
 `pmb`  
 [out] 일치 하는 MethodDef 토큰에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 바깥쪽 클래스 또는 인터페이스를 사용 하는 메서드를 지정 (`td`), 해당 이름 (`szName`), 및 해당 서명 필요에 따라 (`pvSigBlob`). 클래스 또는 인터페이스에서 동일한 이름 가진 여러 메서드가 있을 수 있습니다. 이 경우 고유한 일치 항목을 찾을 메서드 시그니처를 전달 합니다.  
  
 에 전달 된 서명을 `FindMethod` 시그니처는 특정 범위에 바인딩되므로 현재 범위에서 생성 해야 합니다. 시그니처는 바깥쪽 클래스 또는 값 형식을 식별 하는 토큰을 포함할 수 있습니다. 토큰은 로컬 TypeDef 테이블의 인덱스입니다. 현재 범위의 컨텍스트 외부 런타임 시그니처를 만들어 없으며를 사용 하 여 해당 서명을 입력으로 `FindMethod`입니다.  
  
 `FindMethod` 클래스 또는 인터페이스에서 직접 정의 된 메서드를만 찾습니다. 상속 된 메서드를 찾지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Reflection.MethodInfo>
- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
