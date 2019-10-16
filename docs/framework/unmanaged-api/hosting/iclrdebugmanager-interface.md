---
title: ICLRDebugManager 인터페이스
ms.date: 03/30/2017
api_name:
- ICLRDebugManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDebugManager
helpviewer_keywords:
- ICLRDebugManager interface [.NET Framework hosting]
ms.assetid: e835062c-c7d6-4945-8a44-2de7ebf3928e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5a408995793caf879f8d5624ab727102c4859195
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69959606"
---
# <a name="iclrdebugmanager-interface"></a>ICLRDebugManager 인터페이스
호스트에서 작업 집합을 식별자와 이름에 연결할 수 있도록 하는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[BeginConnection 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-beginconnection-method.md)|작업을 식별자와 연결 하기 위해 호스트와 디버거 간에 새 연결을 설정 합니다.|  
|[EndConnection 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-endconnection-method.md)|작업 목록과 식별자 및 이름 간의 연결을 제거 합니다.|  
|[GetDacl 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-getdacl-method.md)|이 메서드가 구현되지 않았습니다.|  
|[IsDebuggerAttached 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-isdebuggerattached-method.md)|디버거가 프로세스에 연결되어 있는지 여부를 나타내는 값을 가져옵니다.|  
|[SetConnectionTasks 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-setconnectiontasks-method.md)|[ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md) 인스턴스 목록을 식별자 및 이름과 연결 합니다.|  
|[SetDacl 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-setdacl-method.md)|이 메서드가 구현되지 않았습니다.|  
|[SetSymbolReadingPolicy 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrdebugmanager-setsymbolreadingpolicy-method.md)|PDB (프로그램 데이터베이스) 파일을 읽기 위한 정책을 설정 합니다. 이 정책은 줄 번호와 파일에 대 한 정보가 호출 스택에 포함 되는지 여부를 결정 합니다.|  
  
## <a name="remarks"></a>설명  
 디버깅 시나리오에서 호스트는 자체 프로그래밍 논리에 따라 작업을 그룹화 할 수 있습니다. 예를 들어, 그룹화를 통해 개발자는 프로세스에서 실행 되는 모든 작업을 확인 하는 대신 개발자의 Api에 필요한 작업만 볼 수 있습니다. `ICLRDebugManager`호스트에서 이러한 종류의 그룹화를 구현할 수 있습니다.  
  
> [!IMPORTANT]
> , `ICLRDebugManager` `SetConnectionTasks` `BeginConnection`및 의`EndConnection`세 가지 메서드는 서로 종속 되어 있습니다. 이러한 작업은 예상 대로 작동 하기 위해 지정 된 순서로 호출 되어야 합니다.  
  
 호스트에서 그룹화에 할당 하는 그룹화 및 식별자와 이름에는 CLR (공용 언어 런타임)에 대 한 의미가 없습니다. CLR은 단순히 디버거로 정보를 전달 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
