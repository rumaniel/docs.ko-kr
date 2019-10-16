---
title: PLINQ의 속도 향상 이해
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, performance tuning
ms.assetid: 53706c7e-397d-467a-98cd-c0d1fd63ba5e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 014adfbf6f9afab0eaacd574cfb181c0eec07b5b
ms.sourcegitcommit: ffd7dd79468a81bbb0d6449f6d65513e050c04c4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65960317"
---
# <a name="understanding-speedup-in-plinq"></a>PLINQ의 속도 향상 이해
PLINQ의 기본 목적은 다중 코어 컴퓨터에서 쿼리 대리자를 병렬로 실행하여 LINQ to Objects 쿼리의 실행 속도를 높이는 것입니다. PLINQ는 소스 컬렉션의 각 요소 처리가 개별 대리자 간에 공유 상태가 관련되지 않고 독립적인 경우 최고의 성능을 발휘합니다. 이러한 작업은 LINQ to Objects 및 PLINQ에서 공통적이고 여러 스레드가 쉽게 예약에 참여하므로 “즐거운 병렬”이라고 합니다. 그러나 모든 쿼리가 완전히 즐거운 병렬 작업으로 구성되는 것은 아니고, 대부분의 경우 쿼리에는 병렬 처리할 수 없거나 병렬 실행을 느리게 하는 일부 연산자가 포함됩니다. 또한 완전히 즐거운 병렬인 쿼리를 사용해도 PLINQ는 스레드에서 데이터 분할하고 작업을 예약해야 하며 일반적으로 쿼리가 완료될 때 결과를 병합해야 합니다. 이러한 모든 작업은 병렬 처리 계산 비용에 추가됩니다. 이러한 병렬 처리 추가 비용을 ‘오버헤드’라고 합니다. PLINQ 쿼리의 성능을 최적화하기 위해 목표는 즐거운 병렬인 파트를 최대화하고 오버헤드가 필요한 파트를 최소화하는 것입니다. 이 문서에서는 올바른 결과를 생성하면서 가능한 한 효율적인 PLINQ 쿼리를 작성하는 데 도움이 되는 정보를 제공합니다.  
  
## <a name="factors-that-impact-plinq-query-performance"></a>PLINQ 쿼리 성능에 영향을 주는 요소  
 다음 섹션에는 병렬 쿼리 성능에 영향을 주는 가장 중요한 요소 중 일부를 보여줍니다. 이들은 모든 경우에 독립적으로 쿼리 성능을 예측할 만큼 충분하지 않은 일반 문입니다. 항상 다양한 대표 구성 및 로드를 사용하여 컴퓨터에서 특정 쿼리의 실제 성능을 측정하는 것이 중요합니다.  
  
1. 전체 작업의 계산 비용.  
  
     속도를 높이기 위해 PLINQ 쿼리에는 오버헤드를 오프셋할 만큼 충분한 즐거운 병렬 작업이 있어야 합니다. 작업은 각 대리자의 계산 비용에 소스 컬렉션의 요소 수를 곱한 값으로 표시될 수 있습니다. 작업이 병렬 처리될 수 있다고 가정하면 계산 비용이 더 많이 들수록 속도를 높일 기회가 더 많습니다. 예를 들어 함수를 실행하는 데 1밀리초가 걸리는 경우 1000개 요소에 대한 순차적 쿼리가 해당 작업을 수행하는 데는 1초가 걸리는 반면 4개 코어가 있는 컴퓨터의 병렬 쿼리는 단 250밀리초가 걸릴 수 있습니다. 이를 통해 750밀리초의 속도가 향상됩니다. 각 요소에 대해 함수를 실행하는 데 1초가 필요한 경우 750초의 속도가 향상됩니다. 대리자의 비용이 매우 높은 경우 PLINQ는 소스 컬렉션의 몇 가지 항목만으로 속도를 상당히 향상할 수 있습니다. 반대로, trivial 대리자가 있는 작은 소스 컬렉션은 일반적으로 PLINQ의 좋은 후보가 아닙니다.  
  
     다음 예제에서 queryA의 Select 함수에 많은 작업이 포함되어 있기 때문에 queryA는 PLINQ에 적합합니다. 그러나 queryB의 Select 문에는 많은 작업이 포함되어 있지 않기 때문에 queryB는 적합하지 않습니다. 병렬 처리에 따른 오버헤드가 속도 향상 폭의 대부분 또는 전부를 오프셋하게 됩니다.  
  
    ```vb  
    Dim queryA = From num In numberList.AsParallel()  
                 Select ExpensiveFunction(num); 'good for PLINQ  
  
    Dim queryB = From num In numberList.AsParallel()  
                 Where num Mod 2 > 0  
                 Select num; 'not as good for PLINQ  
    ```  
  
    ```csharp  
    var queryA = from num in numberList.AsParallel()  
                 select ExpensiveFunction(num); //good for PLINQ  
  
    var queryB = from num in numberList.AsParallel()  
                 where num % 2 > 0  
                 select num; //not as good for PLINQ  
    ```  
  
2. 시스템의 논리 코어 수(병렬 처리 정도).  
  
     이 항목은 이전 섹션에 대한 분명한 필연적인 결과입니다. 더 많은 동시 스레드 간에 작업이 나뉠 수 있으므로 즐거운 병렬인 쿼리는 더 많은 코어가 있는 컴퓨터에서 더 빠르게 실행됩니다. 전체 속도 향상 정도는 병렬 처리 가능한 전체 쿼리 작업의 백분율에 따라 다릅니다. 그러나 모든 쿼리가 4코어 컴퓨터보다 8코어 컴퓨터에서 2배 더 빠르게 실행되는 것으로 간주하지 마세요. 성능을 최적화하기 위해 쿼리를 조정할 경우 코어 수가 다양한 컴퓨터에서 실제 결과를 측정하는 것이 중요합니다. 이 항목은 항목 #1에 관련됩니다. 더 큰 컴퓨팅 리소스를 활용하려면 더 큰 데이터 세트가 필요합니다.  
  
3. 작업 수 및 종류.  
  
     PLINQ는 소스 시퀀스의 요소 순서를 유지해야 하는 상황을 위해 AsOrdered 연산자를 제공합니다. 순서 지정 관련 비용이 있지만 이 비용은 대개 별로 많이 들지 않습니다. GroupBy 및 Join 작업에서도 오버헤드가 발생합니다. PLINQ는 소스 컬렉션의 요소를 임의 순서로 처리한 다음, 준비되면 바로 다음 연산자로 전달할 수 있을 경우 최고의 성능을 발휘합니다. 자세한 내용은 [PLINQ에서 순서 유지](../../../docs/standard/parallel-programming/order-preservation-in-plinq.md)를 참조하세요.  
  
4. 쿼리 실행 양식.  
  
     ToArray 또는 ToList를 호출하여 쿼리 결과를 저장하는 경우 모든 병렬 스레드의 결과를 단일 데이터 구조로 병합해야 합니다. 이 작업에는 불가피한 계산 비용이 포함됩니다. 마찬가지로 foreach(Visual Basic의 For Each) 루프를 사용하여 결과를 반복하면 작업자 스레드의 결과가 열거자 스레드로 직렬화되어야 합니다. 그러나 각 스레드의 결과에 따라서만 일부 작업을 수행하려는 경우에는 ForAll 메서드를 사용하여 여러 스레드에서 이 작업을 수행할 수 있습니다.  
  
5. 병합 옵션 유형.  
  
     PLINQ는 출력을 버퍼링하고 전체 결과 집합이 생성된 후 청크 단위로 또는 모두 한 번에 생성하도록 구성하거나 결과가 생성될 때 개별 결과를 스트리밍하도록 구성할 수 있습니다. 앞의 구성은 전체 실행 시간이 감소하고 나중 구성은 생성된 요소 간의 대기 시간이 감소합니다.  병합 옵션이 항상 전체 쿼리 성능에 큰 영향을 주는 것은 아니지만 병합 옵션은 사용자가 결과를 보기 위해 기다려야 하는 기간을 제어하므로 인식된 성능에 영향을 줄 수 있습니다. 자세한 내용은 [PLINQ의 병합 옵션](../../../docs/standard/parallel-programming/merge-options-in-plinq.md)을 참조하세요.  
  
6. 분할 종류.  
  
     경우에 따라 인덱싱할 수 있는 소스 컬렉션에 대한 PLINQ 쿼리로 인해 작업이 불균형해질 수 있습니다. 이 경우 사용자 지정 파티셔너를 만들어 쿼리 성능을 높일 수 있습니다. 자세한 내용은 [PLINQ 및 TPL에 대한 사용자 지정 파티셔너](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md)를 참조하세요.  
  
## <a name="when-plinq-chooses-sequential-mode"></a>PLINQ가 순차 모드를 선택할 경우  
 PLINQ는 항상 최소한 쿼리가 순차적으로 실행되는 것만큼 쿼리를 빠르게 실행하려고 합니다. PLINQ는 사용자 대리자의 계산 비용이 얼마나 비싼지 또는 입력 소스가 얼마나 큰지 확인하지 않지만 특정 쿼리 “모양”를 검색합니다. 특히, 일반적으로 병렬 모드에서 쿼리를 더 느리게 실행하는 쿼리 연산자 또는 연산자 조합을 검색합니다. 이러한 모양을 찾으면 PLINQ는 기본적으로 순차 모드로 돌아갑니다.  
  
 그러나 특정 쿼리 성능을 측정한 후 실제로 병렬 모드에서 더 빠르게 실행되는 것을 확인할 수 있습니다. 이 경우에는 <xref:System.Linq.ParallelEnumerable.WithExecutionMode%2A> 메서드를 통해 <xref:System.Linq.ParallelExecutionMode.ForceParallelism?displayProperty=nameWithType> 플래그를 사용하여 쿼리를 병렬 처리하도록 PLINQ에 지시할 수 있습니다. 자세한 내용은 [방법: PLINQ에 실행 모드 지정](../../../docs/standard/parallel-programming/how-to-specify-the-execution-mode-in-plinq.md)을 참조하세요.  
  
 다음 목록은 PLINQ가 기본적으로 순차 모드에서 실행할 쿼리 형태를 설명합니다.  
  
- 원래 인덱스를 제거하거나 재정렬한 순서 지정 또는 필터링 연산자 뒤에 Select, 인덱싱된 Where, 인덱싱된 SelectMany 또는 ElementAt 절을 포함하는 쿼리.  
  
- Take, TakeWhile, Skip, SkipWhile 연산자를 포함하고 소스 시퀀스의 인덱스가 원래 순서로 지정되지 않은 쿼리.  
  
- Zip 또는 SequenceEquals를 포함하는 쿼리. 데이터 소스 중 하나에서 원래 순서대로 인덱스가 유지되고 다른 데이터 소스는 인덱싱 가능한 배열 또는 IList(T)가 아닌 경우  
  
- 인덱싱할 수 있는 데이터 소스에 적용되지 않는 한 Concat을 포함하는 쿼리.  
  
- 인덱싱할 수 있는 데이터 소스에 적용되지 않는 한 Reverse를 포함하는 쿼리.  
  
## <a name="see-also"></a>참고 항목

- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
