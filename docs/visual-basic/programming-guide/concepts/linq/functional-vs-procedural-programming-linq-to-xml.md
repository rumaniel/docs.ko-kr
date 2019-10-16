---
title: 함수형 프로그래밍과 절차적 프로그래밍 비교 (LINQ to XML) (Visual Basic)
ms.date: 07/20/2015
ms.assetid: ea1015a5-d4c8-4d79-8e1e-ba17a40a4f39
ms.openlocfilehash: f7e57ab2db5fa20a3a8414058573ca96e30e80d7
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64618264"
---
# <a name="functional-vs-procedural-programming-linq-to-xml-visual-basic"></a>함수형 프로그래밍과 절차적 프로그래밍 비교 (LINQ to XML) (Visual Basic)
다양한 유형의 XML 애플리케이션이 있습니다.  
  
- 일부 애플리케이션에서는 소스 XML 문서를 사용하여 소스 문서와 모양이 다른 새 XML 문서를 생성합니다.  
  
- 소스 XML 문서를 사용하여 HTML 또는 CSV 텍스트 파일과 같이 완전히 다른 형태의 결과 문서를 생성하는 애플리케이션도 있습니다.  
  
- 어떤 애플리케이션에서는 소스 XML 문서를 사용하여 데이터베이스에 레코드를 삽입합니다.  
  
- 데이터베이스 등의 다른 소스에서 데이터를 가져와서 해당 데이터로 XML 문서를 만드는 애플리케이션도 있습니다.  
  
 이러한 애플리케이션이 XML 애플리케이션의 모든 유형은 아니지만 XML 프로그래머가 구현해야 하는 기능 유형의 대표적인 집합을 나타냅니다.  
  
 이러한 유형의 애플리케이션에는 개발자가 선택할 수 있는 두 가지 대조적인 방법이 있습니다.  
  
- 선언적 방법을 사용하는 함수 생성  
  
- 절차적 코드를 사용하는 메모리 내 XML 트리 수정  
  
 LINQ to XML에서는 두 방법을 모두 지원합니다.  
  
 함수 방법을 사용하는 경우 소스 문서를 사용하여 원하는 모양의 완전히 새로운 결과 문서를 생성하는 변환을 작성합니다.  
  
 메모리 내 XML 트리를 수정하는 경우 메모리 내 XML 트리의 노드를 트래버스하고 탐색하여 필요에 따라 노드를 삽입, 삭제 및 수정하는 코드를 작성합니다.  
  
 두 방법 중 하나로 LINQ to XML을 사용할 수 있습니다. 두 방법은 동일한 클래스를 사용하며 경우에 따라 동일한 메서드를 사용합니다. 그러나 두 방법의 구조와 목표는 매우 다릅니다. 예를 들어 상황에 따라 성능이 높고 메모리를 적게 사용하는 방법이 달라집니다. 또한 유지 관리하기가 더 쉬운 코드를 작성하고 생성하는 것이 용이한 방법도 상황에 따라 다릅니다.  
  
 두 방법을 대조하는 내용을 보려면 [메모리 내 XML 트리 수정과 함수 생성 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/in-memory-xml-tree-modification-vs-functional-construction.md)합니다.  
  
 함수 변환 작성에 대 한 자습서를 참조 하세요 [변환 XML의 순수 함수 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/pure-functional-transformations-of-xml.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ to XML 프로그래밍 개요 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
