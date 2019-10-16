---
title: 컴파일러 옵션
description: 사용 하 여 F# 의 컴파일을 제어 하는 컴파일러 명령줄 옵션에 F# 앱 및 라이브러리입니다.
ms.date: 12/10/2018
ms.openlocfilehash: 7d7f8ddc8fddd0fb7605ff57fa323dd03a56bde3
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65642009"
---
# <a name="compiler-options"></a>컴파일러 옵션

에 대 한 컴파일러 명령줄 옵션에 설명 합니다 F# 컴파일러, fsc.exe 합니다. 프로젝트 속성을 설정 하 여 컴파일 환경을 제어할 수도 있습니다.

## <a name="compiler-options-listed-alphabetically"></a>컴파일러 옵션 사전순 목록
다음 표에서 컴파일러 옵션 사전순 목록입니다. 일부는 F# 컴파일러 옵션은 비슷합니다는 C# 컴파일러 옵션입니다. 경우에 대 한 링크 하는 경우는 C# 컴파일러 옵션 항목에서 제공 됩니다.

|컴파일러 옵션|설명|
|---------------|-----------|
|`-a filename.fs`|지정된 된 파일에서 라이브러리를 생성합니다. 이 옵션의 약식 형태는 `--target:library filename.fs`합니다.|
|`--baseaddress:address`|DLL을 로드할 기본 설정 기준 주소를 지정합니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;baseaddress &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/2fdbz5xd.aspx)합니다.|
|`--codepage:id`|필수 페이지가 시스템에 대 한 현재 기본 코드 페이지 없으면 컴파일 중에 사용 하는 코드 페이지를 지정 합니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;코드 페이지 &#40;C&#35; 컴파일러 옵션&#41;](../../csharp/language-reference/compiler-options/codepage-compiler-option.md)합니다.|
|`--consolecolors`|오류 및 경고 사용 콘솔에 색으로 구분 된 텍스트를 지정 합니다.|
|`--crossoptimize[+|-]`|크로스 모듈 최적화를 사용할지 설정 합니다.|
|<code>--delaysign[+&#124;-]</code>|서명을 연기 강력한 이름 키의 공개 부분만 사용 하 여 어셈블리입니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;delaysign &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/ta1sxwy8.aspx)합니다.|
|<code>--checked[+&#124;-]</code>|오버플로 검사 생성을 사용할지 설정 합니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;확인 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/h25wtyxf.aspx)합니다.|
|<code>--debug[+&#124;-]</code><br /><br /><code>-g[+&#124;-]</code><br /><br /><code>--debug:[full&#124;pdbonly]</code><br /><br /><code>-g: [full&#124;pdbonly]</code>|또는 디버그 정보 생성을 사용 하지 않도록 설정 하거나 생성할 디버그 정보의 형식을 지정 합니다. 기본값은 전체 실행 프로그램에 연결할 수 있습니다. 선택할 **pdbonly** pdb (프로그램 데이터베이스) 파일에 저장 하는 제한 된 디버깅 정보를 얻을 수 있습니다.<br /><br />에 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 다음 항목을 참조하세요.<br /><br />[&#47;디버그 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/8cw0bt21.aspx)합니다.|
|`--define:symbol`<br /><br />`-d:symbol`|조건부 컴파일에 사용할 기호를 정의합니다.|
|<code>--deterministic[+&#124;-]</code>|결정적 어셈블리 (모듈 버전 GUID 및 타임 스탬프 포함)를 생성 합니다. 이 옵션을 와일드 카드 버전 번호를 사용 하 여 사용할 수 없습니다 및 embedded 및 이식 가능한 디버깅 형식만 지원|
|`--doc:xmldoc-filename`|지정 된 파일에 XML 문서 주석을 생성 하도록 컴파일러에 지시 합니다. 자세한 내용은 [XML Documentation](xml-documentation.md)을 참조하세요.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;문서 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/3260k4x7.aspx)합니다.|
|`--fullpaths`|정규화 된 경로 생성 하도록 컴파일러에 지시 합니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;fullpaths &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/d315xc66.aspx)합니다.|
|`--help`<br /><br />`-?`|모든 컴파일러 옵션의 간략 한 설명을 포함 하 고 사용 정보를 표시 합니다.|
|<code>--highentropyva[+&#124;-]</code>|높은 엔트로피 주소 공간 레이아웃 불규칙화 (ASLR) 강화 된 보안 기능을 사용 하지 않도록 설정 하거나 사용 합니다. 운영 체제 위치를 임의화 합니다 메모리에 응용 프로그램 (예: 스택 및 힙)에 대 한 인프라를 로드 하는 위치입니다. 이 옵션을 사용 하는 경우 운영 체제 64 비트 컴퓨터에서 전체 64 비트 주소 공간을 사용 하이 불규칙화를 통해 사용할 수 있습니다.|
|`--keycontainer:key-container-name`|강력한 이름의 키 컨테이너를 지정합니다.|
|`--keyfile:filename`|생성된 된 어셈블리를 서명 하는 것에 대 한 공개 키 파일의 이름을 지정 합니다.|
|`--lib:folder-name`<br /><br />`-I:folder-name`|참조 되는 어셈블리에 대 한 검색할 디렉터리를 지정 합니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;lib &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/s5bac5fx.aspx)합니다.|
|`--linkresource:resource-info`|어셈블리에 지정된 된 리소스를 연결합니다. Resource-info의 형식은 <code>filename[name[public&#124;private]]</code><br /><br />이 옵션을 사용 하 여 단일 리소스를 연결 하는 대신 사용 하 여 전체 리소스 파일을 포함 합니다 `--resource` 옵션입니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;linkresource &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/xawyf94k.aspx)합니다.|
|`--mlcompatibility`|다른 ML 버전과의 호환을 위해 설계 된 기능을 사용 하는 경우 표시 되는 경고를 무시 합니다.|
|`--noframework`|.NET Framework 어셈블리에 대 한 기본 참조를 사용 하지 않도록 설정 합니다.|
|`--nointerfacedata`|컴파일러가 포함 하는 어셈블리에는 일반적으로 추가 리소스를 생략 하도록 지시 합니다 F#-특정 메타 데이터입니다.|
|`--nologo`|컴파일러를 시작할 때 배너 텍스트를 표시 하지 않습니다.|
|`--nooptimizationdata`|인라인된 구문을 구현 하는 데 필요한 최적화만 포함 하도록 컴파일러에 지시 합니다. 크로스 모듈 인라인 처리가 금지 되지만 이진 호환성을 향상 시킵니다.|
|`--nowin32manifest`|기본 Win32 매니페스트를 생략 하도록 컴파일러에 지시 합니다.|
|`--nowarn:warning-number-list`|특정 경고 번호로 사용 하지 않도록 설정 합니다. 각 경고 번호를 쉼표로 구분 합니다. 컴파일 출력에서 경고에 대 한 경고 번호를 확인할 수 있습니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;nowarn &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/7f28x9z3.aspx)합니다.|
|<code>--optimize[+&#124;-][optimization-option-list]</code><br /><br /><code>-O[+&#124;-] [optimization-option-list]</code>|사용 하거나 최적화를 사용 하지 않도록 설정 합니다. 일부 최적화 옵션을 사용 하지 않도록 설정 또는 나열 하 여 선택적으로 사용할 수 있습니다. 이들은: `nojitoptimize`, `nojittracking`, `nolocaloptimize`합니다 `nocrossoptimize`, `notailcalls`합니다.|
|`--out:output-filename`<br /><br />`-o:output-filename`|컴파일된 어셈블리 또는 모듈의 이름을 지정합니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;out &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/bw3t50f3.aspx)합니다.|
|`--pdb:pdb-filename`|출력 디버그 PDB (프로그램 데이터베이스) 파일을 이름을 지정 합니다. 만이 옵션은 때 적용 됩니다 `--debug` 도 사용 합니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;pdb &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/ms228625.aspx)합니다.|
|`--platform:platform-name`|생성된 된 코드는 지정된 된 플랫폼 에서만 실행 됩니다 지정 합니다 (`x86`, `Itanium`, 또는 `x64`), 또는 플랫폼 이름을 `anycpu` 을 선택 하면 모든 플랫폼에서 생성 된 코드를 실행할 수 있는지를 지정 합니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;플랫폼 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/zekwfyz4.aspx)합니다.|
|`--preferreduilang:lang`| 기본 출력 언어 문화권 이름을 지정 합니다 (예를 들어 `es-ES`, `ja-JP`). |
|`--quotations-debug`|파생 되는 식에 대 한 추가 디버깅 정보를 내보내지 않아야는 지정 F# 따옴표로 묶인 리터럴 및 반영된 정의 합니다. 디버그 정보를 사용자 지정 특성에 추가 됩니다는 F# 식 트리 노드가 있습니다. 참조 [코드 인용](code-quotations.md) 하 고 [Expr.CustomAttributes](https://msdn.microsoft.com/library/eb89943f-5f5b-474e-b125-030ca412edb3)합니다.|
|`--reference:assembly-filename`<br /><br />`-r:assembly-filename`|코드는 F# 또는.NET Framework 어셈블리 컴파일되는 코드를 사용할 수 있습니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;참조 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/yabyz3h4.aspx)합니다.|
|`--resource:resource-filename`|생성된 된 어셈블리에 관리 되는 리소스 파일을 포함 합니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;리소스 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/c0tyye07.aspx)합니다.|
|`--sig:signature-filename`|생성 된 어셈블리를 기준으로 시그니처 파일을 생성 합니다. 서명 파일에 대 한 자세한 내용은 참조 하세요. [서명을](signatures.md)합니다.|
|`--simpleresolution`|MSBuild 확인 대신 디렉터리 기반의 Mono 규칙을 사용 하 여 어셈블리 참조 해결 되도록 지정 합니다. 기본은 Mono에서 실행 되는 경우를 제외 하 고 MSBuild 확인을 사용 하는 것입니다.|
|`--standalone`|실행 되도록 자체로 없이 추가 어셈블리와 같은 모든 종속성을 포함 하는 어셈블리를 생성 하도록 지정 된 F# 라이브러리입니다.|
|`--staticlink:assembly-name`|지정된 된 어셈블리 및이 어셈블리에 종속 된 모든 참조 Dll을 정적으로 연결 합니다. DLL 이름이 아니라 어셈블리 이름을 사용 합니다.|
|`--subsystemversion`|생성된 된 실행 파일에서 사용할 운영 체제 하위 시스템의 버전을 지정 합니다. Windows 8.1, Windows 7, Windows Vista 용 6.00 6.01 6.02를 사용 합니다. 이 옵션에만 Dll이 아닌 실행 파일에 적용 됩니다 및 응용 프로그램이 OS의 특정 버전에만 사용할 수 있는 특정 보안 기능에 의존 하는 경우에 사용 해야 합니다. 이 옵션을 사용 하 고 사용자가 운영 체제의 하위 버전 응용 프로그램을 실행 하려고 하는 경우 오류 메시지와 함께 실패 합니다.|
|<code>--tailcalls[+&#124;-]</code>|사용 하거나 사용 하면 테일 재귀 함수에 대 한 다시 사용할 스택 프레임 테일 IL 명령을 사용 하지 않도록 설정 합니다. 기본적으로 이 옵션은 사용하도록 설정됩니다.|
|<code>--target:[exe&#124;winexe&#124;library&#124;module] filename</code>|생성된 된 컴파일된 코드의 형식 및 파일 이름을 지정합니다.<ul><li>`exe` 콘솔 응용 프로그램을 의미합니다.<br /></li><li>`winexe` 콘솔 응용 프로그램에는 표준 입력/출력 스트림 (stdin, stdout 및 stderr) 정의 되지 않은 다른 Windows 응용 프로그램을 의미 합니다.<br /></li><li>`library` 진입점이 없는 어셈블리가입니다.<br /></li><li>`module` 나중에 결합할 수 있는 다른 모듈과 함께 어셈블리로.NET Framework 모듈 (.netmodule)입니다.<br /></li><ul/>이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;대상 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/6h25dztx.aspx)합니다.|
|`--times`|컴파일의 타이밍 정보를 표시 합니다.|
|`--utf8output`|U t F-8 인코딩 컴파일러 출력을 인쇄 하는 데 사용 하도록 설정 합니다.|
|`--warn:warning-level`|경고 수준 (0-5)를 설정합니다. 기본 수준은 3입니다. 각 경고에는 그 심각도에 따라 수준이 부여 됩니다. Level 5는 수준 1 보다 더 적은 심각도 경고를 제공합니다.<br /><br />수준 5 경고 다음과 같습니다. (재귀 사용 하 여 런타임 시 확인) 21, 22 (`let rec` 순서가 평가), 45 (완전 추상화) 및 52 (방어 용 복사본). 다른 모든 경고는 수준 2입니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;경고 &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/13b90fz7.aspx)합니다.|
|`--warnon:warning-number-list`|기본적으로 해제 될 수 있습니다 하거나 다른 명령줄 옵션이 사용 하지 않도록 설정 하는 특정 경고를 사용 하도록 설정 합니다. F# 기본적으로 꺼져 3.0에서는 경고 1182 (사용 되지 않는 변수)만 합니다.|
|<code>--warnaserror[+&#124;-] [warning-number-list]</code>|사용 하거나 경고를 오류로 보고 하는 옵션을 사용 하지 않도록 설정 합니다. 특정 경고 번호를 사용 하지 않도록 설정 하거나 사용 하지를 제공할 수 있습니다. 옵션 명령줄의 뒷부분에 나오는 명령줄의 앞부분에서 옵션을 재정의합니다. 예를 들어 오류로 보고 하지 않을 경고를 지정 하려면 지정할 `--warnaserror+` `--warnaserror-:warning-number-list`합니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;warnaserror &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/406xhdz3.aspx)합니다.|
|`--win32manifest:manifest-filename`|Win32 매니페스트 파일을 컴파일에 추가합니다. 이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;win32manifest &#40;C&#35; 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/bb545961.aspx)합니다.|
|`--win32res:resource-filename`|Win32 리소스 파일을 컴파일에 추가합니다.<br /><br />이 컴파일러 옵션은 해당 하는 C# 같은 이름의 컴파일러 옵션입니다. 자세한 내용은 [ &#47;win32res (&#40;C&#35;) 컴파일러 옵션&#41;](https://msdn.microsoft.com/library/8f2f5x2e.aspx)합니다.|

## <a name="related-articles"></a>관련 문서

|제목|설명|
|-----|-----------|
|[F# Interactive 옵션](fsharp-interactive-options.md)|지 원하는 명령줄 옵션에 설명 합니다 F# 인터프리터, fsi.exe 합니다.|
|[프로젝트 속성 참조](/visualstudio/ide/reference/project-properties-reference)|빌드 옵션을 제공 하는 프로젝트 속성 페이지를 비롯 한 프로젝트에 대 한 UI를 설명 합니다.|
