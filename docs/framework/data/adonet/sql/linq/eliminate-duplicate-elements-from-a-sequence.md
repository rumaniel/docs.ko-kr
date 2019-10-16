---
title: 시퀀스에서 중복 요소 제거
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2b224a84-bad5-4843-adcc-14e784d280f5
ms.openlocfilehash: 9b8e19ac76869c33d01a59ee3aad104a7ddbb8f7
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782217"
---
# <a name="eliminate-duplicate-elements-from-a-sequence"></a>시퀀스에서 중복 요소 제거
<xref:System.Linq.Queryable.Distinct%2A> 연산자를 사용하여 시퀀스에서 중복 요소를 제거합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Linq.Queryable.Distinct%2A>를 사용하여 고객이 있는 고유한 도시의 시퀀스를 선택합니다.  
  
 [!code-csharp[DLinqQueryExamples#36](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#36)]
 [!code-vb[DLinqQueryExamples#36](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#36)]  
  
## <a name="see-also"></a>참고자료

- [쿼리 예제](query-examples.md)
