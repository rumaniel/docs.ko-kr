---
title: IAssemblyName 인터페이스
ms.date: 03/30/2017
api_name:
- IAssemblyName
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyName
helpviewer_keywords:
- IAssemblyName interface [.NET Framework fusion]
ms.assetid: f7f8e605-6b67-4151-936f-f04ecd671d90
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: aee9b986c1e26c1b2e34dac7151a00172451bbad
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70796559"
---
# <a name="iassemblyname-interface"></a>IAssemblyName 인터페이스
어셈블리의 고유 id를 설명 하 고 작업 하는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[Clone 메서드](iassemblyname-clone-method.md)|이 `IAssemblyName` 개체의 단순 복사본을 만듭니다.|  
|[Finalize 메서드](iassemblyname-finalize-method.md)|소멸자가 `IAssemblyName` 호출 되기 전에이 개체가 리소스를 해제 하 고 다른 정리 작업을 수행할 수 있도록 허용 합니다.|  
|[GetDisplayName 메서드](iassemblyname-getdisplayname-method.md)|이 `IAssemblyName` 개체가 참조 하는 어셈블리의 사람이 읽을 수 있는 이름을 가져옵니다.|  
|[GetName 메서드](iassemblyname-getname-method.md)|이 `IAssemblyName` 개체가 참조 하는 어셈블리의 단순한 암호화 되지 않은 이름을 가져옵니다.|  
|[GetProperty 메서드](iassemblyname-getproperty-method.md)|지정 `PropertyId`된에서 참조 하는 속성에 대 한 포인터를 가져옵니다.|  
|[GetVersion 메서드](iassemblyname-getversion-method.md)|이 `IAssemblyName` 개체가 참조 하는 어셈블리에 대 한 버전 정보를 가져옵니다.|  
|[IsEqual 메서드](iassemblyname-isequal-method.md)|지정 된 비교 플래그 `IAssemblyName` 에 따라 지정 된 개체가 `IAssemblyName`이와 같은지 여부를 확인 합니다.|  
|[SetProperty 메서드](iassemblyname-setproperty-method.md)|지정 `PropertyId`된에서 참조 하는 속성의 값을 설정 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Fusion. h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [Fusion 인터페이스](fusion-interfaces.md)
- [IAssemblyEnum 인터페이스](iassemblyenum-interface.md)
