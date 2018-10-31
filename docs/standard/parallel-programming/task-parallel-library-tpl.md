---
title: TPL(작업 병렬 라이브러리)
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- .NET, concurrency in
- .NET, parallel programming in
- Parallel Programming
ms.assetid: b8f99f43-9104-45fd-9bff-385a20488a23
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3b08154d1be7a8a5699682b3cee3faad4e384269
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48836570"
---
# <a name="task-parallel-library-tpl"></a>TPL(작업 병렬 라이브러리)
TPL(작업 병렬 라이브러리)은 <xref:System.Threading?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks?displayProperty=nameWithType> 네임스페이스에 포함된 공용 형식 및 API의 집합입니다. TPL의 목적은 응용 프로그램에 병렬 처리 및 동시성 기능을 추가하는 과정을 단순화하여 개발자가 더 생산적으로 작업할 수 있도록 하는 것입니다. TPL은 사용할 수 있는 모든 프로세서를 가장 효율적으로 사용하도록 동시성 수준을 동적으로 조정합니다. 또한 TPL은 작업의 분할, <xref:System.Threading.ThreadPool>에 대한 스레드 예약, 취소 지원, 상태 관리 및 기타 하위 수준 세부 정보를 처리합니다. TPL을 사용하면 프로그램의 설계 목적인 작업을 처리하는 데 집중하면서 코드의 성능을 최대화할 수 있습니다.  
  
 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]부터는 다중 스레드 및 병렬 코드를 작성하는 데 TPL을 사용하는 것이 좋습니다. 그러나 코드에 따라서는 병렬화가 적합하지 않을 수도 있습니다. 예를 들어 루프에서 각 반복에 대해 수행할 작업의 양이 많지 않거나 실행되는 반복 횟수가 많지 않으면 병렬화에 따른 오버헤드로 인해 코드의 실행 속도가 오히려 더 느려질 수 있습니다. 또한 병렬화를 사용하면 다중 스레드 코드의 경우와 마찬가지로 프로그램 실행이 복잡해질 수 있습니다. TPL은 다중 스레드 시나리오를 단순화하기는 하지만 TPL을 효과적으로 사용하려면 잠금, 교착 상태 및 경합 조건과 같이 스레딩과 관련된 기본적인 개념을 이해하고 있는 것이 좋습니다.  
  
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-|-|  
|[데이터 병렬 처리](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)|병렬 `for` 및 `foreach`(Visual Basic의 경우 `For` 및 `For Each`) 루프를 만드는 방법을 설명합니다.|  
|[작업 기반 비동기 프로그래밍](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)|<xref:System.Threading.Tasks.Parallel.Invoke%2A?displayProperty=nameWithType>를 사용하여 암시적으로 또는 <xref:System.Threading.Tasks.Task> 개체를 직접 사용하여 명시적으로 작업을 만들고 실행하는 방법을 설명합니다.|  
|[데이터 흐름](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)|서로 통신해야 하는 여러 작업을 처리하거나 데이터를 사용할 수 있도록 처리하기 위해 TPL 데이터 흐름 라이브러리에서 데이터 흐름 구성 요소를 사용하는 방법을 설명합니다.|  
|[TPL과 기타 비동기 패턴 사용](../../../docs/standard/parallel-programming/using-tpl-with-other-asynchronous-patterns.md)|.NET의 기타 비동기 패턴과 함께 TPL을 사용하는 방법을 설명합니다.|  
|[데이터 및 작업 병렬 처리에서 발생할 수 있는 문제](../../../docs/standard/parallel-programming/potential-pitfalls-in-data-and-task-parallelism.md)|몇 가지 일반적인 실수 및 이를 방지하는 방법을 설명합니다.|  
|[PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)|LINQ 쿼리를 사용하여 데이터 병렬 처리를 구현하는 방법을 설명합니다.|  
|[병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)|.NET 병렬 프로그래밍의 최상위 노드입니다.|  
  
## <a name="see-also"></a>참고 항목

- [NET Framework를 사용한 병렬 프로그래밍 샘플](https://code.msdn.microsoft.com/Samples-for-Parallel-b4b76364)
