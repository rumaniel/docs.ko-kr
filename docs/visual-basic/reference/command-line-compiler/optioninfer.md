---
title: -optioninfer
ms.date: 07/20/2015
f1_keywords:
- -optioninfer
helpviewer_keywords:
- -optioninfer compiler option [Visual Basic]
- /optioninfer compiler option [Visual Basic]
- optioninfer compiler option [Visual Basic]
ms.assetid: f6c09db1-0553-464a-abe3-d4510c61d6ed
ms.openlocfilehash: c6fc7e9dcfbce938ad75b0f357c2bfa9cd10703a
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005317"
---
# <a name="-optioninfer"></a>-optioninfer
변수 선언에서 지역 형식 유추를 사용하도록 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-optioninfer[+ | -]  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`+` &#124; `-`|(선택 사항) 지역 형식 유추를 사용하도록 설정하려면 `-optioninfer+`를 지정하고, 차단하려면 `-optioninfer-`를 지정합니다. 값을 지정하지 않은 `-optioninfer` 옵션은 `-optioninfer+`와 같습니다. `-optioninfer` 스위치가 없을 때의 기본값도 `-optioninfer+`입니다. 기본값은 vbc.rsp 지시 파일에서 설정됩니다.|  
  
> [!NOTE]
> `-noconfig` 옵션을 사용하여 vbc.rsp에 지정된 값 대신 컴파일러의 내부 기본값을 유지할 수 있습니다. 이 옵션에 대한 컴파일러 기본값은 `-optioninfer-`입니다.  
  
## <a name="remarks"></a>설명  
 소스 코드 파일에 [유추할 문이](../../../visual-basic/language-reference/statements/option-infer-statement.md)포함 된 경우 문은 `-optioninfer` 명령줄 컴파일러 설정을 재정의 합니다.  
  
### <a name="to-set--optioninfer-in-the-visual-studio-ide"></a>Visual Studio IDE에서을 설정 하려면  
  
1. **솔루션 탐색기**에서 프로젝트를 선택 합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다.  
  
2. **컴파일** 탭의 **유추 옵션** 상자에서 값을 수정 합니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 지역 형식 유추를 사용하도록 설정한 상태로 `test.vb`를 컴파일합니다.  
  
```console
vbc -optioninfer+ test.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)
- [-optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)
- [-optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Option Infer 문](../../../visual-basic/language-reference/statements/option-infer-statement.md)
- [지역 형식 유추](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [옵션 대화 상자, 프로젝트, Visual Basic 기본값](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
- [프로젝트 디자이너, 컴파일 페이지(Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
- [/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)
- [명령줄에서 빌드](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)
