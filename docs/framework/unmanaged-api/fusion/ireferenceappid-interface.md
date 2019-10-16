---
title: IReferenceAppId 인터페이스
ms.date: 03/30/2017
api_name:
- IReferenceAppId
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IReferenceAppId
helpviewer_keywords:
- IReferenceAppId interface [.NET Framework fusion]
ms.assetid: 8eb9e565-f358-43ce-900e-a8f8a5aa6cfb
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 522ed80f161f114af25e1fa7ad041c8238073d6f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70796374"
---
# <a name="ireferenceappid-interface"></a>IReferenceAppId 인터페이스
현재 범위의 응용 프로그램에 대 한 고유 식별자에 대 한 참조를 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|`IReferenceAppId::get_CodeBase`|이 `IReferenceAppId`에서 참조 하는 응용 프로그램의 코드 식별자에 대 한 문자열 표현에 대 한 포인터를 가져옵니다.|  
|`IReferenceAppId::put_CodeBase`|이 `IReferenceAppId`에서 참조 하는 응용 프로그램에 대 한 코드 식별자를 설정 합니다.|  
|`IReferenceAppId::EnumAppPath`|이 `IReferenceIdentity` `IEnumReferenceIdentity` 의멤버를나타내는인스턴스를포함하는인스턴스에대한인터페이스포인터를가져옵니다.`IReferenceAppId`|  
|`IReferenceAppId::get_SubscriptionId`|이 `IReferenceAppId`에 대 한 구독의 토큰 식별자에 대 한 문자열 표현에 대 한 포인터를 가져옵니다.|  
|`IReferenceAppId::put_SubscriptionId`|이 `IReferenceAppId` 에 대 한 구독의 토큰 식별자를 지정 된 문자열 값으로 설정 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** 격리. h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [Fusion 인터페이스](fusion-interfaces.md)
- [IEnumReferenceIdentity 인터페이스](ienumreferenceidentity-interface.md)
- [IReferenceIdentity 인터페이스](ireferenceidentity-interface.md)
