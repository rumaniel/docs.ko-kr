---
title: ICorDebugSymbolProvider2::GetGenericDictionaryInfo 메서드
ms.date: 03/30/2017
ms.assetid: ba28fe4e-5491-4670-bff7-7fde572d7593
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 65407fca73971546725d9457d25bf1270d2001e2
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67662542"
---
# <a name="icordebugsymbolprovider2getgenericdictionaryinfo-method"></a>ICorDebugSymbolProvider2::GetGenericDictionaryInfo 메서드

제네릭 사전 맵을 검색합니다.

## <a name="syntax"></a>구문

```cpp
HRESULT GetGenericDictionaryInfo(
   [out] ICorDebugMemoryBuffer** ppMemoryBuffer
);
```

## <a name="parameters"></a>매개 변수

`ppMemoryBuffer`\
[out] 주소에 대 한 포인터를 [ICorDebugMemoryBuffer](../../../../docs/framework/unmanaged-api/debugging/icordebugmemorybuffer-interface.md) 제네릭 사전 맵이 포함 된 개체입니다. 자세한 내용은 설명 부분을 참조하세요.

## <a name="remarks"></a>설명

> [!NOTE]
> 이 메서드는 .NET 네이티브에서만 사용할 수 있습니다.

맵은 두 개의 최상위 섹션으로 구성됩니다.

- A [directory](#Directory) 이 맵에 포함 된 모든 사전의 상대 가상 주소 RVA ()를 포함 합니다.

- 바이트 맞춤 [힙](#Heap) 개체 인스턴스화 정보가 들어 있는입니다. 마지막 디렉터리 항목 후에 즉시 시작됩니다.

<a name="Directory"></a>

## <a name="the-directory"></a>디렉터리

디렉터리의 각 항목은 힙 내부의 오프셋을 나타냅니다. 즉, 힙의 시작 부분에 상대적인 오프셋입니다. 개별 항목의 값이 반드시 고유할 필요는 없습니다. 여러 디렉터리 항목이 힙의 동일한 오프셋을 가리킬 수 있습니다.

제네릭 사전 맵의 디렉터리 부분은 다음과 같은 구조로 되어 있습니다.

- 처음 4바이트에는 사전 항목 수(즉, 사전의 상대 가상 주소 수)가 포함됩니다. 이 값으로 이라고 *N*합니다. 상위 비트가 설정된 경우 항목은 상대 가상 주소의 오름차순으로 정렬됩니다.

- 합니다 *N* 디렉터리 항목이 뒤에 나옵니다. 각 항목은 4바이트 세그먼트 2개인 8바이트로 이루어져 있습니다.

  - 바이트 0-3: RVA; 사전의 상대 가상 주소입니다.

  - 바이트 4-7: 오프셋입니다. 힙의 시작에 상대적인 오프셋입니다.

<a name="Heap"></a>

## <a name="the-heap"></a>힙

스트림 판독기는 디렉터리 크기+4에서 스트림 길이를 빼서 힙 크기를 계산할 수 있습니다. 즉, 다음과 같습니다.

```csharp
Heap Size = Stream.Length – (Directory Size + 4)
```

여기서 디렉터리 크기는 `N * 8`입니다.

힙의 각 인스턴스화 정보 항목 형식은 다음과 같습니다.

- 압축된 ECMA 메타데이터 형식에서 이 인스턴스화 정보 항목의 길이(바이트)입니다. 이 길이 정보는 값에서 제외됩니다.

- 제네릭 인스턴스화 형식 수 또는 *T*, 압축 된 ECMA 메타 데이터 형식에서입니다.

- *T* ECMA 형식 서명 형식으로 나타내는 각 형식입니다.

각 힙 요소의 길이를 포함하면 힙에 영향을 주지 않고 디렉터리 섹션을 간단하게 정렬할 수 있습니다.

## <a name="requirements"></a>요구 사항

**플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.

**헤더:** CorDebug.idl, CorDebug.h

**라이브러리:** CorGuids.lib

**.NET Framework 버전:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]

## <a name="see-also"></a>참고자료

- [ICorDebugSymbolProvider2 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugsymbolprovider2-interface.md)
- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
