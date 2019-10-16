---
title: '방법: 여러 개의 취소 요청 수신 대기'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cancellation tokens, joining
- LinkedTokenSource, how to
ms.assetid: 6f4f3804-2ed7-41b4-a97a-6e32b93f6e05
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2684f0fd43f84573933fc0a7107ce4f9035bc092
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69913313"
---
# <a name="how-to-listen-for-multiple-cancellation-requests"></a>방법: 여러 개의 취소 요청 수신 대기
이 예제에서는 두 개의 취소 토큰 중 하나가 작업을 요청할 경우 작업을 취소할 수 있도록 두 개의 취소 토큰을 동시에 수신 대기하는 방법을 보여줍니다.  
  
> [!NOTE]
> “내 코드만”이 사용하도록 설정된 경우 Visual Studio가 예외를 발생시키는 줄에서 중단하고 "예외가 사용자 코드에서 처리되지 않았다"는 오류 메시지를 표시합니다. 이 오류는 심각하지는 않습니다. F5 키를 눌러 계속하고 아래 예제에 설명된 예외 처리 동작을 확인할 수 있습니다. 첫 번째 오류 지점에서 Visual Studio가 실행을 중단하지 않도록 하려면 **도구, 옵션, 디버깅, 일반**을 차례로 선택하고 “내 코드만” 확인란의 선택을 취소하기만 하면 됩니다.  
  
## <a name="example"></a>예  
 다음 예제에서 <xref:System.Threading.CancellationTokenSource.CreateLinkedTokenSource%2A> 메서드는 두 개의 토큰을 하나의 토큰으로 결합하는 데 사용됩니다. 이렇게 하면 하나의 취소 토큰만 인수로 사용하는 메서드에 토큰을 전달할 수 있습니다. 이 예제에서는 메서드가 클래스 외부에서 전달되는 토큰과 클래스 내에서 생성되는 토큰을 모두 관찰해야 하는 일반적인 시나리오를 보여줍니다.  
  
 [!code-csharp[Cancellation#13](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex13.cs#13)]
 [!code-vb[Cancellation#13](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex13.vb#13)]  
  
 연결된 토큰이 <xref:System.OperationCanceledException>을 throw하면 예외에 전달되는 토큰은 선행 작업 토큰이 아닌 연결된 토큰입니다. 취소된 토큰을 확인하려면 선행 작업 토큰의 상태를 직접 확인합니다.  
  
 이 예제에서는 <xref:System.AggregateException>이 throw되면 안 되지만 여기에서는 예외를 catch합니다. 실제 시나리오에서는 작업 대리자에서 throw되는 <xref:System.OperationCanceledException> 이외의 다른 예외가 <xref:System.AggregateException>으로 래핑되기 때문입니다.  
  
## <a name="see-also"></a>참고 항목

- [관리되는 스레드의 취소](../../../docs/standard/threading/cancellation-in-managed-threads.md)
