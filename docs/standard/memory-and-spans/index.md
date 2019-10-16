---
title: 메모리 및 범위
ms.date: 10/03/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- Memory<T>
- Span<T>
- buffers"
- pipeline processing
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fbfd091c821f59febfc8c7a203334454e7b59c12
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666431"
---
# <a name="memory--and-span-related-types"></a>메모리 및 범위 관련 형식

.NET Core 2.1부터 .NET에는 임의 메모리의 인접한 강력한 형식의 영역을 나타내는 여러 개의 상호 연결된 형식이 포함되어 있습니다. 여기에는 다음이 포함됩니다.

- <xref:System.Span%601?displayProperty=nameWithType> - 메모리의 인접한 영역에 액세스하는 데 사용되는 형식입니다. <xref:System.Span%601> 인스턴스는 `T` 형식 배열, <xref:System.String>, [stackalloc](../../csharp/language-reference/operators/stackalloc.md)로 할당된 버퍼 또는 관리되지 않는 메모리에 대한 포인터를 통해 지원할 수 있습니다. 스택에 할당되어야 하므로 여러 가지 제한 사항이 있습니다. 예를 들어 클래스의 필드는 <xref:System.Span%601> 형식일 수 없으며, 비동기 작업에 범위를 사용할 수도 없습니다.

- <xref:System.ReadOnlySpan%601?displayProperty=nameWithType> - 변경할 수 없는 <xref:System.Span%601> 구조체 버전입니다.

- <xref:System.Memory%601?displayProperty=nameWithType> - 스택이 아닌 관리되는 힙에 할당된 메모리의 인접한 영역입니다. <xref:System.Memory%601> 인스턴스는 `T` 형식 배열 또는 <xref:System.String>을 통해 지원할 수 있습니다. 관리되는 힙에 저장될 수 있으므로 <xref:System.Memory%601>에는 <xref:System.Span%601>의 제한 사항이 없습니다.

- <xref:System.ReadOnlyMemory%601?displayProperty=nameWithType> - 변경할 수 없는 <xref:System.Memory%601> 구조체 버전입니다.

- <xref:System.Buffers.MemoryPool%601?displayProperty=nameWithType> - 메모리 풀에서 강력한 형식의 메모리 블록을 소유자에게 할당합니다. <xref:System.Buffers.IMemoryOwner%601> 인스턴스는 <xref:System.Buffers.MemoryPool%601.Rent%2A?displayProperty=nameWithType>을 호출하여 풀에서 대여하고, <xref:System.Buffers.MemoryPool%601.Dispose?displayProperty=nameWithType>을 호출하여 다시 풀로 해제할 수 있습니다.

- <xref:System.Buffers.IMemoryOwner%601?displayProperty=nameWithType> - 메모리 블록의 소유자를 나타내고 해당 수명 관리를 제어합니다.

- <xref:System.Buffers.MemoryManager%601> - SafeHandle 등의 추가 형식을 통해 <xref:System.Memory%601>를 지원할 수 있도록 <xref:System.Memory%601>의 구현을 바꾸는 데 사용할 수 있는 추상 기본 클래스입니다. <xref:System.Buffers.MemoryManager%601>는 고급 시나리오를 위한 것입니다.

- <xref:System.ArraySegment%601> - 특정 인덱스에서 시작하는 특정 개수의 배열 요소에 대한 래퍼입니다.

- <xref:System.MemoryExtensions?displayProperty=nameWithType> - 문자열, 배열 및 배열 세그먼트를 <xref:System.Memory%601> 블록으로 변환하기 위한 확장 메서드 컬렉션입니다.

> [!NOTE]
> 이전 프레임워크의 경우 [System.Memory NuGet 패키지](https://www.nuget.org/packages/System.Memory/)에서 <xref:System.Span%601> 및 <xref:System.Memory%601>를 사용할 수 있습니다.

자세한 내용은 <xref:System.Buffers?displayProperty=nameWithType> 네임스페이스를 참조하세요.

## <a name="working-with-memory-and-span"></a>메모리 및 범위 작업

메모리 및 범위 관련 형식은 일반적으로 데이터를 처리 파이프라인에 저장하는 데 사용되므로 개발자가 <xref:System.Span%601>, <xref:System.Memory%601> 및 관련 형식을 사용할 때 모범 사례 세트를 따르는 것이 중요합니다. 이러한 모범 사례는 [메모리\<T> 및 범위\<T> 사용 지침](memory-t-usage-guidelines.md)에 설명되어 있습니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Memory%601?displayProperty=nameWithType>
- <xref:System.ReadOnlyMemory%601?displayProperty=nameWithType>
- <xref:System.Span%601?displayProperty=nameWithType>
- <xref:System.ReadOnlySpan%601?displayProperty=nameWithType>
- <xref:System.Buffers?displayProperty=nameWithType>
