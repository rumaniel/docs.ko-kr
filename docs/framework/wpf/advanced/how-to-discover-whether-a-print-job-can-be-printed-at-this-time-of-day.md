---
title: '방법: 특정 시간에 인쇄 작업을 인쇄할 수 있는지 확인'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- print queues [WPF], timing
- printers [WPF], availability
- print jobs [WPF], timing
ms.assetid: 7e9c8ec1-abf6-4b3d-b1c6-33b35d3c4063
ms.openlocfilehash: 859dc75169e443d07361951692a428507886fa2e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69947806"
---
# <a name="how-to-discover-whether-a-print-job-can-be-printed-at-this-time-of-day"></a>방법: 특정 시간에 인쇄 작업을 인쇄할 수 있는지 확인
인쇄 큐는 하루 24 시간 동안 항상 사용할 수 있는 것은 아닙니다. 특정 시간에 사용할 수 없도록 설정할 수 있는 시작 및 종료 시간 속성이 있습니다. 예를 들어이 기능을 사용 하 여 오후 5 시에 특정 부서의 독점 사용을 위해 프린터를 예약할 수 있습니다. 해당 부서는 다른 부서에서 사용 하는 것과 다른 큐 서비스를 제공 합니다. 다른 부서에 대 한 큐는 오후 5 시에 사용할 수 없음으로 설정 되 고, 선호 하는 부서의 큐는 항상 사용 가능 하도록 설정 될 수 있습니다.  
  
 또한 인쇄 작업 자체는 지정 된 시간 범위 내 에서만 인쇄 가능 하도록 설정 될 수 있습니다.  
  
 Microsoft .NET <xref:System.Printing.PrintQueue> Framework <xref:System.Printing.PrintSystemJobInfo> 의 api에 노출 되는 및 클래스는 지정 된 인쇄 작업에서 지정 된 큐에 현재 시간에 인쇄할 수 있는지 여부를 원격으로 확인 하는 방법을 제공 합니다.  
  
## <a name="example"></a>예제  
 아래 예제는 인쇄 작업의 문제를 진단할 수 있는 샘플입니다.  
  
 이러한 종류의 함수에 대 한 두 가지 주요 단계는 다음과 같습니다.  
  
1. <xref:System.Printing.PrintQueue.StartTimeOfDay%2A> 의 <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> 및 속성을읽어현재시간사이에있는지여부를확인합니다.<xref:System.Printing.PrintQueue>  
  
2. <xref:System.Printing.PrintSystemJobInfo.StartTimeOfDay%2A> 의 <xref:System.Printing.PrintSystemJobInfo.UntilTimeOfDay%2A> 및 속성을읽어현재시간사이에있는지여부를확인합니다.<xref:System.Printing.PrintSystemJobInfo>  
  
 그러나 이러한 속성이 개체가 아닌 <xref:System.DateTime> 경우에는 복잡 한 상황이 발생 합니다. 대신 자정 이후의 시간 (분)으로 시간을 표현 하는 개체입니다.<xref:System.Int32> 또한 현재 표준 시간대에서 자정은 아니지만 UTC (협정 세계시) 자정입니다.  
  
 첫 번째 코드 예제는를 <xref:System.Printing.PrintSystemJobInfo> 전달 하 고 도우미 메서드를 호출 하 여 작업을 현재 시간에 인쇄할 수 있는지 여부를 확인 하 고, 인쇄 될 수 있는 경우이를 호출 하는 정적 메서드 **reportqueueandjobavailability**를 제공 합니다. <xref:System.Printing.PrintQueue> 는 메서드에 전달 되지 않습니다. 이는의 <xref:System.Printing.PrintSystemJobInfo> <xref:System.Printing.PrintSystemJobInfo.HostingPrintQueue%2A> 속성에 큐에 대 한 참조가 포함 되어 있기 때문입니다.  
  
 하위 메서드는 <xref:System.Printing.PrintQueue> 또는를 <xref:System.Printing.PrintSystemJobInfo> 매개 변수로 사용할 수 있는 오버 로드 된 **ReportAvailabilityAtThisTime** 메서드를 포함 합니다. **ConvertToLocalHumanReadableTime TimeConverter**도 있습니다. 이러한 모든 메서드는 아래에 설명 되어 있습니다.  
  
 **Reportqueueandjobavailability** 메서드는 현재 큐 또는 인쇄 작업을 사용할 수 없는지 확인 하 여 시작 합니다. 둘 중 하나를 사용할 수 없는 경우에는 큐를 사용할 수 없는지 확인 합니다. 사용할 수 없는 경우이 메서드는이 사실을 보고 하 고 큐를 다시 사용할 수 있게 되는 시간을 보고 합니다. 그런 다음 작업을 확인 하 고 사용할 수 없는 경우 다음 시간이 인쇄 될 때 해당 작업을 보고 합니다. 마지막으로 메서드는 작업을 인쇄할 수 있는 가장 빠른 시간을 보고 합니다. 이는 다음의 두 번 이상입니다.  
  
- 인쇄 큐를 다음에 사용할 수 있는 시간입니다.  
  
- 인쇄 작업을 다음에 사용할 수 있는 시간입니다.  
  
 하루 중 시간을 보고 하 <xref:System.DateTime.ToShortTimeString%2A> 는 경우이 메서드는 출력에서 년, 월 및 일을 표시 하지 않기 때문에 메서드가 호출 됩니다. 인쇄 큐 또는 인쇄 작업의 가용성을 특정 연도, 월 또는 일로 제한할 수는 없습니다.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#ReportQueueAndJobAvailability](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#reportqueueandjobavailability)]
 [!code-csharp[DiagnoseProblematicPrintJob#ReportQueueAndJobAvailability](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#reportqueueandjobavailability)]
 [!code-vb[DiagnoseProblematicPrintJob#ReportQueueAndJobAvailability](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#reportqueueandjobavailability)]  
  
 **ReportAvailabilityAtThisTime** 메서드의 두 오버 로드는 전달 되는 형식을 제외 하 고는 동일 하므로 버전은 <xref:System.Printing.PrintQueue> 아래에만 표시 됩니다.  
  
> [!NOTE]
> 메서드는 형식을 제외 하 고는 **\<ReportAvailabilityAtThisTime T >** 제네릭 메서드를 만들지 않는 이유에 대 한 질문을 발생 시킵니다. 이러한 메서드는 메서드가 호출 하는 **Starttimeofday** 및 **system.printing.printqueue.untiltimeofday** 속성이 있는 클래스로 제한 되어야 하지만, 제네릭 메서드는 단일 클래스로만 제한 될 수 있으며, 둘 다에 공통적인 유일한 클래스로 제한 될 수 있기 때문입니다. 상속 트리에 는이러한<xref:System.Printing.PrintSystemObject>속성이없습니다. <xref:System.Printing.PrintQueue> <xref:System.Printing.PrintSystemJobInfo>  
  
 **ReportAvailabilityAtThisTime** 메서드 (아래 코드 예제에 표시)는 <xref:System.Boolean> 센티널 변수를로 `true`초기화 하 여 시작 합니다. 큐를 사용할 수 없는 `false`경우에 다시 설정 됩니다.  
  
 다음으로 메서드는 start와 "until" 시간이 동일한 지 확인 합니다. 인 경우 큐는 항상 사용할 수 있으므로 메서드는를 반환 `true`합니다.  
  
 큐를 항상 사용할 수 없는 경우 메서드는 정적 <xref:System.DateTime.UtcNow%2A> 속성을 사용 하 여 현재 시간 <xref:System.DateTime> 을 개체로 가져옵니다. <xref:System.Printing.PrintQueue.StartTimeOfDay%2A> 및<xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> 속성은 UTC 시간 이므로 현지 시간이 필요 하지 않습니다.  
  
 그러나 이러한 두 속성은 개체가 아닙니다 <xref:System.DateTime> . <xref:System.Int32>시간을 시간 (분)의 시간을 UTC-자정의 수로 표현한 것입니다. 따라서 <xref:System.DateTime> 개체를 자정 이후 시간 (분)으로 변환 해야 합니다. 이 작업이 완료 되 면 메서드는 "now"가 큐의 시작과 "until" 사이에 있는지 확인 하 고, "now"가 두 시간 사이에 있지 않으면 센티널을 false로 설정 하 고 센티널을 반환 합니다.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#PrintQueueStartUntil](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#printqueuestartuntil)]
 [!code-csharp[DiagnoseProblematicPrintJob#PrintQueueStartUntil](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#printqueuestartuntil)]
 [!code-vb[DiagnoseProblematicPrintJob#PrintQueueStartUntil](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#printqueuestartuntil)]  
  
 **TimeConverter ConvertToLocalHumanReadableTime** 메서드 (아래 코드 예제에 표시)는 Microsoft .NET Framework에 도입 된 메서드를 사용 하지 않으므로 간략 한 토론입니다. 메서드에는 이중 변환 태스크가 있습니다 .이 작업은 자정 이후 시간 (분)을 나타내는 정수를 사용 하 고 사용자가 읽을 수 있는 시간으로 변환 해야 하며,이를 현지 시간으로 변환 해야 합니다. 이를 위해 먼저 자정 UTC로 <xref:System.DateTime> 설정 된 개체를 만든 다음 <xref:System.DateTime.AddMinutes%2A> 메서드를 사용 하 여 메서드에 전달 된 분을 추가 합니다. 그러면 메서드에 전달 된 <xref:System.DateTime> 원래 시간을 나타내는 새이 반환 됩니다. 그런 <xref:System.DateTime.ToLocalTime%2A> 다음 메서드는이를 현지 시간으로 변환 합니다.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#TimeConverter](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#timeconverter)]
 [!code-csharp[DiagnoseProblematicPrintJob#TimeConverter](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#timeconverter)]
 [!code-vb[DiagnoseProblematicPrintJob#TimeConverter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#timeconverter)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.DateTime>
- <xref:System.Printing.PrintSystemJobInfo>
- <xref:System.Printing.PrintQueue>
- [WPF의 문서](documents-in-wpf.md)
- [인쇄 개요](printing-overview.md)
