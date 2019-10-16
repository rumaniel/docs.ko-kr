---
title: LINQ to Objects(Visual Basic)
ms.date: 07/20/2015
ms.assetid: dd4c30bc-1c9b-4781-a482-b5eada38deb2
ms.openlocfilehash: c1e2e8fbaaf984fec69322a459fc7c55890965ad
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61791991"
---
# <a name="linq-to-objects-visual-basic"></a>LINQ to Objects(Visual Basic)
“LINQ to Objects”라는 용어는 중간 LINQ 공급자 또는 [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md), [LINQ to XML](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md) 등의 API를 사용하지 않고 모든 <xref:System.Collections.IEnumerable> 또는 <xref:System.Collections.Generic.IEnumerable%601> 컬렉션에 대해 LINQ 쿼리를 직접 사용하는 것입니다. LINQ를 사용하면 <xref:System.Collections.Generic.List%601>, <xref:System.Array>, <xref:System.Collections.Generic.Dictionary%602> 등의 모든 열거 가능 컬렉션을 쿼리할 수 있습니다. 컬렉션은 사용자가 정의할 수도 있고 .NET Framework API에서 반환할 수도 있습니다.  
  
 기본적으로 LINQ to Objects는 새로운 컬렉션 방식을 나타냅니다. 이전에는 컬렉션에서 데이터를 검색하는 방법을 지정하는 복잡한 `For Each` 루프를 작성해야 했습니다. 그러나 LINQ 방식에서는 검색할 항목을 설명하는 선언적 코드를 작성합니다.  
  
 또한 LINQ 쿼리는 기존의 `For Each` 루프에 비해 세 가지 주요 이점을 제공합니다.  
  
1. 보다 간결하며 쉽게 읽을 수 있습니다(특히 여러 조건을 필터링하는 경우).  
  
2. 최소한의 애플리케이션 코드로도 강력한 필터링, 순서 지정 및 그룹화 기능을 제공합니다.  
  
3. 거의 또는 전혀 수정하지 않고도 다른 데이터 소스에 이식할 수 있습니다.  
  
 일반적으로는 데이터에 대해 수행하려는 작업이 복잡할수록 기존의 반복 기술 대신 LINQ를 사용하면 더 큰 이점을 얻을 수 있습니다.  
  
 이 섹션에서는 몇 가지 예제를 통해 LINQ 방식에 대해 설명합니다. 여기서 설명하는 방식 외에도 다양한 방식을 사용할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [LINQ 및 문자열 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)  
 LINQ를 사용하여 문자열 및 문자열 컬렉션을 쿼리하고 변환하는 방법을 설명합니다. 또한 이러한 원칙을 설명하는 항목의 링크도 제공합니다.  
  
 [LINQ 및 리플렉션 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-reflection.md)  
 LINQ에서 리플렉션을 사용하는 방식을 보여 주는 샘플 링크를 제공합니다.  
  
 [LINQ 및 파일 디렉터리(Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-file-directories.md)  
 LINQ를 사용하여 파일 시스템을 조작하는 방법을 설명합니다. 또한 이러한 개념을 설명하는 항목의 링크도 제공합니다.  
  
 [방법: LINQ (Visual Basic)를 사용 하 여 ArrayList 쿼리](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md)  
 C#에서 ArrayList를 쿼리하는 방법을 보여 줍니다.  
  
 [방법: LINQ 쿼리 (Visual Basic)에 대 한 사용자 지정 메서드 추가](../../../../visual-basic/programming-guide/concepts/linq/how-to-add-custom-methods-for-linq-queries.md)  
 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스에 확장 메서드를 추가하여 LINQ 쿼리에 대해 사용할 수 있는 메서드 집합 확장 방법을 설명합니다.  
  
 [LINQ(Language-Integrated Query)(Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/index.md)  
 LINQ 관련 설명과 쿼리를 수행하는 코드 예제를 제공하는 항목의 링크가 나와 있습니다.
