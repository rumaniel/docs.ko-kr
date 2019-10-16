---
title: IMetaDataImport::EnumMembers 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumMembers
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumMembers
helpviewer_keywords:
- IMetaDataImport::EnumMembers method [.NET Framework metadata]
- EnumMembers method [.NET Framework metadata]
ms.assetid: 3fb8e178-342b-4c89-9bcf-f7f834e6cb77
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 50035799fcfa4c4b08404d63fe91e7dba85722fa
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67758840"
---
# <a name="imetadataimportenummembers-method"></a>IMetaDataImport::EnumMembers 메서드
지정한 형식의 멤버를 나타내는 MemberDef 토큰을 열거합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT EnumMembers (   
   [in, out]  HCORENUM    *phEnum,   
   [in]  mdTypeDef   cl,   
   [out] mdToken     rMembers[],   
   [in]  ULONG       cMax,   
   [out] ULONG       *pcTokens  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `phEnum`  
 [out에서] 열거자에 대 한 포인터입니다.  
  
 `cl`  
 [in] 해당 멤버를 열거할 수는 형식을 나타내는 TypeDef 토큰입니다.  
  
 `rMembers`  
 [out] MemberDef 토큰을 보유 하는 데 사용 되는 배열입니다.  
  
 `cMax`  
 [in] `rMembers` 배열의 최대 크기입니다.  
  
 `pcTokens`  
 [out] 실제 MemberDef 토큰에서 반환 된 수가 `rMembers`합니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|Description|  
|-------------|-----------------|  
|`S_OK`|`EnumMembers` 성공적으로 반환 합니다.|  
|`S_FALSE`|열거할 MemberDef 토큰이 있습니다. 이런 경우 `pcTokens` 0입니다.|  
  
## <a name="remarks"></a>설명  
 클래스에 대 한 멤버의 컬렉션을 열거 하는 동안 `EnumMembers` 멤버만 반환 합니다 (필드 및 메서드를 하지만 **하지** 속성 또는 이벤트) 클래스에 직접 정의 합니다. 클래스 상속 된 해당 멤버에 대 한 구현을 제공 하는 경우에 클래스를 상속 하는 모든 멤버 반환 되지 않습니다. 상속 된 멤버를 열거 하려면 호출자에 게 상속 체인을 명시적으로 탐색 해야 합니다. 규칙의 상속 체인을 언어 또는 원래 메타 데이터를 내보낸 컴파일러에 따라 달라질 수 있는 참고 합니다.
 
 속성 및 이벤트에서 열거 되지 않습니다 `EnumMembers`합니다. 이러한 열거를 사용 하 여 [EnumProperties](imetadataimport-enumproperties-method.md) 하거나 [EnumEvents](imetadataimport-enumevents-method.md)합니다.
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
