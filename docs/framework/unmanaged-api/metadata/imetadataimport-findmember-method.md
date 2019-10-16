---
title: IMetaDataImport::FindMember 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindMember
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindMember
helpviewer_keywords:
- IMetaDataImport::FindMember method [.NET Framework metadata]
- FindMember method [.NET Framework metadata]
ms.assetid: ad32fb84-c2b6-41cd-888d-787ff3a90449
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4eefb7ec1e7d0d130ec64531a59d1d5bbce04963
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968929"
---
# <a name="imetadataimportfindmember-method"></a>IMetaDataImport::FindMember 메서드
지정 된로 <xref:System.Type> 묶고 지정 된 이름과 메타 데이터 시그니처가 있는 필드 또는 메서드에 대 한 MemberDef 토큰에 대 한 포인터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT FindMember (  
   [in]  mdTypeDef         td,  
   [in]  LPCWSTR           szName,   
   [in]  PCCOR_SIGNATURE   pvSigBlob,   
   [in]  ULONG             cbSigBlob,   
   [out] mdToken           *pmb  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `td`  
 진행 검색할 멤버를 둘러싸는 클래스 또는 인터페이스의 TypeDef 토큰입니다. 이 값 `mdTokenNil`이 이면 전역 변수나 전역 함수에 대 한 조회가 수행 됩니다.  
  
 `szName`  
 진행 검색할 멤버의 이름입니다.  
  
 `pvSigBlob`  
 진행 멤버의 이진 메타 데이터 서명에 대 한 포인터입니다.  
  
 `cbSigBlob`  
 진행 의 `pvSigBlob`크기 (바이트)입니다.  
  
 `pmb`  
 제한이 일치 하는 MemberDef 토큰에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 바깥쪽 클래스 또는 인터페이스 (`td`), 이름 (`szName`) 및 선택적으로 시그니처 (`pvSigBlob`)를 사용 하 여 멤버를 지정 합니다. 클래스 또는 인터페이스에 이름이 같은 멤버가 여러 개 있을 수 있습니다. 이 경우 멤버의 시그니처를 전달 하 여 고유한 일치 항목을 찾습니다.  
  
 서명이 특정 범위에 `FindMember` 바인딩되기 때문에에 전달 된 시그니처는 현재 범위에서 생성 되어야 합니다. 시그니처에는 바깥쪽 클래스 또는 값 형식을 식별 하는 토큰이 포함 될 수 있습니다. 토큰은 로컬 TypeDef 테이블의 인덱스입니다. 현재 범위의 컨텍스트 외부에서 런타임 서명을 작성 하 고 해당 시그니처를 입력을 `FindMember`위한 입력으로 사용할 수 없습니다.  
  
 `FindMember`클래스 또는 인터페이스에서 직접 정의 된 멤버만 찾습니다. 상속 된 멤버를 찾을 수 없습니다.  
  
> [!NOTE]
> `FindMember`는 도우미 메서드입니다. [IMetaDataImport:: FindMethod;를](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-findmethod-method.md)호출 합니다. 해당 호출에서 일치 하는 항목을 찾지 `FindMember` 못하면은 [IMetaDataImport:: findfield](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-findfield-method.md)를 호출 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
