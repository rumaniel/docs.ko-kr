---
title: -utf8output (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- -utf8output compiler option [Visual Basic]
- utf8output compiler option [Visual Basic]
- /utf8output compiler option [Visual Basic]
ms.assetid: 8ab36b1e-027a-49ac-85b4-f48997d9e4d6
ms.openlocfilehash: adcb518cbe8397549c3ae3b3a8ca9f0ecf9dc38e
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004664"
---
# <a name="-utf8output-visual-basic"></a>-utf8output (Visual Basic)
UTF-8 인코딩을 사용하여 컴파일러 출력을 표시합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-utf8output[+ | -]  
```  
  
## <a name="arguments"></a>인수  
 `+` &#124; `-`  
 (선택 사항) 이 옵션의 기본값은 `-utf8output-`입니다. 즉, 컴파일러 출력에서 UTF-8 인코딩을 사용 하지 않습니다. `-utf8output`를 지정하는 것은 `-utf8output+`를 지정하는 것과 같습니다.  
  
## <a name="remarks"></a>설명  
 일부 국가별 구성에서는 컴파일러 출력이 콘솔에 올바르게 표시 되지 않습니다. 이 경우 `-utf8output`을 사용 하 고 컴파일러 출력을 파일로 리디렉션합니다.  
  
> [!NOTE]
> @No__t-0 옵션은 Visual Studio 개발 환경에서 사용할 수 없습니다. 명령줄에서 컴파일하는 경우에만 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 코드는-0 @no__t 컴파일하고 UTF-8 인코딩을 사용 하 여 출력을 표시 하도록 컴파일러에 지시 합니다.  
  
```console  
vbc -utf8output in.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
