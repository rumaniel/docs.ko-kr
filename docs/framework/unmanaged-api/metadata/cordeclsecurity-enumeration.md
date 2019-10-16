---
title: CorDeclSecurity 열거형
ms.date: 03/30/2017
api_name:
- CorDeclSecurity
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorDeclSecurity
helpviewer_keywords:
- CorDeclSecurity enumeration [.NET Framework metadata]
ms.assetid: 864f1267-d267-4696-8df7-1f83f8444d6f
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 5898f2f0900b0bbe392d4dbaa8fc1db5e0e45c9e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67767008"
---
# <a name="cordeclsecurity-enumeration"></a>CorDeclSecurity 열거형
선언적 보안을 사용하여 수행할 수 있는 보안 작업을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorDeclSecurity {  
  
    dclActionMask               =   0x001f,  
    dclActionNil                =   0x0000,  
    dclRequest                  =   0x0001,  
    dclDemand                   =   0x0002,  
    dclAssert                   =   0x0003,  
    dclDeny                     =   0x0004,  
    dclPermitOnly               =   0x0005,  
    dclLinktimeCheck            =   0x0006,  
    dclInheritanceCheck         =   0x0007,  
    dclRequestMinimum           =   0x0008,  
    dclRequestOptional          =   0x0009,  
    dclRequestRefuse            =   0x000a,  
    dclPrejitGrant              =   0x000b,  
    dclPrejitDenied             =   0x000c,  
    dclNonCasDemand             =   0x000d,  
    dclNonCasLinkDemand         =   0x000e,  
    dclNonCasInheritance        =   0x000f,  
    dclLinkDemandChoice         =   0x0010,  
    dclInheritanceDemandChoice  =   0x0011,  
    dclDemandChoice             =   0x0012,  
    dclMaximumValue             =   0x0012  
  
} CorDeclSecurity;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`dclActionMask`|예약되어 있습니다.|  
|`dclActionNil`|예약됨.|  
|`dclRequest`|예약되어 있습니다.|  
|`dclDemand`|호출 스택의 상위에 있는 모든 호출자에게 현재 사용 권한 개체가 지정한 사용 권한이 부여되었어야 합니다.|  
|`dclAssert`|스택의 상위 호출자가 리소스에 액세스할 권한이 하는 경우에 호출 코드에서 현재 사용 권한 개체로 식별 되는 리소스를 액세스할 수 있습니다.|  
|`dclDeny`|현재 권한 개체에 의해 지정 된 리소스에 액세스할 수 있도록 권한이 부여 된 액세스 권한이 있는 경우에 호출자에 게 액세스가 거부 되었습니다.|  
|`dclPermitOnly`|코드에 다른 리소스에 액세스할 수 있는 권한이 부여되더라도 이 권한 개체가 지정한 리소스에만 액세스할 수 있습니다.|  
|`dclLinktimeCheck`|직접 실행 호출자는 지정 된 기간에 대 한 지정 된 권한을 부여 받아야 합니다.|  
|`dclInheritanceCheck`|다른 클래스를 상속 하거나 메서드를 재정의 하는 파생된 클래스는 지정 된 권한을 부여 받아야 합니다.|  
|`dclRequestMinimum`|호출자가 코드를 실행 하는 데 필요한 최소 사용 권한을 요청할 수 있습니다. 이 작업은 어셈블리 범위 내에서만 사용할 수 있습니다.|  
|`dclRequestOptional`|호출자는 선택 사항 (실행 하려면 필요 없음)는 추가 사용 권한을 요청할 수 있습니다. 이 요청은 특별히 요청되지 않은 다른 모든 사용 권한을 암시적으로 거부합니다. 이 작업은 어셈블리 범위 내에서만 사용할 수 있습니다.|  
|`dclRequestRefuse`|호출자의 요청을 잘못 사용 될 수 있는 권한이 부여 되지 않습니다. 이 작업은 어셈블리 범위 내에서만 사용할 수 있습니다.|  
|`dclPrejitGrant`|예약되어 있습니다.|  
|`dclPrejitDenied`|예약됨.|  
|`dclNonCasDemand`|예약되어 있습니다.|  
|`dclNonCasLinkDemand`|직접 실행 호출자에게 지정된 사용 권한이 부여되었어야 합니다.|  
|`dclNonCasInheritance`|예약되어 있습니다.|  
|`dclLinkDemandChoice`|예약됨.|  
|`dclInheritanceDemandChoice`|예약됨.|  
|`dclDemandChoice`|예약됨.|  
|`dclMaximumValue`|예약되어 있습니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorHdr.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
