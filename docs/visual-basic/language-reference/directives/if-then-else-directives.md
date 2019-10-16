---
title: '#... Then ... #Else 지시문 (Visual Basic)'
ms.date: 04/11/2018
f1_keywords:
- vb.#EndIf
- '#End If'
- '#Then'
- '#ElseIf'
- vb.#ElseIf
- vb.#Else
- vb.#If
helpviewer_keywords:
- Visual Basic code, compiling
- '#If directive [Visual Basic]'
- conditional compilation [Visual Basic], directives
- '#End if directive [Visual Basic]'
- selective compiling
- else directive (#else)
- '#Else directive [Visual Basic]'
ms.assetid: 10bba104-e3fd-451b-b672-faa472530502
ms.openlocfilehash: c5357dca24b03ddd03779866019baf14175be992
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698540"
---
# <a name="ifthenelse-directives"></a>#If...Then...#Else 지시문
선택한 Visual Basic 코드 블록을 조건부로 컴파일합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
#If expression Then  
   statements  
[ #ElseIf expression Then  
   [ statements ]  
...  
#ElseIf expression Then  
   [ statements ] ]  
[ #Else  
   [ statements ] ]  
#End If  
```  
  
## <a name="parts"></a>요소  
 `expression`  
 @No__t-0 및 `#ElseIf` 문에 필요 하며, 다른 위치에 선택적입니다. 하나 이상의 조건부 컴파일러 상수, 리터럴 및 연산자로만 구성 되는 식으로, `True` 또는 `False`로 계산 됩니다.  
  
 `statements`  
 @No__t-0 문 블록에 필요 합니다 (선택 사항). 연결 된 식이 `True`으로 계산 되는 경우 컴파일되는 프로그램 줄 또는 컴파일러 지시문을 Visual Basic 합니다.  
  
 `#End If`  
 @No__t-0 문 블록을 종료 합니다.  
  
## <a name="remarks"></a>설명  
 화면에서 `#If...Then...#Else` 지시문의 동작은 `If...Then...Else` 문과 동일 하 게 표시 됩니다. 그러나 `#If...Then...#Else` 지시문은 컴파일러에 의해 컴파일되는 항목을 평가 하는 반면, `If...Then...Else` 문은 런타임에 조건을 평가 합니다.  
  
 조건부 컴파일은 일반적으로 여러 플랫폼에 대해 동일한 프로그램을 컴파일하는 데 사용 됩니다. 또한 실행 파일에 디버깅 코드가 나타나지 않도록 하는 데 사용 됩니다. 조건부 컴파일을 수행 하는 동안 제외 된 코드는 최종 실행 파일에서 완전히 생략 되므로 크기 또는 성능에 영향을 주지 않습니다.  
  
 모든 계산 결과에 관계 없이 모든 식은 `Option Compare Binary`을 사용 하 여 계산 됩니다. @No__t-0 문은 `#If` 및 `#ElseIf` 문의 식에 영향을 주지 않습니다.  
  
> [!NOTE]
> @No__t-0, `#Else`, `#ElseIf` 및 `#End If` 지시문이 한 줄로 구성 되어 있지 않습니다. 지시문과 동일한 줄에 다른 코드를 표시할 수 없습니다. 

조건부 컴파일 블록 내의 문은 완전 한 논리적 문 이어야 합니다. 예를 들어 함수 특성만 조건부로 컴파일할 수는 없지만 해당 특성과 함께 함수를 조건부로 선언할 수 있습니다.

```vb
   #If DEBUG Then
   <WebMethod()>
   Public Function SomeFunction() As String
   #Else
   <WebMethod(CacheDuration:=86400)>
   Public Function SomeFunction() As String
   #End If
```

## <a name="example"></a>예제
 이 예제에서는 `#If...Then...#Else` 구문을 사용 하 여 특정 문을 컴파일할 것인지 여부를 결정 합니다.  
  
 [!code-vb[VbVbalrConditionalComp#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#1)]  
  
## <a name="see-also"></a>참조

- [#Const 지시문](../../../visual-basic/language-reference/directives/const-directive.md)
- [If...Then...Else 문](../../../visual-basic/language-reference/statements/if-then-else-statement.md)
- [조건부 컴파일](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
- <xref:System.Diagnostics.ConditionalAttribute?displayProperty=nameWithType>
