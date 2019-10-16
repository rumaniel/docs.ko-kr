---
title: '방법: 데이터 흐름 블록 링크 끊기'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dataflow blocks, unlinking in TPL
- Task Parallel Library, dataflows
- TPL dataflow library, unlinking dataflow blocks
ms.assetid: 40f0208d-4618-47f7-85cf-4913d07d2d7d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 989220141e4af5d64c3994479949547136843ff5
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592000"
---
# <a name="how-to-unlink-dataflow-blocks"></a>방법: 데이터 흐름 블록 링크 끊기
이 문서에서는 소스에서 대상 데이터 흐름 블록의 연결을 해제하는 방법을 설명합니다.

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

## <a name="example"></a>예제  
 다음 예제에서는 세 개의 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 개체를 만듭니다. 각 개체는 `TrySolution` 메서드를 호출하여 값을 컴퓨팅합니다. 이 예제는 종료하기 위해서 `TrySolution`에 대한 첫 번째 호출의 결과만 필요로 합니다.  
  
 [!code-csharp[TPLDataflow_ReceiveAny#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_receiveany/cs/dataflowreceiveany.cs#1)]
 [!code-vb[TPLDataflow_ReceiveAny#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_receiveany/vb/dataflowreceiveany.vb#1)]  
  
 종료되는 첫 번째 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 개체에서 값을 받기 위해 이 예제에서는 `ReceiveFromAny(T)` 메서드를 정의합니다. `ReceiveFromAny(T)` 메서드는 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> 개체의 배열을 수락하고 이러한 개체를 각각 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 개체에 연결합니다. <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> 메서드를 사용하여 소스 데이터 흐름 블록을 대상 블록에 연결하는 경우 소스는 데이터를 사용할 수 있게 될 때 메시지를 대상에 전파합니다. <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 클래스가 제공된 첫 번째 메시지만 수락하기 때문에 `ReceiveFromAny(T)` 메서드는 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Receive%2A> 메서드를 호출하여 결과를 생성합니다. 이를 통해 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 개체에 제공되는 첫 번째 메시지가 생성됩니다. <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> 메서드에는 `1`로 설정된 경우 대상이 소스에서 메시지를 받은 후 대상에서 연결을 해제하도록 소스 블록에 지시하는 <xref:System.Threading.Tasks.Dataflow.DataflowLinkOptions.MaxMessages> 속성이 있는 <xref:System.Threading.Tasks.Dataflow.DataflowLinkOptions> 개체를 사용하는 오버로드된 버전이 있습니다. 소스의 배열과 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 개체의 관계는 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 개체가 메시지를 받은 후 더 이상 필요하지 않기 때문에 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 개체는 소스에서 연결을 해제해야 합니다.  
  
 `TrySolution`에 대한 나머지 호출이 한 호출에서 값을 계산한 후 종료될 수 있도록 하기 위해 `TrySolution` 메서드는 <xref:System.Threading.CancellationToken> 호출이 반환된 후 취소되는 `ReceiveFromAny(T)` 개체를 사용합니다. <xref:System.Threading.SpinWait.SpinUntil%2A> 메서드는 이 <xref:System.Threading.CancellationToken> 개체가 취소될 때 반환됩니다.  
  
## <a name="see-also"></a>참고 항목

- [데이터 흐름](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)
