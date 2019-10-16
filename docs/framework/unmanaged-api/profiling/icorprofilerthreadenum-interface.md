---
title: ICorProfilerThreadEnum 인터페이스
ms.date: 03/30/2017
api_name:
- ICorProfilerThreadEnum
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerThreadEnum
helpviewer_keywords:
- ICorProfilerThreadEnum interface [.NET Framework profiling]
ms.assetid: 1e35031b-e095-4c14-9644-8deeb3081e0b
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 47359cd71460732100364f07e0dc5efacc44c760
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61597441"
---
# <a name="icorprofilerthreadenum-interface"></a>ICorProfilerThreadEnum 인터페이스
공용 언어 런타임에서 스레드 컬렉션을 순차적으로 반복하는 메서드를 제공합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[Clone 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerthreadenum-clone-method.md)|이 `ICorProfilerThreadEnum` 인터페이스의 복사본에 대한 인터페이스 포인터를 가져옵니다.|  
|[GetCount 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerthreadenum-getcount-method.md)|애플리케이션에서 사용하는 스레드 수를 가져옵니다.|  
|[Next 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerthreadenum-next-method.md)|시퀀스에서 열거자의 현재 위치부터 시작하여 순차적 스레드 컬렉션에서 지정된 개수의 연속 스레드를 가져옵니다.|  
|[Reset 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerthreadenum-reset-method.md)|열거자의 커서를 시퀀스의 시작 위치로 이동합니다.|  
|[Skip 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerthreadenum-skip-method.md)|지정한 개수의 요소를 건너뛰도록 현재 위치에서 열거자의 커서를 진행합니다.|  
  
## <a name="remarks"></a>설명  
 `ICorProfilerThreadEnum` 인터페이스는 열거자입니다. 배열의 수신기가 수신기에 적합한 속도로 송신기에서 요소를 끌어올 수 있게 합니다. 즉, 수신기가 배열 요소의 흐름을 명시적으로 제어하여 대형 배열을 메서드 매개 변수로 전달하는 기능과 관련된 문제를 방지할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
