---
title: IMetaDataImport::ResolveTypeRef 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.ResolveTypeRef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::ResolveTypeRef
helpviewer_keywords:
- ResolveTypeRef method [.NET Framework metadata]
- IMetaDataImport::ResolveTypeRef method [.NET Framework metadata]
ms.assetid: 556bccfb-61bc-4761-b1d5-de4b1c18a38f
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f323e91e60c9735a51e955eaab6673ca167f294d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69951873"
---
# <a name="imetadataimportresolvetyperef-method"></a>IMetaDataImport::ResolveTypeRef 메서드
지정 된 <xref:System.Type> TypeRef 토큰이 나타내는 참조를 확인 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ResolveTypeRef (  
   [in]  mdTypeRef       tr,  
   [in]  REFIID          riid,  
   [out] IUnknown        **ppIScope,  
   [out] mdTypeDef       *ptd  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `tr`  
 진행 참조 된 형식 정보를 반환할 TypeRef 메타 데이터 토큰입니다.  
  
 `riid`  
 진행 에서 `ppIScope`반환할 인터페이스의 IID입니다. 일반적으로이는 IID_IMetaDataImport입니다.  
  
 `ppIScope`  
 제한이 참조 된 형식이 정의 된 모듈 범위에 대 한 인터페이스입니다.  
  
 `ptd`  
 제한이 참조 된 형식을 나타내는 TypeDef 토큰에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
  
> [!IMPORTANT]
> 여러 응용 프로그램 도메인을 로드 하는 경우에는이 메서드를 사용 하지 마십시오. 이 메서드는 응용 프로그램 도메인 경계를 고려 하지 않습니다. 어셈블리의 여러 버전이 로드 되 고 동일한 네임 스페이스를 가진 동일한 형식을 포함 하는 경우 메서드는 찾은 첫 번째 형식의 모듈 범위를 반환 합니다.  
  
 메서드 `ResolveTypeRef` 는 다른 모듈의 형식 정의를 검색 합니다. 형식 정의가 있으면에서 `ResolveTypeRef` 해당 모듈 범위에 대 한 인터페이스와 형식에 대 한 TypeDef 토큰을 반환 합니다.  
  
 확인할 형식 참조의 확인 범위가 AssemblyRef 인 경우이 메서드는 `ResolveTypeRef` [IMetaDataDispenser:: openscope](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-openscope-method.md) 메서드 또는 [을 호출 하 여 이미 열려 있는 메타 데이터 범위 에서만 일치 하는 항목을 검색 합니다. IMetaDataDispenser:: OpenScopeOnMemory](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-openscopeonmemory-method.md) 메서드 이는에서 `ResolveTypeRef` 디스크 또는 전역 어셈블리 캐시에서 어셈블리가 저장 된 AssemblyRef 범위만 확인할 수 없기 때문입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
