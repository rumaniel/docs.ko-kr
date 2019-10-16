---
title: Visual Basic의 문자열 기본
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], Like operator
- strings [Visual Basic], Visual Basic
- strings [Visual Basic], regular expressions
ms.assetid: 5674418d-f00d-4f72-9f98-d15897793350
ms.openlocfilehash: f1f6b98d7db510373f2729fab2a6e0ad993ea086
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591389"
---
# <a name="string-basics-in-visual-basic"></a>Visual Basic의 문자열 기본
`String` 데이터 형식은 일련의 문자를 나타내며, 각각은 차례로 `Char` 데이터 형식의 인스턴스를 나타냅니다. 이 항목에서는 Visual Basic에서 문자열의 기본 개념을 소개 합니다.  
  
## <a name="string-variables"></a>문자열 변수  
 문자열의 인스턴스에 일련의 문자를 나타내는 리터럴 값을 할당할 수 있습니다. 예를 들어:  
  
 [!code-vb[VbVbalrStrings#63](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#63)]  
  
 또한 `String` 변수는 문자열로 계산되는 모든 식을 허용할 수 있습니다. 예제는 다음과 같습니다.  
  
 [!code-vb[VbVbalrStrings#64](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#64)]  
  
 `String` 변수에 할당되는 모든 리터럴은 큰따옴표("")로 묶어야 합니다. 즉, 문자열 내의 큰따옴표는 큰따옴표로 나타낼 수 없습니다. 예를 들어 다음 코드는 컴파일러 오류를 생성합니다.  
  
 [!code-vb[VbVbalrStrings#65](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#65)]  
  
 이 코드에서는 컴파일러가 두번째 큰따옴표 다음 문자열을 종료하고 문자열의 나머지 부분이 코드로 해석되기 때문에 오류가 생성됩니다. 이 문제를 해결 하려면 Visual Basic를 하나의 따옴표로 문자열에서 리터럴 문자열에 두 개의 따옴표를 해석 합니다. 다음 예제에서는 문자열에 큰따옴표를 포함하는 올바른 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrStrings#66](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#66)]  
  
 이전 예제에서 `Look`이라는 단어 앞에 오는 두 개의 큰따옴표가 문자열에서 하나의 큰따옴표가 됩니다. 줄의 끝에 있는 큰따옴표 세 개는 문자열의 큰따옴표 한 개와 문자열 종료 문자를 나타냅니다.  
  
 문자열 리터럴에 여러 줄이 포함될 수 있습니다.  
  
```vb  
Dim x = "hello  
world"  
```  
  
 결과 문자열에는 문자열 리터럴(vbcr, vbcrlf 등)에서 사용한 줄 바꿈 시퀀스가 포함됩니다.  이전 해결 방법은 더 이상 사용할 필요가 없습니다.  
  
```vb  
Dim x = <xml><![CDATA[Hello  
World]]></xml>.Value  
```  
  
## <a name="characters-in-strings"></a>문자열의 문자  
 문자열은 일련은 `Char` 값으로 간주되며 `String` 형식에는 배열에서 허용하는 조작과 유사한 많은 조작을 문자열에서 수행할 수 있는 기본 제공 함수가 있습니다. .NET Framework의 모든 배열 처럼 이러한 배열은 0부터 시작 합니다. 문자열에서 나타나는 위치를 기준으로 문자에 액세스하는 방법을 제공하는 `Chars` 속성을 통해 문자열의 특정 문자를 참조할 수 있습니다. 예를 들어:  
  
 [!code-vb[VbVbalrStrings#67](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#67)]  
  
 위 예제에서 문자열의 `Chars` 속성은 문자열에서 네 번째 문자인 `D`를 반환하고 `myChar`에 할당합니다. `Length` 속성을 통해 특정 문자열의 길이를 가져올 수도 있습니다. 문자열에서 여러 배열 형식 조작을 수행해야 하는 경우 문자열의 `ToCharArray` 함수를 사용하여 `Char` 인스턴스의 배열로 변환할 수 있습니다. 예를 들어:  
  
 [!code-vb[VbVbalrStrings#68](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#68)]  
  
 이제 변수 `myArray`에 `Char` 값의 배열이 포함되며, 각각은 `myString`의 문자를 나타냅니다.  
  
## <a name="the-immutability-of-strings"></a>문자열의 불변성  
 문자열은 *변경할 수 없는*, 해당 값을 한 번만 변경할 수 없습니다. 즉 만들어졌습니다. 그러나 둘 이상의 값을 문자열 변수에 할당할 수는 있습니다. 다음 예제를 참조하세요.  
  
 [!code-vb[VbVbalrStrings#69](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#69)]  
  
 여기에서는 문자열 변수를 만들고 값을 지정한 다음 해당 값을 변경합니다.  
  
 좀더 구체적으로 첫 번째 줄에서는 `String` 형식의 인스턴스를 만들고 `This string is immutable`값을 지정합니다. 예제의 두 번째 줄에서는 새 인스턴스를 만들고 `Or is it?` 값을 지정합니다. 문자열 변수는 첫 번째 인스턴스에 대한 참조를 삭제하고 새 인스턴스에 대한 참조를 저장합니다.  
  
 다른 내장 데이터 형식과 달리 `String`은 참조 형식입니다. 참조 형식의 변수가 인수로 함수 또는 서브루틴에 전달되면 데이터가 저장되는 메모리 주소에 대한 참조가 문자열의 실제 값 대신 전달됩니다. 따라서 이전 예제에서 변수의 이름은 동일하게 유지되지만 새 값을 보유하는 `String` 클래스의 다른 새 인스턴스를 가리킵니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic의 문자열 소개](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
- [String 데이터 형식](../../../../visual-basic/language-reference/data-types/string-data-type.md)
- [Char 데이터 형식](../../../../visual-basic/language-reference/data-types/char-data-type.md)
- [기본적인 문자열 작업](../../../../standard/base-types/basic-string-operations.md)
