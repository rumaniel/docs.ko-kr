---
title: '방법: SpinWait을 사용하여 2단계 대기 작업 구현'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SpinWait, how to synchronize two-phase wait
ms.assetid: b2ac4e4a-051a-4f65-b4b9-f8e103aff195
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 52b9164546d2061a65c79fb167b14543b0dae5a9
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54576514"
---
# <a name="how-to-use-spinwait-to-implement-a-two-phase-wait-operation"></a>방법: SpinWait을 사용하여 2단계 대기 작업 구현
다음 예제는 <xref:System.Threading.SpinWait?displayProperty=nameWithType> 개체를 사용하여 2단계 대기 작업을 구현하는 방법을 보여줍니다. 첫 번째 단계에서 동기화 개체(`Latch`)는 잠금이 사용 가능해졌는지 여부를 확인하는 동안 몇 주기 동안 회전합니다. 두 번째 단계에서는 잠금이 사용 가능하게 되면 `Wait` 메서드에서 <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType>을 사용하여 대기를 수행하지 않고 반환합니다. 잠금이 사용 가능하지 않으면 `Wait`에서 대기를 수행합니다.  
  
## <a name="example"></a>예제  
 이 예제는 래치 동기화 기본 형식의 매우 기본적인 구현을 보여줍니다. 대기 시간이 매우 짧을 것으로 예상되는 경우 이 데이터 구조를 사용할 수 있습니다. 이 예제는 데모용으로만 제공됩니다. 프로그램에 래치 유형 기능이 필요한 경우 <xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType>을 사용해 보세요.  
  
 [!code-csharp[CDS_SpinWait#03](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinwait/cs/spinwait03.cs#03)]
 [!code-vb[CDS_SpinWait#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinwait/vb/spinwait2.vb#03)]  
  
 `SpinOnce`에 대한 다음 호출로 인해 <xref:System.Threading.SpinWait>에서 스레드의 시간 조각을 생성할 때까지만 래치는 <xref:System.Threading.SpinWait> 개체를 사용하여 적절히 회전합니다. 이 지점에서 래치는 <xref:System.Threading.ManualResetEvent>에서 <xref:System.Threading.WaitHandle.WaitOne%2A>을 호출하고 나머지 시간 제한 값을 전달하여 자체 컨텍스트 전환을 발생시킵니다.  
  
 로깅 출력은 <xref:System.Threading.ManualResetEvent>를 사용하지 않고 잠금을 획득하여 래치가 성능을 향상시킬 수 있었던 빈도를 표시합니다.  
  
## <a name="see-also"></a>참고 항목

- [스핀 대기](../../../docs/standard/threading/spinwait.md)
- [스레딩 개체 및 기능](../../../docs/standard/threading/threading-objects-and-features.md)
