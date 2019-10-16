---
title: '방법: 데이터 흐름 블록 취소'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Task Parallel Library, dataflows
- dataflow blocks, canceling in TPL
- TPL dataflow library,canceling dataflow blocks
ms.assetid: fbddda0d-da3b-4ec8-a1d6-67ab8573fcd7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b95f0a3535716c4a01dae52abe38eb850f080cf0
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59345198"
---
# <a name="how-to-cancel-a-dataflow-block"></a>방법: 데이터 흐름 블록 취소
이 문서에서는 애플리케이션에서 취소를 사용하도록 설정하는 방법을 보여 줍니다. 이 예제에서는 Windows Forms를 사용하여 데이터 흐름 파이프라인에서 작업 항목이 활성 상태인 위치뿐만 아니라 취소의 효과도 보여 줍니다.  

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]
  
## <a name="to-create-the-windows-forms-application"></a>Windows Forms 애플리케이션을 만들려면  
  
1. C# 또는 Visual Basic **Windows Forms 애플리케이션** 프로젝트를 만듭니다. 다음 단계에서 프로젝트의 이름은 `CancellationWinForms`입니다.  
  
2. 기본 폼인 Form1.cs(Visual Basic에서는 Form1.vb)의 폼 디자이너에서 <xref:System.Windows.Forms.ToolStrip> 컨트롤을 추가합니다.  
  
3. <xref:System.Windows.Forms.ToolStripButton> 컨트롤을 <xref:System.Windows.Forms.ToolStrip> 컨트롤에 추가합니다. <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> 속성을 <xref:System.Windows.Forms.ToolStripItemDisplayStyle.Text> 및 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 속성으로 설정하여 **작업 항목을 추가**합니다.  
  
4. 두 번째 <xref:System.Windows.Forms.ToolStripButton> 컨트롤을 <xref:System.Windows.Forms.ToolStrip> 컨트롤에 추가합니다. <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> 속성을 <xref:System.Windows.Forms.ToolStripItemDisplayStyle.Text>로 설정하고, <xref:System.Windows.Forms.ToolStripItem.Text%2A> 속성을 **취소**로 설정하고, <xref:System.Windows.Forms.ToolStripItem.Enabled%2A> 속성을 `False`로 설정합니다.  
  
5. 4개의 <xref:System.Windows.Forms.ToolStripProgressBar> 개체를 <xref:System.Windows.Forms.ToolStrip> 컨트롤에 추가합니다.  
  
## <a name="creating-the-dataflow-pipeline"></a>데이터 흐름 파이프라인 만들기  
 이 섹션에서는 작업 항목을 처리하고 진행률 표시줄을 업데이트하는 데이터 흐름 파이프라인을 만드는 방법을 설명합니다.  
  
### <a name="to-create-the-dataflow-pipeline"></a>데이터 흐름 파이프라인을 만들려면  
  
1. 프로젝트에서 System.Threading.Tasks.Dataflow.dll에 대한 참조를 추가합니다.  
  
2. Form1.cs(Visual Basic에서는 Form1.vb)에 다음 `using` 명령문(Visual Basic에서는 `Imports`)이 포함되어 있는지 확인합니다.  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#1)]
     [!code-vb[TPLDataflow_CancellationWinForms#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#1)]  
  
3. `WorkItem` 클래스를 `Form1` 클래스의 내부 형식으로 추가합니다.  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#2)]
     [!code-vb[TPLDataflow_CancellationWinForms#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#2)]  
  
4. `Form1` 클래스에 다음 데이터 멤버를 추가합니다.  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#3)]
     [!code-vb[TPLDataflow_CancellationWinForms#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#3)]  
  
5. 다음 `CreatePipeline` 메서드를 `Form1` 클래스에 추가합니다.  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#4)]
     [!code-vb[TPLDataflow_CancellationWinForms#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#4)]  
  
 `incrementProgress` 및 `decrementProgress` 데이터 흐름 블록이 사용자 인터페이스에서 작동하기 때문에 이러한 작업은 사용자 인터페이스 스레드에서 발생해야 합니다. 이를 위해 생성 중에 이러한 개체는 각각 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.TaskScheduler%2A> 속성이 <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=nameWithType>로 설정된 <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions> 개체를 제공합니다. <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=nameWithType> 메서드는 현재 동기화 컨텍스트에서 작업을 수행하는 <xref:System.Threading.Tasks.TaskScheduler> 개체를 만듭니다. `Form1` 생성자가 사용자 인터페이스 스레드에서 호출되기 때문에 `incrementProgress` 및 `decrementProgress` 데이터 흐름 블록에 대한 작업도 사용자 인터페이스 스레드에서 실행됩니다.  
  
 이 예제에서는 파이프라인의 멤버를 생성할 때 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> 속성을 설정합니다. <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> 속성은 데이터 흐름 블록 실행을 영구적으로 취소하므로 사용자가 작업을 취소한 다음, 파이프라인에 더 많은 작업 항목을 추가하기를 원하면 전체 파이프라인을 다시 만들어야 합니다. 작업이 취소된 후 다른 작업을 수행할 수 있도록 데이터 흐름 블록을 취소하는 대체 방법을 보여 주는 예제는 [연습: Windows Forms 애플리케이션에서 데이터 흐름 사용](../../../docs/standard/parallel-programming/walkthrough-using-dataflow-in-a-windows-forms-application.md)을 참조하세요.  
  
## <a name="connecting-the-dataflow-pipeline-to-the-user-interface"></a>사용자 인터페이스에 데이터 흐름 파이프라인 연결  
 이 섹션에서는 사용자 인터페이스에 데이터 흐름 파이프라인을 연결하는 방법에 대해 설명합니다. 파이프라인을 만들고 파이프라인에 작업 항목을 추가하는 작업은 모두 **작업 항목 추가** 단추의 이벤트 처리기에서 제어됩니다. 취소는 **취소** 단추를 클릭하면 시작됩니다. 사용자가 이러한 단추 중 하나를 클릭하면 적절한 작업이 비동기식으로 시작됩니다.  
  
### <a name="to-connect-the-dataflow-pipeline-to-the-user-interface"></a>사용자 인터페이스에 데이터 흐름 파이프라인을 연결하려면  
  
1. 기본 폼의 폼 디자이너에서 **작업 항목 추가** 단추에 대한 <xref:System.Windows.Forms.ToolStripItem.Click> 이벤트의 이벤트 처리기를 만듭니다.  
  
2. **작업 항목 추가** 단추에 대한 <xref:System.Windows.Forms.ToolStripItem.Click> 이벤트를 구현합니다.  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#5)]
     [!code-vb[TPLDataflow_CancellationWinForms#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#5)]  
  
3. 기본 폼의 폼 디자이너에서 **취소** 단추에 대한 <xref:System.Windows.Forms.ToolStripItem.Click> 이벤트 처리기의 이벤트 처리기를 만듭니다.  
  
4. **취소** 단추에 대한 <xref:System.Windows.Forms.ToolStripItem.Click> 이벤트 처리기를 구현합니다.  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#6)]
     [!code-vb[TPLDataflow_CancellationWinForms#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#6)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 Form1.cs(Visual Basic에서는 Form1.vb)의 전체 코드를 보여 줍니다.  
  
 [!code-csharp[TPLDataflow_CancellationWinForms#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#100)]
 [!code-vb[TPLDataflow_CancellationWinForms#100](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#100)]  
  
 다음 그림에서는 실행 중인 애플리케이션을 보여 줍니다.  
  
 ![Windows Forms 애플리케이션](../../../docs/standard/parallel-programming/media/tpldataflow-cancellation.png "TPLDataflow_Cancellation")  

## <a name="see-also"></a>참고 항목

- [데이터 흐름](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)
