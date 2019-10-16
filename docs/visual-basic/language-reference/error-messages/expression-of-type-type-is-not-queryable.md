---
title: <type> 형식의 식은 쿼리할 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- bc36593
- vbc36593
helpviewer_keywords:
- BC36593
ms.assetid: 6f1f5860-bf97-4885-9ebb-bc87d028095c
ms.openlocfilehash: 121c0a95a3a6bb695d9c73347c733cba215a0de4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61801623"
---
# <a name="expression-of-type-type-is-not-queryable"></a>형식의 식은 \<유형 >를 쿼리할 수 없습니다
형식의 식은 \<유형 >를 쿼리할 수 없습니다. LINQ 공급자에 대 한 어셈블리 참조 및/또는 네임 스페이스 가져오기가 없습니다 있는지 확인 합니다.  
  
 쿼리 가능 형식에 정의 된 합니다 <xref:System.Linq>, <xref:System.Data.Linq>, 및 <xref:System.Xml.Linq> 네임 스페이스입니다. LINQ 쿼리를 수행 하려면 이러한 네임 스페이스를 하나 이상 가져와야 합니다.  
  
 <xref:System.Linq> 네임 스페이스 수 있도록 컬렉션 및 배열과 같은 쿼리 개체에 LINQ를 사용 하 여 합니다.  
  
 <xref:System.Data.Linq> 네임 스페이스를 사용 하면 LINQ를 사용 하 여 ADO.NET 데이터 집합 및 SQL Server 데이터베이스를 쿼리할 수 있습니다.  
  
 <xref:System.Xml.Linq> 네임 스페이스 수 있도록 쿼리 XML LINQ를 사용 하 여 및 Visual Basic의 XML 기능을 사용 합니다.  
  
 **오류 ID:** BC36593  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 추가 `Import` 문을 합니다 <xref:System.Linq>를 <xref:System.Data.Linq>, 또는 <xref:System.Xml.Linq> 코드 파일에 네임 스페이스입니다. 사용 하 여 프로젝트에 대 한 네임 스페이스를 가져올 수도 있습니다는 **참조가** 프로젝트 디자이너의 페이지 (**My Project**).  
  
2. 원본 쿼리는 쿼리 가능 형식으로 확인 된 형식을 확인 합니다. 구현 하는 형식 이므로 <xref:System.Collections.Generic.IEnumerable%601> 또는 <xref:System.Linq.IQueryable%601>합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Linq>
- <xref:System.Data.Linq>
- <xref:System.Xml.Linq>
- [Visual Basic의 LINQ 소개](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [LINQ](../../../visual-basic/programming-guide/language-features/linq/index.md)
- [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)
- [참조 및 Imports 문](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)
- [Imports 문(.NET 네임스페이스 및 형식)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [프로젝트 디자이너, 참조 페이지(Visual Basic)](/visualstudio/ide/reference/references-page-project-designer-visual-basic)
