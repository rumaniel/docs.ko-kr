---
title: '@(지시 파일 지정)(Visual Basic)'
ms.date: 03/13/2018
helpviewer_keywords:
- '@ (Specify Response File) compiler option [Visual Basic]'
ms.assetid: a6847eaa-e5f9-4303-9421-45b55484b9ca
ms.openlocfilehash: deab111cc669941a1cd7dc143dd699b6521221bb
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004983"
---
# <a name="-specify-response-file-visual-basic"></a>@(지시 파일 지정)(Visual Basic)
컴파일할 소스 코드 파일 및 컴파일러 옵션을 포함 하는 파일을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
@response_file  
```  
  
## <a name="arguments"></a>인수  
 `response_file`  
 필수. 컴파일할 소스 코드 파일이 나 컴파일러 옵션을 나열 하는 파일입니다. 공백을 포함 하는 경우 파일 이름을 따옴표 ("")로 묶습니다.  
  
## <a name="remarks"></a>설명  
 컴파일러는 지시 파일에 지정 된 컴파일러 옵션 및 소스 코드 파일을 명령줄에 지정 된 것 처럼 처리 합니다.  
  
 컴파일에서 둘 이상의 지시 파일을 지정 하려면 다음과 같이 여러 지시 파일 옵션을 지정 합니다.  
  
```console  
@file1.rsp @file2.rsp  
```  
  
 지시 파일에서 여러 컴파일러 옵션 및 소스 코드 파일을 한 줄에 표시할 수 있습니다. 단일 컴파일러 옵션 사양은 한 줄에 표시 되어야 합니다 (여러 줄에 걸쳐 있을 수 없음). 지시 파일에는 `#` 기호로 시작 하는 주석이 있을 수 있습니다.  
  
 명령줄에 지정 된 옵션을 하나 이상의 지시 파일에 지정 된 옵션과 결합할 수 있습니다. 컴파일러는 명령 옵션을 발견할 때이를 처리 합니다. 따라서 명령줄 인수는 지시 파일에서 이전에 나열 된 옵션을 재정의할 수 있습니다. 반대로, 지시 파일의 옵션은 이전에 명령줄 또는 다른 지시 파일에 나열 된 옵션을 재정의 합니다.  
  
 Visual Basic는 vbc.exe 파일과 동일한 디렉터리에 있는 Vbc.exe 파일을 제공 합니다. @No__t-0 옵션을 사용 하지 않으면 Vbc.exe 파일이 기본적으로 포함 됩니다. 자세한 내용은 [-noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)를 참조 하세요.  
  
> [!NOTE]
> @No__t-0 옵션은 Visual Studio 개발 환경에서 사용할 수 없습니다. 명령줄에서 컴파일하는 경우에만 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 줄은 샘플 지시 파일에서 가져온 것입니다.  
  
```console
# build the first output file  
-target:exe   
-out:MyExe.exe  
source1.vb   
source2.vb  
```  
  
## <a name="example"></a>예제  
 다음 예제에서는 `File1.rsp` 이라는 지시 파일에 `@` 옵션을 사용 하는 방법을 보여 줍니다.  
  
```console
vbc @file1.rsp  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
