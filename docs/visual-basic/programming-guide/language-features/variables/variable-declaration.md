---
title: Visual Basic의 변수 선언
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], declaring
- member variables [Visual Basic], declarations
- Dim statement [Visual Basic], variable declaration
- declaring variables [Visual Basic]
- variables [Visual Basic], scope
- variables [Visual Basic], data types
- data types [Visual Basic], variable declarations
- lifetime [Visual Basic], variables
- variables [Visual Basic], lifetime
- access levels [Visual Basic], variables
- scope [Visual Basic], declaration statements
- variables [Visual Basic], access level
- local variables [Visual Basic], declarations
- scope [Visual Basic], variables
ms.assetid: d8f10226-92b1-480f-9f53-df377b2d7e15
ms.openlocfilehash: 726347efc2e12100f7d89348a316037babc785e5
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72003302"
---
# <a name="variable-declaration-in-visual-basic"></a>Visual Basic의 변수 선언
변수를 선언 하 여 해당 이름 및 특성을 지정 합니다. 변수에 대 한 선언문은 [Dim 문](../../../../visual-basic/language-reference/statements/dim-statement.md)입니다. 해당 위치 및 내용에 따라 변수의 특징이 결정 됩니다.  
  
 변수 명명 규칙 및 고려 사항은 선언 된 [요소 이름](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)을 참조 하세요.  
  
## <a name="declaration-levels"></a>선언 수준  
  
### <a name="local-and-member-variables"></a>지역 변수 및 멤버 변수  
 *지역 변수* 는 프로시저 내에서 선언 된 변수입니다. *멤버 변수* 는 Visual Basic 형식의 멤버입니다. 이 클래스는 모듈 수준에서 클래스, 구조체 또는 모듈 내에서 선언 되지만 해당 클래스, 구조체 또는 모듈 내부의 프로시저 내에서는 선언 되지 않습니다.  
  
### <a name="shared-and-instance-variables"></a>공유 및 인스턴스 변수  
 클래스 또는 구조체에서 멤버 변수의 범주는 공유 여부에 따라 달라 집니다. [Shared](../../../../visual-basic/language-reference/modifiers/shared.md) 키워드를 사용 하 여 선언 된 경우 *공유 변수*이며, 클래스 또는 구조체의 모든 인스턴스 간에 공유 되는 단일 복사본에 존재 합니다.  
  
 그렇지 않으면 *인스턴스 변수*이며, 클래스 또는 구조체의 각 인스턴스에 대해 별도의 복사본을 만듭니다. 인스턴스 변수의 지정 된 복사본은 해당 복사본이 생성 된 클래스 또는 구조체의 인스턴스에만 사용할 수 있습니다. 클래스 또는 구조체의 다른 인스턴스에 있는 인스턴스 변수의 복사본과는 독립적입니다.  
  
## <a name="declaring-data-type"></a>데이터 형식 선언  
 선언문의 [As](../../../../visual-basic/language-reference/statements/as-clause.md) 절을 사용 하 여 선언 하는 변수의 데이터 형식 또는 개체 유형을 정의할 수 있습니다. 변수에 대해 다음 형식 중 하나를 지정할 수 있습니다.  
  
- @No__t-0, `Long` 또는 `Decimal`와 같은 기본 데이터 형식  
  
- 복합 데이터 형식 (예: 배열 또는 구조체)  
  
- 응용 프로그램 또는 다른 응용 프로그램에서 정의 된 개체 형식 또는 클래스입니다.  
  
- @No__t-0 또는 <xref:System.Windows.Forms.TextBox>과 같은 .NET Framework 클래스  
  
- @No__t-0 또는 <xref:System.IDisposable>과 같은 인터페이스 형식  
  
 데이터 형식을 반복할 필요 없이 하나의 문에서 여러 변수를 선언할 수 있습니다. 다음 문에서는 변수 `i`, `j`, `k` `Integer`, `l`, `m`, `x`, `Single`, 로 선언 됩니다.  
  
```vb  
Dim i, j, k As Integer  
' All three variables in the preceding statement are declared as Integer.  
Dim l, m As Long, x, y As Single  
' In the preceding statement, l and m are Long, x and y are Single.  
```  
  
 데이터 형식에 대 한 자세한 내용은 [데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/index.md)을 참조 하세요. 개체에 대 한 자세한 내용은 [개체 및 클래스](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md) 및 [구성 요소를 사용한 프로그래밍](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/0ffkdtkf(v=vs.120))을 참조 하세요.  
  
## <a name="local-type-inference"></a>지역 형식 유추  
 *형식 유추* 는 `As` 절 없이 선언 된 지역 변수의 데이터 형식을 결정 하는 데 사용 됩니다. 컴파일러는 초기화 식의 형식에서 변수 형식을 유추 합니다. 이렇게 하면 명시적으로 형식을 명시 하지 않고도 변수를 선언할 수 있습니다. 다음 예제에서는 `num1`과 `num2` 모두 정수로 강력 하 게 형식화 되어 있습니다.  
  
 [!code-vb[VbVbalrTypeInference#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#1)]  
  
 로컬 형식 유추를 사용 하려는 경우 `Option Infer`을 `On`로 설정 해야 합니다. 자세한 내용은 [지역 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md) 및 [Option Infer 문](../../../../visual-basic/language-reference/statements/option-infer-statement.md)을 참조하세요.  
  
## <a name="characteristics-of-declared-variables"></a>선언 된 변수의 특성  
 변수의 *수명은* 이를 사용할 수 있는 기간입니다. 일반적으로 변수는 해당 변수를 선언 하는 요소 (예: 프로시저 또는 클래스)가 계속 존재 하는 동안 존재 합니다. 변수가 포함 하는 요소의 수명을 초과 하 여 기존에 계속할 필요가 없으면 선언에서 특별 한 작업을 수행할 필요가 없습니다. 변수가 포함 하는 요소 보다 더 오래 지속 되어야 하는 경우 `Static` 또는 `Shared` 키워드를 `Dim` 문에 포함할 수 있습니다. 자세한 내용은 [Visual Basic 수명](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)을 참조 하세요.  
  
 변수의 *범위* 는 이름을 한정 하지 않고 참조할 수 있는 모든 코드 집합입니다. 변수의 범위는 선언 된 위치에 따라 결정 됩니다. 지정 된 지역에 있는 코드는 해당 영역에 정의 된 변수를 사용할 수 있습니다. 자세한 내용은 [Scope in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)을 참조하세요.  
  
 변수의 *액세스 수준은* 액세스 권한이 있는 코드의 범위입니다. 이는 `Dim` 문에서 사용 하는 액세스 한정자 (예: [공용](../../../../visual-basic/language-reference/modifiers/public.md) 또는 [개인](../../../../visual-basic/language-reference/modifiers/private.md))에 의해 결정 됩니다. 자세한 내용은 [Visual Basic의 액세스 수준](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조 하세요.  
  
## <a name="see-also"></a>참조

- [방법: 새 변수 @ no__t-0 만들기
- [방법: 변수 내/외부로 데이터 이동 @ no__t-0
- [데이터 형식](../../../../visual-basic/language-reference/data-types/index.md)
- [보호됨](../../../../visual-basic/language-reference/modifiers/protected.md)
- [Friend](../../../../visual-basic/language-reference/modifiers/friend.md)
- [정적](../../../../visual-basic/language-reference/modifiers/static.md)
- [선언 요소의 특징](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)
- [지역 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [Option Infer 문](../../../../visual-basic/language-reference/statements/option-infer-statement.md)
