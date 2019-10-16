---
title: -nowarn
ms.date: 07/20/2015
helpviewer_keywords:
- nowarn compiler option [Visual Basic]
- /nowarn compiler option [Visual Basic]
- -nowarn compiler option [Visual Basic]
ms.assetid: 7ebf2106-0652-4fdc-bf60-70fc86465d83
ms.openlocfilehash: 880fdf4931dadea547d64d0506bd3e978956468e
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005403"
---
# <a name="-nowarn"></a>-nowarn
컴파일러에서 경고를 생성하지 않도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-nowarn[:numberList]  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`numberList`|(선택 사항) 컴파일러가 표시 하지 않아야 하는 경고 ID 번호의 쉼표로 구분 된 목록입니다. 경고 Id를 지정 하지 않으면 모든 경고가 표시 되지 않습니다.|  
  
## <a name="remarks"></a>설명  
 @No__t-0 옵션을 선택 하면 컴파일러에서 경고를 생성 하지 않습니다. 개별 경고를 표시 하지 않으려면 콜론 뒤에 `-nowarn` 옵션에 대 한 경고 ID를 제공 합니다. 여러 경고 번호를 쉼표로 구분 합니다.  
  
 경고 식별자의 숫자 부분만 지정 해야 합니다. 예를 들어 BC42024를 표시 하지 않으려면 사용 하지 않는 지역 변수에 대 한 경고에서-0을 @no__t 지정 합니다.  
  
 경고 ID 번호에 대 한 자세한 내용은 [Visual Basic에서 경고 구성](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조 하세요.  
  
|Visual Studio 통합 개발 환경에서 nowarn로 설정|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다. <br />2.  **컴파일** 탭을 클릭합니다.<br />3.  모든 경고를 사용 하지 않으려면 **모든 경고 사용 안 함** 확인란을 선택 합니다.<br />     -또는-<br />     특정 경고를 사용 하지 않도록 설정 하려면 경고 옆의 드롭다운 목록에서 **없음** 을 클릭 합니다.|  
  
## <a name="example"></a>예제  
 다음 코드는 @no__t를 컴파일하고 경고를 표시 하지 않습니다.  
  
```console
vbc -nowarn t2.vb  
```  
  
## <a name="example"></a>예제  
 다음 코드는 @no__t를 컴파일하고 사용 하지 않는 지역 변수 (42024)에 대 한 경고를 표시 하지 않습니다.  
  
```console
vbc -nowarn:42024 t2.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)
