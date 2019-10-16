---
title: 관리 디버깅 도우미를 사용하여 오류 진단
ms.date: 08/14/2018
f1_keywords:
- EHMDA
helpviewer_keywords:
- run-time error debugging
- managed code, run-time debugging
- resource debugging
- registry, MDAs
- common language runtime, debugging
- MDAs (managed debugging assistants)
- configuration files [.NET Framework], debugging runtime events
- messages, managed debugging assistants
- application configuration files, managed debugging assistants
- debugging [.NET Framework], managed debugging assistants
- environment variables, MDAs
- access violation debugging [.NET Framework]
- diagnostics, managed debugging assistants
- unmanaged code, run-time debugging
- default debug output stream
- memory, debugging
- app.config files, managed debugging assistants
- managed debugging assistants (MDAs)
- debugging [.NET Framework], run-time errors
- trapping events
- runtime, error debugging
- disabling MDAs
- output, managed debugging assistants
- errors [.NET Framework], managed debugging assistants
ms.assetid: 76994ee6-9fa9-4059-b813-26578d24427c
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6cb2a240a2e7e82b7015eb7a6d99c2117fa63045
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052895"
---
# <a name="diagnose-errors-with-managed-debugging-assistants"></a>관리 디버깅 도우미를 사용 하 여 오류 진단

MDA(관리 디버깅 도우미)는 런타임 상태에 대한 정보를 제공하기 위해 CLR(공용 언어 런타임)과 함께 작동하는 디버깅 도우미입니다. 이 도우미는 다른 방법으로는 트래핑할 수 없는 런타임 이벤트에 대한 정보 메시지를 생성합니다. MDA를 사용하면 관리 코드와 비관리 코드 간에 변환할 때 발생하는 찾기 어려운 애플리케이션 버그를 구분할 수 있습니다.

Windows 레지스트리에 키를 추가 하거나 환경 변수를 설정 하 여 모든 Mda를 [사용 하거나 사용 하지 않도록](#enable-and-disable-mdas) 설정할 수 있습니다. 애플리케이션 구성 설정을 사용하여 특정 MDA를 사용하도록 설정할 수 있습니다. 애플리케이션의 구성 파일에서 일부 개별 MDA에 대한 추가 구성 설정을 지정할 수 있습니다. 이러한 구성 파일은 런타임이 로드될 때 구문 분석되므로 관리되는 애플리케이션이 시작되기 전에 MDA를 사용하도록 설정해야 합니다. 이미 시작된 애플리케이션에 대해서는 MDA를 사용하도록 설정할 수 없습니다.

다음 표에서는 .NET Framework와 함께 제공 되는 Mda를 나열 합니다.

|||
|-|-|
|[asynchronousThreadAbort](asynchronousthreadabort-mda.md)|[bindingFailure](bindingfailure-mda.md)|
|[callbackOnCollectedDelegate](callbackoncollecteddelegate-mda.md)|[contextSwitchDeadlock](contextswitchdeadlock-mda.md)|
|[dangerousThreadingAPI](dangerousthreadingapi-mda.md)|[dateTimeInvalidLocalFormat](datetimeinvalidlocalformat-mda.md)|
|[dirtyCastAndCallOnInterface](dirtycastandcalloninterface-mda.md)|[disconnectedContext](disconnectedcontext-mda.md)|
|[dllMainReturnsFalse](dllmainreturnsfalse-mda.md)|[exceptionSwallowedOnCallFromCom](exceptionswallowedoncallfromcom-mda.md)|
|[failedQI](failedqi-mda.md)|[fatalExecutionEngineError](fatalexecutionengineerror-mda.md)|
|[gcManagedToUnmanaged](gcmanagedtounmanaged-mda.md)|[gcUnmanagedToManaged](gcunmanagedtomanaged-mda.md)|
|[illegalPrepareConstrainedRegion](illegalprepareconstrainedregion-mda.md)|[invalidApartmentStateChange](invalidapartmentstatechange-mda.md)|
|[invalidCERCall](invalidcercall-mda.md)|[invalidFunctionPointerInDelegate](invalidfunctionpointerindelegate-mda.md)|
|[invalidGCHandleCookie](invalidgchandlecookie-mda.md)|[invalidIUnknown](invalidiunknown-mda.md)|
|[invalidMemberDeclaration](invalidmemberdeclaration-mda.md)|[invalidOverlappedToPinvoke](invalidoverlappedtopinvoke-mda.md)|
|[invalidVariant](invalidvariant-mda.md)|[jitCompilationStart](jitcompilationstart-mda.md)|
|[loaderLock](loaderlock-mda.md)|[loadFromContext](loadfromcontext-mda.md)|
|[marshalCleanupError](marshalcleanuperror-mda.md)|[marshaling](marshaling-mda.md)|
|[memberInfoCacheCreation](memberinfocachecreation-mda.md)|[moduloObjectHashcode](moduloobjecthashcode-mda.md)|
|[nonComVisibleBaseClass](noncomvisiblebaseclass-mda.md)|[notMarshalable](notmarshalable-mda.md)|
|[openGenericCERCall](opengenericcercall-mda.md)|[overlappedFreeError](overlappedfreeerror-mda.md)|
|[pInvokeLog](pinvokelog-mda.md)|[pInvokeStackImbalance](pinvokestackimbalance-mda.md)|
|[raceOnRCWCleanup](raceonrcwcleanup-mda.md)|[reentrancy](reentrancy-mda.md)|
|[releaseHandleFailed](releasehandlefailed-mda.md)|[reportAvOnComRelease](reportavoncomrelease-mda.md)|
|[streamWriterBufferedDataLost](streamwriterbuffereddatalost-mda.md)|[virtualCERCall](virtualcercall-mda.md)|

기본적으로 .NET Framework는 모든 관리되는 디버거에 대한 MDA의 하위 집합을 활성화합니다. **디버그** 메뉴에서 **Windows** > **예외 설정** 을 선택 하 고 **관리 디버깅 도우미** 목록을 확장 하 여 Visual Studio의 기본 집합을 볼 수 있습니다.

![Visual Studio의 예외 설정 창](./media/diagnosing-errors-with-managed-debugging-assistants/exception-settings-mdas.png)

## <a name="enable-and-disable-mdas"></a>Mda 사용 및 사용 안 함

레지스트리 키, 환경 변수 및 애플리케이션 구성 설정을 사용하여 MDA를 사용하거나 사용하지 않도록 설정할 수 있습니다. 애플리케이션 구성 설정을 사용하려면 레지스트리 키 또는 환경 변수를 사용하도록 설정해야 합니다.

> [!TIP]
> Mda를 사용 하지 않도록 설정 하는 대신 MDA 알림이 수신 될 때마다 Visual Studio에서 MDA 대화 상자를 표시 하지 않도록 할 수 있습니다. 이렇게 하려면 **디버그** 메뉴에서 **Windows** > **예외 설정** 을 선택 하 고 **관리 디버깅 도우미** 목록을 확장 한 다음 개별 MDA에 대 한 **throw 될 때 중단** 확인란을 선택 하거나 선택 취소 합니다.

### <a name="registry-key"></a>레지스트리 키

Mda를 사용 하도록 설정 하려면 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\을 추가 합니다.** Windows 레지스트리에서 NETFramework\MDA 하위 키 (REG_SZ, 값 1)를 입력 합니다. 다음 예제를 *Mdaenable .reg*라는 텍스트 파일에 복사 합니다. Windows 레지스트리 편집기 (Regedit.exe)를 열고 **파일** 메뉴에서 **가져오기**를 선택 합니다. *Mdaenable .reg* 파일을 선택 하 여 해당 컴퓨터에서 mda를 사용 하도록 설정 합니다. 하위 키를 문자열 값 **1** 로 설정 하면 (DWORD 값이 **1**이 아닌 경우) *ApplicationName*파일에서 mda 설정을 읽을 수 있습니다. 예를 들어, 메모장의 MDA 구성 파일은 notepad.exe로 이름이 지정 됩니다.

```text
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework]
"MDA"="1"
```

컴퓨터가 64비트 운영 체제에서 32비트 애플리케이션을 실행 중인 경우 MDA 키는 다음과 같이 설정됩니다.

```text
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework]
"MDA"="1"
```

자세한 내용은 [응용 프로그램별 구성 설정](#application-specific-configuration-settings) 을 참조 하세요. 레지스트리 설정은 COMPLUS_MDA 환경 변수로 재정의할 수 있습니다. 자세한 내용은 [환경 변수](#environment-variable) 를 참조 하세요.

Mda를 사용 하지 않도록 설정 하려면 Windows 레지스트리 편집기를 사용 하 여 MDA 하위 키를 **0** (영)으로 설정 합니다.

기본적으로 일부 MDA는 디버거에 연결된 애플리케이션을 실행하면 레지스트리 키를 추가하지 않더라도 사용하도록 설정됩니다. 이 섹션의 앞부분에서 설명한 대로 *Mdadisable .reg* 파일을 실행 하 여 이러한 도우미를 사용 하지 않도록 설정할 수 있습니다.

### <a name="environment-variable"></a>환경 변수

MDA 활성화는 레지스트리 키를 재정의하는 환경 변수 COMPLUS_MDA에 의해서도 제어됩니다. COMPLUS_MDA 문자열은 대/소문자를 구분하지 않으며, 세미콜론으로 구분된 MDA 이름 또는 기타 특수 제어 문자열의 목록입니다. 관리되는 디버거 또는 관리되지 않는 디버거에서 시작하면 기본적으로 MDA 집합이 사용하도록 설정됩니다. 이러한 설정은 디버거에서 기본적으로 사용하도록 설정된, 세미콜론으로 구분된 MDA 목록을 환경 변수 또는 레지스트리 키 값에 추가하여 암시적으로 수행됩니다. 특수 제어 문자열은 다음과 같습니다.

- `0` - 모든 MDA를 비활성화합니다.

- `1` - *ApplicationName*.mda.config에서 MDA 설정을 읽습니다.

- `managedDebugger` - 관리되는 실행 파일이 디버거에서 시작되면 암시적으로 활성화되는 모든 MDA를 명시적으로 활성화합니다.

- `unmanagedDebugger` - 관리되지 않는 실행 파일이 디버거에서 시작되면 암시적으로 활성화되는 모든 MDA를 명시적으로 활성화합니다.

충돌하는 설정이 있는 경우 최신 설정이 이전 설정을 재정의합니다.

- `COMPLUS_MDA=0`은 디버거에서 암시적으로 사용하도록 설정된 MDA를 포함하여 모든 MDA를 사용하지 않도록 설정합니다.

- `COMPLUS_MDA=gcUnmanagedToManaged`는 디버거에서 암시적으로 사용하도록 설정된 모든 MDA 외에 `gcUnmanagedToManaged`를 사용하도록 설정합니다.

- `COMPLUS_MDA=0;gcUnmanagedToManaged`는 `gcUnmanagedToManaged`를 사용하도록 설정하지만 디버거에서 달리 암시적으로 사용하도록 설정되지 않는 MDA를 사용하지 않도록 설정합니다.

### <a name="application-specific-configuration-settings"></a>응용 프로그램별 구성 설정

애플리케이션의 MDA 구성 파일에서 일부 도우미를 개별적으로 사용하도록 설정, 사용하지 않도록 설정 및 구성할 수 있습니다. MDA를 구성하는 데 애플리케이션 구성 파일을 사용할 수 있으려면 MDA 레지스트리 키 또는 COMPLUS_MDA 환경 변수를 설정해야 합니다. 애플리케이션 구성 파일은 일반적으로 애플리케이션 실행 파일(.exe)과 동일한 디렉터리에 있습니다. 파일 이름은 *ApplicationName*.mda.config 형식을 사용합니다(예: notepad.exe.mda.config). 응용 프로그램 구성 파일에서 사용하도록 설정된 도우미는 특별히 해당 도우미의 동작을 제어하도록 디자인된 특성 또는 요소를 포함할 있습니다.

다음 예제에서는 [마샬링을](marshaling-mda.md)사용 하도록 설정 하 고 구성 하는 방법을 보여 줍니다.

```xml
<mdaConfig>
  <assistants>
    <marshaling>
      <methodFilter>
        <match name="*"/>
      </methodFilter>
      <fieldFilter>
        <match name="*"/>
      </fieldFilter>
    </marshaling>
  </assistants>
</mdaConfig>
```

`Marshaling` MDA는 애플리케이션에서 각 관리되는-관리되지 않는 변환의 관리되지 않는 형식으로 마샬링되는 관리되는 형식에 대한 정보를 내보냅니다. MDA `Marshaling` 는 각각 **methodfilter** 및 **fieldfilter** 자식 요소에 제공 된 메서드 및 구조 필드의 이름을 필터링 할 수도 있습니다.

다음 예제에서는 기본 설정을 사용 하 여 여러 Mda를 사용 하도록 설정 하는 방법을 보여 줍니다.

```xml
<mdaConfig>
  <assistants>
    <illegalPrepareConstrainedRegion />
    <invalidCERCall />
    <openGenericCERCall />
    <virtualCERCall />
  </assistants>
</mdaConfig>
```

> [!IMPORTANT]
> 구성 파일에 둘 이상의 도우미를 지정할 때는 사전순으로 나열해야 합니다. 예를 들어, `virtualCERCall` MDA와 `invalidCERCall` MDA를 둘 다 사용하도록 설정하려면 `<invalidCERCall />` 항목 앞에 `<virtualCERCall />` 항목을 추가해야 합니다. 항목이 사전순이 아니면 처리되지 않은 잘못된 구성 파일 예외 메시지가 표시됩니다.

## <a name="mda-exceptions"></a>MDA 예외

MDA가 활성화 되 면 코드가 디버거에서 실행 되지 않는 경우에도 활성화 됩니다. 디버거가 없을 때 MDA 이벤트가 발생하면 이벤트 메시지가 처리되지 않은 예외가 아니더라도 처리되지 않은 예외 대화 상자에 표시됩니다. 이 대화 상자가 표시되지 않도록 하려면 코드가 디버깅 환경에서 실행되지 않는 경우 MDA 사용 설정을 제거하세요.

Visual Studio IDE (통합 개발 환경)에서 코드가 실행 되는 경우 특정 MDA 이벤트에 대해 표시 되는 예외 대화 상자를 방지할 수 있습니다. 이렇게 하려면 **디버그** 메뉴에서 **Windows** > **예외 설정**을 선택 합니다. **예외 설정** 창에서 **관리 디버깅 도우미** 목록을 확장 한 다음 개별 MDA에 대 한 **throw 될 때 중단** 확인란의 선택을 취소 합니다. 이 대화 상자를 사용 하 여 MDA 예외 대화 *상자를 표시할* 수도 있습니다.

## <a name="mda-output"></a>MDA 출력

Mda 출력은 `PInvokeStackImbalance` mda의 출력을 보여 주는 다음 예제와 유사 합니다.

**PInvoke 함수 ' MDATest!를 호출 합니다. MDATest. Program:: StdCall '이 (가) 스택에서 불균형 했습니다. 이는 관리 되는 PInvoke 서명이 관리 되지 않는 대상 시그니처와 일치 하지 않기 때문일 수 있습니다. PInvoke 시그니처의 호출 규칙 및 매개 변수가 관리 되지 않는 대상 시그니처와 일치 하는지 확인 합니다.**

## <a name="see-also"></a>참고자료

- [디버깅, 추적 및 프로파일링](index.md)
