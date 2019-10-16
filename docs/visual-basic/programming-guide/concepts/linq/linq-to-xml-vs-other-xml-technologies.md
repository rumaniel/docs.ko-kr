---
title: LINQ to XML과 비교 다른 XML Technologies2
ms.date: 07/20/2015
ms.assetid: 72ce3a82-ffc6-488c-98e7-b9b40f3591ec
ms.openlocfilehash: 80d3d034454d4de74e8aafd41679b82d111e6f3e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62021208"
---
# <a name="linq-to-xml-vs-other-xml-technologies"></a>LINQ to XML과 비교 기타 XML 기술 비교
이 항목에서는 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)], <xref:System.Xml.XmlReader>, XSLT, MSXML 및 XmlLite와 같은 XML 기술을 비교합니다. 이 정보는 사용할 기술을 결정할 때 유용할 수 있습니다.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]과 DOM(문서 개체 모델)의 비교는 [LINQ to XML과 DOM (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-vs-dom.md)합니다.  
  
## <a name="linq-to-xml-vs-xmlreader"></a>LINQ to XML과 비교 XmlReader  
 <xref:System.Xml.XmlReader>는 캐시하지 않으며 정방향으로만 작동하는 빠른 파서입니다.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]은 <xref:System.Xml.XmlReader>를 기반으로 구현되었으며 두 기술은 밀접하게 통합되어 있습니다. 그러나 <xref:System.Xml.XmlReader>를 단독으로 사용할 수도 있습니다.  
  
 예를 들어 초당 수백 개의 XML 문서를 구문 분석할 웹 서비스를 빌드하는데 문서의 구조가 동일하여 XML의 구문을 분석하는 코드의 구현을 하나만 작성하면 되는 경우를 가정해 보겠습니다. 이 경우에는 <xref:System.Xml.XmlReader>를 단독으로 사용할 수 있습니다.  
  
 반대로 크기가 작은 다양한 XML 문서의 구문을 분석하는 시스템을 빌드하는데 각 문서의 구조가 서로 다르면 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서 제공하는 성능 향상 기능을 사용할 수 있습니다.  
  
## <a name="linq-to-xml-vs-xslt"></a>LINQ to XML과 비교 XSLT  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]과 XSLT는 모두 광범위한 XML 문서 변환 기능을 제공합니다. XSLT는 규칙 기반의 선언적 방법입니다. 고급 XSLT 프로그래머는 상태 비저장 방법을 강조하는 함수형 프로그래밍 스타일로 XSLT를 작성합니다. 이 경우 부작용 없이 구현되는 순수 함수를 사용하여 변환을 작성할 수 있습니다. 이 규칙 기반 방법 또는 함수 방법은 대부분의 개발자에게 익숙하지 않으며 배우는 데 많은 시간과 노력이 필요할 수 있습니다.  
  
 XSLT는 고성능 애플리케이션을 생성하는 생산성이 매우 높은 시스템일 수 있습니다. 예를 들어 규모가 큰 일부 웹 회사에서는 다양한 데이터 저장소에서 가져온 XML에서 HTML을 생성하는 방법으로 XSLT를 사용합니다. 관리되는 XSLT 엔진은 XSLT를 CLR 코드로 컴파일하며 일부 시나리오에서 네이티브 XSLT 엔진보다 성능이 훨씬 좋습니다.  
  
 그러나 XSLT에서는 개발자가 C# 및 Visual Basic 지식을 활용할 수 없으며 복잡하고 다른 프로그래밍 언어로 코드를 작성해야 합니다. C#(또는 Visual Basic) 및 XSLT와 같은 통합되지 않은 두 가지 개발 시스템을 사용하면 소프트웨어 시스템을 개발하고 유지 관리하기가 더 어렵습니다.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 쿼리 식을 완전히 익히고 나면 강력한 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 변환 기술을 쉽게 사용할 수 있게 됩니다. 기본적으로 다양한 소스에서 데이터를 가져와서 <xref:System.Xml.Linq.XElement> 개체를 동적으로 생성하고 전체 데이터를 새 XML 트리로 어셈블하는 함수 생성을 사용하여 XML 문서를 만듭니다. 변환을 통해 완전히 새로운 문서가 생성될 수 있습니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 비교적 쉽고 직관적으로 변환을 생성할 수 있으며 생성되는 코드도 쉽게 읽을 수 있습니다. 따라서 개발 및 유지 관리 비용이 줄어듭니다.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]은 XSLT를 대체하기 위한 것이 아닙니다. XSLT는 여전히 복잡하고 문서 중심적인 XML(특히 문서 구조가 제대로 정의되지 않은 경우) 변환에 사용할 수 있습니다.  
  
 XSLT는 W3C(World Wide Web 컨소시엄) 표준이라는 장점이 있습니다. 표준 기술만 사용해야 하는 요구 사항이 있는 경우 XSLT가 더 적합할 수 있습니다.  
  
 XSLT는 XML이므로 프로그래밍 방식으로 조작할 수 있습니다.  
  
## <a name="linq-to-xml-vs-msxml"></a>LINQ to XML과 비교 MSXML  
 MSXML은 Microsoft Windows에 포함된 XML을 처리할 수 있는 COM 기반 기술입니다. MSXML은 XPath 및 XSLT를 지원하는 DOM의 기본적인 구현을 제공하며 캐시하지 않는 이벤트 기반의 SAX2 파서도 포함하고 있습니다.  
  
 MSXML은 성능이 좋으며 대부분의 시나리오에서 기본적으로 안전합니다. AJAX 스타일의 애플리케이션에서 클라이언트측 XML 처리를 수행하기 위해 Internet Explorer에서 MSXML에 액세스할 수 있습니다. C++, JavaScript 및 Visual Basic 6.0을 비롯한 COM을 지원하는 모든 프로그래밍 언어에서 MSXML을 사용할 수 있습니다.  
  
 CLR(공용 언어 런타임) 기반의 관리 코드에서는 MSXML을 사용하지 않는 것이 좋습니다.  
  
## <a name="linq-to-xml-vs-xmllite"></a>LINQ to XML과 비교 XmlLite  
 XmlLite는 캐시하지 않으며 정방향으로만 작동하는 가져오기 파서입니다. 개발자는 주로 C++와 함께 XmlLite를 사용합니다. 관리 코드와 함께 XmlLite를 사용하는 것은 권장되지 않습니다.  
  
 XmlLite의 주요 이점은 대부분의 시나리오에서 안전하며 간단하고 빠른 XML 파서라는 점입니다. XmlLite에서 위협에 노출되는 영역은 매우 작습니다. 신뢰할 수 없는 문서의 구문을 분석해야 하고 서비스 거부나 데이터 노출과 같은 공격으로부터 보호하려면 XmlLite를 선택하는 것이 좋습니다.  
  
 XmlLite는 [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)]와 통합되지 않았으며 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]에 핵심적인 프로그래머 생산성 향상 기능을 제공하지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [시작(LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/getting-started-linq-to-xml.md)
