---
title: 상수 식
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 9d98a7be-b110-4edb-8eba-bed10f250b6d
ms.openlocfilehash: b31cd881f1307ec734c026d3c873d7a650e19a20
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251127"
---
# <a name="constant-expressions"></a>상수 식
상수 식은 상수 값으로 구성됩니다. 상수 값은 클라이언트에서 변환하지 않고도 직접 상수 명령 트리 식으로 변환됩니다. 여기에는 상수 값을 결과로 제공하는 식도 포함됩니다. 따라서 상수를 사용하는 모든 식에 대해 데이터 소스 동작이 수행됩니다. 이로 인해 CLR 동작과 다른 동작이 나올 수 있습니다.  
  
 다음 예제에서는 서버에서 계산되는 상수 식을 보여 줍니다.  
  
 [!code-csharp[DP L2E Conceptual Examples#ConstantExpression](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#constantexpression)]
 [!code-vb[DP L2E Conceptual Examples#ConstantExpression](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#constantexpression)]  
  
 LINQ to Entities는 사용자 클래스를 상수로 사용 하도록 지원 하지 않습니다. 하지만 사용자 클래스에서 속성 참조는 상수로 간주되며 명령 트리 상수 식으로 변환되고 데이터 소스에서 실행됩니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ to Entities 쿼리의 식](expressions-in-linq-to-entities-queries.md)
