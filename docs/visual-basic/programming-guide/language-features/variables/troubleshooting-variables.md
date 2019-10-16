---
title: Visual Basic의 변수 문제 해결
ms.date: 07/20/2015
helpviewer_keywords:
- troubleshooting [Visual Basic], variables
- variables [Visual Basic], troubleshooting
ms.assetid: 928a2dc8-e565-4ae4-8ba3-80cc0cb50090
ms.openlocfilehash: 31aca95bb292ecd0bb04fda6ded83d4af8be0e2f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64598620"
---
# <a name="troubleshooting-variables-in-visual-basic"></a>Visual Basic의 변수 문제 해결
이 페이지는 Visual Basic의 변수를 사용 하 여 작업할 때 발생할 수 있는 몇 가지 일반적인 문제를 나열 합니다.  
  
## <a name="unable-to-access-members-of-an-object"></a>개체의 멤버에 액세스할 수 없습니다.  
 코드에서 개체의 속성이나 메서드에 액세스하려고 하면 다음과 같은 두 가지 오류가 발생할 수 있습니다.  
  
- 개체 변수를 특정 형식으로 선언한 다음 해당 형식으로 정의되지 않은 멤버를 참조하면 컴파일러에서 오류 메시지가 생성됩니다.  
  
- 개체 변수에 할당된 개체가 코드에서 액세스하려는 멤버를 노출하지 않는 경우 런타임 <xref:System.MemberAccessException> 이 발생합니다. 변수 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)에 멤버가 없는 경우에이 예외가 발생할 수 있습니다 `Public`합니다. 그 이유는 런타임 바인딩에서는 `Public` 멤버에만 액세스할 수 있기 때문입니다.  
  
  [Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md) 의 형식 검사가 `On`으로 설정된 경우 개체 변수는 선언된 클래스의 메서드와 속성에만 액세스할 수 있습니다. 다음은 이에 대한 예입니다.  

 [!code-vb[VbVbalrVariables#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrVariables/VB/Class1.vb#2)]  
  
 이 예제에서 `p` 는 <xref:System.Object> 클래스 자체의 멤버만 사용할 수 있으므로 `Left` 속성을 포함하지 않습니다. 반면, `q` 형식으로 선언된 <xref:System.Windows.Forms.Label>는 <xref:System.Windows.Forms.Label> 네임스페이스에 있는 <xref:System.Windows.Forms> 클래스의 모든 메서드와 속성을 사용할 수 있습니다.  
  
### <a name="correct-approach"></a>해결 방법  
 특정 클래스 개체의 모든 멤버에 액세스하려면 개체 변수를 해당 클래스의 형식으로 선언합니다. 그렇게 할 수 없는 경우(예: 컴파일 타임에 개체 형식을 모르는 경우)에는 `Option Strict` 를 `Off` 로 설정하고 변수를 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)에서 변수 작업 시 발생할 수 있는 일반적인 문제를 보여 줍니다. 그러면 모든 형식의 개체가 변수에 할당될 수 있으므로 현재 할당된 개체의 형식이 적합한지 확인해야 합니다. 사용할 수는 [TypeOf 연산자](../../../../visual-basic/language-reference/operators/typeof-operator.md) 이 확인 하기 위해.  
  
## <a name="other-components-cannot-access-your-variable"></a>다른 구성 요소에서 사용자 변수에 액세스할 수 없습니다.  
 Visual Basic 이름은 *대/소문자*합니다. 따라서 컴파일러에서는 대/소문자만 다른 두 이름을 동일한 이름으로 간주합니다. 예를 들어, `ABC` 와 `abc` 는 동일한 선언 요소를 참조하는 것으로 간주합니다.  
  
 그러나, CLR(공용 언어 런타임)에서는 *대/소문자를 구분하는* 바인딩을 사용합니다. 그러므로, 어셈블리나 DLL을 작성하여 다른 어셈블리에서 이를 사용하게 되면 이름의 대/소문자가 구분됩니다. 예를 들어, `ABC`라는 이름의 요소를 포함하는 클래스를 정의하고 다른 어셈블리에서 공용 언어 런타임을 통해 이 클래스를 사용할 경우 해당 어셈블리에서 이 요소를 `ABC`로 참조해야 합니다. 클래스를 다시 컴파일하고 요소 이름을 `abc`로 변경하면 이 클래스를 사용하는 다른 어셈블리가 더 이상 이 요소에 액세스할 수 없습니다. 따라서, 어셈블리를 업데이트하여 릴리스하는 경우 공용 요소의 알파벳 대/소문자를 변경하지 않아야 합니다.  
  
 자세한 내용은 [Common Language Runtime](../../../../standard/clr.md)을 참조하세요.  
  
### <a name="correct-approach"></a>해결 방법  
 다른 구성 요소에서 사용자 변수에 액세스할 수 있도록 하려면 이름의 대/소문자를 구분합니다. 클래스나 모듈을 테스트하는 경우에는 다른 어셈블리가 원하는 변수에 바인딩되는지 확인합니다. 구성 요소를 게시한 경우에는 대/소문자 변경을 포함하여 기존 변수 이름을 수정하는 어떤 작업도 수행하지 마세요.  
  
## <a name="wrong-variable-being-used"></a>잘못된 변수 사용  
 동일한 이름 가진 둘 이상의 변수를 설정한 경우 Visual Basic 컴파일러에서는 해당 이름에 대 한 각 참조를 확인 하려고 합니다. 변수 범위가 다른 경우 컴파일러에서는 범위가 가장 작은 선언에 대한 참조를 확인합니다. 변수 범위가 같은 경우에는 확인에 실패하고 컴파일러에서 오류를 발생시킵니다. 자세한 내용은 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)을 참조하세요.  
  
### <a name="correct-approach"></a>해결 방법  
 이름은 같지만 범위가 다른 변수를 사용하지 않습니다. 다른 어셈블리나 프로젝트를 사용하는 경우에는 가능하면 이러한 외부 구성 요소에 정의된 이름을 사용하지 않습니다. 이름이 같은 변수가 두 개 이상 있는 경우 모든 참조를 해당 이름으로 한정해야 합니다. 자세한 내용은 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [변수](../../../../visual-basic/programming-guide/language-features/variables/index.md)
- [변수 선언](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
- [개체 변수](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)
- [개체 변수 선언](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)
- [방법: 개체의 멤버에 액세스](../../../../visual-basic/programming-guide/language-features/variables/how-to-access-members-of-an-object.md)
- [개체 변수 값](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)
- [방법: 개체 변수가 참조 하는 형식 확인](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-what-type-an-object-variable-refers-to.md)
- [선언된 요소 참조](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [선언 요소 이름](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
