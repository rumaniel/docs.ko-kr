---
title: 프로젝션 작성
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 745742df-0eda-479b-83f8-29bd8a80db96
ms.openlocfilehash: 0dfd5d951750de2ab918c51dd9f4f2deeb8a6318
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793823"
---
# <a name="formulate-projections"></a>프로젝션 작성
다음 예에서는 Visual Basic의 문과 `select` `Select` 문을 다른 C# 기능과 결합 하 여 쿼리 프로젝션을 구성할 수 있는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Visual Basic ( `Select` `select` 의 C#절)에서 절을 사용 하 여에 대 한 `Customers`연락처 이름의 시퀀스를 반환 합니다.  
  
 [!code-csharp[DLinqQueryExamples#57](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#57)]
 [!code-vb[DLinqQueryExamples#57](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#57)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 Visual Basic ( `Select` `select` 의 C#절) 및 *익명 형식* 에서 절을 사용 하 여에 대 한 `Customers`연락처 이름 및 전화 번호의 시퀀스를 반환 합니다.  
  
 [!code-csharp[DLinqQueryExamples#58](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#58)]
 [!code-vb[DLinqQueryExamples#58](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#58)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 Visual Basic ( `Select` `select` 의 C#절) 및 *익명 형식* 에서 절을 사용 하 여 직원에 대 한 이름 및 전화 번호의 시퀀스를 반환 합니다. 결과 시퀀스에서 `FirstName`과 `LastName` 필드는 단일 필드(`Name`)로 결합되고 `HomePhone` 필드는 `Phone`으로 이름이 변경됩니다.  
  
 [!code-csharp[DLinqQueryExamples#59](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#59)]
 [!code-vb[DLinqQueryExamples#59](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#59)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 Visual Basic ( `Select` `select` 의 C#절) 및 *무명 형식의* 절을 사용 하 여 모든 `ProductID`의 시퀀스와 이라는 `HalfPrice`계산 된 값을 반환 합니다. 이 값은 2로 나누어진 `UnitPrice`로 설정됩니다.  
  
 [!code-csharp[DLinqQueryExamples#60](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#60)]
 [!code-vb[DLinqQueryExamples#60](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#60)]  
  
## <a name="example"></a>예제  
 다음 `Select` 예에서는 Visual Basic 절 (`select` 의 C#절)과 *조건문* 을 사용 하 여 제품 이름 및 제품 가용성의 시퀀스를 반환 합니다.  
  
 [!code-csharp[DLinqQueryExamples#61](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#61)]
 [!code-vb[DLinqQueryExamples#61](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#61)]  
  
## <a name="example"></a>예제  
 다음 `Select` 예에서는 Visual Basic 절 (`select` 의 C#절)과 *알려진 형식* (Name)을 사용 하 여 직원 이름의 시퀀스를 반환 합니다.  
  
 [!code-csharp[DLinqQueryExamples#62](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#62)]
 [!code-vb[DLinqQueryExamples#62](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#62)]  
  
## <a name="example"></a>예제  
 다음 예에서는 및 `Select` 에서 `Where` 및을 사용`select` 하 여 런던에 있는 고객에 대 한 연락처 이름의 *필터링 된 시퀀스* 를 반환 Visual Basic `where` C#합니다.  
  
 [!code-csharp[DLinqQueryExamples#63](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#63)]
 [!code-vb[DLinqQueryExamples#63](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#63)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 Visual Basic ( `Select` `select` 의 C#절) 및 *익명 형식* 에서 절을 사용 하 여 고객에 대 한 데이터의 모양이 지정 된 *하위 집합* 을 반환 합니다.  
  
 [!code-csharp[DLinqQueryExamples#64](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#64)]
 [!code-vb[DLinqQueryExamples#64](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#64)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 중첩된 쿼리를 사용하여 다음 결과를 반환합니다.  
  
- 모든 주문의 시퀀스와 해당 `OrderID`입니다.  
  
- 할인이 있는 주문 항목에 대한 시퀀스입니다.  
  
- 운송 비용이 포함되지 않은 총 금액입니다.  
  
 [!code-csharp[DLinqQueryExamples#65](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#65)]
 [!code-vb[DLinqQueryExamples#65](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#65)]  
  
## <a name="see-also"></a>참고자료

- [쿼리 예제](query-examples.md)
