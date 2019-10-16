---
title: IMetaDataImport::EnumMethodSemantics 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumMethodSemantics
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumMethodSemantics
helpviewer_keywords:
- EnumMethodSemantics method [.NET Framework metadata]
- IMetaDataImport::EnumMethodSemantics method [.NET Framework metadata]
ms.assetid: e7e3c630-9691-46d6-94df-b5593a7bb08a
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 715e53ae04532214d4011d4a40503b2ade5a014d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782070"
---
# <a name="imetadataimportenummethodsemantics-method"></a>IMetaDataImport::EnumMethodSemantics 메서드
지정한 메서드와 관련된 속성 및 속성 변경 이벤트를 열거합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT EnumMethodSemantics (  
   [in, out] HCORENUM    *phEnum,  
   [in]  mdMethodDef     mb,   
   [out] mdToken         rEventProp[],  
   [in]  ULONG           cMax,  
   [out] ULONG           *pcEventProp  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `phEnum`  
 [out에서] 열거자에 대 한 포인터입니다. 이 메서드의 첫 번째 호출에 대 한 NULL 이어야 합니다.  
  
 `mb`  
 [in] 열거형의 범위를 제한 하는 MethodDef 토큰입니다.  
  
 `rEventProp`  
 [out] 이벤트 또는 속성을 저장 하는 데 사용 되는 배열입니다.  
  
 `cMax`  
 [in] `rEventProp` 배열의 최대 크기입니다.  
  
 `pcEventProp`  
 [out] 이벤트 또는 속성에서 반환 된 수가 `rEventProp`합니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|설명|  
|-------------|-----------------|  
|`S_OK`|`EnumMethodSemantics` 성공적으로 반환 합니다.|  
|`S_FALSE`|이벤트 또는 속성 열거에 없는 합니다. 이런 경우 `pcEventProp` 0입니다.|  
  
## <a name="remarks"></a>설명  
 여러 공용 언어 런타임 형식 정의 *속성* `Changed` 이벤트와 `On` *속성* `Changed` 해당 속성에 관련 된 메서드. 예를 들어, 합니다 <xref:System.Windows.Forms.Control?displayProperty=nameWithType> 형식 정의 <xref:System.Windows.Forms.Control.Font%2A> 속성을 <xref:System.Windows.Forms.Control.FontChanged> 이벤트 및 <xref:System.Windows.Forms.Control.OnFontChanged%2A> 메서드. set 접근자 메서드에 <xref:System.Windows.Forms.Control.Font%2A> 속성 호출 <xref:System.Windows.Forms.Control.OnFontChanged%2A> 발생 하는 메서드는 <xref:System.Windows.Forms.Control.FontChanged> 이벤트입니다. 호출 하는 것 `EnumMethodSemantics` 사용에 대 한 MethodDef <xref:System.Windows.Forms.Control.OnFontChanged%2A> 에 대 한 참조를 가져오려고 합니다 <xref:System.Windows.Forms.Control.Font%2A> 속성 및 <xref:System.Windows.Forms.Control.FontChanged> 이벤트.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
