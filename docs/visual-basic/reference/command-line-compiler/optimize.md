---
title: -optimize
ms.date: 07/20/2015
helpviewer_keywords:
- optimize compiler option [Visual Basic]
- /optimize compiler option [Visual Basic]
- optimization [Visual Basic], enabling
- -optimize compiler option [Visual Basic]
ms.assetid: fcba4a97-3622-4b87-a891-0f77deab4998
ms.openlocfilehash: e8daf4a49123623b6470bc3c6281869f1b9b3d0f
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005375"
---
# <a name="-optimize"></a>-optimize
컴파일러 최적화를 사용 하거나 사용 하지 않도록 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-optimize[ + | - ]  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`+` &#124; `-`|(선택 사항) @No__t-0 옵션은 컴파일러 최적화를 사용 하지 않도록 설정 합니다. @No__t-0 옵션은 최적화를 사용 하도록 설정 합니다. 최적화는 기본적으로 사용되지 않습니다.|  
  
## <a name="remarks"></a>설명  
 컴파일러 최적화를 통해 더 작지만 빠르고 효율적인 출력 파일을 만듭니다. 그러나 최적화를 수행 하면 출력 파일에서 코드가 재배치 되기 때문에 `-optimize+`을 사용 하면 디버깅이 어려워질 수 있습니다.  
  
 어셈블리에 대해 `-target:module`으로 생성 된 모든 모듈은 어셈블리와 동일한 `-optimize` 설정을 사용 해야 합니다. 자세한 내용은 [-target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)을 참조 하세요.  
  
 @No__t-0 및 `-debug` 옵션을 결합할 수 있습니다.  
  
|Visual Studio 통합 개발 환경에서을 설정 하려면|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다.<br />     <br />2.  **컴파일** 탭을 클릭합니다.<br />3.  **고급** 단추를 클릭합니다.<br />4.  **최적화 사용** 확인란을 수정 합니다.|  
  
## <a name="example"></a>예제  
 다음 코드는-0 @no__t 컴파일하고 컴파일러 최적화를 사용 하도록 설정 합니다.  
  
```console
vbc t2.vb -optimize  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-debug (Visual Basic)](../../../visual-basic/reference/command-line-compiler/debug.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [-target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)
