---
title: '방법: 백그라운드 작업을 사용하는 양식 구현'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- threading [Windows Forms], forms
- BackgroundWorker component
- background tasks
- forms [Windows Forms], multithreading
- components [Windows Forms], asynchronous
- forms [Windows Forms], background operations
- background threads
- threading [Windows Forms], background operations
- background operations
ms.assetid: 9f483f93-1613-4be1-a021-b4934e9c78f3
ms.openlocfilehash: e06b18558f6b3fa3cef47613bbaef16fb7c740f0
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046199"
---
# <a name="how-to-implement-a-form-that-uses-a-background-operation"></a>방법: 백그라운드 작업을 사용하는 양식 구현
다음 예제 프로그램은 피보나치 숫자를 계산하는 폼을 만듭니다. 계산은 사용자 인터페이스 스레드와 별개인 스레드에서 실행되므로 계산이 진행될 때 사용자 인터페이스가 지연 없이 계속 실행됩니다.  
  
 Visual Studio에서는 이 작업이 광범위하게 지원됩니다.  
  
 [또한 연습: 백그라운드 작업](walkthrough-implementing-a-form-that-uses-a-background-operation.md)을 사용 하는 폼 구현  
  
## <a name="example"></a>예제  
 [!code-cpp[System.ComponentModel.BackgroundWorker#1](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#1)]
 [!code-csharp[System.ComponentModel.BackgroundWorker#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#1)]
 [!code-vb[System.ComponentModel.BackgroundWorker#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System, System.Drawing 및 System.Windows.Forms 어셈블리에 대한 참조  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
  
> [!CAUTION]
> 모든 종류의 다중 스레딩을 사용할 때는 매우 심각하고 복잡한 버그에 잠재적으로 노출됩니다. 다중 스레딩을 사용하는 솔루션을 구현하기 전에 [관리되는 스레딩을 구현하는 최선의 방법](../../../standard/threading/managed-threading-best-practices.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ComponentModel.BackgroundWorker>
- <xref:System.ComponentModel.DoWorkEventArgs>
- [이벤트 기반 비동기 패턴 개요](../../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)
- [관리되는 스레딩을 구현하는 최선의 방법](../../../standard/threading/managed-threading-best-practices.md)
