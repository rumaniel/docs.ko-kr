---
title: Windows 시스템의 큰 개체 힙
ms.date: 05/02/2018
helpviewer_keywords:
- large object heap (LOH)"
- LOH
- garbage collection, large object heap
- GC [.NET ], large object heap
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4663c42b784334f66318c61d531ab4cee2f8b02e
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71354048"
---
# <a name="the-large-object-heap-on-windows-systems"></a>Windows 시스템의 큰 개체 힙

.NET GC(가비지 수집기)는 개체를 큰 개체 및 작은 개체로 나눕니다. 개체가 크면 그 특성 중 일부는 개체가 작을 때보다 중요합니다. 예를 들어 개체 압축, 즉 힙의 다른 위치에서 메모리에 복사하는 경우 비용이 많이 들 수 있습니다. 이로 인해 .NET 가비지 수집기는 LOH(큰 개체 힙)에 큰 개체를 배치합니다. 이 항목에서는 큰 개체 힙에 대해 자세히 살펴보겠습니다. 즉 개체가 큰 개체로 정규화하는 기능, 이러한 큰 개체를 수집하는 방법 및 큰 개체에서 이용하는 성능에 대한 함축적 유형에 대해 설명합니다.

> [!IMPORTANT]
> 이 항목에서는 Windows 시스템에서만 실행되는 .NET Framework 및 .NET Core의 큰 개체 힙에 대해 설명합니다. 다른 플랫폼의 .NET 구현에서 실행되는 LOH는 다루지 않습니다.

## <a name="how-an-object-ends-up-on-the-large-object-heap-and-how-gc-handles-them"></a>개체가 큰 개체 힙에서 종료하는 방법 및 GC에서 처리하는 방법

개체는 85,000바이트 이상이면 큰 개체로 간주됩니다. 이 숫자는 성능 튜닝으로 결정됩니다. 개체 할당 요청이 85,000바이트 이상이면 런타임에서 이를 큰 개체 힙에 할당합니다.

이 의미를 이해하려면 .NET GC에 대한 몇 가지 기본 사항을 검토하는 것이 유용합니다.

.NET 가비지 수집기는 세대 수집기입니다. 세 개의 세대, 즉 0세대, 1세대 및 2세대가 있습니다. 세 개의 세대가 있는 이유는 잘 조정된 응용 프로그램에서 대부분의 개체가 0세대에서 소멸된다는 것입니다. 예를 들어 서버 응용 프로그램에서는 요청이 완료되면 각 요청과 관련된 할당이 소멸되어야 합니다. 진행 중인 할당 요청은 1세대가 되고 여기서 소멸됩니다. 기본적으로 1세대는 최근에 생성된 개체 영역과 수명이 긴 개체 영역 간의 버퍼 역할을 합니다.

작은 개체는 항상 0세대에 할당되며 수명에 따라 1세대 또는 2세대로 승격될 수 있습니다. 큰 개체는 항상 2세대에 할당됩니다.

큰 개체는 2세대 수집 동안에만 수집되므로 2세대에 속합니다. 특정 세대가 수집되면 그 이전 세대도 모두 수집됩니다. 예를 들어 1세대 GC가 수행되면 0세대와 1세대가 모두 수집되고, 2세대 GC가 수행되면 전체 힙이 수집됩니다. 이러한 이유로 2세대 GC는 *전체 GC*라고도 합니다. 이 문서에서는 전체 GC 대신 2세대 GC를 언급하지만 용어는 서로 바꿔 사용할 수 있습니다.

세대는 GC 힙의 논리적 뷰를 제공합니다. 실제로 개체는 관리되는 힙 세그먼트에 있습니다. *관리되는 힙 세그먼트*는 GC에서 관리 코드 대신 [VirtualAlloc 함수](/windows/desktop/api/memoryapi/nf-memoryapi-virtualalloc)를 호출하여 OS로부터 예약하는 메모리 청크입니다. CLR이 로드되면 GC에서 작은 개체(SOH 또는 작은 개체 힙)와 큰 개체(큰 개체 힙)에 대해 하나씩 두 개의 초기 힙 세그먼트를 할당합니다.

그런 다음, 이러한 관리되는 힙 세그먼트에 관리되는 개체를 배치하여 할당 요청이 충족됩니다. 개체가 85,000바이트보다 작으면 SOH용 세그먼트에 배치되며, 그렇지 않으면 LOH 세그먼트에 배치됩니다. 세그먼트에 더 많은 개체가 할당됨에 따라 세그먼트가 더 작은 청크로 커밋됩니다.
SOH의 경우 GC에 남아 있는 개체는 다음 세대로 승격됩니다. 0세대 수집에서 남아 있는 개체는 이제 1세대 개체로 간주되는 방식 등으로 승격됩니다. 그러나 가장 오래된 세대에 남아 있는 개체는 여전히 가장 오래된 세대로 간주됩니다. 즉 2세대에 남아 있는 개체는 2세대 개체가 되고, LOH에 남아 있는 개체는 LOH 개체가 됩니다(2세대와 함께 수집됨).

사용자 코드에서는 0세대(작은 개체) 또는 LOH(큰 개체)만 할당할 수 있습니다. GC만이 0세대에 남아 있는 개체를 승격하여 1세대에, 1세대와 2세대에 남아 있는 개체를 승격하여 2세대에 "할당"할 수 있습니다.

가비지 수집이 트리거되면 GC에서 남아 있는 개체를 모두 추적하여 압축합니다. 그러나 압축하는 데 비용이 많이 들므로 GC는 LOH를 *정리*합니다. 이 경우 나중에 큰 개체 할당 요청을 충족하는 데 다시 사용할 수 있는 소멸된 개체에서 사용 가능한 개체 목록을 만듭니다. 인접한 소멸된 개체는 하나의 사용 가능한 개체가 됩니다.

.NET Core 및 .NET Framework(.NET Framework 4.5.1 이상)에는 사용자가 다음 번의 전체 GC 차단 중에 LOH를 압축해야 한다고 지정할 수 있는 <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode?displayProperty=nameWithType> 속성이 있습니다. 그리고 앞으로는 .NET에서 LOH를 자동으로 압축하도록 결정할 수 있을 것입니다. 즉, 큰 개체를 할당하고 이동하지 못하도록 하려면 해당 개체를 고정해야 합니다.

그림 1에서는 GC에서 `Obj1`과 `Obj3`이 소멸된 첫 번째 0세대 GC 이후에 1세대를 형성하고, `Obj2`와 `Obj5`가 소멸된 첫 번째 1세대 이후에 2세대를 형성하는 시나리오를 보여 줍니다. 이 그림과 다음 그림은 설명을 위한 것입니다. 여기에는 힙에서 발생하는 작업을 더 잘 보여 주기 위해 매우 적은 수의 개체가 포함되어 있습니다. 실제로 더 많은 개체가 일반적으로 GC에 포함됩니다.

![그림 1: 0세대 GC 및 1세대 GC](media/loh/loh-figure-1.jpg)\
그림 1: 0세대 및 1세대 GC

그림 2에서는 `Obj1`과 `Obj2`가 소멸되었음을 확인한 2세대 GC 이후에 GC가 `Obj1`과 `Obj2`에서 점유하는 데 사용한 메모리에서 연속적인 사용 가능한 공간을 형성하여 `Obj4`에 대한 할당 요청을 충족하는 데 사용했음을 보여 줍니다. 마지막 개체인 `Obj3` 뒤에서 세그먼트 끝까지의 공간도 할당 요청을 충족하는 데 사용할 수 있습니다.

![그림 2: 2세대 GC 이후](media/loh/loh-figure-2.jpg)\
그림 2: 2세대 GC 이후

큰 개체 할당 요청을 수용할 사용 가능한 공간이 부족한 경우 GC는 먼저 OS에서 더 많은 세그먼트를 획득하려고 시도합니다. 이 작업이 실패하면 일부 공간을 확보하기 위해 2세대 GC가 트리거됩니다.

1세대 또는 2세대 GC 동안 가비지 수집기는 [VirtualFree 함수](/windows/desktop/api/memoryapi/nf-memoryapi-virtualfree)를 호출하여 남아 있는 개체가 없는 세그먼트를 OS에 다시 릴리스합니다. 마지막 남아 있는 개체 뒤에서 세그먼트 끝까지의 공간은 커밋 해제됩니다(애플리케이션이 즉시 할당되기 때문에 가비지 수집기에서 커밋된 일부 개체를 유지하는 0세대/1세대가 남아 있는 임시 세그먼트는 제외). 그리고 사용 가능한 공간은 다시 설정되어도 커밋된 상태로 유지되므로 OS에서 데이터를 디스크에 다시 쓸 필요가 없습니다.

LOH는 2세대 GC 동안에만 수집되므로 LOH 세그먼트는 이러한 GC 동안에만 해제될 수 있습니다. 그림 3에서는 가비지 수집기에서 한 세그먼트(세그먼트 2)를 OS로 다시 릴리스하고, 나머지 세그먼트에 대해 더 많은 공간을 커밋 해제하는 시나리오를 보여 줍니다. 큰 개체 할당 요청을 충족하기 위해 세그먼트 끝에 있는 커밋 해제된 공간을 사용해야 하는 경우 메모리를 다시 커밋합니다. 커밋/커밋 해제에 대한 설명은 [VirtualAlloc](/windows/desktop/api/memoryapi/nf-memoryapi-virtualalloc)에 대한 설명서를 참조하세요.

![그림 3: 2세대 GC 이후의 LOH](media/loh/loh-figure-3.jpg)\
그림 3: 2세대 GC 이후의 LOH

## <a name="when-is-a-large-object-collected"></a>큰 개체가 수집되는 경우

일반적으로 다음 3가지 조건 중 하나가 발생하면 GC가 수행됩니다.

- 할당이 0세대 또는 큰 개체 임계값을 초과합니다.

  임계값은 세대의 속성입니다. 세대에 대한 임계값은 가비지 수집기에서 개체를 할당할 때 설정됩니다. 임계값이 초과되면 해당 세대에서 GC가 트리거됩니다. 작은 개체 또는 큰 개체를 할당할 때 0세대 및 LOH의 임계값을 각각 사용합니다. 가비지 수집기에서 1세대와 2세대에 할당하는 경우 해당 임계값을 사용합니다. 이러한 임계값은 프로그램이 실행될 때 동적으로 튜닝됩니다.

  이는 일반적인 경우입니다. 대부분의 GC는 관리되는 힙에 대한 할당으로 인해 수행됩니다.

- <xref:System.GC.Collect%2A?displayProperty=nameWithType> 메서드가 호출됩니다.

  매개 변수가 없는 <xref:System.GC.Collect?displayProperty=nameWithType> 메서드가 호출되거나 다른 오버로드에서 인수로 <xref:System.GC.MaxGeneration?displayProperty=nameWithType>을 전달하면 LOH가 나머지 관리되는 힙과 함께 수집됩니다.

- 시스템 메모리가 부족합니다.

  이는 가비지 수집기에서 OS로부터 높은 메모리 알림을 받을 때 발생합니다. 가비지 수집기에서 2세대 GC 작업이 생산적이라고 인식하면 해당 GC를 트리거합니다.

## <a name="loh-performance-implications"></a>LOH 성능의 함축적 의미

큰 개체 힙에 대한 할당은 다음과 같은 방식으로 성능에 영향을 줍니다.

- 할당 비용

  CLR은 제공하는 모든 새 개체에 대한 메모리를 지울 수 보장합니다. 즉, 큰 개체의 할당 비용은 GC를 트리거하지 않는 한 메모리 지우기를 통해 완전히 결정됩니다. 1바이트를 비우는 데 2회의 주기가 걸리는 경우 가장 작은 큰 개체를 지우는 데 170,000회의 주기가 필요합니다. 2GHz 머신에서 16MB 개체의 메모리를 지우는 데 약 16ms가 걸립니다. 이는 다소 큰 비용입니다.

- 수집 비용

  LOH와 2세대가 함께 수집되므로 어느 하나의 임계값이 초과되면 2세대 수집이 트리거됩니다. LOH로 인해 2세대 수집이 트리거되면 GC 이후에 2세대가 반드시 더 작아질 수는 없습니다. 2세대에 대한 데이터가 많지 않으면 이로 인한 영향을 최소화합니다. 그러나 2세대가 큰 경우 2세대 GC가 많이 트리거되면 성능 문제가 발생할 수 있습니다. 큰 개체가 아주 일시적으로 많이 할당되고 SOH가 큰 경우 GC를 수행하는 데 너무 많은 시간이 걸릴 수 있습니다. 또한 할당 비용은 정말로 큰 개체를 계속 할당하고 내보내는 경우 크게 증가할 수 있습니다.

- 참조 형식이 있는 배열 요소

  LOH의 매우 큰 개체는 일반적으로 배열이며, 실제로 큰 인스턴스 개체는 거의 없습니다. 참조가 많은 배열 요소인 경우 참조가 많지 않은 요소에 존재하지 않는 비용이 발생합니다. 참조가 없는 요소인 경우 배열을 가비지 수집기에서 배열을 거칠 필요가 전혀 없습니다. 예를 들어 배열을 사용하여 노드를 이진 트리에 저장하는 경우, 이를 구현하는 한 가지 방법은 다음과 같이 실제 노드를 통해 오른쪽 노드와 왼쪽 노드를 참조하는 것입니다.

  ```csharp
  class Node
  {
     Data d;
     Node left;
     Node right;
  };

  Node[] binary_tr = new Node [num_nodes];
  ```

  `num_nodes`가 큰 경우 가비지 수집기는 요소당 둘 이상의 참조를 거쳐야 합니다. 또 다른 방법은 다음과 같이 오른쪽 노드와 왼쪽 노드의 인덱스를 저장하는 것입니다.

  ```csharp
  class Node
  {
     Data d;
     uint left_index;
     uint right_index;
  } ;
  ```

  왼쪽 노드의 데이터를 `left.d`로 참조하는 대신 `binary_tr[left_index].d`로 참조합니다. 그리고 가비지 수집기에서는 왼쪽 노드와 오른쪽 노드에 대한 참조를 확인할 필요가 없습니다.

세 가지 요소 중 처음 두 가지는 일반적으로 세 번째 요소보다 더 중요합니다. 이에 따라 임시 개체를 할당하는 대신 다시 사용하는 큰 개체의 풀을 할당하는 것이 좋습니다.

## <a name="collecting-performance-data-for-the-loh"></a>LOH에 대한 성능 데이터 수집

특정 영역에 대한 성능 데이터를 수집하려면 다음 작업을 이미 완료했어야 합니다.

1. 해당 영역을 검토했다는 증명 정보를 찾았습니다.

2. 확인한 성능 문제를 설명할 수 있는 항목을 찾지 못한 채 알고 있는 다른 영역을 모두 소진했습니다.

메모리 및 CPU의 기본 사항에 대한 자세한 내용은 [문제를 파악한 후 해결 방법 찾기](https://devblogs.microsoft.com/dotnet/understand-the-problem-before-you-try-to-find-a-solution/) 블로그를 참조하세요.

LOH 성능에 대한 데이터를 수집하는 데 사용할 수 있는 도구는 다음과 같습니다.

- [.NET CLR 메모리 성능 카운터](#net-clr-memory-performance-counters)

- [ETW 이벤트](#etw-events)

- [디버거](#a-debugger)

### <a name="net-clr-memory-performance-counters"></a>.NET CLR 메모리 성능 카운터

이러한 성능 카운터는 일반적으로 성능 문제를 조사하는 데 유용한 첫 번째 단계입니다(하지만 [ETW 이벤트](#etw-events) 사용이 권장됨). 그림 4와 같이 원하는 카운터를 추가하여 성능 모니터를 구성합니다. LOH와 관련된 카운터는 다음과 같습니다.

- **2세대 수집**

   프로세스가 시작된 이후 수행된 2세대 GC 횟수를 표시합니다. 이 카운터는 2세대 수집(전체 가비지 수집이라고도 함)이 끝날 때 증가합니다. 이 카운터는 마지막으로 관찰된 값을 표시합니다.

- **Large Object Heap size**

   사용 가능한 공간을 포함하여 LOH의 현재 크기(바이트)를 표시합니다. 이 카운터는 각 할당이 아니라 가비지 컬렉션이 끝날 때 업데이트됩니다.

성능 카운터를 확인하는 일반적인 방법은 성능 모니터(perfmon.exe)를 사용하는 것입니다. "카운터 추가" 명령을 사용하여 관심 있는 프로세스에 대해 원하는 카운터를 추가합니다. 그림 4와 같이 성능 카운터 데이터를 로그 파일에 저장할 수 있습니다.

![성능 카운터 추가를 보여주는 스크린샷.](media/large-object-heap/add-performance-counter.png)
그림 4: 2세대 GC 이후의 LOH

또한 성능 카운터는 프로그래밍 방식으로 쿼리할 수도 있습니다. 많은 사람들이 일상적인 테스트 프로세스의 일환으로 이러한 방식으로 성능 데이터를 수집합니다. 정상적이지 않은 값이 있는 카운터가 검색되면 다른 방법을 사용하여 조사하는 데 유용한 더 자세한 정보를 얻을 수 있습니다.

> [!NOTE]
> ETW에서 훨씬 더 많은 정보를 제공하므로 성능 카운터 대신 ETW 이벤트를 사용하는 것이 좋습니다.

### <a name="etw-events"></a>ETW 이벤트

가비지 수집기는 힙에서 수행하는 작업과 그 이유를 파악하는 데 도움이 되는 다양한 ETW 이벤트 집합을 제공합니다. 다음 블로그 게시물에서는 ETW를 통해 GC 이벤트를 수집하고 파악하는 방법을 보여 줍니다.

- [GC ETW 이벤트 - 1](https://devblogs.microsoft.com/dotnet/gc-etw-events-1/)

- [GC ETW 이벤트 - 2](https://devblogs.microsoft.com/dotnet/gc-etw-events-2/)

- [GC ETW 이벤트 - 3](https://devblogs.microsoft.com/dotnet/gc-etw-events-3/)

- [GC ETW 이벤트 - 4](https://devblogs.microsoft.com/dotnet/gc-etw-events-4/)

임시 LOH 할당으로 인해 발생된 과도한 2세대 GC를 확인하려면 GC에 대한 트리거 이유 열을 살펴봅니다. 임시 큰 개체만 할당하는 간단한 테스트의 경우 다음 [PerfView](https://www.microsoft.com/download/details.aspx?id=28567) 명령줄을 사용하여 ETW 이벤트에 대한 정보를 수집할 수 있습니다.

```console
perfview /GCCollectOnly /AcceptEULA /nogui collect
```

결과는 다음과 같습니다.

![PerfView에서 ETW 이벤트를 보여주는 스크린샷.](media/large-object-heap/event-tracing-windows-perfview.png)
그림 5: PerfView를 사용하여 표시된 ETW 이벤트

여기서 알 수 있듯이, 모든 GC는 2세대 GC이며 AllocLarge를 통해 모두 트리거됩니다. 즉, 큰 개체를 할당하면 이 GC가 트리거됩니다. **LOH 잔존율 %** 열이 1%라고 표시되므로 이러한 할당은 일시적입니다.

이러한 큰 개체를 할당한 사람을 알려주는 추가 ETW 이벤트를 수집할 수 있습니다. 다음과 같은 명령줄이 있습니다.

```console
perfview /GCOnly /AcceptEULA /nogui collect
```

이 명령은 대략 100,000개의 할당마다 실행되는 AllocationTick 이벤트를 수집합니다. 즉, 큰 개체가 할당될 때마다 이벤트가 실행됩니다. 큰 개체를 할당한 호출 스택을 보여 주는 GC 힙 할당 보기 중 하나를 살펴볼 수 있습니다.

![가비지 수집기 힙 보기를 보여주는 스크린샷.](media/large-object-heap/garbage-collector-heap.png)
그림 6: GC 힙 할당 보기

여기서 알 수 있듯이, 이는 `Main` 메서드에서 큰 개체를 할당하는 매우 간단한 테스트입니다.

### <a name="a-debugger"></a>디버거

메모리 덤프만 있고 실제로 LOH에 있는 개체를 확인해야 하는 경우 .NET에서 제공하는 [SoS 디버거 확장](../../../docs/framework/tools/sos-dll-sos-debugging-extension.md)을 사용할 수 있습니다.

> [!NOTE]
> 이 섹션에서 설명하는 디버깅 명령은 [Windows 디버거](https://www.microsoft.com/whdc/devtools/debugging/default.mspx)에 적용할 수 있습니다.

다음은 LOH 분석에서 나오는 출력 샘플입니다.

```console
0:003> .loadby sos mscorwks
0:003> !eeheap -gc
Number of GC Heaps: 1
generation 0 starts at 0x013e35ec
sdgeneration 1 starts at 0x013e1b6c
generation 2 starts at 0x013e1000
ephemeral segment allocation context: none
segment   begin allocated     size
0018f2d0 790d5588 790f4b38 0x0001f5b0(128432)
013e0000 013e1000 013e35f8 0x000025f8(9720)
Large object heap starts at 0x023e1000
segment   begin allocated     size
023e0000 023e1000 033db630 0x00ffa630(16754224)
033e0000 033e1000 043cdf98 0x00fecf98(16699288)
043e0000 043e1000 05368b58 0x00f87b58(16284504)
Total Size 0x2f90cc8(49876168)
------------------------------
GC Heap Size 0x2f90cc8(49876168)
0:003> !dumpheap -stat 023e1000 033db630
total 133 objects
Statistics:
MT   Count   TotalSize Class Name
001521d0       66     2081792     Free
7912273c       63     6663696 System.Byte[]
7912254c       4     8008736 System.Object[]
Total 133 objects
```

LOH 힙 크기는 (16,754,224 + 16,699,288 + 16,284,504) = 49,738,016바이트입니다. 023e1000과 033db630 주소 사이에서 <xref:System.Object?displayProperty=nameWithType> 개체의 배열에서 8,008,736바이트, <xref:System.Byte?displayProperty=nameWithType> 개체의 배열에서 6,663,696바이트 및 사용 가능한 공간으로 2,081,792바이트를 차지합니다.

경우에 따라 디버거에서 LOH의 전체 크기가 85,000바이트 미만임을 보여 줍니다. 이는 런타임 자체에서 LOH를 사용하여 큰 개체보다 작은 일부 개체를 할당하기 때문에 발생합니다.

LOH는 압축되지 않으므로 LOH가 조각화의 원인으로 간주되는 경우도 있습니다. 조각화의 의미는 다음과 같습니다.

- 관리되는 힙의 조각화 - 관리되는 개체 간에 사용 가능한 공간 크기로 표시됩니다. SoS에서 `!dumpheap –type Free` 명령은 관리되는 개체 간에 사용 가능한 공간 크기를 표시합니다.

- VM(가상 메모리) 주소 공간의 조각화 - `MEM_FREE`로 표시되는 메모리입니다. windbg에서 다양한 디버거 명령을 사용하여 가져올 수 있습니다.

   다음 예제에서는 VM 공간의 조각화를 보여 줍니다.

   ```console
   0:000> !address
   00000000 : 00000000 - 00010000
   Type     00000000
   Protect 00000001 PAGE_NOACCESS
   State   00010000 MEM_FREE
   Usage   RegionUsageFree
   00010000 : 00010000 - 00002000
   Type     00020000 MEM_PRIVATE
   Protect 00000004 PAGE_READWRITE
   State   00001000 MEM_COMMIT
   Usage   RegionUsageEnvironmentBlock
   00012000 : 00012000 - 0000e000
   Type     00000000
   Protect 00000001 PAGE_NOACCESS
   State   00010000 MEM_FREE
   Usage   RegionUsageFree
   … [omitted]
   -------------------- Usage SUMMARY --------------------------
   TotSize (     KB)   Pct(Tots) Pct(Busy)   Usage
   701000 (   7172) : 00.34%   20.69%   : RegionUsageIsVAD
   7de15000 ( 2062420) : 98.35%   00.00%   : RegionUsageFree
   1452000 (   20808) : 00.99%   60.02%   : RegionUsageImage
   300000 (   3072) : 00.15%   08.86%   : RegionUsageStack
   3000 (     12) : 00.00%   00.03%   : RegionUsageTeb
   381000 (   3588) : 00.17%   10.35%   : RegionUsageHeap
   0 (       0) : 00.00%   00.00%   : RegionUsagePageHeap
   1000 (       4) : 00.00%   00.01%   : RegionUsagePeb
   1000 (       4) : 00.00%   00.01%   : RegionUsageProcessParametrs
   2000 (       8) : 00.00%   00.02%   : RegionUsageEnvironmentBlock
   Tot: 7fff0000 (2097088 KB) Busy: 021db000 (34668 KB)

   -------------------- Type SUMMARY --------------------------
   TotSize (     KB)   Pct(Tots) Usage
   7de15000 ( 2062420) : 98.35%   : <free>
   1452000 (   20808) : 00.99%   : MEM_IMAGE
   69f000 (   6780) : 00.32%   : MEM_MAPPED
   6ea000 (   7080) : 00.34%   : MEM_PRIVATE

   -------------------- State SUMMARY --------------------------
   TotSize (     KB)   Pct(Tots) Usage
   1a58000 (   26976) : 01.29%   : MEM_COMMIT
   7de15000 ( 2062420) : 98.35%   : MEM_FREE
   783000 (   7692) : 00.37%   : MEM_RESERVE

   Largest free region: Base 01432000 - Size 707ee000 (1843128 KB)
   ```

가비지 수집기에서 자주 OS로부터 새 관리되는 힙 세그먼트를 얻고 빈 세그먼트를 OS로 릴리스하는 데 필요한 임시 큰 개체로 인해 가상 메모리 조각화가 발생하는 경우가 더 일반적입니다.

LOH로 인해 VM 조각화가 발생하는지 확인하려면 [VirtualAlloc](/windows/desktop/api/memoryapi/nf-memoryapi-virtualalloc) 및 [VirtualFree](/windows/desktop/api/memoryapi/nf-memoryapi-virtualfree)에 중단점을 설정하고 이를 호출하는 사람을 확인하면 됩니다. 예를 들어 OS에서 8MB보다 큰 가상 메모리 청크를 할당하려고 한 사람을 확인하려면 다음과 같이 중단점을 설정할 수 있습니다.

```console
bp kernel32!virtualalloc "j (dwo(@esp+8)>800000) 'kb';'g'"
```

이 명령은 디버거를 시작하고 8MB(0x800000)보다 큰 할당 크기로 인해 [VirtualAlloc](/windows/desktop/api/memoryapi/nf-memoryapi-virtualalloc)가 호출되는 경우에만 호출 스택을 표시합니다.

CLR 2.0에는 크고 작은 개체 힙에 포함되는 세그먼트를 자주 획득하고 릴리스하는 시나리오에 유용할 수 있는 *VM Hoarding*(VM 비축)이라는 기능이 추가되었습니다. VM Hoarding을 지정하려면 호스팅 API를 통해 `STARTUP_HOARD_GC_VM`이라는 시작 플래그를 지정합니다. CLR은 빈 세그먼트를 OS로 다시 릴리스하는 대신, 이러한 세그먼트의 메모리를 커밋 해제하고 대기 목록에 배치합니다. (CLR은 너무 큰 세그먼트에 대해 이 작업을 수행하지 않습니다.) CLR은 나중에 새 세그먼트 요청을 충족하는 데 이러한 세그먼트를 사용합니다. 다음에 응용 프로그램에 새 세그먼트가 필요할 때 CLR에서 충분히 큰 세크먼트를 찾을 수 있으면 이 대기 목록에 있는 세그먼트를 사용합니다.

또한 VM Hoarding은 메모리 부족 예외를 방지하기 위해 이미 획득한 세그먼트를 유지하려는 애플리케이션(예 시스템에서 실행되는 주요 애플리케이션인 일부 서버 애플리케이션)에 유용합니다.

이 기능을 사용할 때 애플리케이션을 주의 깊게 테스트하여 애플리케이션에서 메모리 사용을 매우 안정적으로 유지하도록 하는 것이 좋습니다.
