---
title: IMethodMalloc 인터페이스
ms.date: 03/30/2017
api_name:
- IMethodMalloc
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- IMethodMalloc
helpviewer_keywords:
- IMethodMalloc interface [.NET Framework profiling]
ms.assetid: 8c8ab5dc-557c-473a-82f2-6e403eca7dac
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c67ce15175f8667139f99cec1ed17531eab473e1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69935655"
---
# <a name="imethodmalloc-interface"></a>IMethodMalloc 인터페이스
새 MSIL (Microsoft 중간 언어) 함수 본문에 대 한 메모리를 할당 하는 메서드를 제공 합니다.  
  
> [!NOTE]
> 인터페이스 `IMethodMalloc` 는 단순 메모리 할당자입니다. 메모리를 할당할 수 있지만 해제할 수는 없습니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[Alloc 메서드](../../../../docs/framework/unmanaged-api/profiling/imethodmalloc-alloc-method.md)|새 MSIL 함수 본문에 지정 된 크기의 메모리를 할당 하려고 시도 합니다.|  
  
## <a name="remarks"></a>설명  
 각 할당자는 모듈에 따라 달라 지 며 함수 본문은 모듈의 기본에서 양의 오프셋에 있게 됩니다. 모듈의 기본 위에 있는 메모리는 유용 하므로 할당자를 사용 하 여 함수 본문에 대해서만 메모리를 할당 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
