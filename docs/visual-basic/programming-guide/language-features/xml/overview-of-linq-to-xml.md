---
title: Visual Basic의 LINQ to XML 개요
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ to XML [Visual Basic], about LINQ to XML
- LINQ [Visual Basic], LINQ to XML
ms.assetid: 01c62a79-6d58-468e-84fb-039c05947701
ms.openlocfilehash: 5080efdf10a8e3b1f6815e836f9fffe968a8e4e0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939253"
---
# <a name="overview-of-linq-to-xml-in-visual-basic"></a>Visual Basic의 LINQ to XML 개요
Visual Basic는 xml 리터럴 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 및 xml 축 속성을 통해에 대 한 지원을 제공 합니다. 이렇게 하면 Visual Basic 코드에서 XML로 작업 하는 데 친숙 하 고 편리한 구문을 사용할 수 있습니다. *Xml 리터럴을* 사용 하면 코드에 xml을 직접 포함할 수 있습니다. *Xml 축 속성* 을 사용 하면 자식 노드, 하위 노드 및 xml 리터럴의 특성에 액세스할 수 있습니다. 자세한 내용은 [Xml 리터럴 개요](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-overview.md) 및 [Visual Basic의 xml 액세스](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)를 참조 하세요.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]는를 활용 [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)]하기 위해 특별히 설계 된 메모리 내 XML 프로그래밍 API입니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] Api를 직접 호출할 수 있지만 Visual Basic만 xml 리터럴을 선언 하 고 xml 축 속성에 직접 액세스할 수 있습니다.  
  
> [!NOTE]
> XML 리터럴 및 XML 축 속성은 ASP.NET 페이지의 선언적 코드에서 지원 되지 않습니다. Visual Basic XML 기능을 사용 하려면 코드를 ASP.NET 응용 프로그램의 코드를 사용 하는 페이지에 저장 합니다.  
  
 [재생 단추](./media/overview-of-linq-to-xml/play-video-icon-example.gif) 관련 비디오 데모를 보려면 [LINQ to XML를 시작 하는 방법](/aspnet/web-forms/videos/data-access/linq-videos-from-the-vb-team/how-do-i-get-started-with-linq-to-xml) 및 [LINQ to XML를 사용 하 여 Excel 스프레드시트를 만드는 방법](/aspnet/web-forms/videos/data-access/linq-videos-from-the-vb-team/how-do-i-create-excel-spreadsheets-using-linq-to-xml)을 참조 하십시오.   
  
## <a name="creating-xml"></a>XML 만들기  
 Visual Basic에서 XML 트리를 만드는 방법에는 두 가지가 있습니다. 코드에서 직접 XML 리터럴을 선언 하거나 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] api를 사용 하 여 트리를 만들 수 있습니다. 두 프로세스 모두 코드에서 XML 트리의 최종 구조를 반영할 수 있습니다. 예를 들어 다음 코드 예제에서는 XML 요소를 만듭니다.  
  
 [!code-vb[VbXmlSamples#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#5)]  
  
 자세한 내용은 [Visual Basic에서 XML 만들기](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)를 참조 하세요.  
  
## <a name="accessing-and-navigating-xml"></a>XML 액세스 및 탐색  
 Visual Basic XML 구조에 액세스 하 고 탐색 하기 위한 XML 축 속성을 제공 합니다. 이러한 속성을 사용 하면 XML 자식 요소 이름을 지정 하 여 XML 요소와 특성에 액세스할 수 있습니다. 또는 요소와 특성을 탐색 하 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 고 찾는 메서드를 명시적으로 호출할 수 있습니다. 예를 들어 다음 코드 예제에서는 xml 축 속성을 사용 하 여 XML 요소의 특성 및 자식 요소를 참조 합니다. 이 코드 예제에서는 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리를 사용 하 여 자식 요소를 검색 하 고 XML 요소로 출력 하 여 변환을 효과적으로 수행 합니다.  
  
 [!code-vb[VbXmlSamples#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples3.vb#8)]  
  
 자세한 내용은 [Visual Basic에서 XML 액세스](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)를 참조 하세요.  
  
## <a name="xml-namespaces"></a>XML 네임스페이스  
 Visual Basic를 사용 하면 `Imports` 문을 사용 하 여 전역 XML 네임 스페이스에 대 한 별칭을 지정할 수 있습니다. 다음 예에서는 `Imports` 문을 사용 하 여 XML 네임 스페이스를 가져오는 방법을 보여 줍니다.  
  
 [!code-vb[VbXMLSamples#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#1)]  
  
 Xml 축 속성에 액세스 하 고 xml 문서 및 요소에 대 한 XML 리터럴을 선언할 때 XML 네임 스페이스 별칭을 사용할 수 있습니다.  
  
 [GetXmlNamespace 연산자](../../../../visual-basic/language-reference/operators/getxmlnamespace-operator.md)를 사용 <xref:System.Xml.Linq.XNamespace> 하 여 특정 네임 스페이스 접두사에 대 한 개체를 검색할 수 있습니다.  
  
 자세한 내용은 [Imports 문 (XML 네임 스페이스)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)을 참조 하세요.  
  
### <a name="using-xml-namespaces-in-xml-literals"></a>XML 리터럴에서 XML 네임 스페이스 사용  
 다음 예제에서는 전역 네임 스페이스 <xref:System.Xml.Linq.XElement> `ns`를 사용 하는 개체를 만드는 방법을 보여 줍니다.  
  
 [!code-vb[VbXMLSamples#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#2)]  
  
 Visual Basic 컴파일러는 xml 네임 스페이스 별칭을 포함 하는 xml 리터럴을 `xmlns` 특성과 함께 xml 네임 스페이스를 사용 하는 xml 표기법을 사용 하는 동등한 코드로 변환 합니다. 이전 섹션 예제의 코드는 컴파일될 때 다음 예제와 같이 기본적으로 동일한 실행 코드를 생성 합니다.  
  
 [!code-vb[VbXMLSamples#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#3)]  
  
### <a name="using-xml-namespaces-in-xml-axis-properties"></a>XML 축 속성에 XML 네임 스페이스 사용  
 Xml 리터럴에 선언 된 xml 네임 스페이스는 XML 축 속성에서 사용할 수 없습니다. 그러나 전역 네임 스페이스는 XML 축 속성과 함께 사용할 수 있습니다. 콜론을 사용 하 여 로컬 요소 이름과 XML 네임 스페이스 접두사를 구분 합니다. 예를 들면 다음과 같습니다.  
  
 [!code-vb[VbXMLSamples#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#4)]  
  
## <a name="see-also"></a>참고자료

- [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)
- [Visual Basic에서 XML 만들기](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [Visual Basic에서 XML에 액세스](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)
- [Visual Basic에서 XML 조작](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)
