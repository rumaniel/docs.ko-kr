---
title: Ngen.exe(네이티브 이미지 생성기)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Native Image Generator
- images [.NET Framework], native
- side-by-side execution, native images
- assemblies [.NET Framework], native image
- Ngen.exe
- native image generation
- native image cache
- publisher policy applied for native images
- invalid images
- BypassNGenAttribute
- System.Runtime.BypassNGenAttribute
ms.assetid: 44bf97aa-a9a4-4eba-9a0d-cfaa6fc53a66
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5079f0243faefaab6ada23cc98f5214a616c1d22
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044371"
---
# <a name="ngenexe-native-image-generator"></a>Ngen.exe(네이티브 이미지 생성기)

네이티브 이미지 생성기(Ngen.exe)는 관리되는 애플리케이션의 성능을 향상시키는 도구입니다. Ngen.exe는 컴파일된 프로세서별 컴퓨터 코드가 포함된 파일인 네이티브 이미지를 만들어서 로컬 컴퓨터의 네이티브 이미지 캐시에 설치합니다. 런타임은 JIT(Just-In-Time) 컴파일러를 사용하지 않고 캐시의 네이티브 이미지를 사용하여 원본 어셈블리를 컴파일할 수 있습니다.

> [!NOTE]
> Ngen.exe는 .NET Framework만을 대상으로 하는 어셈블리에 대한 네이티브 이미지를 컴파일합니다. .NET Core에 해당하는 네이티브 이미지 생성기는 [CrossGen](https://github.com/dotnet/coreclr/blob/master/Documentation/building/crossgen.md)입니다. 

.NET Framework 버전 4에서 Ngen.exe로 변경합니다.

- 이제 Ngen.exe가 완전 신뢰로 어셈블리를 컴파일하고 CAS(코드 액세스 보안) 정책이 더 이상 평가되지 않습니다.

- Ngen.exe로 생성되는 네이티브 이미지는 부분 신뢰로 실행되는 애플리케이션에 더 이상 로드할 수 없습니다.

.NET Framework 버전 2.0에서 Ngen.exe로 변경합니다.

- 어셈블리를 설치하면 종속성도 함께 설치되어 Ngen.exe의 구문이 간단해집니다.

- 이제 애플리케이션 도메인 간에 네이티브 이미지를 공유할 수 있습니다.

- 새로운 작업인 `update`는 무효화된 이미지를 다시 만듭니다.

- 이미지를 생성하고 설치할 컴퓨터에서 유휴 시간에 서비스 실행 작업을 지연시킬 수 있습니다.

- 이미지를 무효화시키는 몇 가지 원인이 제거되었습니다.

Windows 8에서는 [네이티브 이미지 작업](#native-image-task)을 참조하세요.

Ngen.exe 및 네이티브 이미지 서비스 사용에 대한 자세한 내용은 [네이티브 이미지 서비스](#native-image-service)를 참조하세요.

> [!NOTE]
> .NET Framework 버전 1.0 및 1.1의 Ngen.exe 구문은 [네이티브 이미지 생성기(Ngen.exe) 레거시 구문](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms165073(v=vs.100))에 있습니다.

이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.

명령 프롬프트에 다음을 입력합니다.

## <a name="syntax"></a>구문

```console
ngen action [options]
```

```console
ngen /? | /help
```

## <a name="actions"></a>작업

다음 표에서는 각 `action`의 구문을 보여 줍니다. `action`의 각 부분에 대한 설명은 [인수](#ArgumentTable), [우선 순위 수준](#PriorityTable), [시나리오](#ScenarioTable) 및 [구성](#ConfigTable) 표를 참조하세요. [옵션](#OptionTable) 표에서는 `options` 및 도움말 스위치에 대해 설명합니다.

|작업|설명|
|------------|-----------------|
|`install` [`assemblyName` &#124; `assemblyPath`] [`scenarios`] [`config`] [`/queue`[`:`{`1`&#124;`2`&#124;`3`}]]|어셈블리 및 해당 종속성에 대한 네이티브 이미지를 생성하고 그러한 이미지를 네이티브 이미지 캐시에 설치합니다.<br /><br /> `/queue`를 지정하면 네이티브 이미지 서비스에 대한 작업이 큐에 대기합니다. 기본 우선 순위는 3입니다. [우선 순위 수준](#PriorityTable) 표를 참조하세요.|
|`uninstall` [`assemblyName` &#124; `assemblyPath`] [`scenarios`] [`config`]|네이티브 이미지 캐시에서 어셈블리에 대한 네이티브 이미지와 그 종속성을 삭제합니다.<br /><br /> 단일 이미지와 그 종속성을 제거하려면 해당 이미지를 설치할 때 사용한 것과 동일한 명령줄 인수를 사용합니다. **참고:**  .NET Framework 4부터는 `uninstall` * 동작이 더 이상 지원되지 않습니다.|
|`update` [`/queue`]|무효화된 네이티브 이미지를 업데이트합니다.<br /><br /> `/queue`를 지정하면 네이티브 이미지 서비스에 대한 업데이트가 큐에 대기합니다. 업데이트는 항상 우선 순위 3에서 예약되므로 컴퓨터가 유휴 상태일 때 실행됩니다.|
|`display` [`assemblyName` &#124; `assemblyPath`]|어셈블리에 대한 네이티브 이미지와 그 종속성의 상태를 표시합니다.<br /><br /> 인수를 지정하지 않은 경우 네이티브 이미지 캐시에 있는 모든 것이 표시됩니다.|
|`executeQueuedItems` [<code>1&#124;2&#124;3</code>]<br /><br /> 또는<br /><br /> `eqi` [1&#124;2&#124;3]|큐에 대기한 컴파일 작업을 실행합니다.<br /><br /> 우선 순위를 지정하면 우선 순위가 크거나 같은 컴파일 작업이 실행됩니다. 우선 순위를 지정하지 않으면 큐에 대기한 컴파일 작업이 모두 실행됩니다.|
|`queue` {`pause` &#124; `continue` &#124; `status`}|네이티브 이미지 서비스를 일시 중지하거나 일시 중지된 서비스를 계속 수행할 수 있도록 하거나 서비스 상태를 쿼리합니다.|

<a name="ArgumentTable"></a>

## <a name="arguments"></a>인수

|인수|설명|
|--------------|-----------------|
|`assemblyName`|어셈블리의 전체 표시 이름입니다. 예: `"myAssembly, Version=2.0.0.0, Culture=neutral, PublicKeyToken=0038abc9deabfle5"`. **참고:**  `myAssembly` 및 `display` 작업의 경우 `uninstall`와 같은 부분 어셈블리 이름을 제공할 수 있습니다. <br /><br /> Ngen.exe 명령줄 당 어셈블리를 하나만 지정할 수 있습니다.|
|`assemblyPath`|어셈블리의 명시적 경로입니다. 전체 또는 상대 경로를 지정할 수 있습니다.<br /><br /> 경로 없이 파일 이름을 지정하는 경우 어셈블리가 현재 디렉터리에 있어야 합니다.<br /><br /> Ngen.exe 명령줄 당 어셈블리를 하나만 지정할 수 있습니다.|

<a name="PriorityTable"></a>

## <a name="priority-levels"></a>우선 순위 수준

|우선 순위|설명|
|--------------|-----------------|
|`1`|네이티브 이미지는 유휴 시간을 기다리지 않고 즉시 생성 및 설치됩니다.|
|`2`|네이티브 이미지가 유휴 시간을 기다리지 않고 생성 후 설치되지만 모든 우선 순위 1 이후의 작업(및 해당 종속성)은 완료되었습니다.|
|`3`|네이티브 이미지는 네이티브 이미지 서비스에서 컴퓨터의 유휴 상태를 감지할 때 설치됩니다. [네이티브 이미지 서비스](#native-image-service)를 참조하세요.|

<a name="ScenarioTable"></a>

## <a name="scenarios"></a>시나리오

|시나리오|설명|
|--------------|-----------------|
|`/Debug`|디버거에서 사용할 수 있는 네이티브 이미지를 생성합니다.|
|`/Profile`|프로파일러에서 사용할 수 있는 네이티브 이미지를 생성합니다.|
|`/NoDependencies`|지정한 시나리오 옵션에 필요한 최소 네이티브 이미지 수를 생성합니다.|

<a name="ConfigTable"></a>

## <a name="config"></a>Config

|구성|설명|
|-------------------|-----------------|
|`/ExeConfig:` `exePath`|지정한 실행 어셈블리의 구성을 사용합니다.<br /><br /> Ngen.exe는 종속성에 바인딩할 때 로더와 같은 결정을 해야 합니다. 공유 구성 요소가 런타임 시 로드되면 애플리케이션의 구성 파일은 <xref:System.Reflection.Assembly.Load%2A> 메서드를 사용하여 공유 구성 요소에 대해 로드된 종속성을 결정합니다(예: 로드된 종속성 버전). `/ExeConfig` 스위치는 런타임 시 종속성을 로드하는 Ngen.exe 지침을 제공합니다.|
|`/AppBase:` `directoryPath`|종속성을 찾을 때 지정된 디렉터리를 애플리케이션 기본 디렉터리로 사용합니다.|

<a name="OptionTable"></a>

## <a name="options"></a>옵션

|옵션|설명|
|------------|-----------------|
|`/nologo`|Microsoft 시작 배너를 표시하지 않습니다.|
|`/silent`|성공 메시지를 표시하지 않습니다.|
|`/verbose`|디버깅에 대한 자세한 내용을 표시합니다. **참고:**  운영 체제 제한으로 인해 이 옵션은 Windows 98 및 Windows Millennium Edition에 대한 추가 정보를 표시하지 않습니다.|
|`/help`, `/?`|현재 릴리스의 명령 구문 및 옵션을 표시합니다.|

## <a name="remarks"></a>설명

Ngen.exe를 실행하려면 관리자 권한이 있어야 합니다.

> [!CAUTION]
> 완전히 신뢰할 수 없는 어셈블리에서 Ngen.exe를 실행하지 마세요. .NET Framework 4부터는 Ngen.exe가 완전 신뢰로 어셈블리를 컴파일하고 CAS(코드 액세스 보안) 정책이 더 이상 평가되지 않습니다.

.NET Framework 4부터는 Ngen.exe로 생성되는 네이티브 이미지는 부분 신뢰로 실행되는 애플리케이션에 더 이상 로드할 수 없습니다. 대신, JIT(Just-In-Time) 컴파일러가 호출됩니다.

Ngen.exe는 `install` 동작 및 해당하는 모든 종속성에 대한 `assemblyname` 인수로 지정된 네이티브 이미지를 생성합니다. 어셈블리 매니페스트의 참조로 종속성을 확인할 수 있습니다. 종속성을 별도로 설치해야 하는 경우는 애플리케이션에서 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드를 호출하는 것과 같은 방법으로 리플렉션을 사용하여 종속성을 로드하는 경우밖에 없습니다.

> [!IMPORTANT]
> 네이티브 이미지에 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 메서드를 사용하지 마세요. 이 메서드로 로드된 이미지는 실행 컨텍스트의 다른 어셈블리에서 사용할 수 없습니다.

Ngen.exe에서는 종속성 개수가 유지됩니다. 예를 들어 네이티브 이미지 캐시에 `MyAssembly.exe` 및 `YourAssembly.exe`가 모두 설치되어 있고 이 두 가지 모두에 `OurDependency.dll`에 대한 참조가 있는 경우, `MyAssembly.exe`를 제거해도 `OurDependency.dll`은 제거되지 않고 `YourAssembly.exe`도 제거할 때만 제거됩니다.

전역 어셈블리 캐시에 어셈블리에 대한 네이티브 이미지를 생성 중인 경우 해당 표시 이름을 지정합니다. <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType>을 참조하세요.

Ngen.exe에서 생성되는 네이티브 이미지는 애플리케이션 도메인 간에 공유할 수 있습니다. 즉, 애플리케이션 도메인 간에 어셈블리를 공유해야 하는 애플리케이션 시나리오에서는 Ngen.exe를 사용할 수 있습니다. 도메인 중립성을 지정하려면

- <xref:System.LoaderOptimizationAttribute> 특성을 애플리케이션에 적용합니다.

- 새 애플리케이션 도메인에 대한 설치 정보를 만드는 경우 <xref:System.AppDomainSetup.LoaderOptimization%2A?displayProperty=nameWithType> 속성을 설정합니다.

같은 어셈블리를 여러 애플리케이션 도메인으로 로드할 때 항상 도메인 중립 코드를 사용합니다. 네이티브 이미지가 공유 도메인으로 로드된 후 비공유 애플리케이션 도메인으로 로드되면 사용할 수 없습니다.

> [!NOTE]
> 도메인 중립 코드는 특히 정적 멤버에 액세스할 때 언로드할 수 없으며 성능이 저하될 수 있습니다.

설명 섹션 내용:

- [다른 시나리오에 대한 이미지 생성](#Scenarios)

- [네이티브 이미지 사용 시기 결정](#WhenToUse)

  - [향상된 메모리 사용](#Memory)

  - [빠른 애플리케이션 시작](#Startup)

  - [사용 고려 사항 요약](#UsageSummary)

- [어셈블리 기준 주소의 중요성](#BaseAddresses)

- [하드 바인딩](#HardBinding)

  - [종속성에 대한 바인딩 힌트 지정](#DependencyHint)

  - [어셈블리에 대한 기본 바인딩 힌트 지정](#AssemblyHint)

- [처리 지연](#Deferred)

- [네이티브 이미지 및 JIT 컴파일](#JITCompilation)

  - [잘못된 이미지](#InvalidImages)

- [문제 해결](#Troubleshooting)

  - [어셈블리 바인딩 로그 뷰어](#Fusion)

  - [JITCompilationStart 관리 디버깅 도우미](#MDA)

  - [네이티브 이미지 생성 옵트아웃](#OptOut)

<a name="Scenarios"></a>

## <a name="generating-images-for-----different-scenarios"></a>다른 시나리오에 대한 이미지 생성

어셈블리의 네이티브 이미지를 생성하면 런타임에서 해당 어셈블리를 실행할 때마다 자동으로 이 네이티브 이미지를 찾아 사용하려고 합니다. 사용 시나리오에 따라 여러 이미지를 생성할 수 있습니다.

예를 들어, 디버깅 또는 프로파일링 시나리오에서 어셈블리를 실행하는 경우 런타임은 `/Debug` 및 `/Profile` 옵션을 사용하여 생성한 네이티브 이미지를 찾습니다. 일치하는 네이티브 이미지를 찾을 수 없는 경우 런타임은 표준 JIT 컴파일로 되돌아갑니다. 네이티브 이미지를 디버깅하는 유일한 방법은 `/Debug` 옵션으로 네이티브 이미지를 만드는 것입니다.

`uninstall` 작업은 시나리오도 인식하므로 시나리오를 모두 제거하거나 선택한 시나리오만 제거할 수 있습니다.

<a name="WhenToUse"></a>

## <a name="determining-when-to-use-native-images"></a>네이티브 이미지 사용 시기 결정

네이티브 이미지는 향상된 메모리 사용과 시작 시간의 단축으로 성능을 향상시킬 수 있습니다.

> [!NOTE]
> 네이티브 이미지의 성능은 코드 및 데이터 액세스 패턴, 모듈 경계에서의 호출 수, 다른 애플리케이션에서 이미 로드한 종속성 수와 같이 분석을 어렵게 하는 여러 가지 요소에 따라 다릅니다. 네이티브 이미지가 애플리케이션에 이점을 제공하는지 여부를 확인하는 유일한 방법은 키 배포 시나리오에서 성능을 측정하는 것입니다.

<a name="Memory"></a>

### <a name="improved-memory-use"></a>향상된 메모리 사용

네이티브 이미지는 코드가 프로세스 간에 공유되는 경우 메모리 사용을 향상시킬 수 있습니다. 네이티브 이미지는 Windows PE 파일이므로 .dll 파일의 단일 복사본은 여러 프로세스에서 공유할 수 있지만 JIT 컴파일러가 생성한 네이티브 이미지는 개인 메모리에 저장되며 공유할 수 없습니다.

터미널 서비스에서 실행된 애플리케이션은 공유 코드 페이지를 활용할 수도 있습니다.

또한 JIT 컴파일러를 로드하지 않으면 각 애플리케이션 인스턴스의 고정 메모리 양을 저장합니다.

<a name="Startup"></a>

### <a name="faster-application-startup"></a>빠른 애플리케이션 시작

Ngen.exe로 어셈블리를 미리 컴파일하면 일부 애플리케이션의 시작 시간을 줄일 수 있습니다. 일반적으로 애플리케이션을 처음 시작한 후에 공유 구성 요소가 다음 애플리케이션을 위해 이미 로드되므로 애플리케이션이 구성 요소 어셈블리를 공유할 때 이러한 이점을 활용할 수 있습니다. 애플리케이션의 모든 어셈블리를 하드 디스크에서 로드해야 하는 콜드 시작은 하드 디스크 액세스 시간이 우선하므로 네이티브 이미지에서 만큼의 이점은 없습니다.

하드 바인딩은 주 애플리케이션 어셈블리에 하드 바인딩된 모든 이미지를 동시에 로드해야 하므로 시작 시간에 영향을 줄 수 있습니다.

> [!NOTE]
> .NET Framework 3.5 서비스 팩 1 이전에는 로더가 전역 어셈블리 캐시에 없는 강력한 이름의 어셈블리에 대해 추가 유효성 검사를 수행하여 시작 시간에 네이티브 이미지를 통해 얻은 향상된 기능을 모두 제거하기 때문에 전역 어셈블리 캐시에 강력한 이름의 공유 구성 요소를 배치해야 합니다. .NET Framework 3.5 SP1에서 도입된 최적화로 인해 추가 유효성 검사가 제거되었습니다.

<a name="UsageSummary"></a>

### <a name="summary-of-usage-considerations"></a>사용 고려 사항 요약

다음과 같은 일반적인 고려 사항 및 애플리케이션 고려 사항은 애플리케이션에 대한 네이티브 이미지 평가 활동을 수행할지 여부를 결정하는 데 도움이 됩니다.

- 네이티브 이미지를 로드할 때는 JIT 컴파일 및 형식 안전 확인과 같은 여러 가지 시작 동작이 필요하지 않으므로 MSIL보다 로드 속도가 빠릅니다.

- JIT 컴파일러가 필요 없기 때문에 네이티브 이미지에 필요한 초기 작업 집합의 크기가 작습니다.

- 네이티브 이미지를 사용하면 프로세스 간에 코드를 공유할 수 있습니다.

- 네이티브 이미지에는 MSIL 어셈블리보다 하드 디스크 공간이 더 많이 필요하며 생성 시간이 오래 걸릴 수 있습니다.

- 네이티브 이미지를 유지 관리해야 합니다.

  - 원본 어셈블리나 해당 종속성 중 하나가 서비스되는 경우 이미지를 다시 생성해야 합니다.

  - 한 어셈블리를 여러 애플리케이션이나 여러 가지 시나리오에서 사용하려면 네이티브 이미지가 여러 개 필요할 수 있습니다. 예를 들어, 두 애플리케이션에 구성 정보가 있으면 동일한 종속 어셈블리에 대해 여러 가지 바인딩 결정이 내려질 수 있습니다.

  - 네이티브 이미지는 관리자가 생성해야 합니다. 즉, Administrators 그룹의 Windows 계정을 사용하여 생성해야 합니다.

네이티브 이미지가 성능 이점을 제공하는지 여부를 결정할 때는 이러한 일반적인 고려 사항 외에 애플리케이션의 특성을 고려해야 합니다.

- 애플리케이션이 여러 공유 구성 요소를 사용하는 환경에서 실행되면 네이티브 이미지를 사용하여 여러 프로세스에서 구성 요소를 공유할 수 있습니다.

- 애플리케이션이 여러 애플리케이션 도메인을 사용하는 경우 네이티브 이미지를 사용하여 도메인 간에 코드 페이지를 공유할 수 있습니다.

    > [!NOTE]
    > .NET Framework 버전 1.0 및 1.1에서는 애플리케이션 도메인 간에 네이티브 이미지를 공유할 수 없습니다. 버전 2.0 이상에서는 그렇지 않습니다.

- 애플리케이션이 터미널 서버에서 실행되면 네이티브 이미지를 사용하여 코드 페이지를 공유할 수 있습니다.

- 일반적으로 규모가 큰 애플리케이션은 네이티브 이미지로 컴파일하는 것이 좋습니다. 일반적으로 규모가 작은 애플리케이션에는 유용하지 않습니다.

- 장기 실행 애플리케이션의 경우 런타임 JIT 컴파일이 네이티브 이미지보다 성능이 약간 더 좋습니다. 하드 바인딩을 사용하면 이러한 성능 차이를 어느 정도 줄일 수 있습니다.

<a name="BaseAddresses"></a>

## <a name="importance-of-assembly-base-addresses"></a>어셈블리 기준 주소의 중요성

네이티브 이미지는 Windows PE 파일이므로 다른 실행 파일과 마찬가지로 동일한 기준 재지정 문제의 영향을 받습니다. 재배치를 위한 성능 비용은 하드 바인딩이 사용된 경우 훨씬 더 많이 듭니다.

네이티브 이미지에 대한 기준 주소를 설정하려면 컴파일러의 해당 옵션을 사용하여 어셈블리에 대한 기준 주소를 설정합니다. Ngen.exe는 네이티브 이미지에 이러한 기준 주소를 사용합니다.

> [!NOTE]
> 네이티브 이미지는 이미지를 만든 관리되는 어셈블리보다 큽니다. 이러한 큰 크기를 허용할 수 있게 기준 주소를 계산해야 합니다.

dumpbin.exe와 같은 도구를 사용하여 네이티브 이미지의 기본 기준 주소를 볼 수 있습니다.

<a name="HardBinding"></a>

## <a name="hard-binding"></a>하드 바인딩

하드 바인딩은 처리량을 늘리고 네이티브 이미지의 작업 집합 크기를 줄입니다. 하드 바인딩은 어셈블리에 하드 바인딩된 이미지를 어셈블리가 로드될 때 모두 로드해야 한다는 단점이 있습니다. 이렇게 하면 규모가 큰 애플리케이션을 시작하는 데 시간이 오래 걸릴 수 있습니다.

하드 바인딩은 애플리케이션의 성능이 중요한 모든 시나리오에 있어서 로드된 종속성에 적합합니다. 네이티브 이미지 사용 시와 마찬가지로 하드 바인딩이 애플리케이션의 성능을 향상시키는지 여부를 확인하는 유일한 방법은 성능을 신중하게 측정하는 것입니다.

<xref:System.Runtime.CompilerServices.DependencyAttribute> 및 <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> 특성을 사용하여 Ngen.exe에 하드 바인딩 힌트를 제공할 수 있습니다.

> [!NOTE]
> 이러한 특성은 명령이 아니라 Ngen.exe에 대한 힌트입니다. 이러한 특성을 사용한다고 해서 하드 바인딩이 보장되는 것은 아닙니다. 이러한 특성의 의미는 다음 릴리스에서 변경될 수 있습니다.

<a name="DependencyHint"></a>

### <a name="specifying-a-binding-hint-for-a-dependency"></a>종속성에 대한 바인딩 힌트 지정

<xref:System.Runtime.CompilerServices.DependencyAttribute>를 어셈블리에 적용하여 지정된 종속성이 로드될 가능성을 나타냅니다. <xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=nameWithType>는 하드 바인딩이 적합함을, <xref:System.Runtime.CompilerServices.LoadHint.Default>는 종속성에 대한 기본값을 사용해야 함을, <xref:System.Runtime.CompilerServices.LoadHint.Sometimes>는 하드 바인딩이 적합하지 않음을 나타냅니다.

아래 코드에서는 두 개의 종속성이 있는 어셈블리에 대한 특성을 보여 줍니다. 첫 번째 종속성(Assembly1)은 하드 바인딩에 적합한 후보이며 두 번째 종속성(Assembly2)은 적합하지 않은 후보입니다.

```vb
Imports System.Runtime.CompilerServices
<Assembly:DependencyAttribute("Assembly1", LoadHint.Always)>
<Assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)>
```

```csharp
using System.Runtime.CompilerServices;
[assembly:DependencyAttribute("Assembly1", LoadHint.Always)]
[assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)]
```

```cpp
using namespace System::Runtime::CompilerServices;
[assembly:DependencyAttribute("Assembly1", LoadHint.Always)];
[assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)];
```

어셈블리 이름에는 파일 이름 확장명이 없습니다. 표시 이름을 사용할 수 있습니다.

<a name="AssemblyHint"></a>

### <a name="specifying-a-default-binding-hint-for-an-assembly"></a>어셈블리에 대한 기본 바인딩 힌트 지정

기본 바인딩 힌트는 어셈블리에 대한 종속성이 있는 애플리케이션이 즉시 자주 사용하는 어셈블리에만 필요합니다. 하드 바인딩을 사용하도록 지정할 이러한 어셈블리에 <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute>를 사용하여 <xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=nameWithType>를 적용합니다.

> [!NOTE]
> <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> 이외의 값이 있는 특성을 적용하면 특성을 전혀 적용하지 않았을 때와 효과가 동일하므로 이 범주에 속하지 않는 .dll 어셈블리에 <xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=nameWithType>를 적용할 이유는 없습니다.

Microsoft는 <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute>를 사용하여 하드 바인딩이 mscorlib.dll과 같은 .NET Framework의 소수 어셈블리에 대한 기본값이 되도록 지정합니다.

<a name="Deferred"></a>

## <a name="deferred-processing"></a>처리 지연

규모가 큰 애플리케이션의 네이티브 이미지를 생성하는 데 시간이 많이 걸릴 수 있습니다. 마찬가지로 공유 구성 요소를 변경하거나 컴파일러 설정을 변경하려면 업데이트할 네이티브 이미지가 여러 개 필요합니다. `install` 및 `update` 작업에는 네이티브 이미지 서비스가 지연된 실행에 대한 작업을 큐에 대기시키는 `/queue`가 있습니다. 또한 Ngen.exe에는 서비스를 일부 제어하는 `queue` 및 `executeQueuedItems` 작업이 있습니다. 자세한 내용은 [네이티브 이미지 서비스](#native-image-service)를 참조하세요.

<a name="JITCompilation"></a>

## <a name="native-images-and-jit-compilation"></a>네이티브 이미지 및 JIT 컴파일

Ngen.exe는 어셈블리에서 생성할 수 없는 메서드를 발견하면 네이티브 이미지에서 이 메서드를 제외합니다. 런타임에서 이 어셈블리를 실행할 때 네이티브 이미지에 포함되지 않은 메서드에 대한 JIT 컴파일로 되돌아갑니다.

또한 어셈블리가 업그레이드되지 않았거나 이미지가 어떤 이유로 무효화된 경우 네이티브 이미지가 사용되지 않습니다.

<a name="InvalidImages"></a>

### <a name="invalid-images"></a>잘못된 이미지

Ngen.exe를 사용하여 어셈블리의 네이티브 이미지를 만드는 경우 출력은 사용자가 지정한 명령줄 옵션 및 컴퓨터의 특정 설정에 따라 달라지는데 이 설정에는 다음 사항이 포함됩니다.

- .NET Framework 버전

- Windows 9x 제품군에서 Windows NT 제품군으로 변경되는 경우의 운영 체제 버전

- 어셈블리의 정확한 ID(다시 컴파일하면 ID가 변경됨)

- 어셈블리에서 참조하는 모든 어셈블리의 정확한 ID(다시 컴파일하면 ID가 변경됨)

- 보안 요소

Ngen.exe는 네이티브 이미지를 생성할 때 이 정보를 기록합니다. 어셈블리를 실행하는 경우 런타임은 컴퓨터의 현재 환경과 일치하는 옵션 및 설정을 사용하여 생성된 네이티브 이미지를 찾고 일치하는 네이티브 이미지를 찾지 못하는 경우 어셈블리의 JIT 컴파일로 되돌아갑니다. 다음과 같이 컴퓨터 설정과 환경을 변경하면 네이티브 이미지를 사용할 수 없게 됩니다.

- .NET Framework 버전

     .NET Framework에 업데이트를 적용하면 Ngen.exe를 사용하여 만든 네이티브 이미지를 모두 사용할 수 없게 됩니다. 따라서 .NET Framework의 모든 업데이트는 `Ngen Update` 명령을 실행하여 네이티브 이미지가 모두 다시 생성되도록 합니다. .NET Framework는 설치한 .NET Framework 라이브러리에 대한 새로운 네이티브 이미지를 자동으로 만듭니다.

- Windows 9x 제품군에서 Windows NT 제품군으로 변경되는 경우의 운영 체제 버전

     예를 들어 컴퓨터에서 실행되는 운영 체제 버전이 Windows 98에서 Windows XP로 변경되면 네이티브 이미지 캐시에 저장된 모든 네이티브 이미지를 사용할 수 없게 됩니다. 그러나 운영 체제가 Windows 2000에서 Windows XP로 변경되는 경우에는 해당 이미지를 계속 사용할 수 있습니다.

- 어셈블리의 정확한 ID

     어셈블리를 다시 컴파일하면 어셈블리의 해당 네이티브 이미지를 사용할 수 없게 됩니다.

- 어셈블리에서 참조하는 모든 어셈블리의 정확한 ID

     관리되는 어셈블리를 업데이트하면 해당 어셈블리에 직접 또는 간접적으로 종속된 네이티브 이미지가 모두 사용할 수 없게 되므로 다시 생성해야 합니다. 여기에는 일반 참조와 하드 바인딩된 종속성이 모두 포함됩니다. 소프트웨어 업데이트가 적용될 때마다 설치 프로그램에서 `Ngen Update` 명령을 실행하여 종속된 네이티브 이미지가 모두 다시 생성되도록 해야 합니다.

- 보안 요소

     어셈블리에 이전에 부여되었던 사용 권한을 제한하도록 컴퓨터 보안 정책을 변경하면 이전에 컴파일한 해당 어셈블리의 네이티브 이미지를 사용할 수 없게 됩니다.

     공용 언어 런타임에서 코드 액세스 보안을 관리하는 방법과 권한을 사용하는 방법에 대한 자세한 내용은 [코드 액세스 보안](../misc/code-access-security.md)을 참조하세요.

<a name="Troubleshooting"></a>

## <a name="troubleshooting"></a>문제 해결

다음 문제 해결 항목을 통해 어떤 네이티브 이미지가 사용되고 있는지, 애플리케이션에서 사용할 수 없는지, JIT 컴파일러에서 메서드를 컴파일하는 시기를 결정할 수 있는지, 그리고 지정된 메서드의 네이티브 이미지 컴파일을 옵트아웃하는 방법을 확인할 수 있습니다.

<a name="Fusion"></a>

### <a name="assembly-binding-log-viewer"></a>어셈블리 바인딩 로그 뷰어

애플리케이션에서 네이티브 이미지를 사용하고 있는지 확인하려면 [Fuslogvw.exe(어셈블리 바인딩 로그 뷰어)](fuslogvw-exe-assembly-binding-log-viewer.md)를 사용할 수 있습니다. 바인딩 로그 뷰어 창의 **로그 범주** 상자에서 **네이티브 이미지**를 선택합니다. Fuslogvw.exe는 네이티브 이미지를 거부하는 이유에 대한 정보를 제공합니다.

<a name="MDA"></a>

### <a name="the-jitcompilationstart-managed-debugging-assistant"></a>JITCompilationStart 관리 디버깅 도우미

[jitCompilationStart](../debug-trace-profile/jitcompilationstart-mda.md) MDA(관리 디버깅 도우미)를 사용하여 JIT 컴파일러에서 함수 컴파일을 시작하는 시기를 결정할 수 있습니다.

<a name="OptOut"></a>

### <a name="opting-out-of-native-image-generation"></a>네이티브 이미지 생성 옵트아웃

경우에 따라 NGen.exe에서 특정 메서드에 대한 네이티브 이미지를 생성하는 데 문제가 있을 수 있거나, 해당 메서드를 네이티브 이미지로 컴파일하지 않고 JIT 컴파일하려고 할 수도 있습니다. 이 경우 `System.Runtime.BypassNGenAttribute` 특성을 사용하여 NGen.exe에서 특정 메서드에 대한 기본 이미지를 생성하지 못하게 할 수 있습니다. 이 특성은 코드에서 네이티브 이미지에 포함하지 않으려는 각 메서드에 개별적으로 적용해야 합니다. NGen.exe는 특성을 인식하고 해당 메서드의 네이티브 이미지에 코드를 생성하지 않습니다.

그러나 `BypassNGenAttribute`는 .NET Framework 클래스 라이브러리의 형식으로 정의되어 있지 않습니다. 코드에서 이 특성을 사용하려면 먼저 다음과 같이 정의해야 합니다.

[!code-csharp[System.Runtime.BypassNGenAttribute#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/cs/Optout1.cs#1)]
[!code-vb[System.Runtime.BypassNGenAttribute#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/vb/Optout1.vb#1)]

그런 다음 메서드별로 특성을 적용할 수 있습니다. 다음 예제에서는 네이티브 이미지 생성기에 `ExampleClass.ToJITCompile` 메서드에 대한 네이티브 이미지를 생성하지 말아야 한다고 지시합니다.

[!code-csharp[System.Runtime.BypassNGenAttribute#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/cs/Optout1.cs#2)]
[!code-vb[System.Runtime.BypassNGenAttribute#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/vb/Optout1.vb#2)]

## <a name="examples"></a>예

다음 명령은 현재 디렉터리에 있는 `ClientApp.exe`에 대한 네이티브 이미지를 생성하고 그 이미지를 네이티브 이미지 캐시에 저장합니다. 어셈블리에 대해 구성 파일이 존재하는 경우 Ngen.exe는 해당 파일을 사용합니다. 또한 `ClientApp.exe`에서 참조하는 모든 .dll 파일에 대한 네이티브 이미지가 생성됩니다.

```console
ngen install ClientApp.exe
```

Ngen.exe로 설치된 이미지를 루트라고도 합니다. 루트는 애플리케이션 또는 공유 구성 요소일 수 있습니다.

다음 명령은 지정된 경로를 사용하여 `MyAssembly.exe`의 네이티브 이미지를 생성합니다.

```console
ngen install c:\myfiles\MyAssembly.exe
```

어셈블리 및 해당 종속성을 찾을 때 Ngen.exe는 공용 언어 런타임에서 사용한 검색 논리를 사용합니다. 기본적으로 `ClientApp.exe`가 포함된 디렉터리는 애플리케이션 기본 디렉터리로 사용되며 모든 어셈블리 검색은 이 디렉터리에서 시작됩니다. `/AppBase` 옵션을 사용하여 이 동작을 재지정할 수도 있습니다.

> [!NOTE]
> 이것은 애플리케이션 기준이 현재 디렉터리로 설정된 .NET Framework 버전 1.0 및 1.1의 Ngen.exe 동작이 바뀐 것입니다.

예를 들어, 어셈블리에서 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드를 사용하여 .dll 파일을 로드하면 종속성이 참조 없이 어셈블리에 포함될 수 있습니다. `/ExeConfig` 옵션을 사용하는 경우 애플리케이션 어셈블리에 대한 구성 정보를 사용하여 그러한 .dll 파일의 네이티브 이미지를 만들 수 있습니다. 다음 명령은 `MyLib.dll,`에서 구성 정보를 사용하여 `MyApp.exe`의 네이티브 이미지를 생성합니다.

```console
ngen install c:\myfiles\MyLib.dll /ExeConfig:c:\myapps\MyApp.exe
```

이런 식으로 설치한 어셈블리는 애플리케이션을 제거해도 제거되지 않습니다.

종속성을 제거하려면 해당 어셈블리를 설치할 때 사용한 것과 동일한 명령줄 옵션을 사용합니다. 다음 명령은 이전 예제에서 `MyLib.dll`을 제거합니다.

```console
ngen uninstall c:\myfiles\MyLib.dll /ExeConfig:c:\myapps\MyApp.exe
```

전역 어셈블리 캐시에 어셈블리에 대한 네이티브 이미지를 만들려면 어셈블리의 표시 이름을 사용합니다. 예:

```console
ngen install "ClientApp, Version=1.0.0.0, Culture=neutral,
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL"
```

NGen.exe는 설치하는 각 시나리오마다 별도의 이미지 집합을 생성합니다. 예를 들어, 다음 명령은 일반적인 작업을 위한 네이티브 이미지의 전체 집합, 디버깅을 위한 또 다른 전체 집합 및 프로파일링을 위한 집합을 설치합니다.

```console
ngen install MyApp.exe
ngen install MyApp.exe /debug
ngen install MyApp.exe /profile
```

### <a name="displaying-the-native-image-cache"></a>네이티브 이미지 캐시 표시

네이티브 이미지가 캐시에 설치된 후에는 Ngen.exe를 사용하여 표시할 수 있습니다. 다음 명령은 네이티브 이미지 캐시에서 모든 네이티브 이미지를 표시합니다.

```console
ngen display
```

`display` 작업은 먼저 루트 어셈블리를 모두 나열한 다음 모든 네이티브 이미지 목록을 나열합니다.

어셈블리의 단순한 이름을 사용하여 해당 어셈블리에 대한 정보만 표시합니다. 다음 명령은 부분 이름 `MyAssembly`에 일치하는 네이티브 이미지 캐시의 모든 네이티브 이미지, 해당 종속성, `MyAssembly`에서 종속성을 갖는 모든 루트를 표시합니다.

```console
ngen display MyAssembly
```

공유 구성 요소 어셈블리에 의존하는 루트를 알고 있는 것이 공유 구성 요소가 업그레이드된 후 `update` 작업의 영향을 측정하는 데 유용합니다.

어셈블리의 파일 확장명을 지정하는 경우 어셈블리가 포함된 디렉터리에서 경로를 지정하거나 Ngen.exe를 실행해야 합니다.

```console
ngen display c:\myApps\MyAssembly.exe
```

다음 명령은 이름이 `MyAssembly`이고 버전이 1.0.0.0인 네이티브 이미지 캐시의 네이티브 이미지를 모두 표시합니다.

```console
ngen display "myAssembly, version=1.0.0.0"
```

### <a name="updating-images"></a>이미지 업데이트

이미지는 일반적으로 공유 구성 요소가 업그레이드된 후에 업데이트됩니다. 변경되었거나 종속성이 변경된 네이티브 이미지를 모두 업데이트하려면 인수 없이 `update` 작업을 사용합니다.

```console
ngen update
```

모든 이미지를 업데이트하려면 시간이 많이 걸릴 수 있습니다. `/queue` 옵션을 사용하여 네이티브 이미지 서비스에서 실행할 업데이트를 큐에 대기시킬 수 있습니다. `/queue` 옵션 및 설치 우선 순위에 대한 자세한 내용은 [네이티브 이미지 서비스](#native-image-service)를 참조하세요.

```console
ngen update /queue
```

### <a name="uninstalling-images"></a>이미지 제거

Ngen.exe가 종속성 목록을 유지 관리하므로 공유 구성 요소는 공유 구성 요소에 의존하는 모든 어셈블리가 제거된 경우에만 제거됩니다. 또한 공유 구성 요소는 루트로 설치된 경우 제거되지 않습니다.

다음 명령은 루트 `ClientApp.exe`에 대한 시나리오를 모두 제거합니다.

```console
ngen uninstall ClientApp
```

`uninstall` 작업은 특정 시나리오를 제거할 때 사용할 수 있습니다. 다음 명령은 `ClientApp.exe`에 대한 모든 디버그 시나리오를 제거합니다.

```console
ngen uninstall ClientApp /debug
```

> [!NOTE]
> `/debug` 시나리오를 제거해도 `/profile`과 `/debug.`가 모두 포함된 시나리오는 제거되지 않습니다.

다음 명령은 `ClientApp.exe`의 특정 버전에 대한 시나리오를 모두 제거합니다.

```console
ngen uninstall "ClientApp, Version=1.0.0.0"
```

다음 명령은 `"ClientApp, Version=1.0.0.0, Culture=neutral, PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL",`에 대한 모든 시나리오 또는 해당 어셈블리에 대한 디버그 시나리오만 제거합니다.

```console
ngen uninstall "ClientApp, Version=1.0.0.0, Culture=neutral,
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL"
ngen uninstall "ClientApp, Version=1.0.0.0, Culture=neutral,
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL" /debug
```

`install` 작업과 마찬가지로 확장명을 제공하려면 어셈블리가 포함된 디렉터리에서 Ngen.exe를 실행하거나 전체 경로를 지정해야 합니다.

네이티브 이미지 서비스와 관련된 예제는 [네이티브 이미지 서비스](#native-image-service)를 참조하세요.

## <a name="native-image-task"></a>네이티브 이미지 작업

네이티브 이미지 작업은 네이티브 이미지를 생성 및 유지 관리하는 Windows 작업입니다. 네이티브 이미지 작업은 지원되는 시나리오에 대해 자동으로 네이티브 이미지를 생성 및 회수합니다. 또한 설치 관리자가 [Ngen.exe(네이티브 이미지 생성기)](ngen-exe-native-image-generator.md)를 사용하여 지연된 시간에 네이티브 이미지를 만들고 업데이트할 수 있게 합니다.

네이티브 이미지 작업은 각 아키텍처를 대상으로 하는 애플리케이션에 대한 컴파일을 허용하기 위해 컴퓨터에서 지원되는 각 CPU 아키텍처에 대해 한 번 등록됩니다.

|작업 이름|32비트 컴퓨터|64비트 컴퓨터|
|---------------|----------------------|----------------------|
|NET Framework NGEN v4.0.30319|예|예|
|NET Framework NGEN v4.0.30319 64|아니요|예|

Windows 8 이상에서 실행되는 경우 네이티브 이미지 작업은 .NET Framework 4.5 이상 버전에서 사용할 수 있습니다. 이전 버전의 Windows에서는 .NET Framework에서 [네이티브 이미지 서비스](#native-image-service)를 사용합니다.

### <a name="task-lifetime"></a>작업 수명

일반적으로 Windows 작업 스케줄러는 매일 밤 컴퓨터가 유휴 상태일 때 네이티브 이미지 작업을 시작합니다. 작업은 애플리케이션 설치 관리자가 큐에 대기한 지연된 작업, 지연된 네이티브 이미지 업데이트 요청 및 자동 이미지 생성을 모두 확인합니다. 작업은 처리 중인 작업 항목을 완료하고 종료됩니다. 작업이 실행되는 동안 컴퓨터 유휴 상태가 중지되면 작업이 중지됩니다.

작업 스케줄러 UI를 통해 수동으로 또는 NGen.exe 수동 호출을 통해 네이티브 이미지 작업을 시작할 수도 있습니다. 이러한 방법 중 하나로 작업이 시작된 경우 컴퓨터가 더이상 유휴 상태가 아닐 때에도 계속 실행됩니다. NGen.exe를 사용하여 수동으로 만든 이미지는 애플리케이션 설치 관리자에 대해 예측 가능한 동작을 사용할 수 있도록 우선 순위가 지정됩니다.

## <a name="native-image-service"></a>네이티브 이미지 서비스

네이티브 이미지 서비스는 네이티브 이미지를 생성 및 유지 관리하는 Windows 서비스입니다. 네이티브 이미지 서비스를 통해 개발자는 네이티브 이미지의 설치 및 업데이트를 컴퓨터가 유휴 상태인 기간으로 지연시킬 수 있습니다.

일반적으로 네이티브 이미지 서비스는 애플리케이션 또는 업데이트 설치 프로그램(설치 관리자)에 의해 시작됩니다. 우선 순위 3 작업의 경우 서비스가 컴퓨터의 유휴 시간 중에 실행됩니다. 서비스는 상태를 저장하고, 필요한 경우 여러 번 다시 부팅되어도 계속할 수 있습니다. 여러 개의 이미지 컴파일을 큐에 대기시킬 수 있습니다.

또한 서비스는 수동 Ngen.exe 명령과 상호 작용합니다. 수동 명령이 백그라운드 작업보다 우선합니다.

> [!NOTE]
> Windows Vista에서 네이티브 이미지 서비스에 대해 표시되는 이름은 "Microsoft.NET Framework NGEN v2.0.50727_X86" 또는 "Microsoft.NET Framework NGEN v2.0.50727_X64"입니다. Microsoft Windows의 모든 이전 버전에서는 이름이 ".NET Runtime Optimization Service v2.0.50727_X86" 또는 ".NET Runtime Optimization Service v2.0.50727_X64"입니다.

### <a name="launching-deferred-operations"></a>지연된 작업 시작

설치 또는 업그레이드를 시작하기 전에 서비스를 일시 중지하는 것이 좋습니다. 이렇게 하면 설치 관리자가 파일을 복사하거나 어셈블리를 전역 어셈블리 캐시에 저장하는 동안 서비스가 실행되지 않습니다. 다음 Ngen.exe 명령줄은 서비스를 일시 중지합니다.

```console
ngen queue pause
```

지연된 모든 작업이 큐에 대기되고 나면 다음 명령을 통해 서비스를 다시 시작할 수 있습니다.

```console
ngen queue continue
```

새 애플리케이션을 설치하거나 공유 구성 요소를 업데이트할 때 네이티브 이미지 생성을 지연시키려면 `install` 또는 `update` 작업과 함께 `/queue` 옵션을 사용합니다. 다음 Ngen.exe 명령줄은 공유 구성 요소에 대한 네이티브 이미지를 설치하고 영향을 받았을 수 있는 모든 루트의 업데이트를 수행합니다.

```console
ngen install MyComponent /queue
ngen update /queue
```

`update` 작업은 `MyComponent`를 사용하는 이미지뿐 아니라 무효화된 모든 네이티브 이미지를 재생성합니다.

애플리케이션이 많은 루트로 구성된 경우 지연된 작업의 우선 순위를 제어할 수 있습니다. 다음 명령은 세 가지 루트의 설치를 큐에 대기시킵니다. `Assembly1`은 유휴 시간을 기다리지 않고 첫 번째로 설치됩니다. `Assembly2`도 유휴 시간을 기다리지 않고 설치되지만 모든 우선 순위 1 작업이 완료된 후에 설치됩니다. `Assembly3`은 서비스에서 컴퓨터의 유휴 상태를 감지할 때 설치됩니다.

```console
ngen install Assembly1 /queue:1
ngen install Assembly2 /queue:2
ngen install Assembly3 /queue:3
```

`executeQueuedItems` 작업을 사용하여 큐에 대기 중인 작업이 동기적으로 발생하도록 강제할 수 있습니다. 선택적 우선 순위를 제공하는 경우 이 작업은 우선 순위가 같거나 낮은 대기 중인 작업에만 영향을 줍니다. 기본 우선 순위는 3이므로 다음 Ngen.exe 명령은 큐에 대기 중인 모든 작업을 즉시 처리하고 완료될 때까지 반환되지 않습니다.

```console
ngen executeQueuedItems
```

동기 명령은 Ngen.exe에 의해 실행되며 네이티브 이미지 서비스를 사용하지 않습니다. 네이티브 이미지 서비스가 실행되는 동안 Ngen.exe를 사용하여 작업을 실행할 수 있습니다.

### <a name="service-shutdown"></a>서비스 종료

`/queue` 옵션을 포함하는 Ngen.exe 명령을 실행하여 시작된 후 서비스는 모든 작업이 완료 될 때까지 백그라운드에서 실행됩니다. 서비스는 필요한 경우 여러 번 다시 부팅되어도 계속할 수 있도록 상태를 저장합니다. 서비스에서 큐에 대기 중인 작업이 더 이상 없음을 감지하면 다음에 컴퓨터가 부팅될 때 다시 시작되지 않도록 상태를 다시 설정하고 종료됩니다.

### <a name="service-interaction-with-clients"></a>클라이언트와 서비스의 상호 작용

.NET Framework 버전 2.0에서 네이티브 이미지 서비스와의 유일한 상호 작용은 명령줄 도구 Ngen.exe를 통해 수행됩니다. 설치 스크립트의 명령줄 도구를 사용하여 네이티브 이미지 서비스에 대한 작업을 큐에 대기시키고 서비스와 상호 작용할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [도구](index.md)
- [관리되는 실행 프로세스](../../standard/managed-execution-process.md)
- [런타임에서 어셈블리를 찾는 방법](../deployment/how-the-runtime-locates-assemblies.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
