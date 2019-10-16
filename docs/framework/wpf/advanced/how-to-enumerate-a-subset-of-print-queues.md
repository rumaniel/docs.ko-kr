---
title: '방법: 인쇄 큐의 하위 집합 열거'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- enumerating [WPF], subset of print queues
- print queues [WPF], enumerating subset of
ms.assetid: cc4a1b5b-d46f-4c5e-bc26-22c226e4bee0
ms.openlocfilehash: adcfff0196bd0430ec1ae563fbd5489062de11f3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776066"
---
# <a name="how-to-enumerate-a-subset-of-print-queues"></a>방법: 인쇄 큐의 하위 집합 열거
회사 전체 집합이 프린터를 관리 하는 정보 기술 (IT) 전문가 직면 하는 일반적인 상황 특정 특성을 가진 프린터 목록을 생성 하는 것입니다. 이 기능을 제공 합니다 <xref:System.Printing.PrintServer.GetPrintQueues%2A> 메서드를 <xref:System.Printing.PrintServer> 개체 및 <xref:System.Printing.EnumeratedPrintQueueTypes> 열거형입니다.  
  
## <a name="example"></a>예제  
 아래 예제에서 코드를 나열 하려고 하는 인쇄 대기열의 특성을 지정 하는 플래그의 배열을 만들어 시작 합니다. 이 예제에서는 우리가 찾고자 하는 인쇄 서버에 로컬로 설치 되어 있고 공유 되는 인쇄 대기열입니다. <xref:System.Printing.EnumeratedPrintQueueTypes> 열거형은 다른 많은 가능성을 제공 합니다.  
  
 만든 후에 <xref:System.Printing.LocalPrintServer> 개체에서 파생 된 클래스 <xref:System.Printing.PrintServer>합니다. 로컬 인쇄 서버에는 응용 프로그램이 실행 되는 컴퓨터입니다.  
  
 마지막으로 중요 한 단계에 전달 하는 것은 <xref:System.Printing.PrintServer.GetPrintQueues%2A> 메서드.  
  
 마지막으로 결과가 사용자에게 표시됩니다.  
  
 [!code-cpp[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](~/samples/snippets/cpp/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/CPP/Program.cpp#listsubsetofprintqueues)]
 [!code-csharp[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](~/samples/snippets/csharp/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/CSharp/Program.cs#listsubsetofprintqueues)]
 [!code-vb[EnumerateSubsetOfPrintQueues#ListSubsetOfPrintQueues](~/samples/snippets/visualbasic/VS_Snippets_Wpf/EnumerateSubsetOfPrintQueues/visualbasic/program.vb#listsubsetofprintqueues)]  
  
 함으로써이 예제를 확장할 수는 `foreach` 각 인쇄 큐를 통해 단계를 추가로 수행 하는 루프 차단 합니다. 예를 들어, 있습니다 수 숨기 루프 호출 함으로써 양면 인쇄를 지원 하지 않는 프린터 각 인쇄 대기열의 <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A> 메서드와 이루어지는의 존재에 대 한 반환된 값을 테스트 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Printing.PrintServer.GetPrintQueues%2A>
- <xref:System.Printing.PrintServer>
- <xref:System.Printing.LocalPrintServer>
- <xref:System.Printing.EnumeratedPrintQueueTypes>
- <xref:System.Printing.PrintQueue>
- <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>
- [WPF의 문서](documents-in-wpf.md)
- [인쇄 개요](printing-overview.md)
- [Microsoft XPS Document Writer](https://go.microsoft.com/fwlink/?LinkId=147319)
