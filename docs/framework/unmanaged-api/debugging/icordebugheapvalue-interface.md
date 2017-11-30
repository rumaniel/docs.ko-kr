---
title: ICorDebugHeapValue Interface1
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugHeapValue
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugHeapValue
helpviewer_keywords: ICorDebugHeapValue interface [.NET Framework debugging]
ms.assetid: 1bca66db-0359-4ae8-846e-e35f7e547e8b
topic_type: apiref
caps.latest.revision: "14"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 7868fc84ba3003909992334d1a66e1ed243eca18
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugheapvalue-interface1"></a><span data-ttu-id="881bd-102">ICorDebugHeapValue Interface1</span><span class="sxs-lookup"><span data-stu-id="881bd-102">ICorDebugHeapValue Interface1</span></span>
<span data-ttu-id="881bd-103">공용 언어 런타임 (CLR) 가비지 수집기에 의해 수집 된 개체를 나타내는 "ICorDebugValue"의 하위 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="881bd-103">A subclass of "ICorDebugValue" that represents an object that has been collected by the common language runtime (CLR) garbage collector.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="881bd-104">메서드</span><span class="sxs-lookup"><span data-stu-id="881bd-104">Methods</span></span>  
  
|<span data-ttu-id="881bd-105">메서드</span><span class="sxs-lookup"><span data-stu-id="881bd-105">Method</span></span>|<span data-ttu-id="881bd-106">설명</span><span class="sxs-lookup"><span data-stu-id="881bd-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="881bd-107">CreateRelocBreakpoint 메서드</span><span class="sxs-lookup"><span data-stu-id="881bd-107">CreateRelocBreakpoint Method</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugheapvalue-createrelocbreakpoint-method.md)|<span data-ttu-id="881bd-108">구현되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="881bd-108">Not implemented.</span></span>|  
|[<span data-ttu-id="881bd-109">IsValid 메서드</span><span class="sxs-lookup"><span data-stu-id="881bd-109">IsValid Method</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugheapvalue-isvalid-method.md)|<span data-ttu-id="881bd-110">이 나타내는 개체가 있는지 여부를 나타내는 값을 가져옵니다 `ICorDebugHeapValue` 유효 않거나 가비지 수집기에서 회수 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="881bd-110">Gets a value that indicates whether the object represented by this `ICorDebugHeapValue` is valid, or has been reclaimed by the garbage collector.</span></span> <span data-ttu-id="881bd-111">이 메서드는.NET Framework 버전 2.0에서에서 사용 되지 합니다.</span><span class="sxs-lookup"><span data-stu-id="881bd-111">This method has been deprecated in the .NET Framework version 2.0.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="881bd-112">설명</span><span class="sxs-lookup"><span data-stu-id="881bd-112">Remarks</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="881bd-113">이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="881bd-113">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="881bd-114">요구 사항</span><span class="sxs-lookup"><span data-stu-id="881bd-114">Requirements</span></span>  
 <span data-ttu-id="881bd-115">**플랫폼:** 참조 [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="881bd-115">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="881bd-116">**헤더:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="881bd-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="881bd-117">**라이브러리:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="881bd-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="881bd-118">**.NET framework 버전:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="881bd-118">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="881bd-119">참고 항목</span><span class="sxs-lookup"><span data-stu-id="881bd-119">See Also</span></span>  
    
    
    
 [<span data-ttu-id="881bd-120">디버깅 인터페이스</span><span class="sxs-lookup"><span data-stu-id="881bd-120">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)