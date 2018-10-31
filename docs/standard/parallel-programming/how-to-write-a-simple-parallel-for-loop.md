---
title: '방법: 간단한 Parallel.For 루프 작성'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Parallel.For, How to Write
- for loop, parallel construction in .NET
- parallel for loops, how to use
ms.assetid: 9029ba7f-a9d1-4526-8c84-c88716dba5d4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1b2ebf679816684e68a1c13d660ef9fc54e3a175
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2018
ms.locfileid: "48845995"
---
# <a name="how-to-write-a-simple-parallelfor-loop"></a>방법: 간단한 Parallel.For 루프 작성

이 항목에는 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 메서드를 설명하는 두 가지 예제가 포함되어 있습니다. 첫 번째 예제에서는 <xref:System.Threading.Tasks.Parallel.For%28System.Int64%2CSystem.Int64%2CSystem.Action%7BSystem.Int64%7D%29?displayProperty=nameWithType> 메서드 오버로드를 사용하고, 두 번째 예제에서는 <xref:System.Threading.Tasks.Parallel.For%28System.Int32%2CSystem.Int32%2CSystem.Action%7BSystem.Int32%7D%29?displayProperty=nameWithType> 오버로드를 사용합니다. <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 메서드의 가장 간단한 오버로드 중 두 개입니다. 루프를 취소하거나, 루프 반복을 중단하거나, 스레드 로컬 상태를 유지할 필요가 없는 경우 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 메서드의 이러한 두 오버로드를 사용할 수 있습니다.

> [!NOTE]
> 이 문서에서는 람다 식을 사용하여 TPL에 대리자를 정의합니다. C# 또는 Visual Basic의 람다 식을 잘 모르는 경우 [PLINQ 및 TPL의 람다 식](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)을 참조하세요.

첫 번째 예제에서는 단일 디렉터리에 있는 파일의 크기를 계산합니다. 두 번째 예제에서는 두 행렬의 곱을 계산합니다.

## <a name="directory-size-example"></a>디렉터리 크기 예제

이 예제는 디렉터리에 있는 파일의 전체 크기를 계산하는 간단한 명령줄 유틸리티입니다. 단일 디렉터리 경로를 인수로 요구하고 해당 디렉터리에 있는 파일 수와 전체 크기를 보고합니다. 디렉터리가 있는지 확인한 후 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 메서드를 사용하여 디렉터리에 있는 파일을 열거하고 해당 파일 크기를 확인합니다. 각 파일 크기가 `totalSize` 변수에 추가됩니다. 추가가 원자성 작업으로 수행되도록 <xref:System.Threading.Interlocked.Add%2A?displayProperty=nameWithType>를 호출하여 추가가 수행됩니다. 그렇지 않은 경우 여러 작업이 `totalSize` 변수를 동시에 업데이트하려고 할 수 있습니다.

[!code-csharp[Conceptual.Parallel.For#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.parallel.for/cs/for1.cs#1)]
[!code-vb[Conceptual.Parallel.For#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.parallel.for/vb/for1.vb#1)]

## <a name="matrix-and-stopwatch-example"></a>행렬 및 스톱워치 예제

이 예제에서는 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 메서드를 사용하여 두 행렬의 곱을 계산합니다. 또한 <xref:System.Diagnostics.Stopwatch?displayProperty=nameWithType> 클래스를 사용하여 병렬 루프와 비병렬 루프의 성능을 비교하는 방법을 보여 줍니다. 대용량의 출력을 생성할 수 있으므로 예제에서는 출력을 파일로 리디렉션할 수 있도록 합니다.

[!code-csharp[TPL_Parallel#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/simpleparallelfor.cs#01)]
[!code-vb[TPL_Parallel#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/simpleparallelfor.vb#01)]

루프를 포함하여 코드를 병렬 처리하는 경우 한 가지 중요한 목표는 병렬 처리의 오버헤드가 성능 혜택보다 큰 지점까지 과도하게 병렬 처리하지 않고 최대한 많은 프로세서를 활용하는 것입니다. 이 특정 예제에서는 내부 루프에서 많은 작업이 수행되지 않으므로 외부 루프만 병렬 처리됩니다. 적은 작업량과 원치 않는 캐시 결과로 인해 중첩된 병렬 루프에서 성능이 저하될 수 있습니다. 따라서 외부 루프만 병렬 처리하는 것이 대부분의 시스템에서 동시성의 이점을 극대화하는 가장 좋은 방법입니다.

## <a name="the-delegate"></a>대리자

이 <xref:System.Threading.Tasks.Parallel.For%2A> 오버로드의 세 번째 매개 변수는 `Action<int>`(C#) 또는 `Action(Of Integer)`(Visual Basic) 형식의 대리자입니다. `Action` 대리자는 0개, 1개 또는 16개의 형식 매개 변수가 있는지에 관계없이 항상 void를 반환합니다. Visual Basic에서 `Action`의 동작은 `Sub`를 사용하여 정의됩니다. 예제에서는 람다 식을 사용하여 대리자를 만들지만 다른 방법으로도 대리자를 만들 수 있습니다. 자세한 내용은 [PLINQ 및 TPL의 람다 식](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)을 참조하세요.

## <a name="the-iteration-value"></a>반복 값

대리자는 값이 현재 반복인 단일 입력 매개 변수를 사용합니다. 이 반복 값은 런타임에서 제공되며, 해당 시작 값은 현재 스레드에서 처리 중인 소스 세그먼트(파티션)의 첫 번째 요소 인덱스입니다.

동시성 수준보다 더 많은 제어가 필요한 경우 <xref:System.Threading.Tasks.ParallelOptions?displayProperty=nameWithType> 입력 매개 변수를 사용하는 오버로드 중 하나(예: <xref:System.Threading.Tasks.Parallel.For%28System.Int32%2CSystem.Int32%2CSystem.Threading.Tasks.ParallelOptions%2CSystem.Action%7BSystem.Int32%2CSystem.Threading.Tasks.ParallelLoopState%7D%29?displayProperty=nameWithType>)를 사용합니다.

## <a name="return-value-and-exception-handling"></a>반환 값 및 예외 처리

모든 스레드가 완료되면 <xref:System.Threading.Tasks.Parallel.For%2A>에서 <xref:System.Threading.Tasks.ParallelLoopResult?displayProperty=nameWithType> 개체를 반환합니다. 이 반환 값은 <xref:System.Threading.Tasks.ParallelLoopResult>가 완료될 때까지 실행된 마지막 반복과 같은 정보를 저장하기 때문에 루프 반복을 수동으로 중지 또는 중단하는 경우에 유용합니다. 스레드 중 하나에서 하나 이상의 예외가 발생하는 경우 <xref:System.AggregateException?displayProperty=nameWithType>이 발생합니다.

이 예제의 코드에서는 <xref:System.Threading.Tasks.Parallel.For%2A>의 반환 값이 사용되지 않습니다.

## <a name="analysis-and-performance"></a>분석 및 성능

성능 마법사를 사용하여 컴퓨터의 CPU 사용량을 볼 수 있습니다. 실험적으로 행렬의 열과 행 수를 늘려봅니다. 행렬이 클수록 병렬 및 순차적 계산 버전 간의 성능 차이가 커집니다. 행렬이 작으면 병렬 루프를 설정하는 오버헤드 때문에 순차적 버전이 더 빨리 실행됩니다.

콘솔 또는 파일 시스템과 같은 공유 리소스에 대한 동기 호출은 병렬 루프의 성능을 상당히 저하시킵니다. 성능을 측정하는 경우 루프 내에서 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType>과 같은 호출을 사용하지 않도록 하세요.

## <a name="compile-the-code"></a>코드 컴파일

이 코드를 복사하여 Visual Studio 프로젝트에 붙여넣습니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Threading.Tasks.Parallel.For%2A>
- <xref:System.Threading.Tasks.Parallel.ForEach%2A>
- [데이터 병렬 처리](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)
- [병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)
