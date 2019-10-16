---
title: 선택적 매개 변수(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- parameters [Visual Basic], optional
- Visual Basic code, procedures
- procedures [Visual Basic], optional arguments
- optional arguments
- named arguments [Visual Basic], and optional arguments
- optional parameters
- Optional keyword [Visual Basic], optional arguments
- arguments [Visual Basic], optional
- optional arguments [Visual Basic], and named arguments
ms.assetid: 398d2845-1069-4e94-b934-a73b545c8b87
ms.openlocfilehash: 9236080d50638bc38bbdd3ddaf8aabf9e675e43f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64639133"
---
# <a name="optional-parameters-visual-basic"></a>선택적 매개 변수(Visual Basic)
프로시저 매개 변수를 선택적 요소로 지정하여 프로시저를 호출할 때 인수를 지정하지 않아도 되도록 할 수 있습니다. *선택적 매개 변수* 으로 표시 됩니다는 `Optional` 프로시저 정의에서 키워드입니다. 이 때 적용되는 규칙은 다음과 같습니다.  
  
- 프로시저 정의의 모든 선택적 매개 변수에는 기본값을 지정해야 합니다.  
  
- 선택적 매개 변수의 기본값은 상수 식이어야 합니다.  
  
- 프로시저 정의에서 선택적 매개 변수 뒤에 오는 매개 변수도 모두 선택적 요소여야 합니다.  
  
 다음 구문은 선택적 매개 변수를 사용하여 프로시저를 선언하는 방법을 보여 줍니다.  
  
```vb  
Sub name(ByVal parameter1 As datatype1, Optional ByVal parameter2 As datatype2 = defaultvalue)  
```  
  
## <a name="calling-procedures-with-optional-parameters"></a>선택적 매개 변수가 있는 프로시저 호출  
 선택적 매개 변수가 있는 프로시저를 호출하는 경우 해당 인수를 지정할지 여부를 선택할 수 있습니다. 선택하지 않으면 선택적 매개 변수에 대해 선언된 기본값이 사용됩니다.  
  
 인수 목록에서 하나 이상의 선택적 인수를 생략하는 경우 그 자리에 쉼표를 사용하여 생략된 위치를 표시합니다. 다음 호출 샘플에서는 첫 번째와 네 번째 인수가 제공되고 두 번째와 세 번째 인수는 제공되지 않습니다.  
  
```vb  
Sub name(argument 1, , , argument 4)  
```  
  
 다음 예제에서는 `MsgBox` 함수를 여러 번 호출합니다. `MsgBox`에는 필수적 매개 변수 하나와 선택적 매개 변수 두 개가 사용됩니다.  
  
 `MsgBox`에 대한 첫 번째 호출에서 `MsgBox`에서 정의하는 순서대로 세 개의 인수를 모두 제공합니다. 두 번째 호출에서는 필수적 인수만 지정합니다. 세 번째와 네 번째 호출에서는 첫 번째 인수와 세 번째 인수를 지정합니다. 세 번째 호출에서는 위치로 인수를 지정하고, 네 번째 호출에서는 이름으로 인수를 지정합니다.  
  
 [!code-vb[VbVbcnProcedures#47](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#47)]  
  
## <a name="determining-whether-an-optional-argument-is-present"></a>선택적 인수의 존재 여부 확인  
 프로시저는 지정된 인수가 생략되었는지 또는 호출 코드가 명시적으로 기본값을 제공했는지 여부를 런타임에서 감지할 수 없습니다. 이를 알아보려면 특이한 값을 기본값으로 설정하면 됩니다. 다음 절차는 선택적 매개 변수 정의 `office`, 및 해당 기본값에 대 한 테스트 `QJZ`호출에서 생략 된 경우를 참조 하세요.  
  
 [!code-vb[VbVbcnProcedures#46](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#46)]  
  
 선택적 매개 변수가 `String`과 같은 참조 형식일 경우 `Nothing`이 그 인수에 예상된 값이 아니면 이 값을 기본값으로 사용할 수 있습니다.  
  
## <a name="optional-parameters-and-overloading"></a>선택적 매개 변수 및 오버로드  
 선택적 매개 변수가 있는 프로시저를 정의하는 또 다른 방법은 오버로드를 사용하는 것입니다. 선택적 매개 변수가 하나이면 프로시저의 오버로드된 두 버전을 매개 변수를 사용하는 버전과 매개 변수를 사용하지 않는 버전으로 정의할 수 있습니다. 이러한 방식은 선택적 매개 변수의 개수가 증가할수록 더욱 복잡해지지만 호출 프로그램이 각 선택적 인수를 제공했는지 여부를 확실히 알 수 있다는 장점이 있습니다.  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [값 또는 참조로 인수 전달](./passing-arguments-by-value-and-by-reference.md)
- [위치 및 이름으로 인수 전달](./passing-arguments-by-position-and-by-name.md)
- [매개 변수 배열](./parameter-arrays.md)
- [프로시저 오버로딩](./procedure-overloading.md)
- [선택 사항](../../../../visual-basic/language-reference/modifiers/optional.md)
- [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)
