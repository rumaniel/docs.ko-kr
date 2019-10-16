---
title: '방법: 데이터 흐름 블록에서 작업 스케줄러 지정'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TPL dataflow library, linking to task scheduler in TPL
- Task Parallel Library, dataflows
- task scheduler, linking from TPL
ms.assetid: 27ece374-ed5b-49ef-9cec-b20db34a65e8
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 681c0f1f918c8991ed2544189488d1ea25547834
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59345848"
---
# <a name="how-to-specify-a-task-scheduler-in-a-dataflow-block"></a>방법: 데이터 흐름 블록에서 작업 스케줄러 지정
이 문서에서는 애플리케이션에서 데이터 흐름을 사용하는 경우 특정 작업 스케줄러를 연결하는 방법을 보여 줍니다. 예제에서는 Windows Forms 애플리케이션에서 <xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair?displayProperty=nameWithType> 클래스를 사용하여 판독기 작업이 활성화된 경우와 작성기 작업이 활성화된 경우를 표시합니다. 또한 <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=nameWithType> 메서드를 사용하여 데이터 흐름 블록이 사용자 인터페이스 스레드에서 실행될 수 있도록 합니다.

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

## <a name="to-create-the-windows-forms-application"></a>Windows Forms 애플리케이션을 만들려면  
  
1. Visual C# 또는 Visual Basic **Windows Forms 애플리케이션** 프로젝트를 만듭니다. 다음 단계에서 프로젝트의 이름은 `WriterReadersWinForms`입니다.  
  
2. 기본 폼인 Form1.cs(Visual Basic에서는 Form1.vb)의 폼 디자이너에서 네 개 <xref:System.Windows.Forms.CheckBox> 컨트롤을 추가합니다. <xref:System.Windows.Forms.Control.Text%2A> 속성을 `checkBox1`의 경우 **Reader 1**, `checkBox2`의 경우 **Reader 2**, `checkBox3`의 경우 **Reader 3**, `checkBox4`의 경우 **Writer**로 설정합니다. 각 컨트롤의 <xref:System.Windows.Forms.Control.Enabled%2A> 속성을 `False`로 설정합니다.  
  
3. 폼에 <xref:System.Windows.Forms.Timer> 컨트롤을 추가합니다. <xref:System.Windows.Forms.Timer.Interval%2A> 속성을 `2500`으로 설정합니다.  
  
## <a name="adding-dataflow-functionality"></a>데이터 흐름 기능 추가  
 이 단원에서는 애플리케이션에 참여하는 데이터 흐름 블록을 만드는 방법과 각 데이터 흐름 블록을 작업 스케줄러와 연결하는 방법을 설명합니다.  
  
### <a name="to-add-dataflow-functionality-to-the-application"></a>애플리케이션에 데이터 흐름 기능을 추가하려면  
  
1. 프로젝트에서 System.Threading.Tasks.Dataflow.dll에 대한 참조를 추가합니다.  
  
2. Form1.cs(Visual Basic에서는 Form1.vb)에 다음 `using` 명령문(Visual Basic에서는 `Imports`)이 포함되어 있는지 확인합니다.  
  
     [!code-csharp[TPLDataflow_WriterReadersWinForms#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#1)]
     [!code-vb[TPLDataflow_WriterReadersWinForms#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#1)]  
  
3. <xref:System.Threading.Tasks.Dataflow.BroadcastBlock%601> 클래스에 `Form1` 데이터 멤버를 추가합니다.  
  
     [!code-csharp[TPLDataflow_WriterReadersWinForms#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#2)]
     [!code-vb[TPLDataflow_WriterReadersWinForms#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#2)]  
  
4. `Form1` 생성자에서 `InitializeComponent`를 호출한 후 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 개체의 상태를 전환하는 <xref:System.Windows.Forms.CheckBox> 개체를 만듭니다.  
  
     [!code-csharp[TPLDataflow_WriterReadersWinForms#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#3)]
     [!code-vb[TPLDataflow_WriterReadersWinForms#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#3)]  
  
5. `Form1` 생성자에서 <xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair> 개체와 4개의 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 개체를 만듭니다. 이때 각 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 개체에 대해 <xref:System.Windows.Forms.CheckBox> 개체를 하나씩 만듭니다. 각 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 개체에 대해 <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions> 속성이 판독기의 경우 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.TaskScheduler%2A> 속성으로 설정되고 작성기의 경우 <xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair.ConcurrentScheduler%2A> 속성으로 설정된 <xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair.ExclusiveScheduler%2A> 개체를 지정합니다.  
  
     [!code-csharp[TPLDataflow_WriterReadersWinForms#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#4)]
     [!code-vb[TPLDataflow_WriterReadersWinForms#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#4)]  
  
6. `Form1` 생성자에서 <xref:System.Windows.Forms.Timer> 개체를 시작합니다.  
  
     [!code-csharp[TPLDataflow_WriterReadersWinForms#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#5)]
     [!code-vb[TPLDataflow_WriterReadersWinForms#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#5)]  
  
7. 기본 폼의 폼 디자이너에서 타이머에 대한 <xref:System.Windows.Forms.Timer.Tick> 이벤트의 이벤트 처리기를 만듭니다.  
  
8. 타이머에 대한 <xref:System.Windows.Forms.Timer.Tick> 이벤트를 구현합니다.  
  
     [!code-csharp[TPLDataflow_WriterReadersWinForms#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#6)]
     [!code-vb[TPLDataflow_WriterReadersWinForms#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#6)]  
  
 `toggleCheckBox` 데이터 흐름 블록이 사용자 인터페이스에서 동작하기 때문에 이 작업은 사용자 인터페이스 스레드에서 발생해야 합니다. 이를 위해 생성 중에 이 개체는 <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions> 속성이 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.TaskScheduler%2A>로 설정된 <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=nameWithType> 개체를 제공합니다. <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A> 메서드는 현재 동기화 컨텍스트에서 작업을 수행하는 <xref:System.Threading.Tasks.TaskScheduler> 개체를 만듭니다. `Form1` 생성자가 사용자 인터페이스 스레드에서 호출되기 때문에 `toggleCheckBox` 데이터 흐름 블록에 대한 작업도 사용자 인터페이스 스레드에서 실행됩니다.  
  
 또한 이 예제에서는 <xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair> 클래스를 사용하여 일부 데이터 흐름 블록이 동시에 동작할 수 있도록 하고 다른 데이터 흐름 블록이 동일한 <xref:System.Threading.Tasks.ConcurrentExclusiveSchedulerPair> 개체에서 실행되는 다른 모든 데이터 흐름 블록과 독립적으로 동작할 수 있도록 합니다. 이 방법은 여러 데이터 흐름 블록이 리소스를 공유할 때 해당 리소스에 대한 액세스를 수동으로 동기화할 필요를 없애기 위해 일부 데이터 흐름 블록에 해당 리소스에 대한 배타적 액세스 권한이 필요한 경우에 유용합니다. 수동 동기화를 제거하면 코드의 효율성이 향상될 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 Form1.cs(Visual Basic에서는 Form1.vb)의 전체 코드를 보여 줍니다.  
  
 [!code-csharp[TPLDataflow_WriterReadersWinForms#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/cs/writerreaderswinforms/form1.cs#100)]
 [!code-vb[TPLDataflow_WriterReadersWinForms#100](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_writerreaderswinforms/vb/writerreaderswinforms/form1.vb#100)]  
  
## <a name="see-also"></a>참고 항목

- [데이터 흐름](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)
