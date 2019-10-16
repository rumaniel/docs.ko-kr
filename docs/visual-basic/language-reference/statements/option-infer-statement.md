---
title: Option 유추 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.OptionInfer
- vb.Infer
helpviewer_keywords:
- variables [Visual Basic], declaring
- Option Infer statement [Visual Basic]
- Infer keyword [Visual Basic]
- declaring variables [Visual Basic], inferred
- inferred variable declaration
ms.assetid: 4ad3e6e9-8f5b-4209-a248-de22ef6e4652
ms.openlocfilehash: e7f5fcc6d76f654f53eea6677962cb097e98b881
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912308"
---
# <a name="option-infer-statement"></a>Option Infer 문
변수를 선언할 때 지역 형식 유추를 사용하도록 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
Option Infer { On | Off }  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`On`|선택 사항입니다. 지역 형식 유추를 사용하도록 설정합니다.|  
|`Off`|선택 사항입니다. 지역 형식 유추를 사용하지 않도록 설정합니다.|  
  
## <a name="remarks"></a>설명  
 파일에서 `Option Infer`를 설정하려면 파일 맨 위(기타 모든 소스 코드 앞)에 `Option Infer On` 또는 `Option Infer Off`를 입력합니다. 파일에서 `Option Infer`에 대해 설정된 값이 IDE 또는 명령줄에 설정된 값과 충돌하는 경우에는 파일의 값이 우선적으로 적용됩니다.  
  
 `Option Infer`를 `On`으로 설정하면 데이터 형식을 명시적으로 설명하지 않고 로컬 변수를 선언할 수 있습니다. 컴파일러는 초기화 식의 형식에서 변수의 데이터 형식을 유추합니다.  
  
 다음 그림에서는 `Option Infer`가 설정되어 있습니다. `Dim someVar = 2` 선언의 변수는 형식 유추에 의해 정수로 선언됩니다.

 다음 스크린샷은 추론 옵션이 설정 된 경우 IntelliSense를 보여 줍니다. 
  
 ![옵션 추론을 on으로 설정 하는 경우 IntelliSense 보기를 보여 주는 스크린샷](./media/option-infer-statement/option-infer-as-integer-on.png)  
  
 다음 그림에서는 `Option Infer`가 해제되어 있습니다. `Dim someVar = 2` 선언의 변수는 형식 유추에 의해 `Object`로 선언됩니다. 이 예제에서 **Option Strict** 설정은 [컴파일 페이지, 프로젝트 디자이너 (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)에서 **Off** 로 설정 됩니다.  
  
 다음 스크린샷은 추론 옵션이 해제 된 경우 IntelliSense를 보여 줍니다.
 
 ![옵션 추론을 해제 한 경우 IntelliSense 보기를 보여 주는 스크린샷](./media/option-infer-statement/option-infer-as-object-off.png)  
  
> [!NOTE]
> 변수가 `Object`로 선언되면 프로그램을 실행하는 동안 런타임 형식이 변경될 수 있습니다. Visual Basic는 `Object` *boxing* 및 unboxing 작업을 수행 하 여와 값 형식 간에 변환 하는 작업을 수행 하므로 실행 속도가 느려집니다. Boxing 및 unboxing에 대 한 자세한 내용은 [Visual Basic 언어 사양](~/_vblang/spec/conversions.md#value-type-conversions)을 참조 하세요.
  
 형식 유추는 프로시저 수준에서 적용되며 클래스, 구조체, 모듈 또는 인터페이스의 프로시저 외부에는 적용되지 않습니다.  
  
 자세한 내용은 [지역 형식 유추](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)를 참조 하세요.  
  
## <a name="when-an-option-infer-statement-is-not-present"></a>Option Infer 문이 없는 경우  
 소스 코드에 `Option Infer` 문이 포함 되어 있지 않으면 컴파일 페이지에서 설정 **유추 옵션이** 사용 됩니다 [(Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic) . 명령줄 컴파일러를 사용 하는 경우 [/shles](../../../visual-basic/reference/command-line-compiler/optioninfer.md) 컴파일러 옵션이 사용 됩니다.  
  
#### <a name="to-set-option-infer-in-the-ide"></a>IDE에서 Option Infer를 설정하려면  
  
1. **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다.  
  
2. **컴파일** 탭을 클릭합니다.  
  
3. **유추 옵션** 상자에서 값을 설정 합니다.  
  
 새 프로젝트를 만들 때 **컴파일** 탭의 **유추 설정 옵션이** **VB 기본값** 대화 상자의 **유추 옵션** 으로 설정 됩니다. **VB 기본값** 대화 상자에 액세스 하려면 **도구** 메뉴에서 **옵션**을 클릭 합니다. **옵션** 대화 상자에서 **프로젝트 및 솔루션**을 확장하고 **VB 기본값**을 클릭합니다. **VB 기본값** `On`의 초기 기본 설정은입니다.  
  
#### <a name="to-set-option-infer-on-the-command-line"></a>명령줄에서 Option Infer를 설정하려면  
  
- **Vbc** 명령에 [/chleerles](../../../visual-basic/reference/command-line-compiler/optioninfer.md) 옵션을 포함 합니다.  
  
## <a name="default-data-types-and-values"></a>기본 데이터 형식 및 값  
 다음 테이블에는 `Dim` 문에서 데이터 형식과 이니셜라이저를 지정하는 다양한 조합의 결과에 대한 설명이 나와 있습니다.  
  
|데이터 형식 지정 여부|이니셜라이저 지정 여부|예제|결과|  
|---|---|---|---|  
|아니요|아니요|`Dim qty`|`Option Strict`가 off(기본값)이면 변수는 `Nothing`으로 설정됩니다.<br /><br /> `Option Strict`가 on이면 컴파일 시간 오류가 발생합니다.|  
|아니요|예|`Dim qty = 5`|`Option Infer`가 on(기본값)이면 변수가 이니셜라이저의 데이터 형식을 사용합니다. [지역 형식 유추](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)를 참조 하세요.<br /><br /> `Option Infer`가 off이고 `Option Strict`고 off이면 변수가 `Object`의 데이터 형식을 사용합니다.<br /><br /> `Option Infer`가 off이고 `Option Strict`는 on이면 컴파일 시간 오류가 발생합니다.|  
|예|아니요|`Dim qty As Integer`|변수는 데이터 형식의 기본값으로 초기화됩니다. 자세한 내용은 [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)을 참조 하세요.|  
|예|예|`Dim qty  As Integer = 5`|이니셜라이저의 데이터 형식을 지정한 데이터 형식으로 변환할 수 없으면 컴파일 시간 오류가 발생합니다.|  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Option Infer` 문이 지역 형식 유추를 사용하도록 설정하는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrTypeInference#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#6)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 변수가 `Object`로 식별되는 경우 런타임 형식이 달라질 수 있음을 보여 줍니다.  
  
 [!code-vb[VbVbalrTypeInference#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#11)]  
  
## <a name="see-also"></a>참고자료

- [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)
- [지역 형식 유추](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [Option Compare 문](../../../visual-basic/language-reference/statements/option-compare-statement.md)
- [Option Explicit 문](../../../visual-basic/language-reference/statements/option-explicit-statement.md)
- [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [옵션 대화 상자, 프로젝트, Visual Basic 기본값](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
- [/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)
- [boxing 및 unboxing](../../../csharp/programming-guide/types/boxing-and-unboxing.md)
