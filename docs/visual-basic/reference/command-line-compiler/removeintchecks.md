---
title: -removeintchecks
ms.date: 03/13/2018
f1_keywords:
- removeintchecks
- -removeintchecks
helpviewer_keywords:
- removeintchecks compiler option [Visual Basic]
- /removeintchecks compiler option [Visual Basic]
- -removeintchecks compiler option [Visual Basic]
ms.assetid: c1835bd5-1e38-4fba-bd2f-6984774765d4
ms.openlocfilehash: bea6ca24ea6da9000267e754d52fe0ca152f7d7f
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005232"
---
# <a name="-removeintchecks"></a>-removeintchecks
정수 연산에 대해 오버플로 오류 검사를 설정 하거나 해제 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-removeintchecks[+ | -]  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`+` &#124; `-`|(선택 사항) @No__t-0 옵션을 설정 하면 컴파일러가 오버플로 오류에 대 한 모든 정수 계산을 검사 합니다. 기본값은 `-removeintchecks-`입니다.<br /><br /> @No__t-0 또는 `-removeintchecks+`을 지정 하면 오류 검사를 수행 하지 않으며 정수 계산을 더 빠르게 수행할 수 있습니다. 그러나 오류 검사를 수행 하지 않고 데이터 형식 용량이 오버플로 되는 경우 오류를 발생 시 키 지 않고 잘못 된 결과가 저장 될 수 있습니다.|  
  
|Visual Studio 통합 개발 환경에서-removeintchecks를 설정 하려면|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다. <br />2.  **컴파일** 탭을 클릭합니다.<br />3.  **고급** 단추를 클릭합니다.<br />4.  **정수 오버플로 검사 제거** 상자의 값을 수정 합니다.|  
  
## <a name="example"></a>예제  
 다음 코드는-0 @no__t 컴파일하고 정수 오버플로 오류 검사를 해제 합니다.  
  
```console
vbc -removeintchecks+ test.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
