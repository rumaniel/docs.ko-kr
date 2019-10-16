---
title: '연습: 데이터 흐름 파이프라인 만들기'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dataflow pipelines, creating with TPL
- Task Parallel Library, dataflows
- TPL dataflow library, creating dataflow pipeline
ms.assetid: 69308f82-aa22-4ac5-833d-e748533b58e8
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 870f65fdbf263913134d0528c200d3c2990a498c
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59299009"
---
# <a name="walkthrough-creating-a-dataflow-pipeline"></a>연습: 데이터 흐름 파이프라인 만들기
<xref:System.Threading.Tasks.Dataflow.DataflowBlock.Receive%2A?displayProperty=nameWithType>, <xref:System.Threading.Tasks.Dataflow.DataflowBlock.ReceiveAsync%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.TryReceive%2A?displayProperty=nameWithType> 메서드를 사용하여 소스 블록에서 메시지를 받을 수 있지만 메시지 블록을 연결하여 *데이터 흐름 파이프라인*을 만들 수도 있습니다. 데이터 흐름 파이프라인은 일련의 구성 요소 또는 *데이터 흐름 블록*으로, 각 구성 요소는 보다 큰 목표를 위해 특정 작업을 수행합니다. 데이터 흐름 파이프라인의 모든 데이터 흐름 블록은 다른 데이터 흐름 블록에서 메시지를 받으면 작업을 수행합니다. 이는 자동차 제조 조립 라인에 비유될 수 있습니다. 각 자동차가 조립 라인을 통과할 때 한 작업장에서는 프레임을 조립하고 다음 작업장에서는 엔진을 장착하는 식입니다. 조립 라인에서는 여러 대의 자동차를 동시에 조립할 수 있기 때문에 한 번에 자동차 전체를 조립하는 경우보다 처리량이 향상됩니다.

 이 문서에서는 웹 사이트에서 *The Iliad of Homer*라는 책을 다운로드하고 텍스트를 검색하여 개별 단어를 첫 번째 단어의 문자와 반대인 단어와 일치시키는 데이터 흐름 파이프라인을 보여줍니다. 이 문서에서 데이터 흐름 파이프라인을 만드는 단계는 다음과 같습니다.  
  
1. 파이프라인에 참여하는 데이터 흐름 블록을 만듭니다.  
  
2. 각 데이터 흐름 블록을 파이프라인의 다음 블록에 연결합니다. 각 블록은 파이프라인에 있는 이전 블록의 출력을 입력으로 받습니다.  
  
3. 각 데이터 흐름 블록에 대해 이전 블록이 완료된 후 다음 블록을 완료된 상태로 설정하는 연속 작업을 만듭니다.  
  
4. 데이터를 파이프라인의 머리에 게시합니다.  
  
5. 파이프라인의 머리를 완료된 것으로 표시합니다.  
  
6. 파이프라인에서 모든 작업을 완료할 때까지 기다립니다.  
  
## <a name="prerequisites"></a>전제 조건  
 이 연습을 시작하기 전에 [데이터 흐름](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)을 읽어 보세요.  
  
## <a name="creating-a-console-application"></a>콘솔 애플리케이션 만들기  
 Visual Studio에서 Visual C# 또는 Visual Basic 콘솔 애플리케이션 프로젝트를 만듭니다. System.Threading.Tasks.Dataflow NuGet 패키지를 설치합니다.

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

 프로젝트에 다음 코드를 추가하여 기본 애플리케이션을 만듭니다.  
  
 [!code-csharp[TPLDataflow_Palindromes#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#2)]
 [!code-vb[TPLDataflow_Palindromes#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromesemptymain.vb#2)]  
  
## <a name="creating-the-dataflow-blocks"></a>데이터 흐름 블록 만들기  
 다음 코드를 `Main` 메서드에 추가하여 파이프라인에 참여하는 데이터 흐름 블록을 만듭니다. 다음 표에서는 파이프라인에 있는 각 구성원의 역할을 요약합니다.  
  
 [!code-csharp[TPLDataflow_Palindromes#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#3)]
 [!code-vb[TPLDataflow_Palindromes#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#3)]  
  
|멤버|형식|설명|  
|------------|----------|-----------------|  
|`downloadString`|<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>|웹에서 책 텍스트를 다운로드합니다.|  
|`createWordList`|<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>|책 텍스트를 단어의 배열로 나눕니다.|  
|`filterWordList`|<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>|단어 배열에서 짧은 단어와 중복을 제거합니다.|  
|`findReversedWords`|<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>|역순으로 표기된 단어도 단어 배열에 나타나는 모든 단어를 필터링된 단어 배열 컬렉션에서 찾습니다.|  
|`printReversedWords`|<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>|단어 및 해당 역방향 단어를 콘솔에 표시합니다.|  
  
 이 예제에서 데이터 흐름 파이프라인의 여러 단계를 한 단계로 결합할 수도 있지만, 여기에서는 보다 큰 작업을 수행하기 위해 여러 독립적인 데이터 흐름 작업을 구성하는 개념을 보여 줍니다. 이 예제에서는 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602>을 사용하여 파이프라인의 각 구성원이 입력 데이터에 대해 작업을 수행하고 결과를 파이프라인의 다음 단계로 보낼 수 있도록 합니다. 파이프라인의 `findReversedWords` 구성원은 각 입력에 대해 여러 독립적 출력을 생성하기 때문에 <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602> 개체입니다. 파이프라인의 꼬리인 `printReversedWords`는 입력에 대해 작업을 수행하고 결과를 생성하지 않기 때문에 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 개체입니다.  
  
## <a name="forming-the-pipeline"></a>파이프라인 만들기  
 다음 코드를 추가하여 각 블록을 파이프라인의 다음 블록에 연결합니다.  
  
 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.LinkTo%2A> 메서드를 호출하여 소스 데이터 흐름 블록을 대상 데이터 흐름 블록에 연결하는 경우, 소스 데이터 흐름 블록은 데이터를 사용할 수 있게 되면 대상 블록에 데이터를 전파합니다. <xref:System.Threading.Tasks.Dataflow.DataflowLinkOptions.PropagateCompletion>을 true로 설정하고 <xref:System.Threading.Tasks.Dataflow.DataflowLinkOptions>를 제공하면 파이프라인에 있는 한 블록의 완료 성공 및 실패로 인해 파이프라인에서 다음 블록이 완료됩니다.
  
 [!code-csharp[TPLDataflow_Palindromes#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#4)]
 [!code-vb[TPLDataflow_Palindromes#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#4)]  
  
## <a name="posting-data-to-the-pipeline"></a>파이프라인에 데이터 게시  
 다음 코드를 추가하여 *The Iliad of Homer*라는 책의 URL을 데이터 흐름 파이프라인의 머리에 게시합니다.  
  
 [!code-csharp[TPLDataflow_Palindromes#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#6)]
 [!code-vb[TPLDataflow_Palindromes#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#6)]  
  
 이 예제에서는 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A?displayProperty=nameWithType>를 사용하여 파이프라인의 머리에 데이터를 동기적으로 보냅니다. 데이터를 데이터 흐름 노드에 비동기적으로 보내야 하는 경우에는 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.SendAsync%2A?displayProperty=nameWithType> 메서드를 사용합니다.  
  
## <a name="completing-pipeline-activity"></a>파이프라인 작업 완료  
 다음 코드를 추가하여 파이프라인의 머리를 완료된 것으로 표시합니다. 파이프라인의 머리는 버퍼링된 메시지를 모두 처리한 후 완료를 전파합니다.
  
 [!code-csharp[TPLDataflow_Palindromes#7](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#7)]
 [!code-vb[TPLDataflow_Palindromes#7](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#7)]  
  
 이 예제에서는 처리할 URL을 데이터 흐름 파이프라인을 통해 보냅니다. 파이프라인을 통해 둘 이상의 입력을 보내는 경우 모든 입력을 제출한 후 <xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Complete%2A?displayProperty=nameWithType> 메서드를 호출합니다. 데이터를 더 이상 사용할 수 없는 지점이 애플리케이션에 잘 정의되어 있지 않거나 파이프라인이 완료될 때까지 애플리케이션이 대기할 필요가 없는 경우 이 단계를 생략할 수 있습니다.  
  
## <a name="waiting-for-the-pipeline-to-finish"></a>파이프라인이 완료될 때까지 대기  
 다음 코드를 추가하여 파이프라인이 완료될 때까지 대기합니다. 파이프라인의 꼬리가 완료되면 전체 작업이 완료됩니다.  
  
 [!code-csharp[TPLDataflow_Palindromes#8](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#8)]
 [!code-vb[TPLDataflow_Palindromes#8](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#8)]  
  
 동시에 임의의 스레드나 여러 스레드에서 데이터 흐름 완료를 기다릴 수 있습니다.  
  
## <a name="the-complete-example"></a>전체 예제  
 다음 예제에서는 이 연습의 전체 코드를 보여 줍니다.  
  
 [!code-csharp[TPLDataflow_Palindromes#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#1)]
 [!code-vb[TPLDataflow_Palindromes#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#1)]  
  
## <a name="next-steps"></a>다음 단계  
 이 예제에서는 처리할 URL을 데이터 흐름 파이프라인을 통해 보냅니다. 파이프라인을 통해 둘 이상의 입력 값을 보내는 경우, 부품들이 자동차 공장에서 이동할 수 있는 방법과 유사한 형태의 병렬 처리를 애플리케이션에 적용할 수 있습니다. 파이프라인의 첫 번째 구성원이 결과를 두 번째 구성원에 보내는 경우, 두 번째 구성원이 첫 번째 결과를 처리할 때 첫 번째 구성원은 다른 항목을 병렬로 처리할 수 있습니다.  
  
 데이터 흐름 파이프라인을 사용하여 실현되는 병렬 처리는 일반적으로 더 적은 수의 보다 큰 작업으로 구성되어 있기 때문에 *정교하지 않은 병렬 처리*라고 합니다. 데이터 흐름 파이프라인에서 보다 작고 짧게 실행되는 작업의 *세부적인 병렬 처리*를 더 많이 사용할 수도 있습니다. 이 예제에서 파이프라인의 `findReversedWords` 구성원은 [PLINQ](parallel-linq-plinq.md)를 사용하여 작업 목록의 여러 항목을 병렬로 처리합니다. 정교하지 않은 파이프라인에서 세분화된 병렬 처리를 사용하면 전반적인 처리량이 향상될 수 있습니다.  
  
 또한 소스 데이터 흐름 블록을 여러 대상 블록에 연결하여 *데이터 흐름 네트워크*를 만들 수도 있습니다. <xref:System.Threading.Tasks.Dataflow.DataflowBlock.LinkTo%2A> 메서드의 오버로드된 버전은 대상 블록이 값을 기준으로 각 메시지를 수락하는지 여부를 정의하는 <xref:System.Predicate%601> 개체를 사용합니다. 소스 역할을 하는 대부분의 데이터 흐름 블록 형식은 블록 중 하나가 메시지를 수락할 때까지 연결된 모든 대상 블록에 연결순으로 메시지를 제공합니다. 이 필터링 메커니즘을 사용하여 특정 데이터를 한 경로로 보내고 다른 데이터는 또 다른 경로로 보내는 연결된 데이터 흐름 블록의 시스템을 만들 수 있습니다. 필터링을 사용하여 데이터 흐름 네트워크를 만드는 예제는 [연습: Windows Forms 애플리케이션에서 데이터 흐름 사용](../../../docs/standard/parallel-programming/walkthrough-using-dataflow-in-a-windows-forms-application.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [데이터 흐름](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)
