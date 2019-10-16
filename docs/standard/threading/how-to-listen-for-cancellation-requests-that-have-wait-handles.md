---
title: '방법: 대기 핸들이 있는 취소 요청 수신 대기'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cancellation, waiting with wait handles
ms.assetid: 6e2aa49b-fc84-4bcf-962b-17db98b7edcb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 67cf434737257a942e094fcb38ed18d597645d46
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69913340"
---
# <a name="how-to-listen-for-cancellation-requests-that-have-wait-handles"></a>방법: 대기 핸들이 있는 취소 요청 수신 대기
이벤트의 신호를 받을 때까지 대기하는 동안 메서드가 차단된 경우 취소 토큰의 값을 확인하고 적시에 응답할 수 없습니다. 첫 번째 예제는 기본적으로 통합 취소 프레임워크를 지원하지 않는 <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType>와 같은 이벤트에 대해 작업할 때 이 문제점을 해결하는 방법을 보여줍니다. 두 번째 예제는 통합 취소를 지원하는 <xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType>을 사용하는 보다 간소화된 접근 방식을 보여줍니다.  
  
> [!NOTE]
> “내 코드만”이 사용하도록 설정된 경우 Visual Studio가 예외를 발생시키는 줄에서 중단하고 "예외가 사용자 코드에서 처리되지 않았다"는 오류 메시지를 표시합니다. 이 오류는 심각하지는 않습니다. F5 키를 눌러 계속하고 아래 예제에 설명된 예외 처리 동작을 확인할 수 있습니다. 첫 번째 오류 지점에서 Visual Studio가 실행을 중단하지 않도록 하려면 **도구, 옵션, 디버깅, 일반**을 차례로 선택하고 “내 코드만” 확인란의 선택을 취소하기만 하면 됩니다.  
  
## <a name="example"></a>예  
 다음 예제는 <xref:System.Threading.ManualResetEvent>를 사용하여 통합 취소를 지원하지 않는 대기 핸들을 차단 해제하는 방법을 보여줍니다.  
  
 [!code-csharp[Cancellation#9](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex9.cs#9)]
 [!code-vb[Cancellation#9](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex9.vb#9)]  
  
## <a name="example"></a>예  
 다음 예제는 <xref:System.Threading.ManualResetEventSlim>를 사용하여 통합 취소를 지원하는 조정의 기본 형식을 차단 해제하는 방법을 보여줍니다. 동일한 접근 방식을 <xref:System.Threading.Semaphore> `Slim` 및 <xref:System.Threading.CountdownEvent>과 같은 다른 간단한 조정의 기본 형식과 함께 사용할 수 있습니다.  
  
 [!code-csharp[Cancellation#10](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex10.cs#10)]
 [!code-vb[Cancellation#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex10.vb#10)]  
  
## <a name="see-also"></a>참고 항목

- [관리되는 스레드의 취소](../../../docs/standard/threading/cancellation-in-managed-threads.md)
