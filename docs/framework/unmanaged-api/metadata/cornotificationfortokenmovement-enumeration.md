---
title: CorNotificationForTokenMovement 열거형
ms.date: 03/30/2017
api_name:
- CorNotificationForTokenMovement
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorNotificationForTokenMovement
helpviewer_keywords:
- CorNotificationForTokenMovement enumeration [.NET Framework metadata]
ms.assetid: 1edd1670-976a-4fc8-bef7-7c41e60ad989
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 7a7859bd890a2ecc10b5117f697ff8b06ad569f6
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781695"
---
# <a name="cornotificationfortokenmovement-enumeration"></a>CorNotificationForTokenMovement 열거형
토큰 다시 매핑으로 발생할 때 메타 데이터 API 클라이언트에 보낼 알림을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorNotificationForTokenMovement {  
  
    MDNotifyDefault             = 0x0000000f,  
    MDNotifyAll                 = 0xffffffff,  
    MDNotifyNone                = 0x00000000,  
    MDNotifyMethodDef           = 0x00000001,  
    MDNotifyMemberRef           = 0x00000002,  
    MDNotifyFieldDef            = 0x00000004,  
    MDNotifyTypeRef             = 0x00000008,  
  
    MDNotifyTypeDef             = 0x00000010,  
    MDNotifyParamDef            = 0x00000020,  
    MDNotifyInterfaceImpl       = 0x00000040,  
    MDNotifyProperty            = 0x00000080,  
    MDNotifyEvent               = 0x00000100,  
    MDNotifySignature           = 0x00000200,  
    MDNotifyTypeSpec            = 0x00000400,  
    MDNotifyCustomAttribute     = 0x00000800,  
    MDNotifySecurityValue       = 0x00001000,  
    MDNotifyPermission          = 0x00002000,  
    MDNotifyModuleRef           = 0x00004000,  
  
    MDNotifyNameSpace           = 0x00008000,  
  
    MDNotifyAssemblyRef         = 0x01000000,  
    MDNotifyFile                = 0x02000000,  
    MDNotifyExportedType        = 0x04000000,  
    MDNotifyResource            = 0x08000000  
  
} CorNotificationForTokenMovement;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`MDNotifyDefault`|알립니다 `mdTypeRef`, `mdMethodDef`를 `mdMemberRef`, 또는 `mdFieldDef` 토큰이 이동 합니다.|  
|`MDNotifyAll`|모든 토큰 이동할 때 알립니다.|  
|`MDNotifyNone`|토큰 이동 하는 경우를 알리지 않습니다.|  
|`MDNotifyMethodDef`|알릴 시기는 `mdMethodDef` 토큰이 이동 합니다.|  
|`MDNotifyMemberRef`|알릴 시기는 `mdMemberRef` 토큰이 이동 합니다.|  
|`MDNotifyFieldDef`|알릴 시기는 `mdFieldDef` 토큰이 이동 합니다.|  
|`MDNotifyTypeRef`|알릴 시기는 `mdTypeRef` 토큰이 이동 합니다.|  
|`MDNotifyTypeDef`|알릴 시기는 `mdTypeDef` 토큰이 이동 합니다.|  
|`MDNotifyParamDef`|알릴 시기는 `mdParamDef` 토큰이 이동 합니다.|  
|`MDNotifyInterfaceImpl`|알릴 시기는 `mdInterfaceImpl` 토큰이 이동 합니다.|  
|`MDNotifyProperty`|알릴 시기는 `mdProperty` 토큰이 이동 합니다.|  
|`MDNotifyEvent`|알릴 시기는 `mdEvent` 토큰이 이동 합니다.|  
|`MDNotifySignature`|알릴 시기는 `mdSignature` 토큰이 이동 합니다.|  
|`MDNotifyTypeSpec`|알릴 시기는 `mdTypeSpec` 토큰이 이동 합니다.|  
|`MDNotifyCustomAttribute`|알릴 시기는 `mdCustomAttribute` 토큰이 이동 합니다.|  
|`MDNotifySecurityValue`|알릴 시기는 `mdSecurityValue` 토큰이 이동 합니다.|  
|`MDNotifyPermission`|알릴 시기는 `mdPermission` 토큰이 이동 합니다.|  
|`MDNotifyModuleRef`|알릴 시기는 `mdModuleRef` 토큰이 이동 합니다.|  
|`MDNotifyNameSpace`|알릴 시기는 `mdNameSpace` 토큰이 이동 합니다.|  
|`MDNotifyAssemblyRef`|알릴 시기는 `mdAssemblyRef` 토큰이 이동 합니다.|  
|`MDNotifyFile`|알릴 시기는 `mdFile` 토큰이 이동 합니다.|  
|`MDNotifyExportedType`|알릴 시기는 `mdExportedType` 토큰이 이동 합니다.|  
|`MDNotifyResource`|알릴 시기는 `mdManifestResource` 토큰이 이동 합니다.|  
  
## <a name="remarks"></a>설명  
 토큰이 다시 매핑될 수 (이동)이 표시 된 메타 데이터를 병합 하는 동안.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorHdr.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
