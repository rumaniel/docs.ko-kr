---
title: 디버깅 구조체
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged structures [.NET Framework], debugging
- debugging structures [.NET Framework]
- structures [.NET Framework debugging]
ms.assetid: 173ba2c2-ab34-49ae-b6a8-e5c49882bf05
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 45a4b5c2a65ae7e4c01ffc3977875e598d076557
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2019
ms.locfileid: "67025935"
---
# <a name="debugging-structures"></a>디버깅 구조체

이 섹션에서는 디버깅 API에서 사용하는 관리되지 않는 구조체에 대해 설명합니다.

## <a name="in-this-section"></a>섹션 내용
 [CLRDATA_ADDRESS_RANGE 구조](../../../../docs/framework/unmanaged-api/debugging/clrdata-address-range-structure.md) 주소 범위를 정의 합니다.

 [CLRDATA_IL_ADDRESS_MAP 구조](../../../../docs/framework/unmanaged-api/debugging/clrdata-il-address-map-structure.md) IL 주소 매핑 정의

 [CLR_DEBUGGING_VERSION 구조체](../../../../docs/framework/unmanaged-api/debugging/clr-debugging-version-structure.md) 는 CLR (공용 언어 런타임) 디버깅을 위해의 제품 버전을 정의 합니다.

 [CodeChunkInfo 구조체](../../../../docs/framework/unmanaged-api/debugging/codechunkinfo-structure.md) 메모리에서 코드의 단일 청크를 나타냅니다.

 [COR_ACTIVE_FUNCTION](cor-active-function-structure.md) 스레드 프레임에서 현재 활성화 된 함수에 대 한 정보를 포함 합니다.

 [COR_ARRAY_LAYOUT 구조체](../../../../docs/framework/unmanaged-api/debugging/cor-array-layout-structure.md) 메모리 내 배열 개체의 레이아웃에 대 한 정보를 제공 합니다.

 [COR_DEBUG_IL_TO_NATIVE_MAP](cor-debug-il-to-native-map-structure.md) MSIL (Microsoft intermediate language)을 매핑하는 데 사용 되는 오프셋 코드 네이티브 코드를 포함 합니다.

 [COR_DEBUG_STEP_RANGE](cor-debug-step-range-structure.md) 코드의 범위에 대 한 오프셋된 정보를 포함 합니다.

 [COR_FIELD 구조체](../../../../docs/framework/unmanaged-api/debugging/cor-field-structure.md) 개체의 필드에 대 한 정보를 제공 합니다.

 [COR_GC_REFERENCE 구조체](../../../../docs/framework/unmanaged-api/debugging/cor-gc-reference-structure.md) 가비지 수집 될 개체에 대 한 정보를 포함 합니다.

 [COR_HEAPINFO 구조체](../../../../docs/framework/unmanaged-api/debugging/cor-heapinfo-structure.md) 열거 가능 여부를 포함 하 여 가비지 컬렉션 힙에 대 한 일반 정보를 제공 합니다.

 [COR_HEAPOBJECT 구조체](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md) 관리 되는 힙의 개체에 대 한 정보를 제공 합니다.

 [COR_IL_MAP](cor-il-map-structure.md) 함수의 상대 오프셋 변경 내용을 지정 합니다.

 [COR_SEGMENT 구조체](../../../../docs/framework/unmanaged-api/debugging/cor-segment-structure.md) 관리 되는 힙의 메모리 영역에 대 한 정보를 포함 합니다.

 [COR_TYPEID 구조체](../../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md) 유형 식별자를 포함 합니다.

 [COR_TYPE_LAYOUT 구조체](../../../../docs/framework/unmanaged-api/debugging/cor-type-layout-structure.md) 메모리 내 개체의 레이아웃에 대 한 정보를 제공 합니다.

 [COR_VERSION](cor-version-structure.md) 공용 언어 런타임의 표준 네 부분으로 된 버전 번호를 저장 합니다.

 [CorDebugBlockingObject 구조체](../../../../docs/framework/unmanaged-api/debugging/cordebugblockingobject-structure.md) 스레드가 차단 되는 이유는 이유와 스레드를 차단 하는 개체를 정의 합니다.

 [CorDebugEHClause 구조체](../../../../docs/framework/unmanaged-api/debugging/cordebugehclause-structure.md) 지정 된 IL (중간 언어) 부분에 대 한 예외 처리 (EH) 절을 나타냅니다.

 [CorDebugExceptionObjectStackFrame 구조체](../../../../docs/framework/unmanaged-api/debugging/cordebugexceptionobjectstackframe-structure.md) 스택 예외 개체에서 프레임 정보를 나타냅니다.

 [CorDebugGuidToTypeMapping 구조체](../../../../docs/framework/unmanaged-api/debugging/cordebugguidtotypemapping-structure.md) 해당 Windows 런타임 GUID 매핑합니다 [ICorDebugType](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-interface.md) 개체입니다.

 [DacpGetModuleAddress 구조](../../../../docs/framework/unmanaged-api/debugging/dacpgetmoduleaddress-structure.md) 모듈 주소 요청에 대 한 컨테이너를 정의 합니다.

 [DacpMethodDescData 구조](../../../../docs/framework/unmanaged-api/debugging/dacpmethoddescdata-structure.md) 메서드의 런타임 정보에 대 한 전송 버퍼를 정의 합니다.

 [DacpModuleData 구조](../../../../docs/framework/unmanaged-api/debugging/dacpmoduledata-structure.md) 모듈의 런타임 정보에 대 한 전송 버퍼를 정의 합니다.

 [DacpReJitData 구조](../../../../docs/framework/unmanaged-api/debugging/dacprejitdata-structure.md) 지정 된 프로파일러가 계측 메서드에 대 한 기본 정보를 정의 합니다.

 [StackTrace_SimpleContext 구조체](../../../../docs/framework/unmanaged-api/debugging/stacktrace-simplecontext-structure.md) 전체 대신 사용할 수 있는 단순 컨텍스트를 제공 `CONTEXT` 구조입니다.

## <a name="related-sections"></a>관련 단원

 [디버깅 Coclass](../../../../docs/framework/unmanaged-api/debugging/debugging-coclasses.md)

 [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)

 [디버깅 전역 정적 함수](../../../../docs/framework/unmanaged-api/debugging/debugging-global-static-functions.md)

 [디버깅 열거형](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)

 [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
