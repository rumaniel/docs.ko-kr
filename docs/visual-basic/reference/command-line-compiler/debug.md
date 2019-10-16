---
title: /debug(Visual Basic)
ms.date: 03/10/2018
helpviewer_keywords:
- debug compiler switches
- /debug compiler option [Visual Basic]
- -debug compiler option [Visual Basic]
- debug compiler option [Visual Basic]
ms.assetid: c2b0bea5-1d5e-499f-9bd5-4f6c6b715ea2
ms.openlocfilehash: c2fbe5aa6f0b9ac8c99c9b9ec5cdf0a7d9764ab8
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002398"
---
# <a name="-debug-visual-basic"></a>-debug (Visual Basic)
컴파일러가 디버깅 정보를 생성 하 여 출력 파일에 넣습니다.  
  
## <a name="syntax"></a>구문  
  
```console 
-debug[+ | -]  
```

로 구분하거나 여러

```console  
-debug:[full | pdbonly]  
```
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`+` &#124; `-`|(선택 사항) @No__t-0 또는 `/debug`을 지정 하면 컴파일러에서 디버깅 정보를 생성 하 여 .pdb 파일에 저장 합니다. @No__t-0을 지정 하면 `/debug`을 지정 하지 않는 것과 동일한 효과가 있습니다.|  
|`full` &#124; `pdbonly`|(선택 사항) 컴파일러에서 생성되는 디버깅 정보 형식을 지정합니다. @No__t-0을 지정 하지 않으면 기본값은 `full` 이며,이를 통해 실행 중인 프로그램에 디버거를 연결할 수 있습니다. @No__t-0 인수를 사용 하면 디버거에서 프로그램이 시작 될 때 소스 코드 디버깅이 가능 하지만, 실행 중인 프로그램이 디버거에 연결 되어 있는 경우에만 어셈블리 언어 코드가 표시 됩니다.|  
  
## <a name="remarks"></a>설명  
 디버그 빌드를 만들려면 이 옵션을 사용합니다. @No__t-0, `/debug+` 또는 `/debug:full`를 지정 하지 않으면 프로그램의 출력 파일을 디버그할 수 없습니다.  
  
 기본적으로 디버깅 정보는 내보내지 않습니다 (`/debug-`). 디버깅 정보를 내보내려면 `/debug` 또는 `/debug+`을 지정 합니다.  
  
 애플리케이션의 디버그 성능을 구성하는 방법에 대한 자세한 내용은 [쉽게 디버깅할 수 있도록 이미지 만들기](../../../framework/debug-trace-profile/making-an-image-easier-to-debug.md)를 참조하세요.  
  
|Visual Studio 통합 개발 환경에서-debug를 설정 하려면|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택한 상태에서 **프로젝트** 메뉴에서 **속성**을 클릭합니다. <br />2.  **컴파일** 탭을 클릭합니다.<br />3.  **고급 컴파일 옵션**을 클릭합니다.<br />4.  **디버그 정보 생성** 상자에서 값을 수정 합니다.|  
  
## <a name="example"></a>예제  
 다음 예제에서는 출력 파일 `App.exe`에 디버깅 정보를 저장 합니다.  
  
```console  
vbc -debug -out:app.exe test.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
