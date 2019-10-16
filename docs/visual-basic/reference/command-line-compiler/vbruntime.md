---
title: -vbruntime
ms.date: 03/13/2018
f1_keywords:
- vbruntime
- -vbruntime
helpviewer_keywords:
- vbruntime compiler option [Visual Basic]
- -vbruntime compiler option [Visual Basic]
- /vbruntime compiler option [Visual Basic]
ms.assetid: 1aa0239e-511a-4c29-957d-fd72877b350a
ms.openlocfilehash: 8c7789c6af7b82ecb40ecd73d09f64aa1da3fd4b
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005049"
---
# <a name="-vbruntime"></a>-vbruntime
컴파일러에서 Visual Basic 런타임 라이브러리에 대한 참조 없이 컴파일하거나 특정 런타임 라이브러리를 참조하여 컴파일하도록 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-vbruntime:{ - | + | * | path }  
```  
  
## <a name="arguments"></a>인수  
 \-  
 Visual Basic 런타임 라이브러리에 대 한 참조 없이 컴파일합니다.  
  
 \+  
 기본 Visual Basic 런타임 라이브러리에 대 한 참조를 사용 하 여 컴파일합니다.  
  
 \*  
 Visual Basic 런타임 라이브러리에 대 한 참조 없이 컴파일하고 Visual Basic 런타임 라이브러리의 핵심 기능을 어셈블리에 포함 합니다.  
  
 `path`  
 지정 된 라이브러리 (DLL)에 대 한 참조를 사용 하 여 컴파일합니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 컴파일러 옵션을 사용 하면 컴파일러에서 Visual Basic 런타임 라이브러리에 대 한 참조 없이 컴파일하도록 지정할 수 있습니다. Visual Basic 런타임 라이브러리에 대 한 참조 없이 컴파일하는 경우 Visual Basic 런타임 도우미에 대 한 호출을 생성 하는 코드 또는 언어 구문에 오류 또는 경고가 기록 됩니다. *Visual Basic 런타임 도우미* 는 특정 언어 의미 체계를 실행 하기 위해 런타임에 호출 되는 microsoft.visualbasic에 정의 된 함수입니다.  
  
 @No__t-0 옵션은 `-vbruntime` 스위치를 지정 하지 않은 경우에 발생 하는 것과 동일한 동작을 생성 합니다. @No__t-0 옵션을 사용 하 여 이전 `-vbruntime` 스위치를 재정의할 수 있습니다.  
  
 @No__t-1 또는 `-vbruntime:path` 옵션을 사용 하는 경우 `My` 유형의 개체 대부분은 사용할 수 없습니다.  
  
## <a name="embedding-visual-basic-runtime-core-functionality"></a>Visual Basic 런타임 핵심 기능 포함  
 @No__t-0 옵션을 사용 하면 런타임 라이브러리에 대 한 참조 없이 컴파일할 수 있습니다. 대신 Visual Basic 런타임 라이브러리의 핵심 기능이 사용자 어셈블리에 포함 됩니다. Visual Basic 런타임을 포함 하지 않는 플랫폼에서 응용 프로그램을 실행 하는 경우이 옵션을 사용할 수 있습니다.  
  
 다음 런타임 멤버가 포함 되어 있습니다.  
  
- <xref:Microsoft.VisualBasic.CompilerServices.Conversions> 클래스  
  
- <xref:Microsoft.VisualBasic.Strings.AscW%28System.Char%29> 메서드  
  
- <xref:Microsoft.VisualBasic.Strings.AscW%28System.String%29> 메서드  
  
- <xref:Microsoft.VisualBasic.Strings.ChrW%28System.Int32%29> 메서드  
  
- <xref:Microsoft.VisualBasic.Constants.vbBack> 상수  
  
- <xref:Microsoft.VisualBasic.Constants.vbCr> 상수  
  
- <xref:Microsoft.VisualBasic.Constants.vbCrLf> 상수  
  
- <xref:Microsoft.VisualBasic.Constants.vbFormFeed> 상수  
  
- <xref:Microsoft.VisualBasic.Constants.vbLf> 상수  
  
- <xref:Microsoft.VisualBasic.Constants.vbNewLine> 상수  
  
- <xref:Microsoft.VisualBasic.Constants.vbNullChar> 상수  
  
- <xref:Microsoft.VisualBasic.Constants.vbNullString> 상수  
  
- <xref:Microsoft.VisualBasic.Constants.vbTab> 상수  
  
- <xref:Microsoft.VisualBasic.Constants.vbVerticalTab> 상수  
  
- @No__t 유형의 일부 개체  
  
 @No__t-0 옵션을 사용 하 여 컴파일하는 경우 코드에서 핵심 기능에 포함 되지 않은 Visual Basic 런타임 라이브러리의 멤버를 참조 하는 경우 컴파일러는 해당 멤버를 사용할 수 없음을 나타내는 오류를 반환 합니다.  
  
## <a name="referencing-a-specified-library"></a>지정 된 라이브러리 참조  
 @No__t-0 인수를 사용 하 여 기본 Visual Basic 런타임 라이브러리가 아닌 사용자 지정 런타임 라이브러리에 대 한 참조로 컴파일할 수 있습니다.  
  
 @No__t-0 인수의 값이 DLL에 대 한 정규화 된 경로인 경우 컴파일러는 해당 파일을 런타임 라이브러리로 사용 합니다. @No__t-0 인수의 값이 DLL의 정규화 된 경로가 아니면 Visual Basic 컴파일러는 먼저 현재 폴더에서 식별 된 DLL을 검색 합니다. 그런 다음 [-sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md) 컴파일러 옵션을 사용 하 여 지정한 경로를 검색 합니다. @No__t-0 컴파일러 옵션을 사용 하지 않으면 컴파일러는 .NET Framework 폴더 (`%systemroot%\Microsoft.NET\Framework\versionNumber`)에서 식별 된 DLL을 검색 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `-vbruntime` 옵션을 사용 하 여 사용자 지정 라이브러리에 대 한 참조로 컴파일하는 방법을 보여 줍니다.  
  
```console
vbc -vbruntime:C:\VBLibraries\CustomVBLibrary.dll  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic Core – Visual Studio 2010 s p 1의 새로운 컴파일 모드](https://devblogs.microsoft.com/vbteam/vb-core-new-compilation-mode-in-visual-studio-2010-sp1/)
- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [-sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)
