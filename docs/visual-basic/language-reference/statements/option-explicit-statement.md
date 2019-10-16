---
title: Option Explicit 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Explicit
- vb.OptionExplicit
helpviewer_keywords:
- declaring variables [Visual Basic], explicit
- forced variable declaration in Option Explicit statement [Visual Basic]
- Explicit keyword
- explicit variable declaration
- Option Explicit statement [Visual Basic]
ms.assetid: e82ac1ad-2cd3-49b2-b985-8bcf016f3fcc
ms.openlocfilehash: c027964d185d7f69c0a56a4386bedc2d8f9d2eac
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912332"
---
# <a name="option-explicit-statement-visual-basic"></a>Option Explicit 문(Visual Basic)
파일의 모든 변수를 명시적으로 선언 하거나 변수의 암시적 선언을 허용 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
Option Explicit { On | Off }  
```  
  
## <a name="parts"></a>요소  
 `On`  
 선택 사항입니다. 검사 `Option Explicit` 를 사용 하도록 설정 합니다. 또는를 지정 하지 않으면 기본값은 입니다.`On` `Off` `On`  
  
 `Off`  
 선택 사항입니다. 검사 `Option Explicit` 를 사용 하지 않습니다.  
  
## <a name="remarks"></a>설명  
 파일이 파일에 `Option Explicit On` `Dim` 표시 되 면 또는 `ReDim` 문을 사용 하 여 모든 변수를 명시적으로 선언 해야 합니다. `Option Explicit` 선언 되지 않은 변수 이름을 사용 하려고 하면 컴파일 타임에 오류가 발생 합니다. `Option Explicit Off` 문은 변수를 암시적으로 선언할 수 있습니다.  
  
 `Option Explicit` 문은 사용하는 경우 파일에서 다른 소스 코드 문 앞에 나와야 합니다.  
  
> [!NOTE]
> 일반적 `Option Explicit` 으로 `Off` 로 설정 하는 것은 좋은 방법이 아닙니다. 하나 이상의 위치에서 변수 이름을 잘못 입력할 수 있습니다. 그러면 프로그램이 실행될 때 예기치 않은 결과가 발생할 수 있습니다.  
  
## <a name="when-an-option-explicit-statement-is-not-present"></a>Option Explicit 문이 없는 경우  
 소스 코드에 `Option Explicit` 문이 포함 되어 있지 않은 경우에는 [컴파일 페이지, 프로젝트 디자이너 (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic) 에 대 한 **Option Explicit** 설정이 사용 됩니다. 명령줄 컴파일러를 사용 하는 경우 [/chexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md) 컴파일러 옵션이 사용 됩니다.  
  
#### <a name="to-set-option-explicit-in-the-ide"></a>IDE에서 Option Explicit를 설정 하려면  
  
1. **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다.  
  
2. **컴파일** 탭을 클릭합니다.  
  
3. **옵션 Explicit** 상자에서 값을 설정 합니다.  
  
 새 프로젝트를 만들 때 **컴파일** 탭의 **옵션 Explicit** 설정은 **VB 기본값** 대화 상자의 **옵션 explicit** 설정으로 설정 됩니다. **VB 기본값** 대화 상자에 액세스 하려면 **도구** 메뉴에서 **옵션**을 클릭 합니다. **옵션** 대화 상자에서 **프로젝트 및 솔루션**을 확장하고 **VB 기본값**을 클릭합니다. **VB 기본값** `On`의 초기 기본 설정은입니다.  
  
#### <a name="to-set-option-explicit-on-the-command-line"></a>명령줄에서 Option Explicit를 설정 하려면  
  
- **Vbc** 명령에 [/pronameexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md) 컴파일러 옵션을 포함 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `Option Explicit` 문을 사용 하 여 모든 변수를 명시적으로 선언 합니다. 선언 되지 않은 변수를 사용 하려고 하면 컴파일 타임에 오류가 발생 합니다.  
  
 [!code-vb[VbVbalrStatements#47](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#47)]  
  
 [!code-vb[VbVbalrStatements#48](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class2.vb#48)]  
  
## <a name="see-also"></a>참고자료

- [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)
- [ReDim 문](../../../visual-basic/language-reference/statements/redim-statement.md)
- [Option Compare 문](../../../visual-basic/language-reference/statements/option-compare-statement.md)
- [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)
- [/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)
- [/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)
- [옵션 대화 상자, 프로젝트, Visual Basic 기본값](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
