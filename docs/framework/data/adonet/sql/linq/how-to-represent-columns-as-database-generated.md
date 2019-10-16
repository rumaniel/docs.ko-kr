---
title: '방법: 열을 데이터베이스에서 생성된 열로 표현'
ms.date: 03/30/2017
ms.assetid: 6524b8a6-e5d2-4a3b-8e08-beafc4a84fd2
ms.openlocfilehash: bb9510986581ad6d3bcd0711aed681ef3a7c4e45
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781787"
---
# <a name="how-to-represent-columns-as-database-generated"></a>방법: 열을 데이터베이스에서 생성된 열로 표현
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 특성의속성을사용하여데이터베이스에서생성된열을나타내는필드또는<xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A>속성을 지정합니다<xref:System.Data.Linq.Mapping.ColumnAttribute> .  
  
 코드 예는 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A>를 참조하세요.  
  
### <a name="to-designate-a-field-or-property-as-representing-a-database-generated-column"></a>데이터베이스에서 생성된 열을 나타내도록 필드 또는 속성을 지정하려면  
  
1. <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> 특성에 <xref:System.Data.Linq.Mapping.ColumnAttribute> 속성을 추가합니다.  
  
2. 속성 값을 `true`로 설정합니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ to SQL 개체 모델](the-linq-to-sql-object-model.md)
- [방법: 코드 편집기를 사용 하 여 엔터티 클래스 사용자 지정](how-to-customize-entity-classes-by-using-the-code-editor.md)
