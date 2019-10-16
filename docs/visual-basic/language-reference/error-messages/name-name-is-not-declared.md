---
title: "'<name>' 이름이 선언되지 않았습니다."
ms.date: 10/10/2018
f1_keywords:
- bc30451
- vbc30451
helpviewer_keywords:
- BC30451
ms.assetid: 765f099b-e21e-47c6-a906-a065444e56b3
ms.openlocfilehash: dfa1d1600c7943e503b4f5ec2e2b8ecd6fbb9fe0
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70254196"
---
# <a name="name-name-is-not-declared"></a>이름 '\<name > '이 (가) 선언 되지 않았습니다.
문이 프로그래밍 요소를 참조 하지만 컴파일러가 정확한 이름을 가진 요소를 찾을 수 없습니다.  
  
 **오류 ID:** BC30451  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 참조하는 문에서 이름의 철자를 검사합니다. Visual Basic는 대/소문자를 구분 하지 않지만 철자의 다른 모든 변형은 완전히 다른 이름으로 간주 됩니다. 밑줄(`_`)은 이름의 일부이므로 철자의 일부입니다.  
  
2. 개체와 해당 멤버 사이에 멤버 액세스 연산자`.`()가 있는지 확인 합니다. 예를 들어 <xref:System.Windows.Forms.TextBox> 이라는 `TextBox1`컨트롤이 있는 경우 해당 <xref:System.Windows.Forms.TextBoxBase.Text%2A> 속성에 액세스하려면 `TextBox1.Text`를 입력해야 합니다. `TextBox1Text`를 대신 입력하면 다른 이름이 만들어집니다.  
  
3. 철자가 올바르고 개체 멤버 액세스의 구문이 올바르면 요소가 선언 되었는지 확인 합니다. 자세한 내용은 [선언 된 요소](../../programming-guide/language-features/declared-elements/index.md)를 참조 하세요.  
  
4. 프로그래밍 요소가 선언 된 경우 범위에 있는지 확인 합니다. 참조 하는 문이 프로그래밍 요소를 선언 하는 영역 외부에 있는 경우 요소 이름을 한 정해야 할 수 있습니다. 자세한 내용은 [Scope in Visual Basic](../../programming-guide/language-features/declared-elements/scope.md)을 참조하세요.  

5. 정규화 된 형식 또는 형식 및 멤버 이름을 사용 하지 않는 경우 (예: 코드가 `MethodInfo.Name` `System.Reflection.MethodInfo.Name`대신로 속성을 참조 하는 경우) [Imports 문을](../statements/imports-statement-net-namespace-and-type.md)추가 합니다.

6. SDK 스타일 프로젝트 (줄 \* `<Project Sdk="Microsoft.NET.Sdk">`로 시작 하는 .vbproj 파일이 있는 프로젝트)를 컴파일하려고 시도 하 고 오류 메시지가 microsoft.visualbasic 어셈블리의 형식 또는 멤버를 참조 하는 경우 응용 프로그램을 구성 합니다. Visual Basic 런타임 라이브러리에 대 한 참조를 사용 하 여 컴파일합니다. 기본적으로 라이브러리의 하위 집합은 SDK 스타일 프로젝트의 어셈블리에 포함 됩니다.

   예를 들어 다음 예제는 <xref:Microsoft.VisualBasic.CompilerServices.Conversions.ChangeType%2A?displayProperty=fullName> 메서드를 찾을 수 없기 때문에 컴파일되지 않습니다. 응용 프로그램에 포함 된 Visual Basic 런타임의 하위 집합에 포함 되지 않습니다.  

   [!code-vb[BC30451](~/samples/snippets/visualbasic/language-reference/error-messages/bc30451/program1.vb?highlight=7)]

   이 오류를 해결 하려면 다음 Visual Basic `<VBRuntime>Default</VBRuntime>` 프로젝트 파일에 표시 `<PropertyGroup>` 된 것 처럼 프로젝트 섹션에 요소를 추가 합니다.

   [!code-xml[BC30451](~/samples/snippets/visualbasic/language-reference/error-messages/bc30451/vbruntime.vbproj?highlight=6)]

## <a name="see-also"></a>참고자료

- [선언 및 상수 요약](../../../visual-basic/language-reference/keywords/declarations-and-constants-summary.md)
- [Visual Basic 명명 규칙](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)
- [선언 요소 이름](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
- [선언된 요소 참조](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
