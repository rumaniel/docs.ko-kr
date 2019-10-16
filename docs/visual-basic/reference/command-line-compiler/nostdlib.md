---
title: -nostdlib (Visual Basic)
ms.date: 03/13/2018
helpviewer_keywords:
- nostdlib compiler option [Visual Basic]
- -nostdlib compiler option [Visual Basic]
- /nostdlib compiler option [Visual Basic]
ms.assetid: 140381b8-dc96-4ad5-ae11-792c9ed0be4d
ms.openlocfilehash: 819505df2e7d5f93302f9ed601de856e36ed7124
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005406"
---
# <a name="-nostdlib-visual-basic"></a>-nostdlib (Visual Basic)
컴파일러가 표준 라이브러리를 자동으로 참조 하지 않도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-nostdlib  
```  
  
## <a name="remarks"></a>설명  
 @No__t-0 옵션을 선택 하면 System.object 어셈블리에 대 한 자동 참조가 제거 되 고 컴파일러에서 Vbc.rsp 파일을 읽을 수 없습니다. Vbc.exe 파일과 동일한 디렉터리에 있는 Vbc.exe 파일은 일반적으로 사용 되는 .NET Framework 어셈블리를 참조 하 고 `System` 및 `Microsoft.VisualBasic` 인 네임 스페이스를 가져옵니다.  
  
> [!NOTE]
> Mscorlib.dll 및 Microsoft.visualbasic 어셈블리는 항상 참조 됩니다.  
  
> [!NOTE]
> @No__t-0 옵션은 Visual Studio 개발 환경에서 사용할 수 없습니다. 명령줄에서 컴파일하는 경우에만 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 코드는 표준 라이브러리를 참조 하지 않고 `T2.vb`을 컴파일합니다. @No__t-1 개체를 제거 하려면 `_MYTYPE` 조건부 컴파일 상수를 문자열 "Empty"로 설정 해야 합니다.  
  
```console
vbc -nostdlib -define:_MYTYPE=\"Empty\" T2.vb  
```  
  
## <a name="see-also"></a>참조

- [-noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)
- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [My에 사용할 수 있는 개체 사용자 지정](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)
