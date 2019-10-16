---
title: '방법: 클래스로 테이블 표현'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 84dda12b-88a2-4cd2-92b3-8db87b28d14c
ms.openlocfilehash: 1169def4e0180b1d14103d4a968ff3ed56f63d0c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781754"
---
# <a name="how-to-represent-tables-as-classes"></a>방법: 클래스로 테이블 표현
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 특성을사용하여클래스를데이터베이스테이블과연결된<xref:System.Data.Linq.Mapping.TableAttribute> 엔터티 클래스로 지정 합니다.  
  
### <a name="to-map-a-class-to-a-database-table"></a>데이터베이스 테이블에 클래스를 매핑하려면  
  
- <xref:System.Data.Linq.Mapping.TableAttribute> 특성을 클래스 선언에 추가합니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 `Customer` 클래스를 `Customers` 데이터베이스 테이블과 연결된 엔터티 클래스로 설정합니다.  
  
 [!code-csharp[DLinqCustomize#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCustomize/cs/Program.cs#1)]
 [!code-vb[DLinqCustomize#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCustomize/vb/Module1.vb#1)]  
  
 이름을 유추할 수 있는 경우에는 <xref:System.Data.Linq.Mapping.TableAttribute.Name%2A> 속성을 지정할 필요가 없습니다. 이름을 지정하지 않으면 이름은 속성 또는 필드의 이름과 동일한 것으로 간주됩니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ to SQL 개체 모델](the-linq-to-sql-object-model.md)
- [방법: 코드 편집기를 사용 하 여 엔터티 클래스 사용자 지정](how-to-customize-entity-classes-by-using-the-code-editor.md)
