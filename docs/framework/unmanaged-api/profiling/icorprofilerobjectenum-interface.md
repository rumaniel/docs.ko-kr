---
title: ICorProfilerObjectEnum 인터페이스
ms.date: 03/30/2017
api_name:
- ICorProfilerObjectEnum
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerObjectEnum
helpviewer_keywords:
- ICorProfilerObjectEnum interface [.NET Framework profiling]
ms.assetid: 13e1651c-9523-40ef-bfd7-87fb94519f8b
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 92370751b38029435b12c177b75cd4d9402369b2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61597208"
---
# <a name="icorprofilerobjectenum-interface"></a>ICorProfilerObjectEnum 인터페이스
생성 되는 고정 된 개체의 컬렉션을 순차적으로 반복 하는 메서드를 제공 합니다 [Ngen.exe (네이티브 이미지 생성기)](../../../../docs/framework/tools/ngen-exe-native-image-generator.md)합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[Clone 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerobjectenum-clone-method.md)|이 `ICorProfilerObjectEnum` 인터페이스의 복사본에 대한 인터페이스 포인터를 가져옵니다.|  
|[GetCount 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerobjectenum-getcount-method.md)|컬렉션에서 고정 된 개체의 총 수를 가져옵니다.|  
|[Next 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerobjectenum-next-method.md)|시퀀스에서 열거자의 현재 위치부터 시작 하는 개체의 순차적 컬렉션에서 지정 된 개수의 연속 개체를 가져옵니다.|  
|[Reset 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerobjectenum-reset-method.md)|이 열거자의이 커서를 시퀀스의 시작 위치로 이동합니다.|  
|[Skip 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerobjectenum-skip-method.md)|지정 된 개수의 요소를 건너뛰도록 현재 위치에서이 열거자의 커서를 이동 합니다.|  
  
## <a name="remarks"></a>설명  
 `ICorProfilerObjectEnum` 인터페이스는 열거자입니다. 배열의 수신기가 수신기에 적합한 속도로 송신기에서 요소를 끌어올 수 있게 합니다. 즉, 수신자가 수 명시적으로 배열 요소의 흐름을 제어 하려면 하므로 대형 배열을 메서드 매개 변수로 전달에 관련 된 문제를 방지 합니다.  
  
 사용 하 여 [ICorProfilerInfo2::EnumModuleFrozenObjects](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-enummodulefrozenobjects-method.md) 에 대 한 포인터를 가져오려고 합니다 `ICorProfilerObjectEnum` 인터페이스입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [EnumModuleFrozenObjects 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-enummodulefrozenobjects-method.md)
