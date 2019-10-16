---
title: '방법: 작업에서 값 반환'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to return a value
ms.assetid: c4bc0f44-eba2-4e96-9e03-1cc787461e61
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: df928ec6494da6da368b3cef1f1d25a84a692aa2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54741784"
---
# <a name="how-to-return-a-value-from-a-task"></a>방법: 작업에서 값 반환
다음 예제에서는 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> 형식을 사용하여 <xref:System.Threading.Tasks.Task%601.Result%2A> 속성의 값을 반환하는 방법을 보여 줍니다. 이 예제를 실행하려면 C:\Users\Public\Pictures\Sample Pictures\ 디렉터리가 있고 파일을 포함해야 합니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[TPL#10](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/returnavalue10.cs#10)]
 [!code-vb[TPL#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/10_returnavalue.vb#10)]  
  
 <xref:System.Threading.Tasks.Task%601.Result%2A> 속성은 작업이 완료될 때까지 호출 스레드를 차단합니다.  
  
 하나의 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> 결과를 연속 작업에 전달하는 방법을 보려면 [연속 작업을 사용하여 작업 연결](../../../docs/standard/parallel-programming/chaining-tasks-by-using-continuation-tasks.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [작업 기반 비동기 프로그래밍](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)
- [PLINQ 및 TPL의 람다 식](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)
