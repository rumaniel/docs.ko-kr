---
title: 숫자 시퀀스에서 값의 합계 컴퓨팅
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 24e335b0-984e-4825-8721-0a91b533b7c3
ms.openlocfilehash: 3a404068c2d89610aa9b01b392bca40f82e17707
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70247921"
---
# <a name="compute-the-sum-of-values-in-a-numeric-sequence"></a>숫자 시퀀스에서 값의 합계 컴퓨팅
<xref:System.Linq.Enumerable.Sum%2A> 연산자를 사용하여 시퀀스의 숫자 값의 합을 컴퓨팅합니다.  
  
 `Sum`에서 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 연산자의 다음과 같은 특징에 유의하세요.  
  
- 표준 쿼리 연산자의 집계 연산자인 `Sum`은 빈 시퀀스 또는 null만 들어 있는 시퀀스를 0으로 계산합니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 SQL 구문이 바뀌지 않고 남아 있습니다. 따라서 `Sum`은 빈 시퀀스 또는 null만 들어 있는 시퀀스를 0이 아닌 null로 계산합니다.  
  
- 중간 결과에 대한 SQL 제한은 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]의 집계에 적용됩니다. 32비트 정수 수량은 64비트 결과를 사용하여 계산되지 않으며 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]의 `Sum` 변환에 대해 오버플로가 발생할 수 있습니다. 이러한 가능성은 표준 쿼리 연산자 구현이 메모리 내의 해당 시퀀스에 대해 오버플로를 발생시키지 않는 경우에도 존재합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Order` 테이블에서 모든 주문의 총 운송료를 검색합니다.  
  
 이 쿼리를 Northwind 샘플 데이터베이스에 대해 실행하면 `64942.6900`이 출력됩니다.  
  
 [!code-csharp[DLinqQueryExamples#12](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#12)]
 [!code-vb[DLinqQueryExamples#12](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#12)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 모든 주문에 대한 총 단위 수를 검색합니다.  
  
 이 쿼리를 Northwind 샘플 데이터베이스에 대해 실행하면 `780`이 출력됩니다.  
  
 `short`에는 short 형식에 대한 오버로드가 없으므로 `UnitsOnOrder` 형식(예: `Sum`)을 캐스팅해야 합니다.  
  
 [!code-csharp[DLinqQueryExamples#13](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#13)]
 [!code-vb[DLinqQueryExamples#13](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#13)]  
  
## <a name="see-also"></a>참고자료

- [집계 쿼리](aggregate-queries.md)
- [샘플 데이터베이스 다운로드](downloading-sample-databases.md)
