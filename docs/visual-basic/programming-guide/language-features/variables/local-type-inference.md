---
title: 지역 형식 유추(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- local type inference
- vb.TypeInfer
helpviewer_keywords:
- Option Infer statement [Visual Basic]
- local type inference [Visual Basic]
- implicitly-typed local variables [Visual Basic]
- variables [Visual Basic], type inference
- inference [Visual Basic]
- type inference [Visual Basic]
ms.assetid: b8307f18-2e56-4ab3-a45a-826873f400f6
ms.openlocfilehash: 59559f8775a5fd66a567897b009272df1727b1e8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69953326"
---
# <a name="local-type-inference-visual-basic"></a>지역 형식 유추(Visual Basic)
Visual Basic 컴파일러는 *형식 유추* 를 사용 하 여 `As` 절 없이 선언 된 지역 변수의 데이터 형식을 확인 합니다. 컴파일러는 초기화 식의 형식에서 변수 형식을 유추 합니다. 이렇게 하면 다음 예제와 같이 형식을 명시적으로 명시 하지 않고 변수를 선언할 수 있습니다. 선언 결과로 및는 모두 `num1` 정수로 강력 하 `num2` 게 형식화 됩니다.  
  
 [!code-vb[VbVbalrTypeInference#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#1)]  
 
> [!NOTE]
> 이전 예제 `num2` 에서 `Integer`로 형식화 하지 않으려는 경우 또는 `Dim num4 As Double = 3`와 같은 `Dim num3 As Object = 3` 선언을 사용 하 여 다른 형식을 지정할 수 있습니다.  

> [!NOTE]
> 형식 유추는 비정적 지역 변수에만 사용할 수 있습니다. 클래스 필드, 속성 또는 함수의 형식을 결정 하는 데 사용할 수 없습니다.
 
 지역 형식 유추는 프로시저 수준에서 적용 됩니다. 모듈 수준에서 변수를 선언 하는 데 사용할 수 없습니다 (클래스, 구조체, 모듈 또는 인터페이스 내에서 프로시저나 블록 내에서 제외). 이전 `num2` 예제에서 프로시저의 지역 변수가 아닌 클래스의 필드인 경우 선언으로 인해 `Option Strict` 에 오류가 발생 `Object` 하 고가 `Option Strict` off로 분류 `num2` 됩니다. 마찬가지로 지역 형식 유추는로 `Static`선언 된 프로시저 수준 변수에는 적용 되지 않습니다.  
  
## <a name="type-inference-vs-late-binding"></a>형식 유추 및 런타임에 바인딩  
 형식 유추를 사용 하는 코드는 런타임에 바인딩을 사용 하는 코드와 비슷합니다. 그러나 형식 유추는 변수를 그대로 유지 `Object`하는 대신 강력한 형식을 갖습니다. 컴파일러는 변수의 이니셜라이저를 사용 하 여 컴파일 시간에 변수의 형식을 확인 하 여 초기 바인딩된 코드를 생성 합니다. 이전 예제 `num2`에서와 마찬가지로 `num1`는로 `Integer`형식화 됩니다.  
  
 초기 바인딩된 변수의 동작은 런타임에 바인딩된 변수의 동작과 다르며이는 런타임에만 형식을 알 수 있습니다. 초기 형식을 알면 컴파일러가 실행 전에 문제를 식별 하 고, 메모리를 정확 하 게 할당 하 고, 기타 최적화를 수행할 수 있습니다. 또한 초기 바인딩을 사용 하면 Visual Basic IDE (통합 개발 환경)에서 개체의 멤버에 대 한 IntelliSense 도움말을 제공할 수 있습니다. 성능에 대 한 초기 바인딩도 선호 됩니다. 이는 런타임에 바인딩된 변수에 저장 된 모든 데이터를 형식 `Object`으로 래핑해야 하 고 런타임에 형식의 멤버에 액세스 하는 것 때문입니다.  
  
## <a name="examples"></a>예  
 형식 유추는 지역 변수가 `As` 절 없이 선언 되 고 초기화 될 때 발생 합니다. 컴파일러는 할당 된 초기 값의 형식을 변수 형식으로 사용 합니다. 예를 들어 다음 코드 줄은 각각 형식의 `String`변수를 선언 합니다.  
  
 [!code-vb[VbVbalrTypeInference#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#2)]  
  
 다음 코드에서는 두 가지 동일한 방법으로 정수 배열을 만드는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrTypeInference#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#3)]  
  
 형식 유추를 사용 하 여 루프 제어 변수의 형식을 결정 하는 것이 편리 합니다. 다음 코드에서 컴파일러는 이전 예제에서 정수 `number` 배열 `Integer` 이기 때문 `someNumbers2` 에가 인 것으로 유추 합니다.  
  
 [!code-vb[VbVbalrTypeInference#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#4)]  
  
 다음 예제에서 보여 주는 것 처럼 `Using` 문에서 지역 형식 유추를 사용 하 여 리소스 이름의 형식을 설정할 수 있습니다.  
  
 [!code-vb[VbVbalrTypeInference#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#7)]  
  
 다음 예제와 같이 함수의 반환 값에서 변수의 형식을 유추할 수도 있습니다. `Process.GetProcesses` 및 `pList1` 는모두프로세스의배열을반환하기때문에프로세스의배열입니다.`pList2`  
  
 [!code-vb[VbVbalrTypeInference#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#5)]  
  
## <a name="option-infer"></a>옵션 유추  
 `Option Infer`특정 파일에서 로컬 형식 유추가 허용 되는지 여부를 지정할 수 있습니다. 옵션을 사용 하도록 설정 하거나 차단 하려면 파일의 시작 부분에 다음 문 중 하나를 입력 합니다.  
  
 `Option Infer On`  
  
 `Option Infer Off`  
  
 코드 `Option Infer` 에 값을 지정 하지 않으면 컴파일러 기본값은 `Option Infer On`입니다. 
  
 파일에서 `Option Infer`에 대해 설정된 값이 IDE 또는 명령줄에 설정된 값과 충돌하는 경우에는 파일의 값이 우선적으로 적용됩니다.  
  
 자세한 내용은 [Option 유추 문](../../../../visual-basic/language-reference/statements/option-infer-statement.md) 및 [컴파일 페이지, 프로젝트 디자이너 (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [초기 바인딩 및 런타임에 바인딩](../../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)
- [For Each...Next 문](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)
- [For...Next 문](../../../../visual-basic/language-reference/statements/for-next-statement.md)
- [Option Infer 문](../../../../visual-basic/language-reference/statements/option-infer-statement.md)
- [/optioninfer](../../../../visual-basic/reference/command-line-compiler/optioninfer.md)
- [Visual Basic의 LINQ 소개](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
