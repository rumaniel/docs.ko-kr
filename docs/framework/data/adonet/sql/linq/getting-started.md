---
title: 시작하기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: db8a557a-fef8-4f4f-bb91-8cff7250ee25
ms.openlocfilehash: bd82b7e83149aaa53cf1b240cb79f8747bccba47
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793920"
---
# <a name="getting-started"></a>시작하기
을 사용 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]하 여 메모리 내 컬렉션 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 에 액세스 하는 것 처럼 기술을 사용 하 여 SQL 데이터베이스에 액세스할 수 있습니다.  
  
 예를 들어 다음 코드에서 `nw` 개체는 `Northwind` 데이터베이스를 나타내기 위해 만든 것으로 `Customers` 테이블을 대상으로 열은 `Customers`에서 `London`가 필터링되고 `CompanyName`에 대한 문자열은 검색용으로 선택됩니다.  
  
 루프가 실행되면 `CompanyName` 값의 컬렉션이 검색됩니다.  
  
 [!code-csharp[DLinqGettingStarted#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#1)]
 [!code-vb[DLinqGettingStarted#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#1)]  
  
## <a name="next-steps"></a>다음 단계  
 삽입 및 업데이트를 비롯 한 몇 가지 추가 예는 [LINQ to SQL에서 수행할 수 있는 작업](what-you-can-do-with-linq-to-sql.md)을 참조 하세요.  
  
 그런 다음 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]을 사용하는 실제 경험을 가지는 연습과 자습서를 시도해 보세요. [연습 별 학습](learning-by-walkthroughs.md)을 참조 하세요.  
  
 마지막으로 [LINQ to SQL 사용에 대 한 일반적인 단계](typical-steps-for-using-linq-to-sql.md)를 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 참조 하 여 고유한 프로젝트를 시작 하는 방법을 알아봅니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ to SQL](index.md)
- [LINQ 소개 (C#)](../../../../../csharp/programming-guide/concepts/linq/index.md)
- [LINQ 소개(Visual Basic)](../../../../../visual-basic/programming-guide/concepts/linq/introduction-to-linq.md)
- [LINQ to SQL 개체 모델](the-linq-to-sql-object-model.md)
