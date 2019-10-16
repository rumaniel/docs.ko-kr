---
title: '방법: 데이터 흐름 블록에서 데이터를 받을 경우 작업 수행'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Task Parallel Library, dataflows
- TPL dataflow library, receiving data
ms.assetid: fc2585dc-965e-4632-ace7-73dd02684ed3
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 17167467f52ab9afb8d7500f4f0eb744d8f60a6e
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70169029"
---
# <a name="how-to-perform-action-when-a-dataflow-block-receives-data"></a>방법: 데이터 흐름 블록에서 데이터를 받을 경우 작업 수행
*실행 데이터 흐름 블록* 형식은 데이터를 받을 때 사용자가 제공한 대리자를 호출합니다. <xref:System.Threading.Tasks.Dataflow.ActionBlock%601?displayProperty=nameWithType>, <xref:System.Threading.Tasks.Dataflow.TransformBlock%602?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602?displayProperty=nameWithType> 클래스는 실행 데이터 흐름 블록 형식입니다. 실행 데이터 흐름 블록에 작업 함수를 제공할 때 `delegate`(Visual Basic에서는 `Sub`) 키워드, <xref:System.Action%601>, <xref:System.Func%602> 또는 람다 식을 사용할 수 있습니다. 이 문서에서는 <xref:System.Func%602> 및 람다 식을 사용하여 실행 블록에서 작업을 수행하는 방법을 설명합니다.  

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

## <a name="example"></a>예  
 다음 예제에서는 데이터 흐름을 사용하여 디스크에서 파일을 읽고 파일에서 0인 바이트 수를 계산합니다. 이 예제에서는 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602>을 사용하여 파일을 읽고 0바이트의 수를 계산하고, <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>을 사용하여 콘솔에 0바이트의 수를 출력합니다. <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 개체는 블록이 데이터를 받을 때 작업을 수행할 <xref:System.Func%602> 개체를 지정합니다. <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 개체는 람다 식을 사용하여 콘솔에 읽은 0바이트의 수를 출력합니다.  
  
 [!code-csharp[TPLDataflow_ExecutionBlocks#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_executionblocks/cs/dataflowexecutionblocks.cs#1)]
 [!code-vb[TPLDataflow_ExecutionBlocks#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_executionblocks/vb/dataflowexecutionblocks.vb#1)]  
  
 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 개체에 람다 식을 제공할 수 있지만, 이 예제에서는 <xref:System.Func%602>를 사용하여 다른 코드에서 `CountBytes` 메서드를 사용할 수 있도록 합니다. <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 개체는 수행할 작업이 이 작업에 특정하고 다른 코드에서 유용할 가능성이 적기 때문에 람다 식을 사용합니다. 람다 식이 작업 병렬 라이브러리에서 작동하는 방식에 대한 자세한 내용은 [PLINQ 및 TPL의 람다 식](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)을 참조하세요.  
  
 [데이터 흐름](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md) 문서의 대리자 형식 요약 섹션에서는 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>, <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 및 <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602> 개체에 제공할 수 있는 대리자 형식을 요약합니다. 또한 대리자 형식이 동기적으로 작동하는지, 아니면 비동기적으로 작동하는지를 지정합니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 이 예제에서는 <xref:System.Func%602> 형식의 대리자를 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 개체에 제공하여 데이터 흐름 블록의 작업을 동기적으로 수행합니다. 데이터 흐름 블록이 비동기적으로 동작할 수 있도록 하려면 <xref:System.Func%601> 형식의 대리자를 데이터 흐름 블록에 제공합니다. 데이터 흐름 블록이 비동기적으로 동작하는 경우 데이터 흐름 블록의 작업은 반환된 <xref:System.Threading.Tasks.Task%601> 개체가 완료될 때만 완료됩니다. 다음 예제에서는 `CountBytes` 메서드를 수정하고 [async](../../csharp/language-reference/keywords/async.md) 및 [await](../../csharp/language-reference/operators/await.md)(Visual Basic에서는 [Async](../../visual-basic/language-reference/modifiers/async.md) 및 [Await](../../visual-basic/language-reference/operators/await-operator.md)) 연산자를 사용하여 제공된 파일에서 크기가 0인 바이트의 총 수를 비동기적으로 컴퓨팅합니다. <xref:System.IO.FileStream.ReadAsync%2A> 메서드는 비동기적으로 파일 읽기 작업을 수행합니다.  
  
 [!code-csharp[TPLDataflow_ExecutionBlocks#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_executionblocks/cs/dataflowexecutionblocks.cs#2)]
 [!code-vb[TPLDataflow_ExecutionBlocks#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_executionblocks/vb/dataflowexecutionblocks.vb#2)]  
  
 또한 비동기 람다 식을 사용하여 실행 데이터 흐름 블록에서 작업을 수행합니다. 다음 예제에서는 람다 식을 사용하여 비동기적으로 작업을 수행할 수 있도록 이전 예제에서 사용된 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 개체를 수정합니다.  
  
 [!code-csharp[TPLDataflow_ExecutionBlocks#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_executionblocks/cs/dataflowexecutionblocks.cs#3)]
 [!code-vb[TPLDataflow_ExecutionBlocks#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_executionblocks/vb/dataflowexecutionblocks.vb#3)]  
  
## <a name="see-also"></a>참고 항목

- [데이터 흐름](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)
