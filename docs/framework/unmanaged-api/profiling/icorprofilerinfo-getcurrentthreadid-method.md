---
title: "ICorProfilerInfo::GetCurrentThreadID 메서드"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo.GetCurrentThreadID
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo::GetCurrentThreadID
helpviewer_keywords:
- GetCurrentThreadID method, ICorProfilerInfo interface [.NET Framework profiling]
- ICorProfilerInfo::GetCurrentThreadID method [.NET Framework profiling]
ms.assetid: 39bbdb30-6a7a-4202-8da3-67ae9a0ab3a8
topic_type: apiref
caps.latest.revision: "13"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 055a5f56f076cc29ca7ce5d45ecedd650e8f2f44
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2017
---
# <a name="icorprofilerinfogetcurrentthreadid-method"></a><span data-ttu-id="7342c-102">ICorProfilerInfo::GetCurrentThreadID 메서드</span><span class="sxs-lookup"><span data-stu-id="7342c-102">ICorProfilerInfo::GetCurrentThreadID Method</span></span>
<span data-ttu-id="7342c-103">관리 되는 스레드 이면 현재 스레드의 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7342c-103">Gets the ID of the current thread, if it is a managed thread.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7342c-104">구문</span><span class="sxs-lookup"><span data-stu-id="7342c-104">Syntax</span></span>  
  
```  
HRESULT GetCurrentThreadID(  
    [out] ThreadID *pThreadId);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="7342c-105">매개 변수</span><span class="sxs-lookup"><span data-stu-id="7342c-105">Parameters</span></span>  
 `pThreadId`  
 <span data-ttu-id="7342c-106">[out] 관리 되는 스레드의 반환된 된 ID에 대 한 포인터입니다.</span><span class="sxs-lookup"><span data-stu-id="7342c-106">[out] A pointer to the returned ID of the managed thread.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="7342c-107">설명</span><span class="sxs-lookup"><span data-stu-id="7342c-107">Remarks</span></span>  
 <span data-ttu-id="7342c-108">내부 런타임 스레드에서 또는 다른 관리 되지 않는 스레드가 현재 스레드가 경우 `GetCurrentThreadID` CORPROF_E_NOT_MANAGED_THREAD HRESULT, 및의 반환된 된 값으로 반환 된 `pThreadId` 매개 변수는 null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7342c-108">If the current thread is an internal runtime thread or other unmanaged thread, `GetCurrentThreadID` returns CORPROF_E_NOT_MANAGED_THREAD as the HRESULT, and the returned value of the `pThreadId` parameter will be null.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="7342c-109">요구 사항</span><span class="sxs-lookup"><span data-stu-id="7342c-109">Requirements</span></span>  
 <span data-ttu-id="7342c-110">**플랫폼:** 참조 [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7342c-110">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7342c-111">**헤더:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="7342c-111">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="7342c-112">**라이브러리:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="7342c-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="7342c-113">**.NET framework 버전:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7342c-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7342c-114">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7342c-114">See Also</span></span>  
 [<span data-ttu-id="7342c-115">ICorProfilerInfo 인터페이스</span><span class="sxs-lookup"><span data-stu-id="7342c-115">ICorProfilerInfo Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)