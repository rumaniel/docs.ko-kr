---
title: -win32icon
ms.date: 03/13/2018
helpviewer_keywords:
- win32icon compiler option [Visual Basic]
- -win32icon compiler option [Visual Basic]
- /win32icon compiler option [Visual Basic]
ms.assetid: aecaab01-9353-46c5-941c-6edabd4eff92
ms.openlocfilehash: 6b4b69d227c857442de6857fac023090b3698e81
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004636"
---
# <a name="-win32icon"></a>-win32icon
.Ico 파일을 출력 파일에 삽입 합니다. 이 .ico 파일은 **파일 탐색기**에서 출력 파일을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-win32icon:filename  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`filename`|출력 파일에 추가할 .ico 파일입니다. 공백을 포함 하는 경우 파일 이름을 따옴표 ("")로 묶습니다.|  
  
## <a name="remarks"></a>설명  
 Microsoft Windows 리소스 컴파일러 (RC)를 사용 하 여 .ico 파일을 만들 수 있습니다. 리소스 컴파일러는 Visual C++ 프로그램을 컴파일할 때 호출 됩니다. .ico 파일은 .rc 파일에서 만들어집니다. @No__t-0 및 `-win32resource` 옵션은 함께 사용할 수 없습니다.  
  
 .NET Framework 리소스 파일을 첨부 하려면- [linkresource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/linkresource.md) 을 참조 하 여 .NET Framework 리소스 파일 또는 [-리소스 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/resource.md) 를 참조 하세요. .Res 파일을 가져오려면 [-win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md) 를 참조 하세요.  
  
|Visual Studio IDE에서 win32icon로 설정|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다. <br />2.  **응용 프로그램** 탭을 클릭합니다.<br />3.  **아이콘** 상자에서 값을 수정 합니다.|  
  
## <a name="example"></a>예제  
 다음 코드는-0 @no__t 컴파일하고 .ico 파일 (`Rf.ico`)을 첨부 합니다.  
  
```console
vbc -win32icon:rf.ico in.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
