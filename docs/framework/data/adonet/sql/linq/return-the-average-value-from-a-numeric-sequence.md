---
title: 숫자 시퀀스에서 평균 값 반환
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ee3b8673-a2e7-4b2d-9b5c-4972ff9e665d
ms.openlocfilehash: 8d6f5f76787c1110e91b245a3dd2425450b4db7e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781397"
---
# <a name="return-the-average-value-from-a-numeric-sequence"></a>숫자 시퀀스에서 평균 값 반환
<xref:System.Linq.Enumerable.Average%2A> 연산자는 숫자 값 시퀀스의 평균을 계산합니다.  
  
> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 정수 값의 `Average`를 변환하면 두 자리가 아닌 정수로 계산됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Freight` 테이블에서 `Orders` 값의 평균을 반환합니다.  
  
 샘플 Northwind 데이터베이스의 결과는 `78.2442`입니다.  
  
 [!code-csharp[DLinqQueryExamples#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#1)]
 [!code-vb[DLinqQueryExamples#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#1)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Products` 테이블에 있는 모든 `Products` 단가의 평균을 반환합니다.  
  
 샘플 Northwind 데이터베이스의 결과는 `28.8663`입니다.  
  
 [!code-csharp[DLinqQueryExamples#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#2)]
 [!code-vb[DLinqQueryExamples#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#2)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Average` 연산자를 사용하여 제품의 단가가 제품 범주가 속한 단가의 평균보다 비싼 `Products`를 찾습니다. 그룹으로 결과가 표시됩니다.  
  
 이 예제는 반환 형식이 익명이기에 C#에서는 `var` 키워드를 사용해야 합니다.  
  
 [!code-csharp[DLinqQueryExamples#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#3)]
 [!code-vb[DLinqQueryExamples#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#3)]  
  
 Northwind 샘플 데이터베이스에 대한 이 쿼리를 실행할 경우 결과는 다음과 비슷합니다.  
  
 `1`  
  
 `Côte de Blaye`  
  
 `Ipoh Coffee`  
  
 `2`  
  
 `Grandma's Boysenberry Spread`  
  
 `Northwoods Cranberry Sauce`  
  
 `Sirop d'érable`  
  
 `Vegie-spread`  
  
 `3`  
  
 `Sir Rodney's Marmalade`  
  
 `Gumbär Gummibärchen`  
  
 `Schoggi Schokolade`  
  
 `Tarte au sucre`  
  
 `4`  
  
 `Queso Manchego La Pastora`  
  
 `Mascarpone Fabioli`  
  
 `Raclette Courdavault`  
  
 `Camembert Pierrot`  
  
 `Gudbrandsdalsost`  
  
 `Mozzarella di Giovanni`  
  
 `5`  
  
 `Gustaf's Knäckebröd`  
  
 `Gnocchi di nonna Alice`  
  
 `Wimmers gute Semmelknödel`  
  
 `6`  
  
 `Mishi Kobe Niku`  
  
 `Thüringer Rostbratwurst`  
  
 `7`  
  
 `Rössle Sauerkraut`  
  
 `Manjimup Dried Apples`  
  
 `8`  
  
 `Ikura`  
  
 `Carnarvon Tigers`  
  
 `Nord-Ost Matjeshering`  
  
 `Gravad lax`  
  
## <a name="see-also"></a>참고자료

- [집계 쿼리](aggregate-queries.md)
