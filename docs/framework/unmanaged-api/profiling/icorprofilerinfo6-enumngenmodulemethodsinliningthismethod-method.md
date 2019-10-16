---
title: ICorProfilerInfo6::EnumNgenModuleMethodsInliningThisMethod 메서드
ms.date: 03/30/2017
ms.assetid: b933dfe6-7833-40cb-aad8-40842dc3034f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 870a71de2aee2e9b725749157791c49836c6ea00
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65636875"
---
# <a name="icorprofilerinfo6enumngenmodulemethodsinliningthismethod-method"></a>ICorProfilerInfo6::EnumNgenModuleMethodsInliningThisMethod 메서드

인라인 지정된 메서드를 지정 된 NGen 모듈에 정의 된 모든 메서드는 열거자를 반환 합니다.

## <a name="syntax"></a>구문

```cpp
HRESULT EnumNgenModuleMethodsInliningThisMethod(
        [in] ModuleID inlinersModuleId,
        [in] ModuleID inlineeModuleId,
        [in] mdMethodDef inlineeMethodId,
        [out] BOOL *incompleteData,
        [out] ICorProfilerMethodEnum** ppEnum
);
```

## <a name="parameters"></a>매개 변수

`inlinersModuleId`\
[in] NGen 모듈의 식별자입니다.

`inlineeModuleId`\
[in] 정의 하는 모듈의 식별자 `inlineeMethodId`합니다. 자세한 내용은 설명 부분을 참조하세요.

`inlineeMethodId`\
[in] 인라인 메서드의 식별자입니다. 자세한 내용은 설명 부분을 참조하세요.

`incompleteData`\
[out] 나타내는 플래그 있는지 여부를 `ppEnum` 지정된 메서드를 인라인 처리 하는 모든 메서드를 포함 합니다.  자세한 내용은 설명 부분을 참조하세요.

`ppEnum`\
[out] 열거자의 주소에 대 한 포인터

## <a name="remarks"></a>설명

`inlineeModuleId` 및 `inlineeMethodId` 인라인 처리 하지 않을 수 있는 메서드에 대 한 전체 식별자를 결합 합니다. 예를 들어 모듈 `A` 메서드를 정의 `Simple.Add`:

```csharp
Simple.Add(int a, int b)
{ return a + b; }
```

모듈 B 정의 `Fancy.AddTwice`:

```csharp
Fancy.AddTwice(int a, int b)
{ return Simple.Add(a,b) + Simple.Add(a,b); }
```

또한 가정 있습니다 `Fancy.AddTwice` 인라인 호출을 `SimpleAdd`입니다. 프로파일러를 사용 하 여이 열거자는 인라인이 모듈 B의에서 정의 된 모든 메서드를 찾을 `Simple.Add`, 하 고 결과 열거는 `AddTwice`합니다.  `inlineeModuleId` 모듈의 식별자 `A`, 및 `inlineeMethodId` 의 식별자 `Simple.Add(int a, int b)`합니다.

경우 `incompleteData` 함수 뒤도 마찬가지 열거자에 없는 인라인 처리 하는 모든 메서드는 지정 된 메서드를 반환 합니다. 이 경우 발생할 수 있습니다 또는 inliners 모듈의 직접 또는 간접 종속성 보다 아직 로드 하지 않은 합니다. 프로파일러에 정확한 데이터가 필요 이상의 모듈이 로드 되는 경우 가급적 각 모듈을 로드할 때 나중에 재시도 해야 합니다.

`EnumNgenModuleMethodsInliningThisMethod` 에서 제한 사항을 해결 하려면 메서드를 사용할 수 ReJIT에 대 한 인라인 처리 합니다. ReJIT 메서드의 구현을 변경 하 고 만든 다음 새 코드를 즉석에서 프로파일러를 수 있습니다. 예를 들어 변경 수 `Simple.Add` 다음과 같습니다.

```csharp
Simple.Add(int a, int b)
{ return 42; }
```

그러나 때문 `Fancy.AddTwice` 에 이미 인라인 `Simple.Add`, 동일 하 게 동작 이전과 같이 계속 합니다. 호출자가 해당 한계를 해결 하기 위해 인라인 있는 모든 모듈의 모든 메서드에 대 한 검색 `Simple.Add` 사용 하 여 `ICorProfilerInfo5::RequestRejit` 해당 메서드의 각 합니다. 새 동작을 갖습니다 메서드 다시 컴파일된 경우 `Simple.Add` 이전 동작을 대신 합니다.

## <a name="requirements"></a>요구 사항

**플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.

**헤더:** CorProf.idl, CorProf.h

**라이브러리:** CorGuids.lib

**.NET Framework 버전:** [!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]

## <a name="see-also"></a>참고자료

- [ICorProfilerInfo6 인터페이스](icorprofilerinfo6-interface.md)
