---
title: ICorProfilerInfo10 인터페이스
ms.date: 08/06/2019
author: davmason
ms.author: davmason
ms.openlocfilehash: 06cce79fbb2b2eb143e77e3c6fda194e47d4f4f3
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928795"
---
# <a name="icorprofilerinfo10-interface"></a>ICorProfilerInfo10 인터페이스

함수 IL을 수정 하 고, 런타임에서 정보를 쿼리하고, 런타임을 일시 중단 하 고 다시 시작 하는 메서드를 제공 하는 [ICorProfilerInfo9](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo9-interface.md) 의 서브 클래스입니다.

## <a name="methods"></a>메서드  

| 메서드|Description|  
| ------------|-----------------|  
|[EnumerateObjectReferences 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-enumerateobjectreferences-method.md)|ObjectID, callback 및 clientData가 지정 된 경우 각 개체 참조를 열거 합니다 (있는 경우). |
|[IsFrozenObject 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-isfrozenobject-method.md)|ObjectID가 지정 된 경우 개체가 읽기 전용 세그먼트에 있는지 여부를 확인 합니다. |
|[GetLOHObjectSizeThreshold 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-getlohobjectsizethreshold-method.md)|구성 된 LOH 임계값의 값을 가져옵니다. |
|[RequestReJITWithInliners 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-requestrejitwithinliners-method.md)| 요청 된 메서드 뿐 아니라 요청 된 메서드의 모든 inliners ReJITs 합니다.  |
|[SuspendRuntime 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-suspendruntime-method.md)| GC를 수행 하지 않고 런타임을 일시 중단 합니다. |
|[ResumeRuntime 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-resumeruntime-method.md)| GC를 수행 하지 않고 런타임을 다시 시작 합니다. |

## <a name="requirements"></a>요구 사항  
**플랫폼** [.Net Core 지원 운영 체제](../../../core/windows-prerequisites.md#net-core-supported-operating-systems)를 참조 하세요.  
**헤더:** CorProf.idl, CorProf.h  
**.Net 버전:** [!INCLUDE[net_core_22](../../../../includes/net-core-30-md.md)] 

## <a name="see-also"></a>참고자료

- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
