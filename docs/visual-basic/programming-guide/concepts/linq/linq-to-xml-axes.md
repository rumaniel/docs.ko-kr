---
title: LINQ to XML 축 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: ecd3bd00-28e5-4517-a59f-53bff39fd478
ms.openlocfilehash: 4a04c15357b5630de06dc0743523e5a98c91745e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61780980"
---
# <a name="linq-to-xml-axes-visual-basic"></a>LINQ to XML 축 (Visual Basic)
XML 트리를 만들거나 XML 문서를 XML 트리에 로드한 후 XML 트리를 쿼리하여 요소와 특성을 찾고 해당 값을 검색할 수 있습니다.  
  
 쿼리를 작성하려면 먼저 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 축에 대해 이해해야 합니다. 축 메서드는 다음 두 가지 종류가 있습니다. 첫째, 단일 <xref:System.Xml.Linq.XElement> 개체, <xref:System.Xml.Linq.XDocument> 개체 또는 <xref:System.Xml.Linq.XNode> 개체에 대해 호출하는 메서드가 있습니다. 이러한 메서드는 단일 개체에 대해 작동하고 <xref:System.Xml.Linq.XElement>, <xref:System.Xml.Linq.XAttribute> 또는 <xref:System.Xml.Linq.XNode> 개체의 컬렉션을 반환합니다. 둘째, 컬렉션에 대해 작동하고 컬렉션을 반환하는 확장 메서드가 있습니다. 확장 메서드는 소스 컬렉션을 열거하고 컬렉션의 각 항목에 대해 적절한 축 메서드를 호출한 다음 결과를 연결합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|-----------|-----------------|  
|[LINQ to XML 축 개요 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes-overview.md)|축을 정의하고 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 쿼리와 관련하여 축을 사용하는 방법에 대해 설명합니다.|  
|[방법: 요소 (LINQ to XML)의 컬렉션 검색 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-collection-of-elements-linq-to-xml.md)|<xref:System.Xml.Linq.XContainer.Elements%2A> 메서드에 대해 소개합니다. 이 메서드는 요소의 자식 요소 컬렉션을 검색합니다.|  
|[방법: 요소 (LINQ to XML)의 값을 검색 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-element-linq-to-xml.md)|요소의 값을 가져오는 방법을 보여 줍니다.|  
|[방법: (LINQ to XML) 요소 이름 필터링 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-filter-on-element-names-linq-to-xml.md)|축을 사용할 때 요소 이름을 기준으로 필터링하는 방법을 보여 줍니다.|  
|[방법: 축 메서드 호출 (LINQ to XML) 연결 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-chain-axis-method-calls-linq-to-xml.md)|호출을 축 메서드에 연결하는 방법을 보여 줍니다.|  
|[방법: (LINQ to XML)는 단일 자식 요소 검색 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-single-child-element-linq-to-xml.md)|자식 요소의 태그 이름이 제공된 경우 요소의 단일 자식 요소를 검색하는 방법을 보여 줍니다.|  
|[방법: (LINQ to XML) 특성 컬렉션 검색 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-collection-of-attributes-linq-to-xml.md)|<xref:System.Xml.Linq.XElement.Attributes%2A> 메서드에 대해 소개합니다. 이 메서드는 요소의 특성을 검색합니다.|  
|[방법: (LINQ to XML)는 단일 특성 검색 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-single-attribute-linq-to-xml.md)|특성 이름이 제공된 경우 요소의 단일 특성을 검색하는 방법을 보여 줍니다.|  
|[방법: (LINQ to XML) 특성 값 검색 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-attribute-linq-to-xml.md)|특성의 값을 가져오는 방법을 보여 줍니다.|  
|[방법: (Visual Basic) 요소의 단순 값 검색](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-shallow-value-of-an-element.md)|요소의 부분 값을 검색하는 방법을 보여 줍니다.|  
|[Visual Basic (LINQ to XML)의 언어 통합 축](../../../../visual-basic/programming-guide/concepts/linq/language-integrated-axes.md)|통합 Visual Basic 축을 요약 되어 있습니다.|  
  
## <a name="see-also"></a>참고자료

- [프로그래밍 가이드 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/programming-guide-linq-to-xml.md)
