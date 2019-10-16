---
title: 사용자 지정 .NET Core 런타임 호스트 작성
description: .NET Core 런타임의 작동 방식을 제어해야 하는 고급 시나리오를 지원하기 위해 네이티브 코드에서 .NET Core 런타임을 호스트하는 방법을 알아봅니다.
author: mjrousos
ms.date: 12/21/2018
ms.custom: seodec18
ms.openlocfilehash: ec63e1b87c4161dcd0dd3ab37aadbef53d4b3219
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70970854"
---
# <a name="write-a-custom-net-core-host-to-control-the-net-runtime-from-your-native-code"></a>사용자 지정 .NET Core 호스트를 작성하여 네이티브 코드에서 .NET 런타임 제어

모든 관리 코드와 같이 .NET Core 애플리케이션은 호스트에서 실행됩니다. 호스트는 런타임(가비지 수집기 및 JIT와 같은 구성 요소 포함)을 시작하고 관리 진입점을 호출합니다.

.NET Core 런타임 호스트는 고급 시나리오이며, .NET Core 빌드 프로세스는 .NET Core 애플리케이션을 실행하는 기본 호스트를 제공하므로 대부분의 경우 .NET Core 개발자는 호스트에 대해 걱정할 필요가 없습니다. 그러나 일부 특수한 경우, 네이티브 프로세스에서 관리 코드를 호출하는 수단으로나 런타임 작동 방식에 대해 더 많은 제어 권한을 얻기 위해 .NET Core 런타임을 명시적으로 호스트한 것이 유용할 수 있습니다.

이 문서에서는 네이티브 코드에서 .NET Core 런타임을 시작하고 관리 코드를 실행하는 데 필요한 단계에 대한 개요를 제공합니다.

## <a name="prerequisites"></a>전제 조건

호스트는 네이티브 애플리케이션이기 때문에 이 자습서에서는 .NET Core를 호스트하는 C++ 애플리케이션을 생성을 다룹니다. [Visual Studio](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs)에서 제공하는 C++ 개발 환경 같은 C++ 개발 환경이 필요합니다.

또한 호스트를 테스트할 간단한 .NET Core 애플리케이션이 필요하므로 [.NET Core SDK](https://dotnet.microsoft.com/download)를 설치하고 [소규모 .NET Core 테스트 앱](with-visual-studio.md)(예: 'Hello World' 앱)을 빌드해야 합니다. 새로운 .NET Core 콘솔 프로젝트 템플릿으로 만든 'Hello World' 앱으로 충분합니다.

## <a name="hosting-apis"></a>호스팅 API
.NET Core를 호스트하는 데 사용할 수 있는 세 가지 API가 있습니다. 이 문서(및 관련 [샘플](https://github.com/dotnet/samples/tree/master/core/hosting))에서는 모든 옵션에 대해 설명합니다.

* .NET Core 3.0 이상에서 .NET Core 런타임을 호스트하는 기본 방법은 `nethost` 및 `hostfxr` 라이브러리 API를 사용하는 것입니다. 이러한 진입점은 런타임을 찾아 초기화에 대해 설정하는 복잡성을 처리하고, 관리형 애플리케이션 시작과 정적 관리형 메서드 호출을 모두 허용합니다.
* .NET Core 3.0 이전 버전에서 .NET Core 런타임을 호스트하는 기본 방법은 [CoreClrHost.h](https://github.com/dotnet/coreclr/blob/master/src/coreclr/hosts/inc/coreclrhost.h) API를 사용하는 것입니다. 이 API는 런타임을 쉽게 시작 및 중지하고, 관리 코드를 호출하는 데 사용할 수 있는 함수를 제공합니다(관리 exe를 실행하거나 정적 관리 메서드를 호출하는 방식).
* [mscoree.h](https://github.com/dotnet/coreclr/blob/master/src/pal/prebuilt/inc/mscoree.h)의 `ICLRRuntimeHost4` 인터페이스를 사용하여 .NET Core를 호스트할 수도 있습니다. 이 API는 CoreClrHost.h보다 오래 되었으므로 이를 사용하는 이전 호스트를 보았을 것입니다. 이 API도 여전히 사용할 수 있으며, CoreClrHost보다 호스팅 프로세스에 대한 더 세부적인 제어를 지원합니다. 하지만 대부분의 시나리오에서는 이제 CoreClrHost.h가 권장됩니다. 더 간단한 API이기 때문입니다.

## <a name="sample-hosts"></a>샘플 호스트
자습서에 설명된 단계를 보여주는 [샘플 호스트](https://github.com/dotnet/samples/tree/master/core/hosting)는 GitHub의 dotnet/samples 리포지토리에서 사용할 수 있습니다. 샘플에 있는 주석은 이 자습서에서 번호가 매겨진 단계를 샘플에서 수행되는 위치와 명확하게 연결합니다. 다운로드 지침은 [샘플 및 자습서](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)를 참조하세요.

샘플 호스트는 학습 목적으로 사용되므로 오류 검사가 부족하며 효율성보다 가독성을 강조하도록 설계되었습니다.

## <a name="create-a-host-using-nethosth-and-hostfxrh"></a>NetHost.h 및 HostFxr.h를 사용하여 호스트 만들기

다음 단계에서는 `nethost` 및 `hostfxr` 라이브러리를 사용하여 네이티브 애플리케이션에서 .NET Core 런타임을 시작하고 관리형 정적 메서드를 호출하는 방법을 자세히 설명합니다. [샘플](https://github.com/dotnet/samples/tree/master/core/hosting/HostWithHostFxr)은 .NET SDK와 함께 설치된 `nethost` 헤더 및 라이브러리와 [dotnet/core-setup](https://github.com/dotnet/core-setup) 리포지토리의 [`coreclr_delegates.h`](https://github.com/dotnet/core-setup/blob/master/src/corehost/cli/coreclr_delegates.h) 및 [`hostfxr.h`](https://github.com/dotnet/core-setup/blob/master/src/corehost/cli/hostfxr.h) 파일 복사본을 사용합니다.

### <a name="step-1---load-hostfxr-and-get-exported-hosting-functions"></a>1단계 - HostFxr 로드 및 내보낸 호스팅 함수 가져오기

`nethost` 라이브러리는 `hostfxr` 라이브러리를 찾기 위한 `get_hostfxr_path` 함수를 제공합니다. `hostfxr` 라이브러리는 .NET Core 런타임을 호스트하기 위한 함수를 공개합니다. 함수의 전체 목록은 [`hostfxr.h`](https://github.com/dotnet/core-setup/blob/master/src/corehost/cli/hostfxr.h) 및 [기본 호스팅 디자인 문서](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/native-hosting.md)에서 확인할 수 있습니다. 샘플 및 이 자습서는 다음을 사용합니다.

* `hostfxr_initialize_for_runtime_config`: 호스트 컨텍스트를 초기화하고, 지정된 런타임 구성을 사용하여 .NET Core 런타임 초기화를 준비합니다.
* `hostfxr_get_runtime_delegate`: 런타임 기능의 대리자를 가져옵니다.
* `hostfxr_close`: 호스트 컨텍스트를 닫습니다.

`get_hostfxr_path`를 사용하여 `hostfxr` 라이브러리를 찾습니다. 라이브러리가 로드되고, 해당 내보내기가 검색됩니다.

[!code-cpp[HostFxrHost#LoadHostFxr](~/samples/core/hosting/HostWithHostFxr/src/NativeHost/nativehost.cpp#LoadHostFxr)]

### <a name="step-2---initialize-and-start-the-net-core-runtime"></a>2단계 - .NET Core 런타임 초기화 및 시작

`hostfxr_initialize_for_runtime_config` 및 `hostfxr_get_runtime_delegate` 함수는 로드되는 관리형 구성 요소에 대한 런타임 구성을 사용하여 .NET Core 런타임을 초기화하고 시작합니다. `hostfxr_get_runtime_delegate` 함수는 관리형 어셈블리를 로드하고 해당 어셈블리의 정적 메서드에 대한 함수 포인터를 가져올 수 있도록 런타임 대리자를 가져오는 데 사용됩니다.

[!code-cpp[HostFxrHost#Initialize](~/samples/core/hosting/HostWithHostFxr/src/NativeHost/nativehost.cpp#Initialize)]

### <a name="step-3---load-managed-assembly-and-get-function-pointer-to-a-managed-method"></a>3단계 - 관리형 어셈블리 로드 및 관리형 메서드에 대한 함수 포인터 가져오기

관리형 어셈블리를 로드하고 관리형 메서드에 대한 함수 포인터를 가져오기 위해 런타임 대리자가 호출됩니다. 대리자는 어셈블리 경로, 형식 이름 및 메서드 이름을 입력으로 사용하고, 관리형 메서드를 호출하는 데 사용할 수 있는 함수 포인터를 반환합니다.

[!code-cpp[HostFxrHost#LoadAndGet](~/samples/core/hosting/HostWithHostFxr/src/NativeHost/nativehost.cpp#LoadAndGet)]

샘플에서는 런타임 대리자를 호출할 때 `nullptr`을 대리자 형식 이름으로 전달하여 기본 시그니처를 관리형 메서드에 사용합니다.

```csharp
public delegate int ComponentEntryPoint(IntPtr args, int sizeBytes);
```

런타임 대리자를 호출할 때 대리자 형식 이름을 지정하면 다른 시그니처를 사용할 수 있습니다.

### <a name="step-4---run-managed-code"></a>4단계 - 관리 코드 실행!

이제 기본 호스트가 관리형 메서드를 호출하고 원하는 매개 변수를 전달할 수 있습니다.

[!code-cpp[HostFxrHost#CallManaged](~/samples/core/hosting/HostWithHostFxr/src/NativeHost/nativehost.cpp#CallManaged)]

## <a name="create-a-host-using-coreclrhosth"></a>CoreClrHost.h를 사용하여 호스트 만들기

다음 단계에서는 CoreClrHost.h API를 사용하여 네이티브 애플리케이션에서 .NET Core 런타임을 시작하고 관리되는 정적 메서드로 호출하는 방법을 자세히 설명합니다. 이 문서의 코드 조각은 Windows 관련 API를 사용하지만 [전체 샘플 호스트](https://github.com/dotnet/samples/tree/master/core/hosting/HostWithCoreClrHost)는 Windows 및 Linux 코드 경로를 모두 보여줍니다.

[Unix CoreRun 호스트](https://github.com/dotnet/coreclr/tree/master/src/coreclr/hosts/unixcorerun)는 coreclrhost.h를 사용하여 더욱 복잡하고 현실적인 호스팅 예를 보여 줍니다.

### <a name="step-1---find-and-load-coreclr"></a>1단계 - CoreCLR 찾기 및 로드

.NET Core 런타임 API는 *coreclr.dll*(Windows), *libcoreclr.so*(Linux) 또는 *libcoreclr.dylib*(macOS)에 있습니다. .NET Core를 호스트하는 첫 번째 단계는 CoreCLR 라이브러리를 로드하는 것입니다. 여러 경로를 검색하거나 입력 매개 변수를 사용하여 라이브러리를 찾는 호스트가 있는 반면, 특정 경로에서 로드하는 것을 아는 호스트도 있습니다(예: 호스트 옆 또는 머신 수준의 위치에서).

발견된 라이브러리는 `LoadLibraryEx`(Windows) 또는 `dlopen`(Linux/Mac)을 사용하여 로드됩니다.

[!code-cpp[CoreClrHost#1](~/samples/core/hosting/HostWithCoreClrHost/src/SampleHost.cpp#1)]

### <a name="step-2---get-net-core-hosting-functions"></a>2단계 - .NET Core 호스팅 함수 가져오기

CoreClrHost에는 .NET Core를 호스팅하는 데 유용한 중요 메서드가 몇 개 있습니다.

* `coreclr_initialize`: .NET Core 런타임을 시작하고 기본(그리고 유일한) AppDomain을 설정합니다.
* `coreclr_execute_assembly`: 관리되는 어셈블리를 실행합니다.
* `coreclr_create_delegate`: 관리되는 메서드에 대한 함수 포인터를 만듭니다.
* `coreclr_shutdown`: .NET Core 런타임을 종료합니다.
* `coreclr_shutdown_2`: `coreclr_shutdown`과 유사하지만 관리 코드의 종료 코드도 검색합니다.

CoreCLR 라이브러리를 로드한 후 다음 단계는 `GetProcAddress`(Windows) 또는 `dlsym`(Linux/Mac)을 사용하여 이러한 함수에 대한 참조를 가져오는 것입니다.

[!code-cpp[CoreClrHost#2](~/samples/core/hosting/HostWithCoreClrHost/src/SampleHost.cpp#2)]

### <a name="step-3---prepare-runtime-properties"></a>3단계 - 런타임 속성 준비

런타임을 시작하기 전에 동작을 지정하는 일부 속성을 준비해야 합니다(특히 어셈블리 로더 관련).

일반적인 속성은 다음과 같습니다.

* `TRUSTED_PLATFORM_ASSEMBLIES` 런타임이 기본적으로 확인할 수 있는 어셈블리 경로의 목록입니다(Windows에서 ‘;’으로 구분되고 Linux에서 ‘:’으로 구분됨). 일부 호스트에는 로드할 수 있는 어셈블리를 나열하는 하드 코딩된 매니페스트가 있습니다. 다른 호스트는 이 목록의 특정 위치(예: *coreclr.dll* 옆)에 라이브러리를 배치합니다.
* `APP_PATHS` TPA(신뢰할 수 있는 플랫폼 어셈블리) 목록에서 찾을 수 없는 경우 어셈블리에 대해 검색하는 경로 목록입니다. 호스트는 TPA 목록을 사용하여 로드되는 어셈블리를 더 세부적으로 제어할 수 있지만 호스트가 로드해야 하는 어셈블리를 결정하고 명시적으로 나열하는 것이 가장 좋은 방법입니다. 하지만 런타임 시 검색이 필요한 경우 이 속성으로 해당 시나리오를 구현할 수 있습니다.
* `APP_NI_PATHS` 이 목록은 네이티브 이미지에 대해 검색되는 경로를 제외하고, APP_PATHS와 비슷합니다.
* `NATIVE_DLL_SEARCH_DIRECTORIES` 이 속성은 p/invoke를 통해 호출되는 네이티브 라이브러리를 찾을 때 로더에서 검색해야 하는 경로 목록입니다.
* `PLATFORM_RESOURCE_ROOTS` 이 목록에는 (문화권별 하위 디렉터리에서) 리소스 위성 어셈블리에 대해 검색하는 경로가 포함됩니다.

이 샘플 호스트에서는 현재 디렉터리의 모든 라이브러리를 나열하기만 하면 TPA 목록이 작성됩니다.

[!code-cpp[CoreClrHost#7](~/samples/core/hosting/HostWithCoreClrHost/src/SampleHost.cpp#7)]

간단한 샘플이기 때문에 `TRUSTED_PLATFORM_ASSEMBLIES` 속성만 있으면 됩니다.

[!code-cpp[CoreClrHost#3](~/samples/core/hosting/HostWithCoreClrHost/src/SampleHost.cpp#3)]

### <a name="step-4---start-the-runtime"></a>4단계 - 런타임 시작

mscoree.h 호스팅 API(아래에 설명)와 달리 CoreCLRHost.h API는 런타임을 시작하고 기본 AppDomain을 만드는 작업을 모두 단일 호출로 처리합니다. `coreclr_initialize` 함수는 이전에 설명한 기본 경로, 이름, 속성을 허용하고, `hostHandle` 매개 변수를 통해 호스트에 대한 핸들을 다시 반환합니다.

[!code-cpp[CoreClrHost#4](~/samples/core/hosting/HostWithCoreClrHost/src/SampleHost.cpp#4)]

### <a name="step-5---run-managed-code"></a>5단계 - 관리 코드 실행

런타임이 시작되면 호스트가 관리 코드를 호출할 수 있습니다. 이는 두 가지 방법으로 수행할 수 있습니다. 이 자습서에 연결된 샘플 코드는 `coreclr_create_delegate` 함수를 사용하여 정적 관리 메서드에 대한 대리자를 만듭니다. 이 API는 [어셈블리 이름](../../standard/assembly/names.md), 네임스페이스로 한정된 형식 이름, 메서드 이름을 입력으로 허용하고, 메서드를 호출하는 데 사용할 수 있는 대리자를 반환합니다.

[!code-cpp[CoreClrHost#5](~/samples/core/hosting/HostWithCoreClrHost/src/SampleHost.cpp#5)]

이 샘플에서 호스트는 이제 `managedDelegate`를 호출하여 `ManagedWorker.DoWork` 메서드를 실행할 수 있습니다.

또는 `coreclr_execute_assembly` 함수를 사용하여 관리되는 실행 파일을 실행할 수 있습니다. 이 API는 어셈블리 경로 및 인수 배열을 입력매개 변수로 허용합니다. 해당 경로의 어셈블리를 로드하고 기본 메서드를 호출합니다.

```C++
int hr = executeAssembly(
        hostHandle,
        domainId,
        argumentCount,
        arguments,
        "HelloWorld.exe",
        (unsigned int*)&exitCode);
```

### <a name="step-6---shutdown-and-clean-up"></a>6단계 - 종료 및 정리

마지막으로 호스트가 관리 코드 실행을 완료하면 `coreclr_shutdown` 또는 `coreclr_shutdown_2`를 사용하여 .NET Core 런타임이 종료됩니다.

[!code-cpp[CoreClrHost#6](~/samples/core/hosting/HostWithCoreClrHost/src/SampleHost.cpp#6)]

CoreCLR은 다시 초기화 또는 언로드를 지원하지 않습니다. `coreclr_initialize`를 다시 호출하거나 CoreCLR 라이브러리를 언로드하지 마세요.

## <a name="create-a-host-using-mscoreeh"></a>Mscoree.h를 사용하여 호스트 만들기

이전에 말했듯이 .NET Core 런타임을 호스팅할 때 권장되는 방법은 이제 CoreClrHost.h입니다. CoreClrHost.h 인터페이스로 충분하지 않은 경우에는 `ICLRRuntimeHost4` 인터페이스를 여전히 사용할 수 있습니다(예를 들어 비표준 시작 플래그가 필요하거나 기본 도메인에서 AppDomainManager가 필요한 경우). 이러한 지침에서는 mscoree.h를 사용하여 .NET Core를 호스트하는 방법을 안내합니다.

[CoreRun 호스트](https://github.com/dotnet/coreclr/tree/master/src/coreclr/hosts/corerun)는 mscoree.h를 사용하여 더욱 복잡하고 현실적인 호스팅 예를 보여 줍니다.

### <a name="a-note-about-mscoreeh"></a>mscoree.h에 대한 정보
`ICLRRuntimeHost4` .NET Core 호스팅 인터페이스는 [MSCOREE.IDL](https://github.com/dotnet/coreclr/blob/master/src/inc/MSCOREE.IDL)에 정의됩니다. 호스트에서 참조해야 할 이 파일의 헤더 버전(mscoree.h)은 [.NET Core 런타임](https://github.com/dotnet/coreclr/)이 빌드될 때 MIDL을 통해 생성됩니다. .NET Core 런타임을 빌드하지 않으려는 경우 mscoree.h는 dotnet/coreclr 리포지토리에 [미리 빌드된 헤더](https://github.com/dotnet/coreclr/tree/master/src/pal/prebuilt/inc)로 제공됩니다. [.NET Core 런타임 빌드에 대한 지침](https://github.com/dotnet/coreclr#building-the-repository)은 GitHub 리포지토리에서 찾을 수 있습니다.

### <a name="step-1---identify-the-managed-entry-point"></a>1단계 - 관리되는 진입점 식별
필요한 헤더(예: [mscoree.h](https://github.com/dotnet/coreclr/tree/master/src/pal/prebuilt/inc/mscoree.h) 및 stdio.h)를 참조한 후 .NET Core 호스트에서는 가장 먼저 사용할 관리되는 진입점을 찾아야 합니다. 샘플 호스트에서는 `main` 메서드가 실행될 관리되는 이진 파일에 대한 경로로 첫 번째 명령줄 인수를 호스트로 사용하여 관리되는 진입점을 찾습니다.

[!code-cpp[NetCoreHost#1](~/samples/core/hosting/HostWithMscoree/host.cpp#1)]

### <a name="step-2---find-and-load-coreclr"></a>2단계 - CoreCLR 찾기 및 로드
.NET Core 런타임 API는 *CoreCLR.dll*(Windows)에 있습니다. 호스팅 인터페이스(`ICLRRuntimeHost4`)를 가져오려면 *CoreCLR.dll*를 찾고 로드해야 합니다. 호스트에 따라 *CoreCLR.dll*을 찾는 방법에 대한 규칙을 정의합니다. 일부 호스트에서는 잘 알려진 머신 수준의 위치(예: *%programfiles%\dotnet\shared\Microsoft.NETCore.App\2.1.6*)에 파일이 있습니다. 다른 호스트에서는 *CoreCLR.dll*이 호스트 자체 또는 호스트되는 앱 옆의 위치에서 로드됩니다. 라이브러리를 찾기 위해 환경 변수를 참조할 수 있습니다.

Linux 또는 Mac에서 핵심 런타임 라이브러리는 각각 *libcoreclr.so* 또는 *libcoreclr.dylib*입니다.

샘플 호스트는 *CoreCLR.dll*에 대해 몇 가지 일반적인 위치를 검색합니다. 위치를 찾으면 `LoadLibrary`(또는 Linux/Mac에서`dlopen`)를 통해 로드되어야 합니다.

[!code-cpp[NetCoreHost#2](~/samples/core/hosting/HostWithMscoree/host.cpp#2)]

### <a name="step-3---get-an-iclrruntimehost4-instance"></a>3단계 - ICLRRuntimeHost4 인스턴스 가져오기
`ICLRRuntimeHost4` 호스팅 인터페이스는 `GetCLRRuntimeHost`에서 `GetProcAddress`(또는 Linux/Mac에서 `dlsym`)를 호출한 다음 해당 함수를 호출하여 검색됩니다.

[!code-cpp[NetCoreHost#3](~/samples/core/hosting/HostWithMscoree/host.cpp#3)]

### <a name="step-4---set-startup-flags-and-start-the-runtime"></a>4단계 - 시작 플래그 설정 및 런타임 시작
`ICLRRuntimeHost4`를 사용하여 이제 전체 런타임의 시작 플래그를 지정하고 런타임을 시작할 수 있습니다. 시작 플래그는 사용할 GC(가비지 수집기)(동시 또는 서버), 단일 AppDomain을 사용할지 여러 AppDomain을 사용할지 여부, 사용할 로더 최적화 정책(도메인 중립적인 어셈블리 로드에 대해)을 결정합니다.

[!code-cpp[NetCoreHost#4](~/samples/core/hosting/HostWithMscoree/host.cpp#4)]

런타임은 `Start` 함수에 대한 호출로 시작됩니다.

```C++
hr = runtimeHost->Start();
```

### <a name="step-5---preparing-appdomain-settings"></a>5단계 - AppDomain 설정 준비
런타임이 시작되면 AppDomain을 설정합니다. .NET AppDomain을 만들 때 지정해야 하는 옵션이 여러 개 있지만 먼저 그러한 옵션을 준비해야 합니다.

AppDomain 플래그는 보안 및 interop와 관련된 AppDomain 동작을 지정합니다. 이전 Silverlight 호스트는 샌드박스 사용자 코드에 이러한 설정을 사용했지만, 최신.NET Core 호스트는 완전 신뢰 상태로 사용자 코드를 실행하고 interop을 사용하도록 설정합니다.

[!code-cpp[NetCoreHost#5](~/samples/core/hosting/HostWithMscoree/host.cpp#5)]

사용할 AppDomain 플래그를 결정한 후 AppDomain 속성을 정의해야 합니다. 속성은 문자열의 키/값 쌍입니다. 많은 속성은 AppDomain이 어셈블리를 로드하는 방법과 관련됩니다.

일반적인 AppDomain 속성에는 다음이 포함됩니다.

* `TRUSTED_PLATFORM_ASSEMBLIES` AppDomain에서 로드의 우선 순위를 지정하고 완전 신뢰(부분적으로 신뢰할 수 있는 도메인에서도)를 제공해야 하는 어셈블리 경로 목록입니다(Windows에서 `;`으로 구분되고 Linux/Mac에서 `:`으로 구분됨). 이 목록에는 'Framework' 어셈블리 및 .NET Framework 시나리오에서 GAC와 비슷한 기타 신뢰할 수 있는 모듈이 포함됩니다. 일부 호스트는 이 목록에서 *coreclr.dll* 옆에 라이브러리를 배치하고, 일부에는 목적에 대해 신뢰할 수 있는 어셈블리를 나열하는 하드 코드된 매니페스트가 있습니다.
* `APP_PATHS` TPA(신뢰할 수 있는 플랫폼 어셈블리) 목록에서 찾을 수 없는 경우 어셈블리에 대해 검색하는 경로 목록입니다. 호스트는 TPA 목록을 사용하여 로드되는 어셈블리를 더 세부적으로 제어할 수 있지만 호스트가 로드해야 하는 어셈블리를 결정하고 명시적으로 나열하는 것이 가장 좋은 방법입니다. 하지만 런타임 시 검색이 필요한 경우 이 속성으로 해당 시나리오를 구현할 수 있습니다.
* `APP_NI_PATHS` 이 목록은 네이티브 이미지에 대해 검색되는 경로를 제외하고, APP_PATHS와 아주 비슷합니다.
* `NATIVE_DLL_SEARCH_DIRECTORIES` 이 속성은 p/invoke를 통해 호출되는 네이티브 DLL을 찾을 때 로더에서 검색해야 하는 경로 목록입니다.
* `PLATFORM_RESOURCE_ROOTS` 이 목록에는 (문화권별 하위 디렉터리에서) 리소스 위성 어셈블리에 대해 검색하는 경로가 포함됩니다.

[간단한 샘플 호스트](https://github.com/dotnet/samples/tree/master/core/hosting/HostWithMscoree)에서는 이러한 속성이 다음과 같이 설정됩니다.

[!code-cpp[NetCoreHost#6](~/samples/core/hosting/HostWithMscoree/host.cpp#6)]

### <a name="step-6---create-the-appdomain"></a>6단계 - AppDomain 만들기
모든 AppDomain 플래그 및 속성이 준비되면 `ICLRRuntimeHost4::CreateAppDomainWithManager`를 사용하여 AppDomain을 설정할 수 있습니다. 이 함수는 선택적으로 정규화된 어셈블리 이름 및 형식 이름을 가져와서 도메인의 AppDomain 관리자로 사용합니다. AppDomain 관리자는 호스트에서 AppDomain 동작의 일부 측면을 제어하도록 허용할 수 있고, 호스트에서 사용자 코드를 직접 호출하지 않는 경우 관리 코드를 실행하기 위한 진입점을 제공할 수 있습니다.

[!code-cpp[NetCoreHost#7](~/samples/core/hosting/HostWithMscoree/host.cpp#7)]

### <a name="step-7---run-managed-code"></a>7단계 - 관리 코드 실행
AppDomain이 실행 중이면 호스트에서 이제 관리 코드를 실행할 수 있습니다. `ICLRRuntimeHost4::ExecuteAssembly`를 사용하여 관리되는 어셈블리의 진입점 메서드를 호출하면 가장 쉽게 관리 코드를 실행할 수 있습니다. 이 함수는 단일 도메인 시나리오에서만 작동합니다.

[!code-cpp[NetCoreHost#8](~/samples/core/hosting/HostWithMscoree/host.cpp#8)]

`ExecuteAssembly`가 호스트의 요구 사항을 충족하지 않는 경우 `CreateDelegate`를 사용하여 정적 관리 메서드에 대한 함수 포인터를 만듭니다. 이 경우 호스트에서 호출하는 메서드의 시그니처를 알아야 하지만(함수 포인터 형식을 만들기 위해) 호스트는 어셈블리의 진입점이 아닌 코드를 호출할 수 있습니다. 두 번째 매개 변수에 제공된 어셈블리 이름은 로드할 라이브러리의 [전체 관리형 어셈블리 이름](../../standard/assembly/names.md) 입니다.

```C++
void *pfnDelegate = NULL;
hr = runtimeHost->CreateDelegate(
    domainId,
    L"HW, Version=1.0.0.0, Culture=neutral", // Target managed assembly
    L"ConsoleApplication.Program",           // Target managed type
    L"Main",                                 // Target entry point (static method)
    (INT_PTR*)&pfnDelegate);

((MainMethodFp*)pfnDelegate)(NULL);
```

### <a name="step-8---clean-up"></a>8단계 - 정리
마지막으로 호스트는 AppDomain을 언로드하고, 런타임을 중지하고, `ICLRRuntimeHost4` 참조를 릴리스하여 자체 정리해야 합니다.

[!code-cpp[NetCoreHost#9](~/samples/core/hosting/HostWithMscoree/host.cpp#9)]

CoreCLR은 언로드를 지원하지 않습니다. CoreCLR 라이브러리를 언로드하지 마세요.

## <a name="conclusion"></a>결론
호스트가 빌드되면 명령줄에서 실행하고 호스트에서 예상하는 인수(예: mscoree example 호스트에서 실행할 관리 앱)를 전달하여 테스트할 수 있습니다. 실행할 호스트에 대해 .NET Core 앱을 지정할 때 `dotnet build`로 생성된 .dll을 사용하세요. 자체 포함된 애플리케이션에 대해 `dotnet publish`로 생성된 실행 파일(.exe 파일)이 실제로 기본 .NET Core 호스트이며(앱이 주 시나리오의 명령줄에서 직접 실행될 수 있음), 사용자 코드는 동일한 이름의 DLL로 컴파일됩니다.

처음에 작동되지 않으면, 호스트가 예상한 위치에서 *coreclr.dll*을 사용할 수 있고, 필요한 프레임워크 라이브러리가 모두 TPA 목록에 있으며 CoreCLR의 비트 수(32비트 또는 64비트)가 호스트가 빌드된 방식과 일치하는지 다시 확인합니다.

.NET Core 런타임 호스트는 일부 개발자만 필요로 하는 고급 시나리오이지만, 네이티브 프로세스에서 관리 코드를 실행해야 하거나 .NET Core 런타임의 동작에 대해 더 많은 제어권이 필요한 경우 아주 유용할 수 있습니다.
