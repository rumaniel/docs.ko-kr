---
title: '연습: 사용자 지정 데이터 흐름 블록 형식 만들기'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Task Parallel Library, dataflows
- TPL dataflow library, creating custom dataflow blocks
- dataflow blocks, creating custom in TPL
ms.assetid: a6147146-0a6a-4d9b-ab0f-237b3c1ac691
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 62e2a25e48ead730112a37af451d64c6ccc2e141
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65593439"
---
# <a name="walkthrough-creating-a-custom-dataflow-block-type"></a>연습: 사용자 지정 데이터 흐름 블록 형식 만들기
TPL 데이터 흐름 라이브러리는 다양한 기능을 구현하는 여러 데이터 흐름 블록 형식을 제공하지만 사용자 지정 블록 형식을 만들 수도 있습니다. 이 문서에서는 사용자 지정 동작을 구현하는 데이터 흐름 블록 형식을 만드는 방법을 설명합니다.  
  
## <a name="prerequisites"></a>전제 조건  
 이 문서를 읽기 전에 [데이터 흐름](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)을 읽어 보세요.  

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]
  
## <a name="defining-the-sliding-window-dataflow-block"></a>슬라이딩 윈도우 데이터 흐름 블록 정의  
 입력 값을 버퍼링한 다음, 슬라이딩 윈도우 방식으로 출력해야 하는 데이터 흐름 애플리케이션을 고려합니다. 예를 들어 입력 값 {0, 1, 2, 3, 4, 5} 및 윈도우 크기가 3인 경우 슬라이딩 윈도우 데이터 흐름 블록은 출력 배열 {0, 1, 2}, {1, 2, 3}, {2, 3, 4}, {3, 4, 5}를 생성합니다. 다음 섹션에서는 이 사용자 지정 동작을 구현하는 데이터 흐름 블록 형식을 만드는 두 가지 방법을 보여줍니다. 첫 번째 방법은 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Encapsulate%2A> 메서드를 사용하여 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> 개체와 <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> 개체의 기능을 하나의 전파자 블록으로 결합합니다. 두 번째 방법은 <xref:System.Threading.Tasks.Dataflow.IPropagatorBlock%602>에서 파생되는 클래스를 정의하고 기존 기능을 결합하여 사용자 지정 동작을 수행합니다.  
  
## <a name="using-the-encapsulate-method-to-define-the-sliding-window-dataflow-block"></a>Encapsulate 메서드를 사용하여 슬라이딩 윈도우 데이터 흐름 블록 정의  
 다음 예제에서는 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Encapsulate%2A> 메서드를 사용하여 대상과 소스에서 전파자 블록을 만듭니다. 전파자 블록을 사용하면 소스 블록과 대상 블록이 데이터 수신자 및 송신자 역할을 할 수 있습니다.  
  
 이 방법은 사용자 지정 데이터 흐름 기능이 필요하지만 추가 메서드, 속성 또는 필드를 제공하는 형식이 필요하지 않은 경우 유용합니다.  
  
 [!code-csharp[TPLDataflow_SlidingWindowBlock#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_slidingwindowblock/cs/slidingwindowblock.cs#1)]
 [!code-vb[TPLDataflow_SlidingWindowBlock#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_slidingwindowblock/vb/slidingwindowblock.vb#1)]  
  
## <a name="deriving-from-ipropagatorblock-to-define-the-sliding-window-dataflow-block"></a>IPropagatorBlock에서 파생시켜 슬라이딩 윈도우 데이터 흐름 블록 정의  
 다음 예제에서는 `SlidingWindowBlock` 클래스를 보여줍니다. 이 클래스는 <xref:System.Threading.Tasks.Dataflow.IPropagatorBlock%602>에서 파생되므로 데이터의 소스 및 대상 역할을 할 수 있습니다. 이전 예제와 같이 `SlidingWindowBlock` 클래스는 기존 데이터 흐름 블록 형식에 빌드됩니다. 그러나 `SlidingWindowBlock` 클래스는 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601>, <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> 및 <xref:System.Threading.Tasks.Dataflow.IDataflowBlock> 인터페이스에 필요한 메서드도 구현합니다. 이러한 메서드는 모두 미리 정의된 데이터 흐름 블록 형식 멤버에 대한 작업을 전달합니다. 예를 들어 `Post` 메서드는 작업을 <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> 개체이기도 한 `m_target` 데이터 멤버로 전달합니다.  
  
 이 방법은 사용자 지정 데이터 흐름 기능이 필요하고 추가 메서드, 속성 또는 필드를 제공하는 형식도 필요한 경우 유용합니다. 예를 들어 `SlidingWindowBlock` 클래스는 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601>에서 파생되므로 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> 및 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceiveAll%2A> 메서드를 제공할 수 있습니다. 또한 `SlidingWindowBlock` 클래스는 슬라이딩 윈도우에서 요소 수를 검색하는 `WindowSize` 속성을 제공하여 확장성을 보여줍니다.  
  
 [!code-csharp[TPLDataflow_SlidingWindowBlock#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_slidingwindowblock/cs/slidingwindowblock.cs#2)]
 [!code-vb[TPLDataflow_SlidingWindowBlock#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_slidingwindowblock/vb/slidingwindowblock.vb#2)]  
  
## <a name="the-complete-example"></a>전체 예제  
 다음 예제에서는 이 연습의 전체 코드를 보여 줍니다. 또한 블록에 쓰고, 블록에서 읽고, 콘솔에 결과를 인쇄하는 메서드에서 두 슬라이딩 윈도우 블록을 모두 사용하는 방법을 보여줍니다.  
  
 [!code-csharp[TPLDataflow_SlidingWindowBlock#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_slidingwindowblock/cs/slidingwindowblock.cs#100)]
 [!code-vb[TPLDataflow_SlidingWindowBlock#100](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_slidingwindowblock/vb/slidingwindowblock.vb#100)]  
  
## <a name="see-also"></a>참고 항목

- [데이터 흐름](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)
