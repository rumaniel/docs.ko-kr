---
title: -warnaserror(Visual Basic)
ms.date: 03/13/2018
helpviewer_keywords:
- warnaserror compiler option [Visual Basic]
- /warnaserror compiler option [Visual Basic]
- -warnaserror compiler option [Visual Basic]
ms.assetid: 49819f1d-a1bd-4201-affe-5afe6d9712e1
ms.openlocfilehash: 8af6d3ef4efecd53dcf38c33d0aa2cf182f07d30
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004655"
---
# <a name="-warnaserror-visual-basic"></a>-warnaserror(Visual Basic)
컴파일러가 첫 번째 발생하는 경고를 오류로 처리하도록 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-warnaserror[+ | -][:numberList]  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|+ &#124; -|(선택 사항) 기본적으로 `-warnaserror-`가 적용됩니다. 경고가 발생해도 컴파일러가 출력 파일을 생성하지 못하도록 하지 않습니다. `-warnaserror+`와 동일한 `-warnaserror` 옵션은 경고가 오류로 처리되도록 합니다.|  
|`numberList`|(선택 사항) `-warnaserror` 옵션이 적용되는 경고 ID 번호의 쉼표로 구분된 목록입니다. 경고 ID를 지정하지 않으면 `-warnaserror` 옵션이 모든 경고에 적용됩니다.|  
  
## <a name="remarks"></a>설명  
 `-warnaserror` 옵션은 모든 경고를 오류로 처리합니다. 일반적으로 경고로 보고되는 모든 메시지가 대신 오류로 보고됩니다. 컴파일러는 이후 발생하는 같은 경고를 경고로 보고합니다.  
  
 기본적으로 `-warnaserror-`이 적용되며 경고가 정보 제공용으로만 사용되게 합니다. `-warnaserror+`와 동일한 `-warnaserror` 옵션은 경고가 오류로 처리되도록 합니다.  
  
 몇 개의 특정 경고만 오류로 처리하려는 경우 오류로 처리할 경고 번호의 쉼표로 구분된 목록을 지정할 수 있습니다.  
  
> [!NOTE]
> `-warnaserror` 옵션은 경고가 표시되는 방법을 제어하지 않습니다. 경고를 사용하지 않도록 설정하려면 [-nowarn](../../../visual-basic/reference/command-line-compiler/nowarn.md) 옵션을 사용합니다.  
  
|Visual Studio IDE에서 모든 경고를 오류로 처리하도록 -warnaserror을 설정하려면|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다. <br />2.  **컴파일** 탭을 클릭합니다.<br />3.  **모든 경고 사용 안 함** 확인란이 선택 취소되어 있는지 확인합니다.<br />4.  **모든 경고를 오류로 처리** 확인란을 선택합니다.|  
  
|Visual Studio IDE에서 특정 경고를 오류로 처리하도록 -warnaserror을 설정하려면|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다.<br />2.  **컴파일** 탭을 클릭합니다.<br />3.  **모든 경고 사용 안 함** 확인란이 선택 취소되어 있는지 확인합니다.<br />4.  **모든 경고를 오류로 처리** 확인란이 선택 취소되어 있는지 확인합니다.<br />5.  오류로 처리할 경고 옆의 **알림** 열에서 **오류**를 선택합니다.|  
  
## <a name="example"></a>예제  
 다음 코드에서는 `In.vb`를 컴파일하고 컴파일러가 찾는 모든 경고의 첫 번째 발생을 오류로 표시하도록 합니다.  
  
```console
vbc -warnaserror in.vb  
```  
  
## <a name="example"></a>예제  
 다음 코드에서는 `T2.vb`를 컴파일하고 사용되지 않는 지역 변수(42024)에 대한 경고만 오류로 처리합니다.  
  
```console
vbc -warnaserror:42024 t2.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)
