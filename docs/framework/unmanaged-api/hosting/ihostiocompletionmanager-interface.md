---
title: IHostIoCompletionManager 인터페이스
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager
helpviewer_keywords:
- IHostIoCompletionManager interface [.NET Framework hosting]
ms.assetid: c28d1983-83f7-46e2-990f-dbb9dc07c818
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3c3bebe8eabd4d5fd5faec21e0b0efc408353bc2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61796834"
---
# <a name="ihostiocompletionmanager-interface"></a>IHostIoCompletionManager 인터페이스
CLR (공용 언어 런타임) 호스트에서 제공 하는 I/O 완료 포트를 사용 하 여 상호 작용할 수 있도록 하는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[Bind 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-bind-method.md)|I/O 완료 포트에 대 한 핸들을 바인딩합니다.|  
|[CloseIoCompletionPort 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-closeiocompletionport-method.md)|에 대 한 이전 호출을 통해 생성 된 포트를 닫습니다 `CreateIoCompletionPort`합니다.|  
|[CreateIoCompletionPort 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-createiocompletionport-method.md)|호스트에 새 I/O 완료 포트를 만든 요청 합니다.|  
|[GetAvailableThreads 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-getavailablethreads-method.md)|현재 요청을 처리 하 고 있지는 I/O 완료 스레드 수를 가져옵니다.|  
|[GetHostOverlappedSize 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-gethostoverlappedsize-method.md)|호스트에서 I/O 요청에 추가 하려는 모든 사용자 지정 데이터의 크기를 가져옵니다.|  
|[GetMaxThreads 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-getmaxthreads-method.md)|I/O 요청을 처리 하는 호스트를 할당할 수 있는 스레드의 최대 수를 가져옵니다.|  
|[GetMinThreads 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-getminthreads-method.md)|I/O 요청을 처리 하는 호스트를 제공 하는 스레드의 최소 수를 가져옵니다.|  
|[InitializeHostOverlapped 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-initializehostoverlapped-method.md)|I/O 요청에 대 한 사용자 지정 데이터를 초기화할 수 있는 호스트를 제공 합니다.|  
|[SetCLRIoCompletionManager 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-setclriocompletionmanager-method.md)|호스트에 대 한 인터페이스 포인터에 제공을 [ICLRIoCompletionManager](../../../../docs/framework/unmanaged-api/hosting/iclriocompletionmanager-interface.md) 인스턴스는 CLR에서 구현 합니다.|  
|[SetMaxThreads 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-setmaxthreads-method.md)|I/o 호스트를 할당 하는 스레드의 최대 수를 설정 합니다.|  
|[SetMinThreads 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-setminthreads-method.md)|I/O 완료 될 때까지 호스트를 할당 해야 하는 스레드의 최소 수를 설정 합니다.|  
  
## <a name="remarks"></a>설명  
 `IHostIoCompletionManager` 에 해당 하는 `ICLRIoCompletionManager` CLR에 의해 구현 되는 인터페이스입니다. 메서드를 호출 하는 CLR `IHostIoCompletionManager` 처리를 호스트가 제공 및 호스트의 메서드를 호출 하는 포트를 바인딩할 `ICLRIoCompletionManager` I/O 요청의 완료를 보고 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
