---
title: -optioncompare
ms.date: 07/20/2015
f1_keywords:
- /optioncompare
- -optioncompare
helpviewer_keywords:
- optioncompare compiler option [Visual Basic]
- -optioncompare compiler option [Visual Basic]
- /optioncompare compiler option [Visual Basic]
ms.assetid: 7237b766-b44d-4cc5-9a3c-885348a7d9e4
ms.openlocfilehash: ee130073b95dfbab5616a54c188b09fa92ccc930
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005355"
---
# <a name="-optioncompare"></a>-optioncompare
문자열 비교 방법을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-optioncompare:{binary | text}  
```  
  
## <a name="remarks"></a>설명  
 두 가지 형식 중 하나에 `-optioncompare`을 지정할 수 있습니다. @no__t는 이진 문자열 비교를 사용 하 고, `-optioncompare:text`는 텍스트 문자열 비교를 사용 합니다. 기본적으로 컴파일러는 `-optioncompare:binary`을 사용 합니다.  
  
 Microsoft Windows에서 현재 코드 페이지는 이진 정렬 순서를 결정 합니다. 일반적인 이진 정렬 순서는 다음과 같습니다.  
  
 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`  
  
 텍스트 기반 문자열 비교는 시스템의 로캘에서 결정 되는 대/소문자를 구분 하지 않는 텍스트 정렬 순서를 기반으로 합니다. 일반적인 텍스트 정렬 순서는 다음과 같습니다.  
  
 `(A = a) < (À = à) < (B=b) < (E=e) < (Ê = ê) < (Z=z) < (Ø = ø)`  
  
### <a name="to-set--optioncompare-in-the-visual-studio-ide"></a>Visual Studio IDE에서-기능 비교를 설정 하려면  
  
1. **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다.   
  
2. **컴파일** 탭을 클릭합니다.  
  
3. **옵션 비교** 상자에서 값을 수정 합니다.  
  
### <a name="to-set--optioncompare-programmatically"></a>프로그래밍 방식으로 설정 하려면  
  
- [Option Compare 문](../../../visual-basic/language-reference/statements/option-compare-statement.md)을 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 코드는-0 @no__t 컴파일하고 이진 문자열 비교를 사용 합니다.  
  
```console
vbc -optioncompare:binary projFile.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)
- [-optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)
- [-optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Option Compare 문](../../../visual-basic/language-reference/statements/option-compare-statement.md)
- [옵션 대화 상자, 프로젝트, Visual Basic 기본값](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
