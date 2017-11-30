---
title: "ICorProfilerCallback::AssemblyLoadStarted 메서드"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerCallback.AssemblyLoadStarted
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerCallback::AssemblyLoadStarted
helpviewer_keywords:
- ICorProfilerCallback::AssemblyLoadStarted method [.NET Framework profiling]
- AssemblyLoadStarted method [.NET Framework profiling]
ms.assetid: 67e8209d-a0ca-4118-a6e6-c1ee0abc2221
topic_type: apiref
caps.latest.revision: "13"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 654cc5fb445184bd07d145701898239bee3e9c8b
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2017
---
# <a name="icorprofilercallbackassemblyloadstarted-method"></a><span data-ttu-id="cac85-102">ICorProfilerCallback::AssemblyLoadStarted 메서드</span><span class="sxs-lookup"><span data-stu-id="cac85-102">ICorProfilerCallback::AssemblyLoadStarted Method</span></span>
<span data-ttu-id="cac85-103">어셈블리 로드 되 고 있음을 프로파일러에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="cac85-103">Notifies the profiler that an assembly is being loaded.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="cac85-104">구문</span><span class="sxs-lookup"><span data-stu-id="cac85-104">Syntax</span></span>  
  
```  
HRESULT AssemblyLoadStarted(  
    [in] AssemblyID assemblyId);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="cac85-105">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cac85-105">Parameters</span></span>  
 `assemblyId`  
 <span data-ttu-id="cac85-106">[in] 로드 되는 어셈블리를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac85-106">[in] Identifies the assembly that is being loaded.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="cac85-107">설명</span><span class="sxs-lookup"><span data-stu-id="cac85-107">Remarks</span></span>  
 <span data-ttu-id="cac85-108">값 `assemblyId` 될 때까지 정보 요청에 유효 하지는 [icorprofilercallback:: Assemblyloadfinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-assemblyloadfinished-method.md) 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac85-108">The value of `assemblyId` is not valid for an information request until the [ICorProfilerCallback::AssemblyLoadFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-assemblyloadfinished-method.md) method is called.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="cac85-109">요구 사항</span><span class="sxs-lookup"><span data-stu-id="cac85-109">Requirements</span></span>  
 <span data-ttu-id="cac85-110">**플랫폼:** 참조 [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cac85-110">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="cac85-111">**헤더:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="cac85-111">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="cac85-112">**라이브러리:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="cac85-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="cac85-113">**.NET framework 버전:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="cac85-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="cac85-114">참고 항목</span><span class="sxs-lookup"><span data-stu-id="cac85-114">See Also</span></span>  
 [<span data-ttu-id="cac85-115">ICorProfilerCallback 인터페이스</span><span class="sxs-lookup"><span data-stu-id="cac85-115">ICorProfilerCallback Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)