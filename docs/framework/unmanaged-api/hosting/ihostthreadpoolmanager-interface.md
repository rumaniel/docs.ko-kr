---
title: IHostThreadPoolManager 인터페이스
ms.date: 03/30/2017
api_name:
- IHostThreadPoolManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostThreadPoolManager
helpviewer_keywords:
- IHostThreadPoolManager interface [.NET Framework hosting]
ms.assetid: c3a2cd90-7c4e-4374-bb87-b41befb8344f
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2e7976740a79efda8e5ab569f2efb55444012c5d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61796574"
---
# <a name="ihostthreadpoolmanager-interface"></a>IHostThreadPoolManager 인터페이스
CLR (공용 언어 런타임) 스레드 풀을 구성 하 고 작업 항목을 스레드 풀 큐에 사용할 수 있는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[GetAvailableThreads 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-getavailablethreads-method.md)|현재 작업 항목을 처리 하 고 있지는 스레드 풀의 스레드 수를 가져옵니다.|  
|[GetMaxThreads 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-getmaxthreads-method.md)|스레드 풀에 동시에 호스트를 유지 하는 스레드의 최대 수를 가져옵니다.|  
|[GetMinThreads 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-getminthreads-method.md)|요청에 대비 하 여에서 호스트를 유지 관리 하는 유휴 상태 스레드의 최소 수를 가져옵니다.|  
|[QueueUserWorkItem 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-queueuserworkitem-method.md)|함수 실행에 대 한 큐 대기 하 고 함수에서 사용할 데이터를 포함 하는 개체를 제공 합니다.|  
|[SetMaxThreads 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-setmaxthreads-method.md)|스레드 풀에서 호스트를 유지할 수 있는 스레드의 최대 수를 설정 합니다.|  
|[SetMinThreads 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-setminthreads-method.md)|요청에 대비 하 여에서 호스트를 유지 해야 하는 유휴 상태 스레드의 최소 수를 설정 합니다.|  
  
## <a name="remarks"></a>설명  
 호스트에 대 한 호출에서 지정 된 값을 사용 하 여 스레드 풀을 구성할 필요가 없습니다 합니다 `SetMaxThreads` 고 `SetMinThreads` 메서드. 이 경우 호스트는 이러한 메서드에서 e_notimpl HRESULT 값을 반환 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Threading>
- <xref:System.Threading.ThreadPool>
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
