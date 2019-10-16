---
title: -target (Visual Basic)
ms.date: 03/13/2018
helpviewer_keywords:
- target compiler options [Visual Basic]
- -target compiler options [Visual Basic]
- /target compiler options [Visual Basic]
ms.assetid: e0954147-548b-461f-9c4b-a8f88845616c
ms.openlocfilehash: 2d7ccfc6b033a9021e683a4a2501ca2ccc29956d
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004931"
---
# <a name="-target-visual-basic"></a>-target (Visual Basic)
컴파일러 출력의 형식을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-target:{exe | library | module | winexe | appcontainerexe | winmdobj}  
```  
  
## <a name="remarks"></a>설명  
 다음 표에서는 `-target` 옵션의 효과를 요약 하 여 보여 줍니다.  
  
|**옵션**|**동작**|  
|----------------|------------------|  
|`-target:exe`|컴파일러가 실행 가능한 콘솔 응용 프로그램을 만들도록 합니다.<br /><br /> 이 옵션은 `-target` 옵션이 지정 되지 않은 경우의 기본 옵션입니다. 실행 파일은 .exe 확장명을 사용 하 여 만들어집니다.<br /><br /> @No__t-0 옵션으로 지정 하지 않는 한 출력 파일 이름은 `Sub Main` 프로시저를 포함 하는 입력 파일의 이름을 사용 합니다.<br /><br /> .Exe 파일로 컴파일되는 소스 코드 파일에는 하나의 `Sub Main` 프로시저만 필요 합니다. @No__t-0 컴파일러 옵션을 사용 하 여 `Sub Main` 프로시저를 포함 하는 클래스를 지정 합니다.|  
|`-target:library`|컴파일러가 DLL (동적 연결 라이브러리)을 만들도록 합니다.<br /><br /> Dll 확장명을 사용 하 여 동적 연결 라이브러리 파일을 만듭니다.<br /><br /> @No__t-0 옵션으로 지정 하지 않으면 첫 번째 입력 파일의 이름이 출력 파일의 이름으로 사용 됩니다.<br /><br /> DLL을 빌드할 때 `Sub Main` 프로시저가 필요 하지 않습니다.|  
|`-target:module`|컴파일러가 어셈블리에 추가할 수 있는 모듈을 생성 하도록 합니다.<br /><br /> 출력 파일은 .netmodule 확장명을 사용 하 여 생성 됩니다.<br /><br /> .NET 공용 언어 런타임에서는 어셈블리가 없는 파일을 로드할 수 없습니다. 그러나 `-reference`을 사용 하 여 이러한 파일을 어셈블리의 어셈블리 매니페스트에 통합할 수 있습니다.<br /><br /> 한 모듈의 코드가 다른 모듈의 내부 형식을 참조 하는 경우 `-reference`을 사용 하 여 두 모듈을 모두 어셈블리 매니페스트에 통합 해야 합니다.<br /><br /> [-Addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md) 옵션은 모듈에서 메타 데이터를 가져옵니다.|  
|`-target:winexe`|컴파일러가 실행 가능한 Windows 기반 응용 프로그램을 만들도록 합니다.<br /><br /> 실행 파일은 .exe 확장명을 사용 하 여 만들어집니다. Windows 기반 응용 프로그램은 .NET Framework 클래스 라이브러리나 Windows Api를 사용 하 여 사용자 인터페이스를 제공 하는 응용 프로그램입니다.<br /><br /> @No__t-0 옵션으로 지정 하지 않는 한 출력 파일 이름은 `Sub Main` 프로시저를 포함 하는 입력 파일의 이름을 사용 합니다.<br /><br /> .Exe 파일로 컴파일되는 소스 코드 파일에는 하나의 `Sub Main` 프로시저만 필요 합니다. 코드에 `Sub Main` 프로시저를 포함 하는 클래스가 둘 이상 있는 경우 `-main` 컴파일러 옵션을 사용 하 여 `Sub Main` 프로시저를 포함 하는 클래스를 지정 합니다.|  
|`-target:appcontainerexe`|컴파일러가 앱 컨테이너에서 실행 해야 하는 실행 가능한 Windows 기반 응용 프로그램을 만들도록 합니다. 이 설정은 @no__t 0 응용 프로그램에 사용 하도록 설계 되었습니다.<br /><br /> **Appcontainerexe** 설정은 [이식 가능한 실행](/windows/desktop/Debug/pe-format) 파일의 특성 필드에 비트를 설정 합니다. 이 비트는 앱이 앱 컨테이너에서 실행 되어야 함을 나타냅니다. 이 비트가 설정 되 면 `CreateProcess` 메서드가 앱 컨테이너 외부에서 응용 프로그램을 시작 하려고 하면 오류가 발생 합니다. 이 비트 설정 외에 **-target: appcontainerexe** 는 **-target: winexe**와 동일 합니다.<br /><br /> 실행 파일은 .exe 확장명을 사용 하 여 만들어집니다.<br /><br /> @No__t-0 옵션을 사용 하 여 달리 지정 하지 않는 한, 출력 파일 이름은 `Sub Main` 프로시저를 포함 하는 입력 파일의 이름을 사용 합니다.<br /><br /> .Exe 파일로 컴파일되는 소스 코드 파일에는 하나의 `Sub Main` 프로시저만 필요 합니다. 코드에 `Sub Main` 프로시저를 포함 하는 클래스가 두 개 이상 포함 된 경우 `-main` 컴파일러 옵션을 사용 하 여 `Sub Main` 프로시저를 포함 하는 클래스를 지정 합니다.|  
|`-target:winmdobj`|컴파일러가 Windows 런타임 이진 파일 (winmd)로 변환할 수 있는 중간 파일을 만들도록 합니다. 관리 되는 언어 프로그램 외에도 JavaScript 및 C++ 프로그램에서 winmd 파일을 사용할 수 있습니다.<br /><br /> 중간 파일은 winmdobj 확장명을 사용 하 여 만들어집니다.<br /><br /> @No__t-0 옵션을 사용 하 여 지정 하지 않으면 첫 번째 입력 파일의 이름이 출력 파일의 이름으로 사용 됩니다. @No__t-0 프로시저는 필요 하지 않습니다.<br /><br /> Winmdobj 파일은 Windows 메타 데이터 (WinMD) 파일을 생성 하기 위해 <xref:Microsoft.Build.Tasks.WinMDExp> 내보내기 도구에 대 한 입력으로 사용 하도록 디자인 되었습니다. WinMD 파일은 확장명이 winmd 이며 원래 라이브러리의 코드와 JavaScript, C++및 Windows 런타임 사용 하는 WinMD 정의를 모두 포함 합니다.|  
  
 @No__t-0을 지정 하지 않으면 `-target` 이면 .NET Framework 어셈블리 매니페스트가 출력 파일에 추가 됩니다.  
  
 Vbc.exe의 각 인스턴스는 최대 하나의 출력 파일을 생성 합니다. @No__t-0 또는 `-target`과 같은 컴파일러 옵션을 두 번 이상 지정 하는 경우 컴파일러 프로세스가 마지막으로 적용 됩니다. 컴파일에 있는 모든 파일에 대 한 정보가 매니페스트에 추가 됩니다. @No__t-0으로 만든 파일을 제외한 모든 출력 파일에는 매니페스트의 어셈블리 메타 데이터가 포함 됩니다. [Ildasm.exe (IL 디스어셈블러)](../../../framework/tools/ildasm-exe-il-disassembler.md) 를 사용 하 여 출력 파일에서 메타 데이터를 볼 수 있습니다.  
  
 `-target`의 약식은 `-t`입니다.  
  
### <a name="to-set--target-in-the-visual-studio-ide"></a>Visual Studio IDE에서 대상으로 설정 하려면  
  
1. **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다.   
  
2. **응용 프로그램** 탭을 클릭합니다.  
  
3. **응용 프로그램 유형** 상자의 값을 수정 합니다.  
  
## <a name="example"></a>예제  
 다음 코드는 `in.vb`을 컴파일하여 `in.dll`을 만듭니다.  
  
```console
vbc -target:library in.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-main](../../../visual-basic/reference/command-line-compiler/main.md)
- [-out (Visual Basic)](../../../visual-basic/reference/command-line-compiler/out.md)
- [-reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)
- [-addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)
- [-moduleassemblyname](../../../visual-basic/reference/command-line-compiler/moduleassemblyname.md)
- [.NET 어셈블리](../../../standard/assembly/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
