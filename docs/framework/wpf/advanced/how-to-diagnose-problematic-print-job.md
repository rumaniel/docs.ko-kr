---
title: '방법: 인쇄 작업 문제 진단'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- troubleshooting print job problems [WPF]
- print jobs [WPF], troubleshooting
- print jobs [WPF], diagnosing problems
ms.assetid: b081a170-84c6-48f9-a487-5766a8d58a82
ms.openlocfilehash: 181248f69684860fd43648952ef4eb3cced1c0ba
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69944633"
---
# <a name="how-to-diagnose-problematic-print-job"></a>방법: 인쇄 작업 문제 진단
네트워크 관리자는 사용자로부터 인쇄 작업이 인쇄되지 않거나 느리게 인쇄되는 문제에 대한 불만을 흔히 처리합니다. Microsoft .NET Framework의 Api에 노출 된 다양 한 인쇄 작업 속성은 인쇄 작업의 신속한 원격 진단을 수행 하는 수단을 제공 합니다.  
  
## <a name="example"></a>예제  
 이러한 종류의 유틸리티를 만드는 주요 단계는 다음과 같습니다.  
  
1. 사용자가 불만족하는 인쇄 작업을 식별합니다. 사용자는 흔히 이런 작업을 정확하게 수행할 수 없습니다. 인쇄 서버 또는 프린터의 이름을 모를 수 있습니다. 해당 <xref:System.Printing.PrintQueue.Location%2A> 속성을 설정 하는 데 사용 된 것과 다른 용어로 프린터 위치를 설명할 수 있습니다. 따라서 사용자가 현재 제출한 작업 목록을 생성하는 것이 좋습니다. 둘 이상인 경우 사용자와 인쇄 시스템 관리자 간의 통신을 사용하여 문제가 있는 작업을 찾을 수 있습니다. 하위단계는 다음과 같습니다.  
  
    1. 모든 인쇄 서버 목록을 가져옵니다.  
  
    2. 서버를 반복하여 해당 인쇄 큐를 쿼리합니다.  
  
    3. 서버 루프의 각 단계 내에서 해당 작업을 쿼리하는 모든 서버의 큐를 반복합니다.  
  
    4. 큐 루프의 각 단계 내에서 해당 작업을 반복하고 불만이 있는 사용자가 제출한 작업에 대한 식별 정보를 수집합니다.  
  
2. 인쇄 작업 문제를 식별하는 경우 관련 속성을 검사하여 문제가 무엇인지를 확인합니다. 예를 들어 작업이 오류 상태이거나 작업이 인쇄되기 전에 큐를 제공하는 프린터가 오프라인으로 전환되었는지와 같은 문제입니다.  
  
 아래 코드는 일련의 코드 예제입니다. 첫 번째 코드 예제는 인쇄 대기열을 통한 루프를 포함합니다. (위의 1c 단계.) 변수 `myPrintQueues` 는 현재 인쇄 <xref:System.Printing.PrintQueueCollection> 서버에 대 한 개체입니다.  
  
 코드 예제는를 사용 <xref:System.Printing.PrintQueue.Refresh%2A?displayProperty=nameWithType>하 여 현재 인쇄 큐 개체를 새로 고쳐 시작 합니다. 이렇게 하면 개체의 속성이 나타내는 실제 프린터의 상태를 정확하게 표시합니다. 그런 다음 응용 프로그램은를 사용 <xref:System.Printing.PrintQueue.GetPrintJobInfoCollection%2A>하 여 인쇄 큐에 현재 인쇄 작업의 컬렉션을 가져옵니다.  
  
 그런 다음 응용 프로그램은 컬렉션 <xref:System.Printing.PrintSystemJobInfo> 을 반복 하 고 <xref:System.Printing.PrintSystemJobInfo.Submitter%2A> 각 속성과 불만이 사용자의 별칭을 비교 합니다. 일치하는 경우 애플리케이션은 표시될 문자열 작업에 대한 식별 정보를 추가합니다. (`userName` 및 `jobList` 변수는 애플리케이션의 앞부분에서 초기화됩니다.)  
  
 [!code-cpp[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#enumeratejobsinqueues)]
 [!code-csharp[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#enumeratejobsinqueues)]
 [!code-vb[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#enumeratejobsinqueues)]  
  
 다음 코드 예제에서는 2단계의 애플리케이션을 선택합니다. (위를 참조) 문제가 있는 작업이 식별되고 애플리케이션이 식별되는 정보를 묻는 메시지를 표시합니다. 이 정보에서, <xref:System.Printing.PrintServer> <xref:System.Printing.PrintQueue>및 <xref:System.Printing.PrintSystemJobInfo> 개체를 만듭니다.  
  
 이 시점에서 애플리케이션에는 인쇄 작업의 상태를 검사하는 두 가지 방법에 해당하는 분기 구조가 포함되어 있습니다.  
  
- <xref:System.Printing.PrintSystemJobInfo.JobStatus%2A> 형식의<xref:System.Printing.PrintJobStatus>속성에 대 한 플래그를 읽을 수 있습니다.  
  
- <xref:System.Printing.PrintSystemJobInfo.IsBlocked%2A> 및<xref:System.Printing.PrintSystemJobInfo.IsInError%2A>와 같은 관련 된 각 속성을 읽을 수 있습니다.  
  
 이 예제에서는 두 메서드를 모두 보여 줍니다. 따라서 사용자는 이전에 사용할 메서드를 묻는 메시지를 표시 하 고 <xref:System.Printing.PrintSystemJobInfo.JobStatus%2A> 속성의 플래그를 사용 하려는 경우 "Y"로 응답 했습니다. 두 가지 방법에 대한 자세한 내용은 아래를 참조하세요. 마지막으로 애플리케이션이 **ReportQueueAndJobAvailability**라는 메서드를 사용하여 이 시간에 작업을 인쇄할 수 있는지 여부를 보고합니다. [인쇄 작업을 현재 인쇄할 수 있는지 확인](how-to-discover-whether-a-print-job-can-be-printed-at-this-time-of-day.md)에서 이 메서드를 설명합니다.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#identifyanddiagnoseproblematicjob)]
 [!code-csharp[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#identifyanddiagnoseproblematicjob)]
 [!code-vb[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#identifyanddiagnoseproblematicjob)]  
  
 <xref:System.Printing.PrintSystemJobInfo.JobStatus%2A> 속성의 플래그를 사용 하 여 인쇄 작업 상태를 확인 하려면 각 관련 플래그를 검사 하 여 설정 되었는지 확인 합니다. 일련의 비트 플래그에 하나의 비트가 설정되었는지 확인하는 표준 방법은 일련의 플래그가 있는 논리적 AND 연산을 하나의 피연산자로 수행하고 플래그 자체를 다른 피연산자로 수행하는 것입니다. 플래그 자체가 하나의 비트만 설정하므로 논리적 AND의 결과는 비트가 설정되는 것과 거의 동일합니다. 여부를 확인하려면 플래그 자체와 논리적 AND의 결과를 비교합니다. 자세한 내용은 <xref:System.Printing.PrintJobStatus> [& 연산자 (C# 참조)](../../../csharp/language-reference/operators/bitwise-and-shift-operators.md#logical-and-operator-)및 <xref:System.FlagsAttribute>을 참조 하십시오.  
  
 비트가 설정된 각 특성의 경우 코드는 콘솔 화면에 이를 보고하고 경우에 따라 응답하는 방법을 제안합니다. 작업 또는 큐가 일시 중지되는 경우 호출되는 **HandlePausedJob** 메서드는 아래에 설명됩니다.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#spottroubleusingjobattributes)]
 [!code-csharp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#spottroubleusingjobattributes)]
 [!code-vb[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#spottroubleusingjobattributes)]  
  
 별도 속성을 사용하여 인쇄 작업 상태를 확인하려면 단순히 각 속성을 읽고 속성이 `true`인 경우 콘솔 화면에 보고하고 응답하는 방법을 제안할 수 있습니다. 작업 또는 큐가 일시 중지되는 경우 호출되는 **HandlePausedJob** 메서드는 아래에 설명됩니다.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#spottroubleusingjobproperties)]
 [!code-csharp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#spottroubleusingjobproperties)]
 [!code-vb[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#spottroubleusingjobproperties)]  
  
 **HandlePausedJob** 메서드를 사용하면 응용 프로그램의 사용자가 원격으로 일시 중지된 작업을 다시 시작할 수 있습니다. 인쇄 대기열이 일시 중지된 이유가 있을 수 있기 때문에 다시 시작할지 여부에 대한 사용자 결정을 묻는 메시지를 표시하여 메서드를 시작합니다. 대답이 "Y" <xref:System.Printing.PrintQueue.Resume%2A?displayProperty=nameWithType> 이면 메서드가 호출 됩니다.  
  
 다음으로 작업이 인쇄 대기열에서 독립적으로 일시 중지된 경우 사용자에게 작업 자체를 다시 시작할지를 결정하라는 메시지가 표시됩니다. (와 <xref:System.Printing.PrintQueue.IsPaused%2A?displayProperty=nameWithType> <xref:System.Printing.PrintSystemJobInfo.IsPaused%2A?displayProperty=nameWithType>비교) 대답이 "Y" <xref:System.Printing.PrintSystemJobInfo.Resume%2A?displayProperty=nameWithType> 이면이 호출 되 고, 그렇지 않으면 <xref:System.Printing.PrintSystemJobInfo.Cancel%2A> 가 호출 됩니다.  
  
 [!code-cpp[DiagnoseProblematicPrintJob#HandlePausedJob](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#handlepausedjob)]
 [!code-csharp[DiagnoseProblematicPrintJob#HandlePausedJob](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#handlepausedjob)]
 [!code-vb[DiagnoseProblematicPrintJob#HandlePausedJob](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#handlepausedjob)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Printing.PrintJobStatus>
- <xref:System.Printing.PrintSystemJobInfo>
- <xref:System.FlagsAttribute>
- <xref:System.Printing.PrintQueue>
- [& 연산자 (C# 참조)](../../../csharp/language-reference/operators/bitwise-and-shift-operators.md#logical-and-operator-)
- [WPF의 문서](documents-in-wpf.md)
- [인쇄 개요](printing-overview.md)
