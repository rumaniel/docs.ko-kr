---
title: ReadOnly(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.ReadOnly
helpviewer_keywords:
- ReadOnly keyword [Visual Basic]
- variables [Visual Basic], read-only
- ReadOnly property
- properties [Visual Basic], read-only
- read-only variables
ms.assetid: e868185d-6142-4359-a2fd-a7965cadfce8
ms.openlocfilehash: 748c38835cec83cefe54535f90d40ec3a030e4f4
ms.sourcegitcommit: d7c298f6c2e3aab0c7498bfafc0a0a94ea1fe23e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72250386"
---
# <a name="readonly-visual-basic"></a>ReadOnly(Visual Basic)
변수 또는 속성을 읽을 수 있지만 쓸 수는 없도록 지정 합니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="rules"></a>규칙  
  
- **선언 컨텍스트입니다.** `ReadOnly`는 모듈 수준에서만 사용할 수 있습니다. 즉, `ReadOnly` 요소의 선언 컨텍스트는 클래스, 구조체 또는 모듈 이어야 하며 소스 파일, 네임 스페이스 또는 프로시저일 수 없습니다.  
  
- **결합 된 한정자입니다.** 동일한 선언에서-0을 `Static`과 함께 @no__t 지정할 수 없습니다.  
  
- **값 할당** @No__t-0 속성을 사용 하는 코드는 해당 값을 설정할 수 없습니다. 하지만 기본 저장소에 대 한 액세스 권한이 있는 코드는 언제 든 지 값을 할당 하거나 변경할 수 있습니다.  
  
     선언 또는 정의 된 클래스 또는 구조체의 생성자 에서만 `ReadOnly` 변수에 값을 할당할 수 있습니다.  
  
## <a name="when-to-use-a-readonly-variable"></a>ReadOnly 변수를 사용 하는 경우  
 상수 값을 선언 하 고 할당 하는 데 [Const 문을](../../../visual-basic/language-reference/statements/const-statement.md) 사용할 수 없는 경우가 있습니다. 예를 들어 `Const` 문은 할당 하려는 데이터 형식을 허용 하지 않거나 컴파일 타임에 상수 식으로 값을 계산할 수 없습니다. 컴파일 시간에 값을 알 수 없습니다. 이 경우 `ReadOnly` 변수를 사용 하 여 상수 값을 저장할 수 있습니다.  
  
> [!IMPORTANT]
> 변수의 데이터 형식이 배열 또는 클래스 인스턴스와 같은 참조 형식이 면 변수 자체가-0 @no__t 경우에도 해당 멤버를 변경할 수 있습니다. 다음은 이에 대한 예입니다.  
  
 ```vb
 ReadOnly characterArray() As Char = {"x"c, "y"c, "z"c}
 Sub ChangeArrayElement()
     characterArray(1) = "M"c
 End Sub
 ```
  
 초기화 될 때 `characterArray()`이 가리키는 배열은 "x", "y" 및 "z"를 포함 합니다. 변수 `characterArray`은 @no__t 이므로 값을 초기화 한 후에는 변경할 수 없습니다. 즉, 새 배열을 할당할 수 없습니다. 그러나 하나 이상의 배열 멤버의 값을 변경할 수 있습니다. @No__t-0 프로시저를 호출 하 고 `characterArray()`에서 가리키는 배열은 "x", "M" 및 "z"를 포함 합니다.
  
 프로시저 매개 변수를 [ByVal](byval.md)로 선언 하는 것과 유사 합니다. 그러면 프로시저에서 호출 인수 자체를 변경 하는 것이 아니라 해당 멤버를 변경할 수 있습니다.  
  
## <a name="example"></a>예제

다음 예에서는 직원이 고용 된 날짜에 대 한 `ReadOnly` 속성을 정의 합니다. 클래스는 내부적으로 `Private` 변수로 속성 값을 저장 하 고 클래스 내의 코드만이 값을 변경할 수 있습니다. 그러나 속성은 `Public` 이며 클래스에 액세스할 수 있는 모든 코드는 속성을 읽을 수 있습니다.
  
[!code-vb[VbVbalrKeywords#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class1.vb#4)]
  
`ReadOnly` 한정자는 다음 컨텍스트에서 사용할 수 있습니다.
  
- [Dim 문](../statements/dim-statement.md) 
- [Property 문](../statements/property-statement.md)  
  
## <a name="see-also"></a>참조

- [WriteOnly](writeonly.md)
- [C++ 키워드](../keywords/index.md)
