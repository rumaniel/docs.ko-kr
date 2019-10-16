---
title: IDefinitionIdentity 인터페이스
ms.date: 03/30/2017
api_name:
- IDefinitionIdentity
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IDefinitionIdentity
helpviewer_keywords:
- IDefinitionIdentity interface [.NET Framework fusion]
ms.assetid: ce5ba888-5fbe-4efd-91cf-f0ff94d8428b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 84c595bfdcca84ee43a53e2ea913cc978ae0953e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70796531"
---
# <a name="idefinitionidentity-interface"></a>IDefinitionIdentity 인터페이스
현재 범위에서 응용 프로그램을 정의 하는 코드의 고유 서명을 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|`IDefinitionIdentity::Clone`|지정 된 특성이 변경 되는 경우 `IDefinitionIdentity` 를 제외 하 고이 `IDefinitionIdentity`와 동일한 새 개체에 대 한 인터페이스 포인터를 가져옵니다.|  
|`IDefinitionIdentity::EnumAttributes`|이`IDefinitionIdentity`와 연결 된 특성을 포함 하는 [IEnumIDENTITY_ATTRIBUTE](ienumidentity-attribute-interface.md) 개체에 대 한 인터페이스 포인터를 가져옵니다.|  
|`IDefinitionIdentity::GetAttribute`|지정 된 네임 스페이스에서 지정 된 이름을 가진 특성의 값을 가져옵니다.|  
|`IDefinitionIdentity::SetAttribute`|지정 된 네임 스페이스에서 지정 된 이름을 가진 특성을 지정 된 값으로 설정 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** 격리. h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [Fusion 인터페이스](fusion-interfaces.md)
