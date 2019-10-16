---
title: MDbg.exe(.NET Framework 명령줄 디버거)
ms.date: 03/30/2017
helpviewer_keywords:
- command-line debugger [.NET Framework]
- MDbg.exe
ms.assetid: 28a3f509-07e2-4dbe-81df-874c5e969cc4
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e2b8f96e9a042681642225ad4e644c6fd1f001cb
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044427"
---
# <a name="mdbgexe-net-framework-command-line-debugger"></a>MDbg.exe(.NET Framework 명령줄 디버거)
도구 공급업체와 애플리케이션 개발자는 .NET Framework 명령줄 디버거를 사용하여 .NET Framework 공용 언어 런타임을 대상으로 하는 프로그램에서 버그를 찾고 수정할 수 있습니다. 이 도구에는 디버깅 서비스를 제공하기 위해 런타임 디버깅 API가 사용됩니다. MDbg.exe를 사용하여 관리 코드만 디버깅할 수 있습니다. 관리되지 않는 코드의 디버깅은 지원하지 않습니다.  
  
이 도구는 NuGet을 통해 사용할 수 있습니다. 설치 정보는 [MDbg 0.1.0](https://www.nuget.org/packages/MDbg/0.1.0)을 참조하세요. 도구를 실행하려면 패키지 관리자 콘솔을 사용합니다. 패키지 관리자 콘솔을 사용하는 방법에 대한 자세한 내용은 [패키지 관리자 콘솔](/nuget/tools/package-manager-console) 문서를 참조하세요.
  
패키지 관리자 프롬프트에 다음을 입력합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
MDbg [ProgramName[arguments]] [options]  
```  
  
## <a name="commands"></a>명령  
 디버거에 있을 때(**mdbg>** 프롬프트에 의해 표시됨) 다음 섹션에서 설명한 명령 중 하나를 입력합니다.  
  
 **명령** [*인수*]  
  
 MDbg.exe 명령에서는 대/소문자가 구분됩니다.  
  
|명령|설명|  
|-------------|-----------------|  
|**ap**[**rocess**] [*number*]|다른 디버깅된 프로세스로 전환하거나 사용 가능한 프로세스를 인쇄합니다. 숫자는 실제 프로세스 ID(PID)가 아니지만 0부터 시작하여 인덱싱되는 목록입니다.|  
|**a**[**ttach**] [*pid*]|프로세스에 연결하거나 사용 가능한 프로세스를 인쇄합니다.|  
|**b**[**reak**] [*ClassName.Method* &#124; *FileName:LineNo*]|지정한 메서드에 중단점을 설정합니다. 모듈은 순차적으로 검사됩니다.<br /><br /> -   **break** *FileName:LineNo*는 소스의 한 위치에서 중단점을 설정합니다.<br />-   **break** *~number*는 **x** 명령과 함께 최근에 표시된 기호에서 중단점을 설정합니다.<br />-   **break** *module!ClassName.Method+IlOffset*은 정규화된 위치에서 중단점을 설정합니다.|  
|**block**[**ingObjects**]|스레드를 차단하는 모니터 잠금을 표시합니다.|  
|**ca**[**tch**] [*exceptionType*]|처리되지 않은 예외만이 아니라 디버거가 모든 예외에서 중단되도록 합니다.|  
|**cl**[**earException**]|실행을 계속할 수 있도록 현재 예외가 처리된 것으로 표시합니다. 예외의 원인이 처리되지 않은 경우 예외가 빠르게 다시 throw될 수 있습니다.|  
|**conf**[**ig**] [*option value*]|모든 구성 가능한 옵션을 표시하고 옵션 값을 사용하지 않고 옵션을 호출하는 방법을 보여줍니다. 옵션이 지정되어 있으면 `value`를 현재 옵션으로 설정합니다. 현재 사용할 수 있는 옵션은 다음과 같습니다.<br /><br /> -   `extpath`는 `load` 명령이 사용될 때 확장을 검색할 경로를 설정합니다.<br />-   `extpath+`는 확장을 로드할 경로를 추가합니다.|  
|**del**[**ete**]|중단점을 삭제합니다.|  
|**de**[**tach**]|디버깅된 프로세스에서 분리합니다.|  
|**d**[**own**] [*frames*]|활성 스택 프레임을 아래로 이동합니다.|  
|**echo**|콘솔에 메시지를 표시합니다.|  
|**enableNotif**[**ication**] *typeName* 0&#124;1|지정한 형식에 대해 (1) 사용자 지정 알림을 사용하도록 설정하거나 (0) 사용자 지정 알림을 사용하지 않도록 설정합니다.|  
|**ex**[**it**] [*exitcode*]|MDbg.exe 셸을 종료하고 프로세스 종료 코드를 선택적으로 지정합니다.|  
|**fo**[**reach**] [*OtherCommand*]|모든 스레드에서 명령을 수행합니다. *OtherCommand*는 한 스레드에서 작동하는 유효한 명령이고, **foreach** *OtherCommand*는 모든 스레드에서 같은 명령을 수행합니다.|  
|**f**[**unceval**] [`-ad` *Num*] *functionName* [*args ...* ]|실행할 함수가 *functionName*인 현재 활성 스레드에서 함수 실행을 수행합니다. 함수 이름은 네임스페이스를 포함하는 정규화된 이름이어야 합니다.<br /><br /> `-ad` 옵션은 함수 확인에 사용할 애플리케이션 도메인을 지정합니다. `-ad` 옵션을 지정하지 않으면 확인에 사용되는 애플리케이션 도메인이 기본적으로 함수 실행에 사용된 스레드가 있는 애플리케이션으로 지정됩니다.<br /><br /> 실행 중인 함수가 정적 함수가 아닌 경우 전달된 첫 번째 매개 변수는 `this` 포인터여야 합니다. 모든 애플리케이션 도메인에서 함수 실행에 대한 인수가 검색됩니다.<br /><br /> 애플리케이션 도메인에서 값을 요청하려면 변수에 접두사를 모듈과 애플리케이션 도메인 이름으로 붙입니다(예: `funceval -ad 0 System.Object.ToString hello.exe#0!MyClass.g_rootRef`). 이 명령은 애플리케이션 도메인 `System.Object.ToString`에서 `0` 함수를 실행합니다. `ToString` 메서드는 인스턴스 함수이므로 첫 번째 매개 변수는 `this` 포인터여야 합니다.|  
|**g**[**o**]|중단점을 만나거나 프로그램이 종료되거나 이벤트(예: 처리되지 않은 예외)가 프로그램을 중단시킬 때까지 프로그램이 계속되도록 합니다.|  
|**h**[**elp**] [*command*]<br /><br /> 또는<br /><br /> **?** [*command*]|모든 명령에 대한 설명이나 지정한 명령에 대한 자세한 설명을 표시합니다.|  
|**ig**[**nore**] [*event*]|디버거가 처리되지 않은 예외에서만 중지되도록 합니다.|  
|**int**[**ercept**] *FrameNumber*|디버거를 지정한 프레임 번호로 롤백합니다.<br /><br /> 디버거에서 예외가 발생한 경우 디버거를 지정한 프레임 번호로 롤백하려면 이 명령을 사용합니다. **set** 명령을 사용하여 프로그램 상태를 변경하고 **go** 명령을 사용하여 계속할 수 있습니다.|  
|**k**[**ill**]|활성 프로세스를 중지합니다.|  
|**l**[**ist**] [*modules* &#124; *appdomains* &#124; *assemblies*]|로드된 모듈, 애플리케이션 도메인 또는 어셈블리를 표시합니다.|  
|**lo**[**ad**] *assemblyName*|다음 방법으로 확장을 로드합니다. 지정한 어셈블리가 로드되고 `Microsoft.Tools.Mdbg.Extension.Extension` 형식에서 정적 메서드 `LoadExtension`을 실행하려고 시도합니다.|  
|**log** [*eventType*]|기록할 이벤트를 설정 또는 표시합니다.|  
|**mo**[**de**] [*option on/off*]|다양한 디버거 옵션을 설정합니다. 옵션 없이 `mode`를 사용하여 디버깅 모드와 현재 설정 목록을 가져옵니다.|  
|**mon**[**itorInfo**] *monitorReference*|개체 모니터 잠금 정보를 표시합니다.|  
|**newo**[**bj**] *typeName* [*arguments...* ]|*typeName* 형식의 새 개체를 만듭니다.|  
|**n**[**ext**]|코드를 실행하여 다음 줄에 여러 함수 호출이 포함된 경우에도 다음 줄로 이동합니다.|  
|**Opendump** *pathToDumpFile*|디버깅에 대해 지정된 덤프 파일을 엽니다.|  
|**o**[**ut**]|현재 함수의 끝으로 이동합니다.|  
|**pa**[**th**] [*pathName*]|이진 파일의 위치를 사용할 수 없는 경우 지정한 경로에서 소스 파일을 검색합니다.|  
|**p**[**rint**] [*var*] &#124; [`-d`]|범위 안에 있는 모든 변수를 인쇄하거나(**print**), 지정한 변수를 인쇄하거나(**print** *var*), 디버거 변수를 인쇄합니다(**print**`-d`).|  
|**printe**[**xception**] [ *-r*]|현재 스레드에 마지막 예외를 출력합니다. `–r`(재귀) 옵션을 사용하여 예외 개체에서 `InnerException` 속성을 트래버스함으로써 전체 예외 체인에 대한 정보를 가져옵니다.|  
|**pro**[**cessenum**]|활성 프로세스를 표시합니다.|  
|**q**[**uit**] [*exitcode*]|선택적으로 프로세스 종료 코드를 지정하여 MDbg.exe 셸을 종료합니다.|  
|**re**[**sume**] [`*` &#124; [`~`]*threadNumber*]|현재 스레드나 *threadNumber* 매개 변수에 의해 지정된 스레드를 다시 시작합니다.<br /><br /> *threadNumber* 매개 변수가 `*`로 지정되거나 스레드 번호가 `~`로 시작하는 경우 *threadNumber*에 의해 지정된 스레드를 제외한 모든 스레드에 명령이 적용됩니다.<br /><br /> 중단되지 않은 스레드를 다시 시작하는 것은 아무 효과가 없습니다.|  
|**r**[**un**] [`-d`(`ebug`) &#124; -`o`(`ptimize`) &#124;`-enc`] [[*path_to_exe*] [*args_to_exe*]]|현재 프로세스를 중단하고 새 프로세스를 시작합니다. 실행 가능한 인수를 전달하지 않으면 이전에 `run` 명령으로 실행된 프로그램이 실행되고, 실행 가능한 인수를 제공하면 선택적으로 제공된 인수를 사용하여 지정한 프로그램이 실행됩니다.<br /><br /> 클래스 로드 이벤트, 모듈 로드 이벤트 및 스레드 시작 이벤트를 무시하는 경우(기본값) 프로그램은 주 스레드의 첫 번째 실행 가능한 명령에서 중단됩니다.<br /><br /> 다음 세 가지 플래그 중 하나를 사용하여 JIT(just-in-time)의 디버거가 코드를 컴파일하도록 합니다.<br /><br /> -   `-d` *(* `ebug` *)* 는 최적화를 사용하지 않도록 설정합니다. 이것은 MDbg.exe의 기본값입니다.<br />-   `-o` *(* `ptimize` *)* 는 디버거 외부에서 수행하는 것처럼 코드를 강제로 실행시키지만 디버깅을 더 어렵게 만듭니다. 이는 디버거 외부에서 사용하는 기본값입니다.<br />-   `-enc`를 사용하면 편집하며 계속하기 기능을 사용할 수 있지만 성능이 저하됩니다.|  
|**Set** *variable*=*value*|범위 안에 있는 변수의 값을 변경합니다.<br /><br /> 고유한 디버거 변수를 만들고 애플리케이션 내에서 이 변수에 참조 값을 할당할 수 있습니다. 이 값은 원래 값에 대한 핸들로 사용되며 원본 값도 범위를 벗어납니다. 모든 디버거 변수는 `$`처럼 `$var`로 시작해야 합니다. 명령을 사용하여 이 핸들을 Nothing으로 설정하면 이 핸들이 지워집니다.<br /><br /> `set $var=`|  
|**Setip** [`-il`] *number*|파일의 현재 IP(명령 포인터)를 지정한 위치로 설정합니다. `-il` 옵션을 지정하면 메서드에서 번호는 MSIL(Microsoft Intermediate Language) 오프셋을 나타냅니다. 그렇지 않으면 소스 줄 번호를 나타냅니다.|  
|**sh**[**ow**] [*lines*]|표시할 줄 수를 지정합니다.|  
|**s**[**tep**]|현재 줄에 있는 다음 함수를 실행하거나 실행할 함수가 없으면 다음 줄로 이동합니다.|  
|**su**[**spend**] [\* &#124; [~]*threadNumber*]|현재 스레드나 *threadNumber* 매개 변수에 의해 지정된 스레드를 일시 중단합니다.  *threadNumber*가 `*`로 지정된 경우 명령은 모든 스레드에 적용됩니다. 스레드 번호가 `~`로 시작하면 *threadNumber*에 의해 지정된 스레드를 제외한 모든 스레드에 명령이 적용됩니다. **go** 또는 **step** 명령으로 프로세스를 실행하면 일시 중단된 스레드가 실행에서 제외됩니다. 프로세스에 일시 중단되지 않은 스레드가 없는 상태에서 **go** 명령을 실행하면 프로세스가 계속되지 않습니다. 이 경우 Ctrl-C를 눌러 프로세스를 중단합니다.|  
|**sy**[**mbol**] *commandName* [*commandValue*]|다음 명령 중 하나를 지정합니다.<br /><br /> -   `symbol path` [`"value"`] - 현재 기호 경로를 표시하거나 설정합니다.<br />-   `symbol addpath` `"value"` - 현재 기호 경로에 추가합니다.<br />-   `symbol reload` [`"module"`] - 모든 기호 또는 지정한 모듈의 기호를 다시 로드합니다.<br />-   `symbol list` [`module`] - 모든 모듈 또는 지정한 모듈의 현재 로드된 기호를 표시합니다.|  
|**t**[**hread**] [*newThread*] [-*nick nickname*`]`|매개 변수가 없는 스레드 명령은 현재 프로세스의 관리되는 모든 스레드를 표시합니다. 스레드는 대개 해당 스레드 번호로 식별되지만 스레드에 할당된 애칭이 있는 경우 애칭이 대신 표시됩니다. `-nick` 매개 변수를 사용하여 애칭을 스레드에 할당할 수 있습니다.<br /><br /> -   **thread** `-nick` *threadName*은 현재 실행 중인 스레드에 애칭을 할당합니다.<br /><br /> 애칭은 숫자일 수 없습니다. 현재 스레드에 이미 할당된 애칭이 있으면 이전 애칭이 새 애칭으로 대체됩니다. 새로운 애칭이 빈 문자열("")인 경우 현재 스레드의 애칭이 삭제되고 스레드에 지정되는 새로운 애칭은 없습니다.|  
|**u**[**p**]|활성 스택 프레임을 위로 이동합니다.|  
|**uwgc**[**handle**] [*var*] &#124; [*address*]|핸들에 의해 추적되는 변수를 인쇄합니다. 핸들을 이름이나 주소로 지정할 수 있습니다.|  
|**when**|현재 활성 `when` 문을 표시합니다.<br /><br /> **when** **delete all** &#124; `num` [`num` [`num` …]] - 번호로 지정된 `when` 문을 삭제하며 `all`이 지정된 경우는 모든 `when` 문을 삭제합니다.<br /><br /> **when** `stopReason` [`specific_condition`] **do**`cmd` [`cmd` [`cmd` …] ] - *stopReason* 매개 변수는 다음 중 하나일 수 있습니다.<br /><br /> `StepComplete`, `ProcessExited`, `ThreadCreated`, `BreakpointHit`, `ModuleLoaded`, `ClassLoaded`, `AssemblyLoaded`, `AssemblyUnloaded`, `ControlCTrapped`, `ExceptionThrown`, `UnhandledExceptionThrown`, `AsyncStop`, `AttachComplete`, `UserBreak`, `EvalComplete`, `EvalException`, `RemapOpportunityReached`, `NativeStop`.<br /><br /> *specific_condition*은 다음 중 하나일 수 있습니다.<br /><br /> -   *number* - `ThreadCreated` 및 `BreakpointHit`의 경우 같은 값을 가진 스레드 ID/중단점 번호에 의해 중단될 때만 작업을 트리거합니다.<br />-   [`!`]*name* - `ModuleLoaded`, `ClassLoaded`, `AssemblyLoaded`, `AssemblyUnloaded`, `ExceptionThrown` 및 `UnhandledExceptionThrown`의 경우 이름이 *stopReason* 이름과 일치할 때만 작업을 트리거합니다.<br /><br /> *specific_condition*은 *stopReason*의 다른 값을 위해 비어 있어야 합니다.|  
|**w**[**here**] [`-v`] [`-c` *depth*] [*threadID*]|스택 프레임에 대한 디버그 정보를 표시합니다.<br /><br /> -   `-v` 옵션은 표시된 각 스택 프레임에 대한 자세한 정보를 제공합니다.<br />-   `depth`의 수를 지정하면 표시되는 프레임 수가 제한됩니다. 모든 프레임을 표시하려면 **all** 명령을 사용합니다. 기본값은 100입니다.<br />-   *threadID* 매개 변수를 지정하면 스택과 연결할 스레드를 제어할 수 있습니다. 기본값은 현재 스레드만입니다. 모든 스레드를 가져오려면 **all** 명령을 사용합니다.|  
|**x** [`-c`*numSymbols*] [*module*[`!`*pattern*]]|모듈의 `pattern`이 일치하는 함수를 표시합니다.<br /><br /> *numSymbols*를 지정하면 출력이 지정한 수로 제한됩니다. *pattern*에 대해 `!`(정규식을 나타냄)를 지정하지 않으면 모든 함수가 표시됩니다. *module*을 제공하지 않으면 로드된 모든 모듈이 표시됩니다. 기호( *~#* )를 사용하면 **break** 명령을 통해 중단점을 설정할 수 있습니다.|  
  
## <a name="remarks"></a>설명  
 컴파일러가 디버깅 기호를 생성하도록 하는 컴파일러 특정 플래그를 사용하여 디버깅할 애플리케이션을 컴파일합니다. 이러한 플래그에 대한 자세한 내용은 해당 컴파일러의 설명서를 참조하십시오. 최적화된 애플리케이션을 디버깅할 수 있지만 일부 디버깅 정보가 손실됩니다. 예를 들어, 다수의 지역 변수가 표시되지 않으며 소스 줄이 정확하지 않게 됩니다.  
  
 애플리케이션을 컴파일한 후에 명령 프롬프트에 **mdbg**를 입력하여 다음 예제에 표시된 대로 디버깅 세션을 시작합니다.  
  
```console  
C:\Program Files\Microsoft Visual Studio 8\VC>mdbg  
MDbg (Managed debugger) v2.0.50727.42 (RTM.050727-4200) started.  
Copyright (C) Microsoft Corporation. All rights reserved.  
  
For information about commands type "help";  
to exit program type "quit".  
mdbg>  
```  
  
 `mdbg>` 프롬프트는 현재 디버거를 실행 중임을 나타냅니다.  
  
 디버거에서는 이전 섹션에 설명된 명령과 인수를 사용하십시오.  
  
## <a name="see-also"></a>참고 항목

- [도구](index.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
