---
title: 위치 및 이름으로 인수 전달(Visual Basic)
ms.date: 02/01/2018
helpviewer_keywords:
- arguments [Visual Basic], passing by name
- procedures [Visual Basic], arguments
- := passing arguments
- procedure arguments
- Visual Basic code, procedures
- named arguments [Visual Basic], passing arguments
- arguments [Visual Basic], passing by position
- Function procedures [Visual Basic], passing arguments
- named parameters [Visual Basic], passing arguments
- named arguments
- passing parameters [Visual Basic], named parameter arguments
- passing parameters [Visual Basic], by position
- procedures [Visual Basic], calling
- named parameters
- Sub procedures [Visual Basic], passing arguments
- argument passing
- passing parameters [Visual Basic], by name
- argument passing [Visual Basic], by position
- arguments [Visual Basic], listing by name
ms.assetid: 1ad7358f-1da9-48da-a95b-f3c7ed41eff3
ms.openlocfilehash: b872eda97d1e349ad781b12810e4b166d6e46fe1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61791887"
---
# <a name="passing-arguments-by-position-and-by-name-visual-basic"></a>위치 및 이름으로 인수 전달(Visual Basic)
호출 하는 경우는 `Sub` 또는 `Function` 프로시저 인수를 전달할 수 있습니다 *위치별* -프로시저의 정의에 나타나는 순서로-또는 전달할 수 있습니다 *이름별*를 하지 않고 위치에 관계입니다.  
  
 인수 선언 된 이름에 콜론 및 등호 뒤에 지정할 이름으로 인수를 전달 하는 경우 (`:=`), 인수 값입니다. 순서에 관계 없이 명명 된 인수를 제공할 수 있습니다.  
  
 예를 들어, 다음 `Sub` 프로시저에 3 개 인수:  
  
 [!code-vb[SampleProcedure](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#1)]  
  
 이 프로시저를 호출할 때 위치, 이름 또는 둘 모두를 사용 하 여 인수를 제공할 수 있습니다.  
  
## <a name="passing-arguments-by-position"></a>위치 인수 전달  
 호출할 수 있습니다는 `Display` 메서드 인수를 사용 하 여 위치로 전달 하 고 다음 예제에서와 같이 쉼표로 구분 된:  
  
[!code-vb[ByPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#2)] 
  
 위치 인수 목록에는 선택적 인수를 생략할 경우 쉼표를 사용 하 여 해당 위치를 보유 해야 합니다. 다음 예제에서는 합니다 `Display` 없이 메서드를 `age` 인수:  
  
[!code-vb[ByPositionWithOptionalArgument](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#3)] 
  
## <a name="passing-arguments-by-name"></a>이름으로 인수 전달  
 호출할 수 있습니다 `Display` 이름으로 전달 된 인수를 사용 하 여 또한 쉼표로 분리 하 여 다음 예와에서 같이:  
  
[!code-vb[ByName](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#4)] 

 이러한 방식으로 이름으로 인수를 전달 합니다. 선택적 인수를 둘 이상 있는 프로시저를 호출할 때 특히 유용 합니다. 이름으로 인수를 제공 하는 경우 연속 된 쉼표를 사용 하 여 생략 된 위치 인수를 나타내는 필요가 없습니다. 이름으로 인수를 전달 합니다. 또한 쉽게 전달 하는 생략 되는 시나리오는 인수를 추적 하 합니다.  
  
## <a name="mixing-arguments-by-position-and-by-name"></a>이름 및 위치 인수 혼합  

다음 예제에서와 같이 위치 및 단일 프로시저 호출에서 이름으로 인수를 제공할 수 있습니다.  
  
[!code-vb[ByNameAndPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#5)] 
  
 앞의 예에서 없습니다 여분의 쉼표는 생략 된 위치를 포함 하는 데 필요한 `age` 인수를 있으므로 `birth` 이름으로 전달 됩니다.  
  
15.5 이전 버전의 Visual Basic의 위치 및 이름, 위치 인수를 사용 하 여 인수를 제공 하는 경우 모든 첫 번째 항목 이어야 합니다. 이름으로 인수를 제공한 후 모든 나머지 인수 모두 전달 되어야 합니다 이름별.  다음을 호출 하는 예를 들어 합니다 `Display` 컴파일러 오류를 표시 하는 메서드 [BC30241: 명명 된 인수가 필요](../../../misc/bc30241.md)합니다.

[!code-vb[ByNameAndPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#6)] 

Visual Basic 15.5부터 위치 인수 수에 따라 명명 된 인수 끝 위치 인수를 올바른 위치에 있는 경우. Visual Basic 15.5 이전 호출에서 컴파일된 경우에 `Display` 메서드가 성공적으로 컴파일되고 컴파일러 오류가 더 이상 [BC30241](../../../misc/bc30241.md)합니다.  

명명 되 고 위치 인수를 사용 하는 순서에 맞게 조정할 수는이 기능은 코드를 더 쉽게 읽을 수 있도록 명명된 된 인수를 사용 하려는 경우에 특히 유용 합니다. 다음 예를 들어 `Person` 클래스 생성자를 사용 하려면 두 인수 `Person`, 둘 다 수 `Nothing`합니다. 

[!code-vb[ByNameAndPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#7)] 

코드의 의도 할 수 있습니다 시기의 선택을 취소 하는 혼합된 명명 되 고 위치 인수를 사용 하 여 값을 `father` 하 고 `mother` 인수는 `Nothing`:

[!code-vb[ByNameAndPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#8)] 

명명 된 인수를 사용 하 여 위치 인수를 수행 하려면 Visual Basic 프로젝트에 다음 요소를 추가 해야 합니다 (\*.vbproj) 파일:

```xml
<PropertyGroup>
  <LangVersion>15.5</LangVersion>
</PropertyGroup>
```

자세한 내용은 참조 [Visual Basic 언어 버전을 설정](../../../language-reference/configure-language-version.md)합니다.

## <a name="restrictions-on-supplying-arguments-by-name"></a>이름으로 인수에 대 한 제한  

필수 인수를 입력 하지 않으려면 이름별 인수를 전달할 수 없습니다. 선택적 인수를 생략할 수 있습니다.  
  
매개 변수 배열을 이름으로 전달할 수 없습니다. 프로시저를 호출 하면 불특정 개수의 매개 변수 배열에 대 한 쉼표로 구분 된 인수를 제공 하 고 컴파일러가 단일 이름으로 둘 이상의 인수를 연결할 수 없습니다 때문입니다.  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [방법: 프로시저에 인수 전달](./how-to-pass-arguments-to-a-procedure.md)
- [값 또는 참조로 인수 전달](./passing-arguments-by-value-and-by-reference.md)
- [선택적 매개 변수](./optional-parameters.md)
- [매개 변수 배열](./parameter-arrays.md)
- [선택 사항](../../../../visual-basic/language-reference/modifiers/optional.md)
- [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)
