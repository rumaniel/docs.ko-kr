---
title: '방법: 이벤트 기반 비동기 패턴의 클라이언트 구현'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- components [.NET Framework], asynchronous
- AsyncOperation class
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 21a858c1-3c99-4904-86ee-0d17b49804fa
ms.openlocfilehash: 50aa36d2caf774638ad20323813f0de3703aab2f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950713"
---
# <a name="how-to-implement-a-client-of-the-event-based-asynchronous-pattern"></a>방법: 이벤트 기반 비동기 패턴의 클라이언트 구현
다음 코드 예제는 [이벤트 기반 비동기 패턴 개요](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)를 준수하는 구성 요소를 사용하는 방법을 보여줍니다. `PrimeNumberCalculator` 구성 요소를 사용하는 이 예제의 양식은 [방법: 이벤트 기반 비동기 패턴을 지 원하는 구성 요소 구현](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)을 참조하세요.  
  
 이 예제를 사용하는 프로젝트를 실행하면 그리드와 두 개의 단추가 있는 "소수 계산기" 양식이 표시됩니다. **새 작업 시작** 및 **취소**. **새 작업 시작** 단추를 연속으로 여러 번 클릭할 수 있습니다. 클릭할 때마다 비동기 작업이 무작위로 생성된 테스트 숫자가 소수인지 여부를 확인하기 위해 계산을 시작합니다. 양식은 진행률 및 증분 결과를 주기적으로 표시합니다. 각 작업에는 고유한 작업 ID가 할당됩니다. 계산의 결과는 **결과** 열에 표시됩니다. 테스트 숫자가 소수가 아닌 경우 **합성수**로 레이블이 지정되며 첫 번째 약수가 표시됩니다.  
  
 보류 중인 작업은 **취소** 단추로 취소할 수 있습니다. 여러 번 선택할 수 있습니다.  
  
> [!NOTE]
> 대부분의 숫자는 소수가 아닙니다. 몇 가지 작업을 완료한 후에도 소수를 찾지 못한 경우 단지 더 많은 작업을 시작하면 결국 몇 개의 소수를 찾을 수 있습니다.  
  
## <a name="example"></a>예  
 [!code-csharp[System.ComponentModel.AsyncOperationManager#10](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#10)]
 [!code-vb[System.ComponentModel.AsyncOperationManager#10](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#10)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.ComponentModel.AsyncOperation>
- <xref:System.ComponentModel.AsyncOperationManager>
- <xref:System.Windows.Forms.WindowsFormsSynchronizationContext>
