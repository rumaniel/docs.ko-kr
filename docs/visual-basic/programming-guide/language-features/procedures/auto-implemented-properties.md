---
title: 자동 구현 속성(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.AutoProperty
- vb.AutoImplementedProperty
helpviewer_keywords:
- properties [Visual Basic], auto-implemented
- auto-implemented properties [Visual Basic]
ms.assetid: 5c669f0b-cf95-4b4e-ae84-9cc55212ca87
ms.openlocfilehash: f2e25c7bcd3556f93dfedee7aa8e49bb14888123
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70254028"
---
# <a name="auto-implemented-properties-visual-basic"></a>자동 구현 속성(Visual Basic)
*자동 구현 속성* 을 사용 하면 `Get` 및 `Set` 속성에 코드를 작성 하지 않고도 클래스의 속성을 신속 하 게 지정할 수 있습니다. 자동 구현 속성에 대한 코드를 작성하면 Visual Basic 컴파일러에서 관련 `Get` 및 `Set` 프로시저가 생성될 뿐만 아니라 속성 변수를 저장하는 전용 필드가 자동으로 만들어집니다.  
  
 자동 구현 속성을 사용하면 기본값을 포함한 속성을 한 줄에 선언할 수 있습니다. 다음 예제에서는 3개의 속성 선언을 보여 줍니다.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrautoimplementedproperties/vb/module1.vb#1)]  
  
 자동 구현 속성은 해당 속성 값이 전용 필드에 저장되는 속성과 동일합니다. 다음 코드 예제에서는 자동 구현 속성을 보여 줍니다.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrautoimplementedproperties/vb/module1.vb#5)]  
  
 다음 코드 예제에서는 앞의 자동 구현 속성 예제에 해당하는 코드를 보여 줍니다.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrautoimplementedproperties/vb/module1.vb#2)]  
  
 다음 코드에서는 읽기 전용 속성 구현을 보여 줍니다.  
  
```vb  
Class Customer  
   Public ReadOnly Property Tags As New List(Of String)  
   Public ReadOnly Property Name As String = ""  
   Public ReadOnly Property File As String  
  
   Sub New(file As String)  
      Me.File = file  
   End Sub  
End Class  
```  
  
 예제처럼 초기화 식을 사용해 속성에 할당할 수 있습니다. 또는 포함하는 형식의 생성자에서 속성에 할당할 수 있습니다.  언제든지 읽기 전용 속성의 지원 필드에 할당할 수 있습니다.  
  
## <a name="backing-field"></a>지원 필드  
 자동 구현 속성을 선언 하면 Visual Basic는 속성 값을 포함 하기 위해 *지원 필드* 라는 숨겨진 private 필드를 자동으로 만듭니다. 지원 필드 이름은 밑줄(_) 다음에 자동 구현 속성 이름이 나오는 형태입니다. 예를 들어 `ID`라는 자동 구현 속성을 선언하는 경우 지원 필드의 이름은 `_ID`가 됩니다. 이름이 `_ID`인 클래스의 멤버를 포함하는 경우 이름 충돌이 발생하며 Visual Basic에서 컴파일러 오류가 보고됩니다.  
  
 지원 필드에는 또한 다음과 같은 특징이 있습니다.  
  
- 속성 자체에 `Public`과 같은 다른 액세스 수준이 있는 경우에도, 지원 필드에 대한 액세스 한정자는 항상 `Private`입니다.  
  
- 속성이 `Shared`로 표시된 경우 지원 필드도 공유됩니다.  
  
- 속성에 대해 지정된 특성은 지원 필드에 적용되지 않습니다.  
  
- 클래스 내의 코드에서, 그리고 조사식 창과 같은 디버깅 도구에서 지원 필드에 액세스할 수 있습니다. 그러나 지원 필드는 IntelliSense 단어 완성 목록에 표시되지 않습니다.  
  
## <a name="initializing-an-auto-implemented-property"></a>자동 구현 속성 초기화  
 필드를 초기화하는 데 사용할 수 있는 모든 식이 자동 구현 속성을 초기화하는 데 유효합니다. 자동 구현 속성을 초기화하면 식이 계산되어 속성에 대한 `Set` 프로시저에 전달됩니다. 다음 코드 예제에서는 초기 값이 포함된 일부 자동 구현 속성을 보여 줍니다.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrautoimplementedproperties/vb/module1.vb#3)]  
  
 `Interface`의 멤버이거나 `MustOverride`로 표시된 자동 구현 속성은 초기화할 수 없습니다.  
  
 자동 구현 속성을 `Structure`의 멤버로 선언하는 경우 `Shared`로 표시된 자동 구현 속성만 초기화할 수 있습니다.  
  
 자동 구현 속성을 배열로 선언하는 경우 명시적 배열 범위를 지정할 수 없습니다. 그러나 다음 예에서와 같이 배열 이니셜라이저를 사용하여 값을 제공할 수 있습니다.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrautoimplementedproperties/vb/module1.vb#4)]  
  
## <a name="property-definitions-that-require-standard-syntax"></a>표준 구문이 요구되는 속성 정의  
 자동 구현 속성은 편리하며 많은 프로그래밍 시나리오를 지원합니다. 그러나 자동으로 구현 된 속성을 사용할 수 없으며 대신 표준 또는 *확장*된 속성 구문을 사용 해야 하는 경우도 있습니다.  
  
 다음 중 하나를 수행하려는 경우 확장된 속성 정의 구문을 사용해야 합니다.  
  
- 속성의 `Get` 또는 `Set` 프로시저에 추가합니다. 예를 들어 `Set` 프로시저에 들어오는 값의 유효성을 검사하는 코드를 추가합니다. 예를 들어 해당 속성 값을 설정하기 전에 전화번호를 나타내는 문자열에 필요한 수의 숫자가 포함되었는지 확인해야 할 수 있습니다.  
  
- `Get` 및 `Set` 프로시저에 대해 다른 접근성을 지정합니다. `Set` 프로시저를 `Private`으로, `Get` 프로시저를 `Public`으로 만들려는 경우를 예로 들 수 있습니다.  
  
- `WriteOnly`인 속성을 만듭니다.  
  
- 매개 변수가 있는 속성을 사용합니다(`Default` 속성 포함). 속성에 대한 매개 변수를 지정하기 위해, 또는 `Set` 프로시저에 대해 추가 매개 변수를 지정하기 위해서는 확장된 속성을 선언해야 합니다.  
  
- 지원 필드에 특성을 배치하거나 지원 필드의 액세스 수준을 변경합니다.  
  
- 지원 필드에 대한 XML 주석을 제공합니다.  
  
## <a name="expanding-an-auto-implemented-property"></a>자동 구현 속성 확장명  
 자동 구현 속성을 `Get` 또는 `Set` 프로시저가 포함된 확장된 속성으로 변환해야 하는 경우 Visual Basic 코드 편집기는 속성에 대한 `Get` 및 `Set` 프로시저와 `End Property` 문을 자동으로 생성할 수 있습니다. `Property` 문 뒤에 있는 `G` 빈 줄에 커서를 놓고 `S` (의 `Get`경우) 또는 (의 `Set`경우)를 입력 하 고 enter 키를 누르면 코드가 생성 됩니다. `Property` 문 끝에서 Enter 키를 누르면 Visual Basic 코드 편집기에서 읽기 전용 및 쓰기 전용 속성에 대한 `Get` 또는 `Set` 프로시저가 자동으로 생성됩니다.  
  
## <a name="see-also"></a>참고자료

- [방법: Visual Basic에서 기본 속성을 선언 하 고 호출 합니다.](./how-to-declare-and-call-a-default-property.md)
- [방법: 혼합 된 액세스 수준으로 속성 선언](./how-to-declare-a-property-with-mixed-access-levels.md)
- [Property 문](../../../../visual-basic/language-reference/statements/property-statement.md)
- [ReadOnly](../../../../visual-basic/language-reference/modifiers/readonly.md)
- [WriteOnly](../../../../visual-basic/language-reference/modifiers/writeonly.md)
- [개체 및 클래스](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
