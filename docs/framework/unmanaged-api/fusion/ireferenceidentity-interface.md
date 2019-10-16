---
title: IReferenceIdentity 인터페이스
ms.date: 03/30/2017
api_name:
- IReferenceIdentity
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IReferenceIdentity
helpviewer_keywords:
- IReferenceIdentity interface [.NET Framework fusion]
ms.assetid: 9180ac5a-7019-4716-9f83-8a91d157239a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2bb151d7c77104d8e24acefaac2e1f109b67f168
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70796362"
---
# <a name="ireferenceidentity-interface"></a>IReferenceIdentity 인터페이스
코드 개체의 고유 서명에 대 한 참조를 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|`IReferenceIdentity::Clone`|지정 된 특성이 변경 되는 경우 `IReferenceIdentity` 를 제외 하 고이 `IReferenceIdentity`와 동일한 새 인스턴스에 대 한 인터페이스 포인터를 가져옵니다.|  
|`IReferenceIdentity::EnumAttributes`|`IEnumIDENTITY_ATTRIBUTE` 이`IReferenceIdentity`와 연결 된 특성을 포함 하는 인스턴스에 대 한 인터페이스 포인터를 가져옵니다.|  
|`IReferenceIdentity::GetAttribute`|지정 된 이름을 사용 하 여 지정 된 네임 스페이스에 있는 특성의 값을 가져옵니다.|  
|`IReferenceIdentity::SetAttribute`|지정 된 네임 스페이스와 지정 된 이름을 가진 특성을 지정 된 값으로 설정 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** 격리. h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [Fusion 인터페이스](fusion-interfaces.md)
- [IEnumIDENTITY_ATTRIBUTE 인터페이스](ienumidentity-attribute-interface.md)
