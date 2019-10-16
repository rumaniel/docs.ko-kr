---
title: CorCheckDuplicatesFor 열거형
ms.date: 03/30/2017
api_name:
- CorCheckDuplicatesFor
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorCheckDuplicatesFor
helpviewer_keywords:
- CorCheckDuplicatesFor enumeration [.NET Framework metadata]
ms.assetid: d8ec8d3c-70f7-4cc6-9957-68068fd8f49c
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a82ce9709e008e092c5f31372a89bf9a16e1f88b
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67767020"
---
# <a name="corcheckduplicatesfor-enumeration"></a>CorCheckDuplicatesFor 열거형
중복 확인 되는 메타 데이터 토큰을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorCheckDuplicatesFor {  
  
    MDDupAll                    = 0xffffffff,  
    MDDupENC                    = MDDupAll,  
    MDNoDupChecks               = 0x00000000,  
    MDDupTypeDef                = 0x00000001,  
    MDDupInterfaceImpl          = 0x00000002,  
    MDDupMethodDef              = 0x00000004,  
    MDDupTypeRef                = 0x00000008,  
    MDDupMemberRef              = 0x00000010,  
    MDDupCustomAttribute        = 0x00000020,  
    MDDupParamDef               = 0x00000040,  
    MDDupPermission             = 0x00000080,  
    MDDupProperty               = 0x00000100,  
    MDDupEvent                  = 0x00000200,  
    MDDupFieldDef               = 0x00000400,  
    MDDupSignature              = 0x00000800,  
    MDDupModuleRef              = 0x00001000,  
    MDDupTypeSpec               = 0x00002000,  
    MDDupImplMap                = 0x00004000,  
    MDDupAssemblyRef            = 0x00008000,  
    MDDupFile                   = 0x00010000,  
    MDDupExportedType           = 0x00020000,  
    MDDupManifestResource       = 0x00040000,  
    MDDupGenericParam           = 0x00080000,  
    MDDupMethodSpec             = 0x00100000,  
    MDDupGenericParamConstraint = 0x00200000,  
  
    MDDupAssembly               = 0x10000000,  
  
    MDDupDefault =   
        MDNoDupChecks | MDDupTypeRef | MDDupMemberRef |   
        MDDupSignature | MDDupTypeSpec | MDDupMethodSpec  
  
} CorCheckDuplicatesFor;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`MDDupAll`|중복 항목에 대 한 모든 메타 데이터 토큰을 확인 합니다.|  
|`MDDupENC`|사용되지 않습니다.|  
|`MDNoDupChecks`|중복 항목에 대 한 메타 데이터 토큰을 검사 하지 않습니다.|  
|`MDDupTypeDef`|중복 확인 `mdTypeDef` 토큰입니다.|  
|`MDDupInterfaceImpl`|중복 확인 `mdInterfaceImpl` 토큰입니다.|  
|`MDDupMethodDef`|중복 확인 `mdMethodDef` 토큰입니다.|  
|`MDDupTypeRef`|중복 확인 `mdTypeRef` 토큰입니다.|  
|`MDDupMemberRef`|중복 확인 `mdMemberRef` 토큰입니다.|  
|`MDDupCustomAttribute`|중복 확인 `mdCustomAttribute` 토큰입니다.|  
|`MDDupParamDef`|중복 확인 `mdParamDef` 토큰입니다.|  
|`MDDupPermission`|중복 확인 `mdPermission` 토큰입니다.|  
|`MDDupProperty`|중복 확인 `mdProperty` 토큰입니다.|  
|`MDDupEvent`|중복 확인 `mdEvent` 토큰입니다.|  
|`MDDupFieldDef`|중복 확인 `mdFieldDef` 토큰입니다.|  
|`MDDupSignature`|중복 확인 `mdSignature` 토큰입니다.|  
|`MDDupModuleRef`|중복 확인 `mdModuleRef` 토큰입니다.|  
|`MDDupTypeSpec`|중복 확인 `mdTypeSpec` 토큰입니다.|  
|`MDDupImplMap`|중복 확인 `mdImplMap` 토큰입니다.|  
|`MDDupAssemblyRef`|중복 확인 `mdAssemblyRef` 토큰입니다.|  
|`MDDupFile`|중복 확인 `mdFile` 토큰입니다.|  
|`MDDupExportedType`|중복 확인 `mdExportedType` 토큰입니다.|  
|`MDDupManifestResource`|중복 확인 `mdManifestResource` 토큰입니다.|  
|`MDDupGenericParam`|중복 확인 `mdGenericParam` 토큰입니다.|  
|`MDDupMethodSpec`|중복 확인 `mdMethodSpec` 토큰입니다.|  
|`MDDupGenericParamConstraint`|중복 확인 `mdGenericParamConstraint` 토큰입니다.|  
|`MDDupAssembly`|중복 확인 `mdAssembly` 토큰입니다.|  
|`MDDupDefault`|중복 여부를 확인 `mdMemberRef`, `mdTypeRef`, `mdSignature`합니다 `mdTypeSpec`, 및 `mdMethodSpec` 토큰입니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorHdr.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
