---
title: IMetaDataImport::FindMemberRef 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindMemberRef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindMemberRef
helpviewer_keywords:
- IMetaDataImport::FindMemberRef method [.NET Framework metadata]
- FindMemberRef method [.NET Framework metadata]
ms.assetid: 1ccda329-d752-4d89-abe8-511af3c3f4c9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0d446e2b78f41d43aa70f429e23f1f4be22fd799
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782503"
---
# <a name="imetadataimportfindmemberref-method"></a>IMetaDataImport::FindMemberRef 메서드
지정 된로 묶인 멤버에 대 한 MemberRef 토큰에 대 한 포인터는 참조를 가져옵니다 <xref:System.Type> 지정 된 이름 및 메타 데이터 서명을 하 고 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT FindMemberRef (  
   [in]  mdTypeRef          td,  
   [in]  LPCWSTR            szName,   
   [in]  PCCOR_SIGNATURE    pvSigBlob,   
   [in]  ULONG              cbSigBlob,   
   [out] mdMemberRef        *pmr  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `td`  
 [in] 클래스 또는 인터페이스에 대 한 검색에 대 한 멤버 참조를 포함 하는 TypeRef 토큰입니다. 이 값이 `mdTokenNil`, 전역 변수 또는 전역 함수 참조에 대 한 조회가 수행 됩니다.  
  
 `szName`  
 [in] 검색할 멤버 참조의 이름입니다.  
  
 `pvSigBlob`  
 [in] 멤버 참조가 이진 메타 데이터 서명의 포인터입니다.  
  
 `cbSigBlob`  
 [in] 크기 (바이트) `pvSigBlob`합니다.  
  
 `pmr`  
 [out] 일치 하는 MemberRef 토큰에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 바깥쪽 클래스 또는 인터페이스를 사용 하 여 멤버를 지정할 수 (`td`), 해당 이름 (`szName`), 및 해당 서명 필요에 따라 (`pvSigBlob`).  
  
 에 전달 된 서명을 `FindMemberRef` 시그니처는 특정 범위에 바인딩되므로 현재 범위에서 생성 해야 합니다. 시그니처는 바깥쪽 클래스 또는 값 형식을 식별 하는 토큰을 포함할 수 있습니다. 토큰은 로컬 TypeDef 테이블의 인덱스입니다. 현재 범위의 컨텍스트 외부 런타임 시그니처를 한에 대 한 입력으로 사용할 수는 없습니다 `FindMemberRef`합니다.  
  
 `FindMemberRef` 클래스 또는 인터페이스에서 직접 정의 된 멤버 참조를 찾습니다. 상속 된 멤버 참조를 찾지는 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
