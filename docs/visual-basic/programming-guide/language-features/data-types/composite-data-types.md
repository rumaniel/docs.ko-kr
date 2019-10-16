---
title: 복합 데이터 형식(Visual Basic)
ms.date: 04/25/2017
helpviewer_keywords:
- classes [Visual Basic], composite data types
- composite types [Visual Basic]
- composite data types [Visual Basic]
- data types [Visual Basic], composite
- arrays [Visual Basic], composite data types
- structures [Visual Basic], composite data types
- classes [Visual Basic], composite types
- types [Visual Basic], composite
ms.assetid: 62970f2e-52c0-4369-8963-613820f1f434
ms.openlocfilehash: 65ee23c59958eefb94c7ab0c6bef4a7e992a121c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64601176"
---
# <a name="composite-data-types-visual-basic"></a>복합 데이터 형식(Visual Basic)
기본 데이터 형식 Visual Basic에서 제공 하는 것 외에도 수 조합 하 여 만들려는 다른 형식의 항목 *복합 데이터 형식* 클래스, 구조체 및 배열 등입니다. 기본 형식에서 다른 복합 형식의 복합 데이터 형식을 빌드할 수 있습니다. 예를 들어, 배열 멤버를 사용 하 여 한 구조 요소, 배열 또는 구조를 정의할 수 있습니다.  
  
## <a name="data-types"></a>데이터 형식  
 복합 형식 구성 요소 데이터 형식에서 다릅니다. 예를 들어 배열을 `Integer` 요소는 아닙니다는 `Integer` 데이터 형식입니다.  
  
 배열 데이터 형식은 요소 형식, 괄호 및 쉼표를 사용 하 여 필요에 따라 일반적으로 표시 됩니다. 예를 들어, 1 차원 배열이 `String` 요소가 표시 됩니다 `String()`, 및 2 차원 배열을 `Boolean` 요소가 표시 됩니다 `Boolean(,)`합니다.  
  
## <a name="structure-types"></a>구조체 형식  
 모든 구조를 포함 하는 단일 데이터 형식은 없습니다. 대신 구조체의 각 정의 두 구조체가 동일한 순서로 동일한 요소를 정의 하는 경우에 고유 데이터 형식을 나타냅니다. 그러나 같은 구조의 두 개 이상의 인스턴스를 만드는 경우 Visual Basic 데이터 형식이 동일한 것으로 간주 합니다.  
  
## <a name="tuples"></a>튜플

튜플은은 형식이 미리 정의 된 두 개 이상의 필드를 포함 하는 간단한 구조체입니다. 튜플은 Visual Basic 2017부터 지원 됩니다. 참조로 인수를 전달할 필요 없이 더 많은 가중치 클래스 또는 구조체에서 반환 되는 필드를 패키징 단일 메서드 호출에서 여러 값을 반환할 튜플 가장 흔히 사용 됩니다. 참조 된 [튜플](tuples.md) 튜플에 대 한 자세한 내용은 항목입니다.

## <a name="array-types"></a>배열 형식  
 모든 배열을 포함 하는 단일 데이터 형식은 없습니다. 데이터 형식의 배열의 특정 인스턴스를 다음에 의해 결정 됩니다.  
  
- 배열 이라는 사실  
  
- 배열의 차수 (차원 수)  
  
- 배열의 요소 형식  
  
 특히 지정 된 차원의 길이 인스턴스의 데이터 형식의 일부가 아닙니다. 다음은 이에 대한 예입니다.  
  
```  
Dim arrayA( ) As Byte = New Byte(12) {}  
Dim arrayB( ) As Byte = New Byte(100) {}  
Dim arrayC( ) As Short = New Short(100) {}  
Dim arrayD( , ) As Short  
Dim arrayE( , ) As Short = New Short(4, 10) {}  
```  
  
 앞의 예제에서 배열 변수 `arrayA` 하 고 `arrayB` 동일한 데이터 형식으로 간주 됩니다- `Byte()` -길이가 다른 초기화 되는 경우에 합니다. 변수 `arrayB` 고 `arrayC` 는 요소 형식이 다른 동일한 형식이 아닙니다. 변수 `arrayC` 및 `arrayD` 는 차수가 다른 동일한 형식이 아닙니다. 변수 `arrayD` 하 고 `arrayE` 형식이 같은- `Short(,)` -같기 때문에 해당 순위 및 요소 형식에도 `arrayD` 아직 초기화 되지 않았습니다.  
  
 배열에 대 한 자세한 내용은 참조 하세요. [배열](../../../../visual-basic/programming-guide/language-features/arrays/index.md)합니다.  
  
## <a name="class-types"></a>클래스 형식  
 모든 클래스를 포함 하는 단일 데이터 형식은 없습니다. 하나의 클래스에서는 다른 클래스에서 상속할 수 있지만 각각 별도 데이터 형식입니다. 동일한 클래스의 여러 인스턴스는 동일한 데이터 형식입니다. 다른 하나의 클래스 인스턴스 변수를 할당 하는 경우 뿐 아니라 동일한 데이터 형식이 있는지, 메모리에서 동일한 클래스 인스턴스를 가리키도록 합니다.  
  
 클래스에 대 한 자세한 내용은 참조 하세요. [개체 및 클래스](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
- [기본 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)
- [Visual Basic의 제네릭 형식](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)
- [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
- [Visual Basic의 형식 변환](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
- [구조체](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [데이터 형식 문제 해결](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [방법: 변수에 두 개 이상의 값 사용](../../../../visual-basic/programming-guide/language-features/data-types/how-to-hold-more-than-one-value-in-a-variable.md)
