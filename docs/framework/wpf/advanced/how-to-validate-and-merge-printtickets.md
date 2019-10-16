---
title: '방법: PrintTicket 유효성 검사 및 병합'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- merging PrintTickets [WPF]
- PrintTicket [WPF], merging
- validation of PrintTickets [WPF]
- PrintTicket [WPF], validation
ms.assetid: 4fe2d501-d0b0-4fef-86af-6ffe6c162532
ms.openlocfilehash: 9e5242c07179501e6b39840a36f8dd6364d65b84
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69918341"
---
# <a name="how-to-validate-and-merge-printtickets"></a>방법: PrintTicket 유효성 검사 및 병합
[!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] [인쇄 스키마](https://go.microsoft.com/fwlink/?LinkId=186397) 에는 유연 하 고 확장 <xref:System.Printing.PrintCapabilities> 가능한 <xref:System.Printing.PrintTicket> 및 요소가 포함 됩니다. 이전에는 인쇄 장치의 기능을 항목별로 요약, 후자는 특정 문서 시퀀스, 개별 문서 또는 개별 페이지와 관련 하 여 장치에서 이러한 기능을 사용 하는 방법을 지정 합니다.  
  
 인쇄를 지 원하는 응용 프로그램에 대 한 일반적인 작업 시퀀스는 다음과 같습니다.  
  
1. 프린터 기능을 결정 합니다.  
  
2. 이러한 기능 <xref:System.Printing.PrintTicket> 을 사용 하도록를 구성 합니다.  
  
3. 의 <xref:System.Printing.PrintTicket>유효성을 검사 합니다.  
  
 이 문서에서는이 작업을 수행 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 아래 간단한 예제에서는 프린터가 양면 인쇄 (양면 인쇄)를 지원 하는지 여부에 대해서만 관심이 있습니다. 주요 단계는 다음과 같습니다.  
  
1. 메서드<xref:System.Printing.PrintQueue.GetPrintCapabilities%2A> 를 <xref:System.Printing.PrintCapabilities> 사용 하 여 개체를 가져옵니다.  
  
2. 원하는 기능이 있는지 테스트 합니다. 아래 예제에서는 시트의 긴 쪽을 <xref:System.Printing.PrintCapabilities.DuplexingCapability%2A> 따라 "페이지 <xref:System.Printing.PrintCapabilities> 넘기기"를 사용 하 여 용지의 양쪽에서 인쇄 기능이 있는지 여부를 확인 하기 위해 개체의 속성을 테스트 합니다. 는 <xref:System.Printing.PrintCapabilities.DuplexingCapability%2A> 컬렉션 이므로의 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>메서드를 `Contains` 사용 합니다.  
  
    > [!NOTE]
    > 이 단계는 반드시 필요한 것은 아닙니다. 아래에서 사용 되는 <xref:System.Printing.PrintQueue.MergeAndValidatePrintTicket%2A> 메서드는의 각 요청을 프린터의 기능에 <xref:System.Printing.PrintTicket> 대해 확인 합니다. 프린터에서 요청 된 기능을 지원 하지 않는 경우 프린터 드라이버는 메서드에서 반환 된 <xref:System.Printing.PrintTicket> 의 대체 요청을 대체 합니다.  
  
3. 프린터에서 양면 인쇄를 지 원하는 경우 샘플 코드는 <xref:System.Printing.PrintTicket> 양면를 요청 하는을 만듭니다. 그러나 응용 프로그램은 <xref:System.Printing.PrintTicket> 요소에서 사용할 수 있는 모든 프린터 설정을 지정 하지 않습니다. 프로그래머와 프로그램 시간 모두에 불필요 합니다. 대신, 코드는 이중 요청만 설정 하 고 완전히 구성 되 고 <xref:System.Printing.PrintTicket> <xref:System.Printing.PrintTicket>유효성이 검사 된 기존와이를 병합 합니다 .이 경우에는 사용자의 기본값 <xref:System.Printing.PrintTicket>입니다.  
  
4. 따라서이 샘플에서는 메서드를 <xref:System.Printing.PrintQueue.MergeAndValidatePrintTicket%2A> 호출 하 여 사용자의 기본값 <xref:System.Printing.PrintTicket>을 <xref:System.Printing.PrintTicket> 사용 하 여 새를 최소한으로 병합 합니다. 그러면 새 <xref:System.Printing.ValidationResult> <xref:System.Printing.PrintTicket> 를 해당 속성 중 하나로 포함 하는이 반환 됩니다.  
  
5. 그런 다음이 샘플에서는 새 <xref:System.Printing.PrintTicket> 요청을 이중으로 요청 하는지 테스트 합니다. 이 경우 샘플은 사용자에 대 한 새로운 기본 인쇄 티켓을 만듭니다. 위의 2 단계를 중단 한 경우 프린터에서 긴 쪽의 이중 양면을 지원 하지 않으면 테스트 결과 `false`는이 됩니다. 위의 메모를 참조 하세요.  
  
6. 마지막으로 중요 한 단계는 <xref:System.Printing.PrintQueue.UserPrintTicket%2A> <xref:System.Printing.PrintQueue.Commit%2A> 메서드를 <xref:System.Printing.PrintQueue> 사용 하 여의 속성에 대 한 변경 내용을 커밋하는 것입니다.  
  
 [!code-csharp[PrintTicketManagment#UsingMergeAndValidate](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintTicketManagment/CSharp/printticket.cs#usingmergeandvalidate)]
 [!code-vb[PrintTicketManagment#UsingMergeAndValidate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintTicketManagment/visualbasic/printticket.vb#usingmergeandvalidate)]  
  
 이 예제를 빠르게 테스트할 수 있도록 그 나머지는 아래에 나와 있습니다. 프로젝트 및 네임 스페이스를 만든 다음이 문서의 코드 조각을 모두 네임 스페이스 블록에 붙여넣습니다.  
  
 [!code-csharp[PrintTicketManagment#UIForMergeAndValidatePTUtility](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintTicketManagment/CSharp/printticket.cs#uiformergeandvalidateptutility)]
 [!code-vb[PrintTicketManagment#UIForMergeAndValidatePTUtility](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintTicketManagment/visualbasic/printticket.vb#uiformergeandvalidateptutility)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Printing.PrintCapabilities>
- <xref:System.Printing.PrintTicket>
- <xref:System.Printing.PrintServer.GetPrintQueues%2A>
- <xref:System.Printing.PrintServer>
- <xref:System.Printing.EnumeratedPrintQueueTypes>
- <xref:System.Printing.PrintQueue>
- <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>
- [WPF의 문서](documents-in-wpf.md)
- [인쇄 개요](printing-overview.md)
- [인쇄 스키마](https://go.microsoft.com/fwlink/?LinkId=186397)
