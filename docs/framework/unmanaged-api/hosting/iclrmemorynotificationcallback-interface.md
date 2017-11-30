---
title: "ICLRMemoryNotificationCallback 인터페이스"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICLRMemoryNotificationCallback
api_location: mscoree.dll
api_type: COM
f1_keywords: ICLRMemoryNotificationCallback
helpviewer_keywords: ICLRMemoryNotificationCallback interface [.NET Framework hosting]
ms.assetid: 873639e2-4837-4568-83b3-4493e67e4174
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 6b998f8af2c7f4add3ecbb905928b5956409bf00
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="iclrmemorynotificationcallback-interface"></a><span data-ttu-id="c0530-102">ICLRMemoryNotificationCallback 인터페이스</span><span class="sxs-lookup"><span data-stu-id="c0530-102">ICLRMemoryNotificationCallback Interface</span></span>
<span data-ttu-id="c0530-103">호스트가 win32과 유사한 방법을 사용 하 여 메모리 부족 상태를 보고할 수 있도록 `CreateMemoryResourceNotification` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="c0530-103">Allows the host to report memory pressure conditions using an approach similar to that of the Win32 `CreateMemoryResourceNotification` function.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="c0530-104">메서드</span><span class="sxs-lookup"><span data-stu-id="c0530-104">Methods</span></span>  
  
|<span data-ttu-id="c0530-105">메서드</span><span class="sxs-lookup"><span data-stu-id="c0530-105">Method</span></span>|<span data-ttu-id="c0530-106">설명</span><span class="sxs-lookup"><span data-stu-id="c0530-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="c0530-107">OnMemoryNotification 메서드</span><span class="sxs-lookup"><span data-stu-id="c0530-107">OnMemoryNotification Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrmemorynotificationcallback-onmemorynotification-method.md)|<span data-ttu-id="c0530-108">공용 언어 런타임을 (CLR)의 컴퓨터에 메모리 사용량에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="c0530-108">Notifies the common language runtime (CLR) of the memory load on the computer.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="c0530-109">설명</span><span class="sxs-lookup"><span data-stu-id="c0530-109">Remarks</span></span>  
 <span data-ttu-id="c0530-110">호스트가 사용 하는 `ICLRMemoryNotificationCallback` CLR 메모리 리소스를 해제 요청에 대 한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c0530-110">The host uses the `ICLRMemoryNotificationCallback` interface to request that the CLR free memory resources.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c0530-111">요구 사항</span><span class="sxs-lookup"><span data-stu-id="c0530-111">Requirements</span></span>  
 <span data-ttu-id="c0530-112">**플랫폼:** 참조 [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0530-112">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c0530-113">**헤더:** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="c0530-113">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="c0530-114">**라이브러리:** MSCorEE.dll에 리소스로 포함</span><span class="sxs-lookup"><span data-stu-id="c0530-114">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="c0530-115">**.NET framework 버전:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c0530-115">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c0530-116">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c0530-116">See Also</span></span>  
 [<span data-ttu-id="c0530-117">IHostMemoryManager 인터페이스</span><span class="sxs-lookup"><span data-stu-id="c0530-117">IHostMemoryManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-interface.md)  
 [<span data-ttu-id="c0530-118">호스팅 인터페이스</span><span class="sxs-lookup"><span data-stu-id="c0530-118">Hosting Interfaces</span></span>](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)