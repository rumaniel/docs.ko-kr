---
title: "COR_PRF_GC_ROOT_KIND 열거형"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: COR_PRF_GC_ROOT_KIND
api_location: mscorwks.dll
api_type: COM
f1_keywords: COR_PRF_GC_ROOT_KIND
helpviewer_keywords: COR_PRF_GC_ROOT_KIND enumeration [.NET Framework profiling]
ms.assetid: b9fb1c03-417f-41d4-aed4-02cb4ade8def
topic_type: apiref
caps.latest.revision: "9"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: d60b851dc16fca825526562585fbfcec76f9d20a
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2017
---
# <a name="corprfgcrootkind-enumeration"></a><span data-ttu-id="d3f67-102">COR_PRF_GC_ROOT_KIND 열거형</span><span class="sxs-lookup"><span data-stu-id="d3f67-102">COR_PRF_GC_ROOT_KIND Enumeration</span></span>
<span data-ttu-id="d3f67-103">에 의해 노출 되는 가비지 수집 루트의 종류를 나타내는 [icorprofilercallback2:: Rootreferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-rootreferences2-method.md) 콜백 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3f67-103">Indicates the kind of garbage collection root that is exposed by the [ICorProfilerCallback2::RootReferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-rootreferences2-method.md) callback.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d3f67-104">구문</span><span class="sxs-lookup"><span data-stu-id="d3f67-104">Syntax</span></span>  
  
```  
typedef enum {  
    COR_PRF_GC_ROOT_STACK = 1,  
    COR_PRF_GC_ROOT_FINALIZER = 2,  
    COR_PRF_GC_ROOT_HANDLE = 3,  
    COR_PRF_GC_ROOT_OTHER = 0  
} COR_PRF_GC_ROOT_KIND;  
```  
  
## <a name="members"></a><span data-ttu-id="d3f67-105">멤버</span><span class="sxs-lookup"><span data-stu-id="d3f67-105">Members</span></span>  
  
|<span data-ttu-id="d3f67-106">멤버</span><span class="sxs-lookup"><span data-stu-id="d3f67-106">Member</span></span>|<span data-ttu-id="d3f67-107">설명</span><span class="sxs-lookup"><span data-stu-id="d3f67-107">Description</span></span>|  
|------------|-----------------|  
|`COR_PRF_GC_ROOT_STACK`|<span data-ttu-id="d3f67-108">루트 스택에 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d3f67-108">The root is a variable on the stack.</span></span>|  
|`COR_PRF_GC_ROOT_FINALIZER`|<span data-ttu-id="d3f67-109">루트는 종료자 큐에 있는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d3f67-109">The root is an entry in the finalizer queue.</span></span>|  
|`COR_PRF_GC_ROOT_HANDLE`|<span data-ttu-id="d3f67-110">루트에 대 한 가비지 컬렉션 핸들입니다.</span><span class="sxs-lookup"><span data-stu-id="d3f67-110">The root is a garbage collection handle.</span></span>|  
|`COR_PRF_GC_ROOT_OTHER`|<span data-ttu-id="d3f67-111">루트의 종류 지정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="d3f67-111">The kind of root is unspecified.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="d3f67-112">요구 사항</span><span class="sxs-lookup"><span data-stu-id="d3f67-112">Requirements</span></span>  
 <span data-ttu-id="d3f67-113">**플랫폼:** 참조 [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3f67-113">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d3f67-114">**헤더:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="d3f67-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="d3f67-115">**라이브러리:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="d3f67-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d3f67-116">**.NET framework 버전:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d3f67-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d3f67-117">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d3f67-117">See Also</span></span>  
 [<span data-ttu-id="d3f67-118">프로 파일링 열거형</span><span class="sxs-lookup"><span data-stu-id="d3f67-118">Profiling Enumerations</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)