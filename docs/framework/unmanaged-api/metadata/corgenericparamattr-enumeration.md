---
title: CorGenericParamAttr 열거형
ms.date: 03/30/2017
api_name:
- CorGenericParamAttr
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorGenericParamAttr
helpviewer_keywords:
- CorGenericParamAttr enumeration [.NET Framework metadata]
ms.assetid: 36c76266-71d8-48dc-bd89-54943fa659c1
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 981829500e499be05a8de7c1ffb4683429a903e6
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781854"
---
# <a name="corgenericparamattr-enumeration"></a>CorGenericParamAttr 열거형
설명 하는 값을 포함 합니다 <xref:System.Type> 호출에서 사용된 된 제네릭 형식에 대 한 매개 변수 [IMetaDataEmit2::DefineGenericParam](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-definegenericparam-method.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorGenericParamAttr {  
  
    gpVarianceMask                     =   0x0003,  
    gpNonVariant                       =   0x0000,   
    gpCovariant                        =   0x0001,  
    gpContravariant                    =   0x0002,  
  
    gpSpecialConstraintMask            =   0x001C,  
    gpNoSpecialConstraint              =   0x0000,  
    gpReferenceTypeConstraint          =   0x0004,   
    gpNotNullableValueTypeConstraint   =   0x0008,  
    gpDefaultConstructorConstraint     =   0x0010  
  
} CorGenericParamAttr;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`gpVarianceMask`|매개 변수 분산 인터페이스 및 대리자에 제네릭 매개 변수에 적용 됩니다.|  
|`gpNonVariant`|분산이 없음을 나타냅니다.|  
|`gpCovariant`|공변성 (covariance)을 나타냅니다.|  
|`gpContravariant`|반 공변성을 나타냅니다.|  
|`gpSpecialConstraintMask`|모든 특수 제약 조건을 적용할 수 <xref:System.Type> 매개 변수입니다.|  
|`gpNoSpecialConstraint`|제약 조건이 없는 적용 된다고 합니다 <xref:System.Type> 매개 변수입니다.|  
|`gpReferenceTypeConstraint`|나타내는 <xref:System.Type> 매개 변수는 참조 형식 이어야 합니다.|  
|`gpNotNullableValueTypeConstraint`|나타내는 <xref:System.Type> 매개 변수는 null 값을 사용할 수 없는 값 형식 이어야 합니다.|  
|`gpDefaultConstructorConstraint`|나타내는 <xref:System.Type> 매개 변수는 매개 변수가 없는 기본 public 생성자를 있어야 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorHdr.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
