---
title: '방법: JoinBlock을 사용하여 여러 소스에서 데이터 읽기'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Task Parallel Library, dataflows
- TPL dataflow library, joining blocks in
- dataflow blocks, joining in TPL
ms.assetid: e9c1ada4-ac57-4704-87cb-2f5117f8151d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a7becba9c7626e79f9d001a6a21ed92a336e9d11
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591986"
---
# <a name="how-to-use-joinblock-to-read-data-from-multiple-sources"></a>방법: JoinBlock을 사용하여 여러 소스에서 데이터 읽기
이 문서에서는 <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> 클래스를 사용하여 여러 소스에서 데이터를 사용할 수 있는 경우 작업을 수행하는 방법을 설명합니다. 또한 non-greedy 모드를 사용하여 여러 조인 블록이 데이터 소스를 보다 효율적으로 공유할 수 있도록 하는 방법을 보여 줍니다.

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

## <a name="example"></a>예제  
 다음 예제에서는 세 가지 리소스 형식인 `NetworkResource`, `FileResource` 및 `MemoryResource`를 정의하고 리소스를 사용할 수 있게 되면 작업을 수행합니다. 이 예제에서는 첫 번째 작업을 수행하기 위해 `NetworkResource` 및 `MemoryResource` 쌍이 필요하고, 두 번째 작업을 수행하기 위해 `FileResource` 및 `MemoryResource` 쌍이 필요합니다. 필요한 리소스를 모두 사용할 수 있을 때 이러한 작업이 수행될 수 있도록 하기 위해 이 예제에서는 <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> 클래스를 사용합니다. <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> 개체는 모든 소스에서 데이터를 받으면 해당 데이터를 대상에 전파합니다. 이 예제에서 대상은 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 개체입니다. 두 <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> 개체 모두 `MemoryResource` 개체의 공유 풀에서 읽습니다.  
  
 [!code-csharp[TPLDataflow_NonGreedyJoin#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_nongreedyjoin/cs/nongreedyjoin.cs#1)]
 [!code-vb[TPLDataflow_NonGreedyJoin#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_nongreedyjoin/vb/nongreedyjoin.vb#1)]  
  
 `MemoryResource` 개체의 공유 풀을 효율적으로 사용할 수 있도록 하기 위해 이 예제에서는 <xref:System.Threading.Tasks.Dataflow.GroupingDataflowBlockOptions> 속성이 <xref:System.Threading.Tasks.Dataflow.GroupingDataflowBlockOptions.Greedy%2A>로 설정된 `False` 개체를 지정하여 non-greedy 모드에서 작동하는 <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> 개체를 만듭니다. non-greedy 조인 블록은 각 소스에서 메시지를 사용할 수 있을 때까지 들어오는 메시지를 모두 연기합니다. 연기된 메시지 중 하나라도 다른 블록에서 수락된 경우 조인 블록은 프로세스를 다시 시작합니다. non-greedy 모드에서 하나 이상의 소스 블록을 공유하는 조인 블록은 다른 블록이 데이터를 기다릴 때 작업을 진행할 수 있습니다. 이 예제에서 `MemoryResource` 개체가 `memoryResources` 풀에 추가되는 경우 두 번째 데이터 소스를 받을 첫 번째 조인 블록은 작업을 진행할 수 있습니다. 이 예제에서 기본값인 greedy 모드를 사용한다면 한 조인 블록이 `MemoryResource` 개체를 사용하고 두 번째 리소스를 사용할 수 있을 때까지 기다릴 수도 있습니다. 그러나 다른 조인 블록이 두 번째 데이터 소스를 사용할 수 있는 경우 `MemoryResource` 개체가 또 다른 조인 블록에서 사용되었기 때문에 작업을 진행할 수 없습니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 non-greedy 조인을 사용하면 애플리케이션에서 교착 상태를 방지하는 데도 도움이 될 수 있습니다. 소프트웨어 애플리케이션에서 *교착 상태*는 두 개 이상의 프로세스가 각각 리소스를 보유하고 함께 다른 프로세스가 다른 리소스를 해제할 때까지 대기하는 경우 발생합니다. 두 가지 <xref:System.Threading.Tasks.Dataflow.JoinBlock%602> 개체를 정의하는 애플리케이션의 경우, 두 개체는 각각 두 공유 소스 블록에서 데이터를 읽습니다. greedy 모드에서 한 조인 블록이 첫 번째 소스에서 읽고 두 번째 조인 블록이 두 번째 소스에서 읽는 경우 두 조인 블록은 상대방이 리소스를 해제하기를 서로 기다리기 때문에 애플리케이션에서 교착 상태가 발생할 수 있습니다. non-greedy 모드에서는 각 조인 블록이 모든 데이터를 사용할 수 있는 경우에만 소스에서 읽으므로 교착 상태의 위험이 제거됩니다.  
  
## <a name="see-also"></a>참고 항목

- [데이터 흐름](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)
