---
title: IHostMalloc 인터페이스
ms.date: 03/30/2017
api_name:
- IHostMAlloc
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMAlloc
helpviewer_keywords:
- IHostMAlloc interface [.NET Framework hosting]
ms.assetid: e3c6643b-6fc7-4a99-959d-4b7b4e63fdee
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f2a7a29ef1dc85c2ad554995286e5137fcb104be
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61757640"
---
# <a name="ihostmalloc-interface"></a>IHostMalloc 인터페이스
CLR (공용 언어 런타임)에서 호스트를 통해 힙의 세분화 된 할당을 요청할 수 있도록 하는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[Alloc 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmalloc-alloc-method.md)|힙에서 호스트 요청 된 메모리 양을 할당 하도록 요청 합니다.|  
|[DebugAlloc 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmalloc-debugalloc-method.md)|호스트 힙에에서 요청 된 크기의 메모리를 할당 하 고 또한 메모리가 할당 된 위치를 추적을 요청 합니다.|  
|[Free 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmalloc-free-method.md)|사용 하 여 할당 된 메모리를 해제 합니다 `Alloc` 메서드.|  
  
## <a name="remarks"></a>설명  
 CLR에 대 한 인터페이스 포인터를 가져옵니다는 `IHostMalloc` 를 호출 하 여 인스턴스를 [ihostmemorymanager:: Createmalloc](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-createmalloc-method.md) 메서드.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IHostMemoryManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
