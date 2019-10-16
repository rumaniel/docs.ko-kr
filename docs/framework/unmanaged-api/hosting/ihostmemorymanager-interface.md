---
title: IHostMemoryManager 인터페이스
ms.date: 03/30/2017
api_name:
- IHostMemoryManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager
helpviewer_keywords:
- IHostMemoryManager interface [.NET Framework hosting]
ms.assetid: a945d439-3b34-4aa4-b575-8413dd7806ce
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 57f34ed1796f6fa411d31fca83baeff693f85d70
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61760183"
---
# <a name="ihostmemorymanager-interface"></a>IHostMemoryManager 인터페이스
표준 Win32 가상 메모리 함수를 사용 하는 대신는 CLR (공용 언어 런타임) 호스트를 통해 가상 메모리 요청을 허용 하는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[AcquiredVirtualAddressSpace 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-acquiredvirtualaddressspace-method.md)|CLR (공용 언어 런타임) 운영 체제에서 지정된 된 메모리를 획득에 호스트에 알립니다.|  
|[CreateMAlloc 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-createmalloc-method.md)|한 인터페이스 포인터를 가져옵니다는 [IHostMAlloc](../../../../docs/framework/unmanaged-api/hosting/ihostmalloc-interface.md) 호스트에서 만든 힙에서 메모리 할당을 요청 하는 데 사용 되는 인스턴스.|  
|[GetMemoryLoad 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-getmemoryload-method.md)|호스트에서 보고 있는 현재 사용 중인 실제 메모리의 양을 가져옵니다.|  
|[NeedsVirtualAddressSpace 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-needsvirtualaddressspace-method.md)|CLR이 지정 된 메모리 사용을 시도 하려는 호스트에 알립니다.|  
|[RegisterMemoryNotificationCallback 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-registermemorynotificationcallback-method.md)|호스트 컴퓨터의 현재 메모리 로드 CLR에 알리기 위해 호출 되는 콜백 함수에 대 한 포인터를 등록 합니다.|  
|[ReleasedVirtualAddressSpace 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-releasedvirtualaddressspace-method.md)|지정된 된 메모리를 사용 하 여 CLR가 완료 했음을 호스트에 알립니다.|  
|[VirtualAlloc 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-virtualalloc-method.md)|예약 또는 호출 프로세스의 가상 주소 공간에서 페이지의 영역을 커밋에 해당 Win32 함수에 대 한 논리적 래퍼 역할을 합니다.|  
|[VirtualFree 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-virtualfree-method.md)|릴리스, 커밋 또는 해제 하 고 호출 하는 프로세스의 가상 주소 공간 내의 페이지 영역을 커밋 해제 하는 해당 Win32 함수에 대 한 논리적 래퍼 역할을 합니다.|  
|[VirtualProtect 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-virtualprotect-method.md)|호출 프로세스의 가상 주소 공간에서 커밋된 페이지의 지역에 대 한 보호를 변경 하는 해당 Win32 함수에 대 한 논리적 래퍼 역할을 합니다.|  
|[VirtualQuery 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-virtualquery-method.md)|호출 프로세스의 가상 주소 공간에서 페이지 범위에 대 한 정보를 검색 하는 해당 Win32 함수에 대 한 논리적 래퍼 역할을 합니다.|  
  
## <a name="remarks"></a>설명  
 `IHostMemoryManager` 또한 호스트에 의해 보고 되는 힙의 메모리 요청을 확인 하 고 프로세스의 메모리 압력 수준에 대 한 포인터를 가져오려면 CLR에 대 한 메서드를 제공 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IHostMalloc 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostmalloc-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
