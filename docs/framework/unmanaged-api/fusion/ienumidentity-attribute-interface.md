---
title: IEnumIDENTITY_ATTRIBUTE 인터페이스
ms.date: 03/30/2017
api_name:
- IEnumIDENTITY_ATTRIBUTE
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IEnumIDENTITY_ATTRIBUTE
helpviewer_keywords:
- IEnumIDENTITY_ATTRIBUTE interface [.NET Framework fusion]
ms.assetid: c2ec2748-e9ae-4e1b-80db-6fcec5cb81a1
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: dbb3ac150ebfe9fe3698427d8bb2bfb3e3347c07
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70796459"
---
# <a name="ienumidentity_attribute-interface"></a>IEnumIDENTITY_ATTRIBUTE 인터페이스
현재 범위에 있는 코드 개체의 특성에 대 한 열거자 역할을 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|`IEnumIDENTITY_ATTRIBUTE::Clone`|`IEnumIDENTITY_ATTRIBUTE` 이`IEnumIDENTITY_ATTRIBUTE`와 동일한 멤버를 포함 하는 새에 대 한 인터페이스 포인터를 가져옵니다.|  
|`IEnumIDENTITY_ATTRIBUTE::CurrentIntoBuffer`|이 `IEnumIDENTITY_ATTRIBUTE` 의 요소에 포함 된 데이터를 지정 된 데이터 버퍼에 씁니다.|  
|`IEnumIDENTITY_ATTRIBUTE::Next`|현재 위치에서 시작 하 여 지정 된 수의 특성을 가져옵니다.|  
|`IEnumIDENTITY_ATTRIBUTE::Reset`|명령 포인터를이 `IEnumIDENTITY_ATTRIBUTE`의 시작 부분으로 이동 합니다.|  
|`IEnumIDENTITY_ATTRIBUTE::Skip`|명령 포인터를 현재 위치에서 시작 하 여 지정 된 요소 수 만큼 앞으로 이동 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** 격리. h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [Fusion 인터페이스](fusion-interfaces.md)
