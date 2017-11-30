---
title: "ICorProfilerObjectEnum::Clone 메서드"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerObjectEnum.Clone
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerObjectEnum::Clone
helpviewer_keywords:
- Clone method, ICorProfilerObjectEnum interface [.NET Framework profiling]
- ICorProfilerObjectEnum::Clone method [.NET Framework profiling]
ms.assetid: b0b2facd-5991-4f4c-932d-c4937f45cef9
topic_type: apiref
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: e077115863ab3371570463d0bfd9244b69888f9e
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2017
---
# <a name="icorprofilerobjectenumclone-method"></a><span data-ttu-id="4a0b8-102">ICorProfilerObjectEnum::Clone 메서드</span><span class="sxs-lookup"><span data-stu-id="4a0b8-102">ICorProfilerObjectEnum::Clone Method</span></span>
<span data-ttu-id="4a0b8-103">이 파일의 복사본에 대 한 인터페이스 포인터를 가져옵니다 [ICorProfilerObjectEnum](../../../../docs/framework/unmanaged-api/profiling/icorprofilerobjectenum-interface.md) 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4a0b8-103">Gets an interface pointer to a copy of this [ICorProfilerObjectEnum](../../../../docs/framework/unmanaged-api/profiling/icorprofilerobjectenum-interface.md) interface.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4a0b8-104">구문</span><span class="sxs-lookup"><span data-stu-id="4a0b8-104">Syntax</span></span>  
  
```  
HRESULT Clone (  
    [out] ICorProfilerObjectEnum   **ppEnum);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="4a0b8-105">매개 변수</span><span class="sxs-lookup"><span data-stu-id="4a0b8-105">Parameters</span></span>  
 `ppEnum`  
 <span data-ttu-id="4a0b8-106">[out] 이 복사본을 가리키고 있는 인터페이스 포인터에 대 한 포인터 `ICorProfilerObjectEnum` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4a0b8-106">[out] A pointer to the interface pointer that in turn points to the copy of this `ICorProfilerObjectEnum` interface.</span></span> <span data-ttu-id="4a0b8-107">복사본은이 이와 별도로 자체 열거형의 상태를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0b8-107">The copy maintains its own enumeration state separately from this one.</span></span> <span data-ttu-id="4a0b8-108">그러나이 열거자의 현재 커서 위치와 동일 복사본의 초기 커서 위치가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a0b8-108">However, the copy's initial cursor position will be the same as this enumerator's current cursor position.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4a0b8-109">요구 사항</span><span class="sxs-lookup"><span data-stu-id="4a0b8-109">Requirements</span></span>  
 <span data-ttu-id="4a0b8-110">**플랫폼:** 참조 [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0b8-110">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4a0b8-111">**헤더:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="4a0b8-111">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="4a0b8-112">**라이브러리:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="4a0b8-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="4a0b8-113">**.NET framework 버전:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4a0b8-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4a0b8-114">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4a0b8-114">See Also</span></span>  
 [<span data-ttu-id="4a0b8-115">ICorProfilerObjectEnum 인터페이스</span><span class="sxs-lookup"><span data-stu-id="4a0b8-115">ICorProfilerObjectEnum Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerobjectenum-interface.md)