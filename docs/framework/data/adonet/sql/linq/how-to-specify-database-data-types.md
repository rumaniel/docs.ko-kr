---
title: '방법: 데이터베이스 데이터 형식 지정'
ms.date: 03/30/2017
ms.assetid: 2228fdad-7e6a-4b1b-b4d1-79d0198b7c28
ms.openlocfilehash: 09ca8dc6fa440138523bcd2905335a04517dd806
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793263"
---
# <a name="how-to-specify-database-data-types"></a>방법: 데이터베이스 데이터 형식 지정
특성의 속성을 사용 하 여 t-sql 테이블 선언에서 열을 정의 하는 정확한 텍스트를 지정할 수 있습니다. <xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Mapping.ColumnAttribute>  
  
 <xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A>를 사용하여 데이터베이스 인스턴스를 만들려고 계획한 경우에만 <xref:System.Data.Linq.DataContext.CreateDatabase%2A> 속성을 지정해야 합니다.  
  
 코드 예는 <xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A>를 참조하세요.  
  
### <a name="to-specify-text-to-define-a-data-type-in-a-t-sql-table"></a>T-SQL 테이블에서 데이터 형식을 정의하기 위한 텍스트를 지정하려면  
  
1. <xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A> 특성에 <xref:System.Data.Linq.Mapping.ColumnAttribute> 속성을 추가합니다.  
  
2. <xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A> 속성 값을 T-SQL에서 사용되는 정확한 텍스트로 설정합니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ to SQL 개체 모델](the-linq-to-sql-object-model.md)
- [방법: 코드 편집기를 사용 하 여 엔터티 클래스 사용자 지정](how-to-customize-entity-classes-by-using-the-code-editor.md)
