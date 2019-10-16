---
title: -doc
ms.date: 03/10/2018
helpviewer_keywords:
- doc compiler option [Visual Basic]
- -doc compiler option [Visual Basic]
- /doc compiler option [Visual Basic]
ms.assetid: 5fc32ec9-a149-4648-994c-a8d0cccd0a65
ms.openlocfilehash: 3da049b912d791f26814bb4b6cbb70998803726a
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005640"
---
# <a name="-doc"></a>-doc
XML 파일에 대해 문서 주석을 처리합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-doc[+ | -]  
```

로 구분하거나 여러  

```console
-doc:file  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`+` &#124; `-`|(선택 사항) \+ 또는 `-doc`만 지정하면 컴파일러가 문서 정보를 생성하여 XML 파일에 넣습니다. `-`를 지정하면 `-doc`를 지정하지 않는 것과 같으며, 문서 정보를 생성하지 않게 합니다.|  
|`file`|`-doc:`를 사용하는 경우 필수입니다. 출력 XML 파일을 지정하며, 이 파일은 컴파일의 소스 코드 파일에 있는 주석으로 채워집니다. 파일 이름에 공백이 있으면 이름을 따옴표(“ ”)로 묶습니다.|  
  
## <a name="remarks"></a>설명  
 `-doc` 옵션은 컴파일러가 문서 주석을 포함하는 XML 파일을 생성하는지 여부를 제어합니다. `-doc:file` 구문을 사용하는 경우 `file` 매개 변수에서 XML 파일 이름을 지정합니다. `-doc` 또는 `-doc+`를 사용하는 경우 컴파일러는 컴파일러가 생성하는 실행 파일 또는 라이브러리에서 XML 파일 이름을 가져옵니다. `-doc-`를 사용하거나 `-doc` 옵션을 지정하지 않는 경우 컴파일러는 XML 파일을 생성하지 않습니다.  
  
 소스 코드 파일에서 문서 주석은 다음 정의보다 앞에 올 수 있습니다.  
  
- [class](../../../visual-basic/language-reference/statements/class-statement.md) 또는 [interface](../../../visual-basic/language-reference/statements/interface-statement.md) 같은 사용자 정의 형식  
  
- field, [event](../../../visual-basic/language-reference/statements/event-statement.md), [property](../../../visual-basic/language-reference/statements/property-statement.md), [function](../../../visual-basic/language-reference/statements/function-statement.md) 또는 [subroutine](../../../visual-basic/language-reference/statements/sub-statement.md) 같은 멤버  
  
 Visual Studio [IntelliSense](/visualstudio/ide/using-intellisense) 기능에서 생성된 XML 파일을 사용하려면 XML 파일의 파일 이름을 지원하려는 어셈블리와 동일하게 지정할 수 있습니다. 어셈블리가 Visual Studio 프로젝트에서 참조되면 .xml 파일도 검색되도록 XML 파일이 어셈블리와 동일한 디렉터리에 있는지 확인합니다. IntelliSense에서 프로젝트 내의 코드나 프로젝트에서 참조하는 프로젝트 내의 코드를 작업하는 데는 XML 문서 파일이 필요하지 않습니다.  
  
 `/target:module`로 컴파일하는 경우 외에는 XML 파일에 `<assembly></assembly>` 태그가 포함됩니다. 이러한 태그는 컴파일 출력 파일의 어셈블리 매니페스트를 포함하는 파일의 이름을 지정합니다.  
  
 코드의 주석에서 문서를 생성하는 방법은 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/index.md)(XML 주석 태그)를 참조하세요.  
  
|Visual Studio 통합 개발 환경에서 -doc를 설정하려면|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다. <br />2.  **컴파일** 탭을 클릭합니다.<br />3.  **XML 문서 파일 생성** 상자에 값을 설정합니다.|  
  
## <a name="example"></a>예제  
 샘플은 [Documenting Your Code with XML](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)(XML과 함께 코드 문서화)을 참조하세요.  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [코드를 XML로 문서화](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)
