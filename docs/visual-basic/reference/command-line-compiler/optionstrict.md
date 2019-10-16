---
title: -optionstrict
ms.date: 07/20/2015
f1_keywords:
- -optionstrict
helpviewer_keywords:
- -optionstrict compiler option [Visual Basic]
- optionstrict compiler option [Visual Basic]
- /optionstrict compiler option [Visual Basic]
ms.assetid: c7b10086-0fa4-49db-b3c8-4ae0db5957da
ms.openlocfilehash: 6d281fe07754f0471f8d6c0e31cf3ea890060504
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005341"
---
# <a name="-optionstrict"></a>-optionstrict
엄격한 형식 의미 체계를 적용 하 여 암시적 형식 변환을 제한 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-optionstrict[+ | -]  
-optionstrict[:custom]  
```  
  
## <a name="arguments"></a>인수  
 `+` &#124; `-`  
 (선택 사항) @No__t-0 옵션은 암시적 형식 변환을 제한 합니다. 이 옵션의 기본값은 `-optionstrict-`입니다. @No__t-0 옵션은 `-optionstrict`과 같습니다. 관대 한 형식 의미 체계에 대해 둘 다 사용할 수 있습니다.  
  
 `custom`  
 필수. 엄격한 언어 의미 체계를 준수 하지 않을 때 경고 합니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0이 적용 되 면 확장 형식 변환만 암시적으로 수행 될 수 있습니다. 정수 형식 개체에 `Decimal` 형식 개체를 할당 하는 등의 암시적 축소 형식 변환은 오류로 보고 됩니다.  
  
 암시적 축소 형식 변환에 대 한 경고를 생성 하려면 `-optionstrict:custom`을 사용 합니다. @No__t-0을 사용 하 여 특정 경고를 무시 하 고-1 @no__t 하 여 특정 경고를 오류로 처리 합니다.  
  
### <a name="to-set--optionstrict-in-the-visual-studio-ide"></a>Visual Studio IDE에서-option strict를 설정 하려면  
  
1. **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 속성을 클릭 **합니다.**   
  
2. **컴파일** 탭을 클릭합니다.  
  
3. **Option Strict** 상자에서 값을 수정 합니다.  
  
### <a name="to-set--optionstrict-programmatically"></a>프로그래밍 방식으로-option strict 설정  
  
- [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)을 참조 하십시오.  
  
## <a name="example"></a>예제  
 다음 코드는 엄격한 형식 의미 체계를 사용 하 여 `Test.vb`을 컴파일합니다.  
  
```console
vbc -optionstrict+ test.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)
- [-optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)
- [-optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)
- [-nowarn](../../../visual-basic/reference/command-line-compiler/nowarn.md)
- [-warnaserror (Visual Basic)](../../../visual-basic/reference/command-line-compiler/warnaserror.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [옵션 대화 상자, 프로젝트, Visual Basic 기본값](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
