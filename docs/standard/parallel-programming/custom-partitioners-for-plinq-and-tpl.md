---
title: PLINQ 및 TPL에 대한 사용자 지정 파티셔너
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, partitioners
ms.assetid: 96153688-9a01-47c4-8430-909cee9a2887
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 42df511857d367859fc68e2d881dd5b5e2e0bfbc
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67662559"
---
# <a name="custom-partitioners-for-plinq-and-tpl"></a>PLINQ 및 TPL에 대한 사용자 지정 파티셔너

데이터 소스에 대한 작업을 병렬화하기 위한 필수 단계 중 하나는 다중 스레드에서 동시에 액세스 가능한 여러 섹션으로 소스를 ‘분할’하는 것입니다.  PLINQ 및 TPL(작업 병렬 라이브러리)은 병렬 쿼리 또는 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 루프를 쓸 때 투명하게 작동하는 기본 파티셔너를 제공합니다. 더 높은 수준의 시나리오에서는 고유한 파티셔너를 연결할 수 있습니다.

## <a name="kinds-of-partitioning"></a>분할 유형

데이터 소스를 분할하는 여러 가지 방법이 있습니다. 가장 효율적인 방법에서는 소스를 여러 하위 시퀀스로 물리적으로 나누는 대신 여러 스레드가 공동 작업으로 원래 소스 시퀀스를 처리합니다. 미리 길이가 알려진 <xref:System.Collections.IList> 컬렉션과 같은 배열 및 기타 인덱싱된 소스의 경우 ‘범위 분할’은 가장 간단한 분할 유형입니다.  모든 스레드는 고유한 시작 및 끝 인덱스를 수신하므로 다른 스레드가 덮어쓰거나 다른 스레드를 덮어쓰지 않고 소스의 해당 범위를 처리할 수 있습니다. 범위 분할에 관련된 유일한 오버헤드는 범위를 만드는 초기 작업입니다. 그 이후에는 추가적인 동기화가 필요하지 않습니다. 따라서 워크로드가 균등하게 나누어지면 좋은 성능을 제공할 수 있습니다. 범위 분할의 단점은 한 스레드가 조기에 완료되는 경우 다른 스레드가 작업을 완료하도록 도울 수 없다는 것입니다.

연결된 목록 또는 길이가 알려지지 않은 기타 컬렉션의 경우 ‘청크 분할’을 사용할 수 있습니다.  청크 분할에서 병렬 루프 또는 쿼리의 모든 스레드 또는 작업은 소스 요소 중 일부를 하나의 청크로 사용하여 처리한 다음, 돌아와서 추가 요소를 검색합니다. 파티셔너는 모든 요소가 분배되고 중복이 없는지 확인합니다. 청크는 크기에 제한이 없습니다. 예를 들어 [방법: 동적 파티션 구현](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md)에 설명된 파티셔너는 하나의 요소만 포함하는 청크를 만듭니다. 청크가 너무 크지 않다면 스레드에 대한 요소 할당이 미리 결정되지 않으므로 이 분할 유형은 기본적으로 부하 분산됩니다. 그러나 파티셔너는 스레드가 다른 청크를 가져와야 할 때마다 동기화 오버헤드를 발생시킵니다. 이러한 경우에 발생하는 동기화 양은 청크 크기에 반비례합니다.

일반적으로 범위 분할은 대리자의 실행 시간이 짧거나 중간 정도이고 소스에 많은 요소가 포함된 경우에만 더 빠르고 각 파티션의 전체 작업은 거의 동일합니다. 따라서 청크 분할은 일반적으로 대부분의 경우 더 빠릅니다. 대리자에 대한 실행 시간이 더 길거나 요소 수가 적은 소스에서는 청크 및 범위 분할 성능이 거의 같습니다.

또한 TPL 파티셔너는 동적 파티션 수를 지원합니다. 즉, 이 파티셔너는 예를 들어 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 루프가 새 작업을 생성할 경우 파티션을 즉시 만들 수 있습니다. 이 기능을 사용하면 파티셔너가 루프 자체와 함께 확장될 할 수 있습니다. 동적 파티셔너는 기본적으로 부하 분산됩니다. 사용자 지정 파티셔너를 만드는 경우 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 루프에서 사용할 수 있도록 동적 분할을 지원해야 합니다.

### <a name="configuring-load-balancing-partitioners-for-plinq"></a>PLINQ에 대한 부하 분산 파티셔너 구성

<xref:System.Collections.Concurrent.Partitioner.Create%2A?displayProperty=nameWithType> 메서드의 일부 오버로드를 사용하면 배열 또는 <xref:System.Collections.IList> 소스에 대한 파티셔너를 만들고 스레드 간에 워크로드를 분산하려고 시도할지 여부를 지정할 수 있습니다. 파티셔너가 부하 분산되도록 구성된 경우에는 청크 분할이 사용되고 요소가 요청 시 작은 청크로 각 파티션에 전달됩니다. 이 방법은 전체 루프 또는 쿼리가 완료될 때까지 모든 파티션에 처리할 요소가 있는지 확인하는 데 도움이 됩니다. 추가 오버로드를 사용하여 <xref:System.Collections.IEnumerable> 소스의 부하 분산 분할을 제공할 수 있습니다.

일반적으로 부하 분산을 사용하려면 파티션이 파티셔너의 요소를 비교적 자주 요청해야 합니다. 반대로 정적 분할을 수행하는 파티셔너는 범위 또는 청크 분할을 사용하여 각 파티셔너에 요소를 한 번에 할당할 수 있습니다. 이 작업에 필요한 오버헤드는 부하 분산보다 적지만 한 스레드가 다른 스레드보다 훨씬 더 많은 작업으로 종료될 경우 실행에 시간이 더 오래 걸릴 수 있습니다. 기본적으로 IList 또는 배열을 전달할 때 PLINQ는 항상 부하 분산 없이 범위 분할을 사용합니다. PLINQ에 대한 부하 분산을 사용하려면 다음 예제에 표시된 것처럼 `Partitioner.Create` 메서드를 사용합니다.

[!code-csharp[TPL_Partitioners#02](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioners.cs#02)]
[!code-vb[TPL_Partitioners#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/partitionsnippets_vb.vb#02)]

해당 시나리오에서 부하 분산을 사용할지 여부를 결정하려면 대표적인 부하 및 컴퓨터 구성에서 작업 완료에 걸리는 시간을 실제로 실험 및 측정하는 것이 가장 좋습니다. 예를 들어 정적 분할은 몇 개의 코어만 있는 멀티 코어 컴퓨터에서 상당한 속도 향상을 제공할 수 있지만, 비교적 많은 코어가 있는 컴퓨터에서는 속도 저하가 발생할 수 있습니다.

다음 표에는 <xref:System.Collections.Concurrent.Partitioner.Create%2A> 메서드의 사용 가능한 오버로드가 나와 있습니다. 이 파티셔너는 PLINQ 또는 <xref:System.Threading.Tasks.Task>와 함께 사용하도록 제한되지 않습니다. 사용자 지정 병렬 구문과 함께 사용할 수도 있습니다.

|오버로드|부하 분산 사용|
|--------------|-------------------------|
|<xref:System.Collections.Concurrent.Partitioner.Create%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29>|항상|
|<xref:System.Collections.Concurrent.Partitioner.Create%60%601%28%60%600%5B%5D%2CSystem.Boolean%29>|부울 인수가 true로 지정될 경우|
|<xref:System.Collections.Concurrent.Partitioner.Create%60%601%28System.Collections.Generic.IList%7B%60%600%7D%2CSystem.Boolean%29>|부울 인수가 true로 지정될 경우|
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int32%2CSystem.Int32%29>|Never|
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int32%2CSystem.Int32%2CSystem.Int32%29>|Never|
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int64%2CSystem.Int64%29>|Never|
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int64%2CSystem.Int64%2CSystem.Int64%29>|Never|

### <a name="configuring-static-range-partitioners-for-parallelforeach"></a>Parallel.ForEach에 대한 정적 범위 파티셔너 구성

<xref:System.Threading.Tasks.Parallel.For%2A> 루프에서 루프 본문은 메서드에 대리자로 제공됩니다. 해당 대리자를 호출하는 비용은 가상 메서드 호출과 거의 같습니다. 일부 시나리오에서 병렬 루프의 본문은 각 루프 반복에 대한 대리자 호출 비용이 매우 커질 만큼 충분히 작을 수 있습니다. 이 경우 <xref:System.Collections.Concurrent.Partitioner.Create%2A> 오버로드 중 하나를 사용하여 소스 요소에 대해 범위 분할의 <xref:System.Collections.Generic.IEnumerable%601>을 만들 수 있습니다. 그런 다음, 본문이 일반 `for` 루프로 구성된 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 메서드에 이 범위 컬렉션을 전달할 수 있습니다. 이 방법의 장점은 대리자 호출 비용이 요소당 한 번이 아니라 범위당 한 번만 발생한다는 점입니다. 다음 예제에서는 기본 패턴을 보여줍니다.

[!code-csharp[TPL_Partitioners#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioner01.cs#01)]
[!code-vb[TPL_Partitioners#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/partitionercreate01.vb#01)]

루프의 모든 스레드는 지정된 하위 범위의 시작 및 끝 인덱스 값을 포함하는 자체 <xref:System.Tuple%602>을 수신합니다. 내부 `for` 루프는 `fromInclusive` 및 `toExclusive` 값을 사용하여 배열 또는 <xref:System.Collections.IList>를 반복합니다.

<xref:System.Collections.Concurrent.Partitioner.Create%2A> 오버로드 중 하나를 사용하여 파티션 크기와 파티션 수를 지정할 수 있습니다. 이 오버로드는 요소당 가상 메서드 호출이 하나라도 성능에 큰 영향을 미치도록 요소당 작업이 느린 시나리오에서 사용할 수 있습니다.

## <a name="custom-partitioners"></a>사용자 지정 파티셔너

일부 시나리오에서는 이것이 고유한 파티셔너를 구현하는 데 유용하거나 필요할 수도 있습니다. 예를 들어 클래스의 내부 구조에 대한 지식을 바탕으로 기본 파티셔너가 분할할 수 있는 것보다 더 효율적으로 분할할 수 있는 사용자 지정 컬렉션 클래스가 있을 수 있습니다. 또는 소스 컬렉션의 여러 위치에서 요소를 처리하는 데 걸리는 시간에 대한 지식을 바탕으로 다양한 크기의 범위 파티션을 만들 수 있습니다.

기본 사용자 지정 파티셔너를 만들려면 <xref:System.Collections.Concurrent.Partitioner%601?displayProperty=nameWithType>에서 클래스를 파생시키고 다음 표에 설명된 대로 가상 메서드를 재정의합니다.

|||
|-|-|
|<xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>|이 메서드는 기본 스레드에 의해 한 번 호출되고 IList(IEnumerator(TSource))를 반환합니다. 루프 또는 쿼리의 각 작업자 스레드는 목록에서 `GetEnumerator`를 호출하여 별도의 파티션에서 <xref:System.Collections.Generic.IEnumerator%601>를 검색할 수 있습니다.|
|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>|<xref:System.Collections.Concurrent.Partitioner%601.GetDynamicPartitions%2A>를 구현하는 경우 `true`를 반환하고, 그렇지 않으면 `false`를 반환합니다.|
|<xref:System.Collections.Concurrent.Partitioner%601.GetDynamicPartitions%2A>|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>가 `true`이면 선택적으로 <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A> 대신 이 메서드가 호출될 수 있습니다.|

결과가 정렬 가능해야 하거나 요소에 대한 인덱싱된 액세스가 필요한 경우 <xref:System.Collections.Concurrent.OrderablePartitioner%601?displayProperty=nameWithType>에서 파생시키고 다음 표에 설명된 대로 해당 가상 메서드를 재정의합니다.

|||
|-|-|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetPartitions%2A>|이 메서드는 기본 스레드에 의해 한 번 호출되고 `IList(IEnumerator(TSource))`를 반환합니다. 루프 또는 쿼리의 각 작업자 스레드는 목록에서 `GetEnumerator`를 호출하여 별도의 파티션에서 <xref:System.Collections.Generic.IEnumerator%601>를 검색할 수 있습니다.|
|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetDynamicPartitions%2A>를 구현하는 경우 `true`를 반환하고, 그렇지 않으면 false를 반환합니다.|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetDynamicPartitions%2A>|일반적으로 <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A>만 호출합니다.|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A>|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>가 `true`이면 선택적으로 <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A> 대신 이 메서드가 호출될 수 있습니다.|

다음 표에서는 세 종류의 부하 분산 파티셔너가 <xref:System.Collections.Concurrent.OrderablePartitioner%601> 클래스를 구현하는 방법을 추가로 자세히 설명합니다.

|메서드/속성|부하 분산 없는 IList/배열|부하 분산 있는 IList/배열|IEnumerable|
|----------------------|-------------------------------------------|----------------------------------------|-----------------|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderablePartitions%2A>|범위 분할을 사용합니다.|지정된 partitionCount에 대해 최적화된 청크 분할을 사용합니다.|정적 개수의 파티션을 만들어 청크 분할을 사용합니다.|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A?displayProperty=nameWithType>|지원되지 않는 예외를 throw합니다.|목록 및 동적 파티션에 최적화된 청크 분할을 사용합니다.|동적 개수의 파티션을 만들어 청크 분할을 사용합니다.|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.KeysOrderedInEachPartition%2A>|`true`를 반환합니다.|`true`를 반환합니다.|`true`를 반환합니다.|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.KeysOrderedAcrossPartitions%2A>|`true`를 반환합니다.|`false`를 반환합니다.|`false`를 반환합니다.|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.KeysNormalized%2A>|`true`를 반환합니다.|`true`를 반환합니다.|`true`를 반환합니다.|
|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>|`false`를 반환합니다.|`true`를 반환합니다.|`true`를 반환합니다.|

### <a name="dynamic-partitions"></a>동적 파티션

<xref:System.Threading.Tasks.Parallel.ForEach%2A> 메서드에서 파티셔너를 사용하도록 하려면 동적 개수의 파티션을 반환할 수 있어야 합니다. 즉, 파티셔너는 루프 실행 중에 언제든지 요청 시 새 파티션에 대한 열거자를 제공할 수 있습니다. 기본적으로 루프는 새 병렬 작업을 추가할 때마다 해당 작업에 대한 새 파티션을 요청합니다. 데이터의 순서가 지정 가능해야 하는 경우 각 파티션의 각 항목에 고유한 인덱스가 할당되도록 <xref:System.Collections.Concurrent.OrderablePartitioner%601?displayProperty=nameWithType>에서 파생시킵니다.

자세한 내용과 예제는 [방법: 동적 파티션 구현](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md)을 참조하세요.

### <a name="contract-for-partitioners"></a>파티셔너에 대한 계약

사용자 지정 파티셔너를 구현할 경우 다음 지침에 따르면 TPL에서 PLINQ 및 <xref:System.Threading.Tasks.Parallel.ForEach%2A>를 올바르게 조작할 수 있습니다.

- <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>가 `partitionsCount`에 대해 0보다 작거나 같은 인수를 사용하여 호출되면 <xref:System.ArgumentOutOfRangeException>을 throw합니다. PLINQ 및 TPL이 0과 같은 `partitionCount`로는 전달되지 않더라도 가능성을 방지하는 것이 좋습니다.

- <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A> 및 <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderablePartitions%2A>는 항상 `partitionsCount`개의 파티션을 반환해야 합니다. 파티셔너가 데이터를 모두 사용해서 요청한 만큼 파티션을 만들 수 없는 경우 메서드는 나머지 파티션에 대해 각각 빈 열거자를 반환해야 합니다. 그렇지 않으면 PLINQ 및 TPL이 둘 다 <xref:System.InvalidOperationException>을 throw합니다.

- <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>, <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderablePartitions%2A>, <xref:System.Collections.Concurrent.Partitioner%601.GetDynamicPartitions%2A> 및 <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A>는 `null`(Visual Basic의 `Nothing`)을 반환하면 안 됩니다. 반환할 경우 PLINQ/TPL이 <xref:System.InvalidOperationException>을 throw합니다.

- 파티션을 반환하는 메서드는 항상 데이터 소스를 완전히 고유하게 열거할 수 있는 파티션을 반환해야 합니다. 파티셔너의 디자인에 특별히 필요한 경우가 아니면 데이터 소스 또는 건너뛴 항목에는 중복이 없어야 합니다. 이 규칙을 따르지 않으면 출력 순서가 변경될 수 있습니다.

- 다음 부울 getter는 출력 순서가 변경되지 않도록 항상 다음 값을 정확하게 반환해야 합니다.

  - `KeysOrderedInEachPartition`: 각 파티션이 키 인덱스가 증가하는 요소를 반환합니다.

  - `KeysOrderedAcrossPartitions`: 반환되는 모든 파티션에서 파티션의 키 인덱스 *i*는 파티션의 키 인덱스 *i*-1보다 큽니다.

  - `KeysNormalized`: 모든 키 인덱스는 0부터 시작하여 공백 없이 순차적으로 증가합니다.

- 모든 인덱스는 고유해야 합니다. 중복 인덱스가 없어야 합니다. 이 규칙을 따르지 않으면 출력 순서가 변경될 수 있습니다.

- 모든 인덱스는 음수가 아니어야 합니다. 이 규칙을 따르지 않으면 PLINQ/TPL이 예외를 throw할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)
- [방법: 동적 파티션 구현](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md)
- [방법: 정적 분할을 위한 파티셔너 구현](../../../docs/standard/parallel-programming/how-to-implement-a-partitioner-for-static-partitioning.md)
