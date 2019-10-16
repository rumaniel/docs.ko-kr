---
title: IAssemblyCache 인터페이스
ms.date: 03/30/2017
api_name:
- IAssemblyCache
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyCache
helpviewer_keywords:
- IAssemblyCache interface [.NET Framework fusion]
ms.assetid: 71ea170f-872d-4fc5-81b6-27da1dec9b19
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6dab5fe941fce3c23ba718906b29c80c6d257c2f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70796775"
---
# <a name="iassemblycache-interface"></a>IAssemblyCache 인터페이스
Fusion 기술에서 사용할 전역 어셈블리 캐시를 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[CreateAssemblyCacheItem 메서드](iassemblycache-createassemblycacheitem-method.md)|새 [Iassemblycacheitem](iassemblycacheitem-interface.md)에 대 한 참조를 가져옵니다.|  
|[CreateAssemblyScavenger 메서드](iassemblycache-createassemblyscavenger-method.md)|Fusion 기술에서 내부용으로 사용 하도록 예약 되어 있습니다.|  
|[InstallAssembly 메서드](iassemblycache-installassembly-method.md)|지정 된 어셈블리를 전역 어셈블리 캐시에 설치 합니다.|  
|[QueryAssemblyInfo 메서드](iassemblycache-queryassemblyinfo-method.md)|지정 된 어셈블리에 대 한 요청 된 데이터를 가져옵니다.|  
|[UninstallAssembly 메서드](iassemblycache-uninstallassembly-method.md)|전역 어셈블리 캐시에서 지정 된 어셈블리를 제거 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Fusion. h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [Fusion 인터페이스](fusion-interfaces.md)
- [전역 어셈블리 캐시](../../app-domains/gac.md)
