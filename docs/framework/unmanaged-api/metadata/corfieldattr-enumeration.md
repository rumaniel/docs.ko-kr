---
title: CorFieldAttr 열거형
ms.date: 03/30/2017
api_name:
- CorFieldAttr
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorFieldAttr
helpviewer_keywords:
- CorFieldAttr enumeration [.NET Framework metadata]
ms.assetid: 6ae2c4be-212c-4e74-9288-40a11dc26522
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e909680428c7957da2283d13f5676329d953bf22
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781886"
---
# <a name="corfieldattr-enumeration"></a>CorFieldAttr 열거형
필드에 대한 메타데이터를 설명하는 값을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorFieldAttr {  
  
    fdFieldAccessMask           =   0x0007,  
    fdPrivateScope              =   0x0000,  
    fdPrivate                   =   0x0001,  
    fdFamANDAssem               =   0x0002,  
    fdAssembly                  =   0x0003,  
    fdFamily                    =   0x0004,  
    fdFamORAssem                =   0x0005,  
    fdPublic                    =   0x0006,  
  
    fdStatic                    =   0x0010,  
    fdInitOnly                  =   0x0020,  
    fdLiteral                   =   0x0040,  
    fdNotSerialized             =   0x0080,  
  
    fdSpecialName               =   0x0200,  
  
    fdPinvokeImpl               =   0x2000,  
  
    fdReservedMask              =   0x9500,  
    fdRTSpecialName             =   0x0400,  
    fdHasFieldMarshal           =   0x1000,  
    fdHasDefault                =   0x8000,  
    fdHasFieldRVA               =   0x0100  
  
} CorFieldAttr;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`fdFieldAccessMask`|내게 필요한 옵션 정보를 지정합니다.|  
|`fdPrivateScope`|필드는 참조할 수 없음을 지정 합니다.|  
|`fdPrivate`|필드에 해당 부모 형식에 의해서만 액세스할 수 있는지를 지정 합니다.|  
|`fdFamANDAssem`|필드에 해당 어셈블리의 파생된 클래스에서 액세스할 수 있는지를 지정 합니다.|  
|`fdAssembly`|필드에 해당 어셈블리의 모든 형식에서 액세스할 수 있는지를 지정 합니다.|  
|`fdFamily`|필드는 해당 형식에 의해서만 액세스할 수 있습니다 하 고 파생 클래스를 지정 합니다.|  
|`fdFamORAssem`|필드에 해당 어셈블리의 모든 형식 및 파생된 클래스에서 액세스할 수 있는지를 지정 합니다.|  
|`fdPublic`|필드에이 범위의 표시 여부를 사용 하 여 모든 형식에서 액세스할 수 있는지를 지정 합니다.|  
|`fdStatic`|해당 형식의 멤버 대신 인스턴스 멤버가 필드 임을 지정 합니다.|  
|`fdInitOnly`|초기화 한 후 필드를 변경할 수 없습니다 지정 합니다.|  
|`fdLiteral`|필드 값은 컴파일 타임 상수 임을 지정 합니다.|  
|`fdNotSerialized`|해당 형식이 원격 필드가 직렬화 되지 않습니다 지정 합니다.|  
|`fdSpecialName`|필드가 특별 하 고 이름과 설명 하는지 지정 하는 방법입니다.|  
|`fdPinvokeImpl`|필드 구현이 PInvoke를 통해 전달 되는 것을 지정 합니다.|  
|`fdReservedMask`|공용 언어 런타임에서 내부 용도로 예약 되어 있습니다.|  
|`fdRTSpecialName`|공용 언어 런타임 메타 데이터 내부 Api 인코딩을 확인 하도록 이름을 지정 합니다.|  
|`fdHasFieldMarshal`|필드에 마샬링 정보가 포함 되도록 지정 합니다.|  
|`fdHasDefault`|필드 기본값을 갖도록 지정 합니다.|  
|`fdHasFieldRVA`|필드의 상대 가상 주소를 지정 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorHdr.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
