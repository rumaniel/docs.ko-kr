---
title: -optionexplicit
ms.date: 07/20/2015
f1_keywords:
- /optionexplicit
- -optionexplicit
helpviewer_keywords:
- /optionexplicit compiler option [Visual Basic]
- optionexplicit compiler option [Visual Basic]
- -optionexplicit compiler option [Visual Basic]
ms.assetid: 5d296ab3-bafe-4c4d-9887-78f162ed86c7
ms.openlocfilehash: 5c0946b94bfe02d797d1a484088869375703eb6a
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005314"
---
# <a name="-optionexplicit"></a>-optionexplicit
변수가 사용 되기 전에 선언 되지 않은 경우 컴파일러가 오류를 보고 하도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-optionexplicit[+ | -]  
```  
  
## <a name="arguments"></a>인수  
 `+` &#124; `-`  
 (선택 사항) 명시적 변수 선언이 필요 하면 `-optionexplicit+`을 지정 합니다. @No__t-0 옵션이 기본값이 며 `-optionexplicit`과 동일 합니다. @No__t-0 옵션은 변수의 암시적 선언을 가능 하 게 합니다.  
  
## <a name="remarks"></a>설명  
 소스 코드 파일에 [Option Explicit 문이](../../../visual-basic/language-reference/statements/option-explicit-statement.md)포함 되어 있으면 문이 `-optionexplicit` 명령줄 컴파일러 설정을 재정의 합니다.  
  
### <a name="to-set--optionexplicit-in-the-visual-studio-ide"></a>Visual Studio IDE에서-기능을 명시적으로 설정 하려면  
  
1. **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다.   
  
2. **컴파일** 탭을 클릭합니다.  
  
3. **옵션 Explicit** 상자에서 값을 수정 합니다.  
  
## <a name="example"></a>예제  
 다음 코드는 `-optionexplicit-`이 사용 될 때 컴파일됩니다.  
  
 [!code-vb[VbVbalrCompiler#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/OptionExplicitOff.vb#5)]  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)
- [-optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)
- [-optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Option Explicit 문](../../../visual-basic/language-reference/statements/option-explicit-statement.md)
- [옵션 대화 상자, 프로젝트, Visual Basic 기본값](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
