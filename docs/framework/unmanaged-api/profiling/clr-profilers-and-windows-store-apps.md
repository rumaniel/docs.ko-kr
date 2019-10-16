---
title: CLR 프로파일러 및 Windows 스토어 앱
ms.date: 03/30/2017
dev_langs:
- csharp
applies_to:
- Windows 10
- Windows 8
helpviewer_keywords:
- profiling API
- profiling API [.NET Framework]
- profiling managed code
- profiling managed code [Windows Store Apps]
ms.assetid: 1c8eb2e7-f20a-42f9-a795-71503486a0f5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8368930e60210b0cb470700e9c9470c57d536c13
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291418"
---
# <a name="clr-profilers-and-windows-store-apps"></a>CLR 프로파일러 및 Windows 스토어 앱

이 항목에서는 Windows 스토어 응용 프로그램 내에서 실행 되는 관리 코드를 분석 하는 진단 도구를 작성할 때 고려해 야 할 사항에 대해 설명 합니다. 또한 Windows 스토어 앱에 대해 실행 하는 경우에도 계속 작동 하도록 기존 개발 도구를 수정 하는 지침을 제공 합니다. 이 정보를 이해 하려면 공용 언어 런타임 프로 파일링 API에 대해 잘 알고 있는 것이 좋습니다. Windows 데스크톱 응용 프로그램에 대해 올바르게 실행 되는 진단 도구에서이 API를 이미 사용 했으므로 이제 도구를 수정 하는 데 관심이 있습니다. Windows 스토어 앱에 대해 올바르게 실행 됩니다.

## <a name="introduction"></a>소개

소개 단락을 지난 후에는 CLR 프로 파일링 API에 대해 잘 알고 있습니다. 관리 되는 데스크톱 응용 프로그램에 대해 잘 작동 하는 진단 도구를 이미 작성 했습니다. 이제 도구가 관리 되는 Windows 스토어 앱에서 작동 하도록 할 수 있습니다. 아마도 이미이 작업을 수행 하려고 했 고 간단한 작업이 아니라는 것을 발견 했습니다. 실제로 모든 도구 개발자에 게 명확 하지 않을 수 있는 몇 가지 고려 사항이 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

- Windows 스토어 앱은 심각 하 게 감소 된 권한으로 컨텍스트에서 실행 됩니다.

- Windows 메타 데이터 파일은 기존의 관리 되는 모듈에 비해 고유한 특성을 가집니다.

- Windows 스토어 앱은 대화형 작업이 중단 될 때 스스로를 일시 중단 하는 습관을 갖습니다.

- 프로세스 간 통신 메커니즘은 다양 한 이유로 더 이상 작동 하지 않을 수 있습니다.

이 항목에서는 알고 있어야 하는 항목과이를 적절히 처리 하는 방법을 보여 줍니다.

CLR 프로 파일링 API를 처음 접하는 경우이 항목의 끝에 있는 리소스를 건너뛰어 서 더 나은 소개 정보를 찾을 수 있습니다.

특정 Windows Api에 대 한 세부 정보를 제공 하 고이 Api를 사용 하는 방법에 대해서도이 항목에서 다루지 않습니다. 여기에서 참조 하는 Windows Api에 대 한 자세한 내용을 보려면이 항목을 시작 하 고 MSDN을 참조 하십시오.

## <a name="architecture-and-terminology"></a>아키텍처 및 용어

일반적으로 진단 도구에는 다음 그림에 표시 된 것과 같은 아키텍처가 있습니다. "Profiler" 라는 용어를 사용 하지만 대부분의 이러한 도구는 코드 검사, 모의 개체 프레임 워크, 시간 이동 디버깅, 응용 프로그램 모니터링 등의 영역으로 일반적인 성능 또는 메모리 프로 파일링 보다 효과적입니다. 편의상이 항목에서는 이러한 모든 도구를 프로파일러로 계속 참조 합니다.

이 항목 전체에서 사용 되는 용어는 다음과 같습니다.

**응용 프로그램**

프로파일러가 분석 중인 응용 프로그램입니다. 일반적으로이 응용 프로그램의 개발자는 이제 프로파일러를 사용 하 여 응용 프로그램의 문제를 진단 하는 데 도움이 됩니다. 일반적으로이 응용 프로그램은 Windows 데스크톱 응용 프로그램 이지만이 항목에서는 Windows 스토어 앱을 살펴보겠습니다.

**프로파일러 DLL**

분석 중인 응용 프로그램의 프로세스 공간에 로드 되는 구성 요소입니다. 프로파일러 "에이전트" 라고도 하는이 구성 요소는 [ICorProfilerCallback](icorprofilercallback-interface.md)[ICorProfilerCallback 인터페이스](icorprofilercallback-interface.md)(2, 3 등) 인터페이스를 구현 하 고 [ICorProfilerInfo](icorprofilerinfo-interface.md)(2, 3 등) 인터페이스를 사용 하 여에 대 한 데이터를 수집 합니다. 응용 프로그램을 분석 하 고 잠재적으로 응용 프로그램 동작의 측면을 수정 합니다.

**프로파일러 UI**

이 응용 프로그램은 프로파일러 사용자가 상호 작용 하는 데스크톱 응용 프로그램입니다. 사용자에 게 응용 프로그램 상태를 표시 하 고 분석 된 응용 프로그램의 동작을 제어 하는 수단을 제공 합니다. 이 구성 요소는 프로 파일링 되는 응용 프로그램의 프로세스 공간과는 별도로 항상 자체 프로세스 공간에서 실행 됩니다. 프로파일러 UI는 [ICLRProfiling:: AttachProfiler](iclrprofiling-attachprofiler-method.md) 메서드를 호출 하 여 분석 된 응용 프로그램이 시작 시 프로파일러 dll이 로드 되지 않은 경우에 프로파일러 dll을 로드 하도록 하는 "attach 트리거" 역할도 할 수도 있습니다.

> [!IMPORTANT]
> 프로파일러 UI는 windows 스토어 앱을 제어 하 고 보고 하는 데 사용 되는 경우에도 Windows 데스크톱 응용 프로그램으로 유지 되어야 합니다. Windows 스토어에서 진단 도구를 패키지 하 고 배송 하지 못할 수 있습니다. 도구는 Windows 스토어 앱에서 수행할 수 없는 작업을 수행 해야 하며 대부분의 작업은 프로파일러 UI 내에 있습니다.

이 문서 전체에서 샘플 코드는 다음을 가정 합니다.

- 프로파일러 DLL은 CLR 프로 파일링 C++API의 요구 사항에 따라 네이티브 DLL 이어야 하므로로 작성 됩니다.

- 프로파일러 UI는로 C#작성 됩니다. 이렇게 해야 하는 것은 아니지만 프로파일러 UI의 프로세스에 대 한 언어에 대 한 요구 사항이 없기 때문에 간결 하 고 간단한 언어를 선택 하지 않는 이유는 무엇 인가요?

### <a name="windows-rt-devices"></a>Windows RT 장치

Windows RT 장치는 매우 잠금 상태입니다. 타사 프로파일러는 이러한 장치에서 로드 될 수 없습니다. 이 문서에서는 Windows 8 Pc에 대해 집중적으로 설명 합니다.

## <a name="consuming-windows-runtime-apis"></a>Windows 런타임 Api 사용

다음 섹션에서 설명 하는 다양 한 시나리오에서 프로파일러 UI 데스크톱 응용 프로그램은 몇 가지 새로운 Windows 런타임 Api를 사용 해야 합니다. 데스크톱 응용 프로그램에서 사용할 수 있는 Windows 런타임 Api와 데스크톱 응용 프로그램 및 Windows 스토어 앱에서 호출 하는 경우 해당 동작이 다른 지를 이해 하려면 설명서를 참조 합니다.

프로파일러 UI를 관리 코드로 작성 하는 경우 이러한 Windows 런타임 Api를 쉽게 사용 하기 위해 수행 해야 하는 몇 가지 단계가 있습니다. 자세한 내용은 [관리 되는 데스크톱 앱 및 Windows 런타임](https://go.microsoft.com/fwlink/?LinkID=271858) 문서를 참조 하세요.

## <a name="loading-the-profiler-dll"></a>프로파일러 DLL 로드

이 섹션에서는 프로파일러 UI를 통해 Windows 스토어 앱이 프로파일러 DLL을 로드 하는 방법을 설명 합니다. 이 섹션에서 설명 하는 코드는 프로파일러 UI 데스크톱 앱에 속해 있으므로 데스크톱 앱에 안전 하지만 Windows 스토어 앱에 안전 하지 않을 수 있는 Windows Api를 사용 해야 합니다.

프로파일러 UI를 통해 다음과 같은 두 가지 방법으로 프로파일러 DLL이 응용 프로그램의 프로세스 공간에 로드 될 수 있습니다.

- 응용 프로그램 시작 시, 환경 변수에 의해 제어 됩니다.

- 시작 후 응용 프로그램에 연결 하 여 [ICLRProfiling:: AttachProfiler](iclrprofiling-attachprofiler-method.md) 메서드를 호출 합니다.

첫 번째 장애물 중 하나는 Windows 스토어 앱에서 제대로 작동 하기 위해 프로파일러 DLL의 시작 로드 및 연결 로드를 가져오는 것입니다. 두 가지 형식의 로드는 공통적으로 몇 가지 특별 한 고려 사항을 공유 하므로 시작 해 보겠습니다.

### <a name="common-considerations-for-startup-and-attach-loads"></a>시작 및 연결 로드에 대 한 일반적인 고려 사항

**프로파일러 DLL 서명**

Windows에서 프로파일러 DLL을 로드 하려고 하면 프로파일러 DLL이 올바르게 서명 되었는지 확인 합니다. 그렇지 않은 경우 기본적으로 로드에 실패 합니다. 이때 다음과 같은 두 가지 방법을 사용할 수 있습니다.

- 프로파일러 DLL이 서명 되었는지 확인 합니다.

- 도구를 사용 하기 전에 Windows 8 컴퓨터에 개발자 라이선스를 설치 해야 한다는 사실을 사용자에 게 알려줍니다. 이 작업은 Visual Studio에서 자동으로 수행 하거나 명령 프롬프트에서 수동으로 수행할 수 있습니다. 자세한 내용은 [개발자 라이선스 가져오기](https://docs.microsoft.com/previous-versions/windows/apps/hh974578(v=win.10))를 참조 하세요.

**파일 시스템 권한**

Windows 스토어 앱은 기본적으로 s를 다시 사용 하는 파일 시스템의 위치에서 프로파일러 DLL을 로드 하 고 실행할 수 있는 권한이 있어야 합니다. 대부분의 디렉터리에 대해 Windows 스토어 앱에 이러한 권한이 없고 프로파일러 DLL을 로드 하려는 시도가 실패 했습니다. 는 Windows 응용 프로그램 이벤트 로그에 다음과 같은 항목을 생성 합니다.

```output
NET Runtime version 4.0.30319.17929 - Loading profiler failed during CoCreateInstance.  Profiler CLSID: '{xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}'.  HRESULT: 0x80070005.  Process ID (decimal): 4688.  Message ID: [0x2504].
```

일반적으로 Windows 스토어 앱은 디스크의 제한 된 위치 집합에만 액세스할 수 있습니다. 각 Windows 스토어 앱은 모든 Windows 스토어 앱에 대 한 액세스 권한이 부여 된 파일 시스템의 다른 몇 가지 영역 뿐만 아니라 자체 응용 프로그램 데이터 폴더에도 액세스할 수 있습니다. 모든 Windows 스토어 앱에는 기본적으로 모든 Windows 스토어 앱에 대 한 읽기 및 실행 권한이 있으므로 프로파일러 DLL 및 해당 종속성을 Program Files 또는 Program Files (x86)의 어딘가에 설치 하는 것이 가장 좋습니다.

### <a name="startup-load"></a>시작 로드

일반적으로 데스크톱 앱에서 프로파일러 UI는 필요한 CLR 프로 파일링 API 환경 변수 (예: `COR_PROFILER`, `COR_ENABLE_PROFILING`, `COR_PROFILER_PATH`)를 포함 하는 환경 블록을 초기화 하 고 새를 만들어 프로파일러 DLL의 시작 로드를 확인 합니다. 해당 환경 블록을 사용 하는 프로세스입니다. Windows 스토어 앱의 경우에도 마찬가지 이지만 메커니즘은 다릅니다.

**관리자 권한으로 실행 안 함**

프로세스가 Windows 스토어 앱 프로세스 B를 생성 하려고 시도 하는 경우 프로세스 A는 높은 무결성 수준이 아닌 보통 무결성 수준에서 실행 되어야 합니다 (승격 되지 않음). 즉, 프로파일러 UI는 보통 무결성 수준에서 실행 되어야 합니다. 그렇지 않으면 Windows 스토어 앱 시작을 처리 하기 위해 중간 무결성 수준에서 다른 데스크톱 프로세스를 생성 해야 합니다.

**프로 파일링 할 Windows 스토어 앱 선택**

먼저 시작할 Windows 스토어 앱을 프로파일러 사용자에 게 요청 하는 것이 좋습니다. 데스크톱 앱의 경우 파일 찾아보기 대화 상자를 표시 하 고 사용자가 .exe 파일을 찾아 선택 합니다. 그러나 Windows 스토어 앱은 서로 다르며 찾아보기 대화 상자를 사용 하는 것은 적합 하지 않습니다. 대신, 해당 사용자가 선택할 수 있도록 설치 된 Windows 스토어 앱 목록을 사용자에 게 표시 하는 것이 좋습니다.

@No__t-0 클래스를 사용 하 여이 목록을 생성할 수 있습니다. `PackageManager`은 데스크톱 앱에서 사용할 수 있는 Windows 런타임 클래스 이며 실제로 데스크톱 응용 프로그램 *에서만* 사용할 수 있습니다.

에서 C# 데스크톱 응용 프로그램으로 작성 된 가상 프로파일러 UI의 다음 코드 예제는 `PackageManager`을 사용 하 여 Windows 앱 목록을 생성 합니다.

```csharp
string currentUserSID = WindowsIdentity.GetCurrent().User.ToString();
IAppxFactory appxFactory = (IAppxFactory) new AppxFactory();
PackageManager packageManager = new PackageManager();
IEnumerable<Package> packages = packageManager.FindPackagesForUser(currentUserSID);
```

**사용자 지정 환경 블록 지정**

새 COM 인터페이스인 [Ipackagedebugsettings](/windows/desktop/api/shobjidl_core/nn-shobjidl_core-ipackagedebugsettings)를 사용 하면 일부 형식의 진단을 더 쉽게 수행할 수 있도록 Windows 스토어 앱의 실행 동작을 사용자 지정할 수 있습니다. 이러한 메서드 중 하나인 [Enabledebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-enabledebugging)을 사용 하면 자동 프로세스 일시 중단을 사용 하지 않도록 설정 하는 것과 같은 다른 유용한 효과와 함께 환경 블록이 시작 될 때 Windows 스토어 앱에 전달할 수 있습니다. 환경 블록은 CLR에서 프로파일러 DLL을 로드 하는 데 사용 하는 환경 변수 (`COR_PROFILER`, `COR_ENABLE_PROFILING` 및 `COR_PROFILER_PATH)`)를 지정 해야 하기 때문에 중요 합니다.

다음 코드 조각을 살펴봅니다.

```csharp
IPackageDebugSettings pkgDebugSettings = new PackageDebugSettings();
pkgDebugSettings.EnableDebugging(packageFullName, debuggerCommandLine,
                                                                 (IntPtr)fixedEnvironmentPzz);
```

다음과 같은 몇 가지 항목을 받아야 합니다.

- `packageFullName`은 패키지를 반복 하 고 `package.Id.FullName`을 잡기는 동안 결정 될 수 있습니다.

- `debuggerCommandLine`은 조금 더 흥미로운 부분입니다. Windows 스토어 앱에 사용자 지정 환경 블록을 전달 하려면 간단 하 고 간단한 더미 디버거를 작성 해야 합니다. Windows에서 Windows 스토어 앱이 일시 중단 된 후 다음 예제와 같이 명령줄을 사용 하 여 디버거를 시작 하 여 디버거를 연결 합니다.

    ```console
    MyDummyDebugger.exe -p 1336 -tid 1424
    ```

     여기서 `-p 1336`은 Windows 스토어 앱의 프로세스 ID 1336을 의미 하 고 `-tid 1424`은 스레드 ID 1424이 일시 중단 된 스레드 임을 의미 합니다. 더미 디버거는 명령줄에서 ThreadID를 구문 분석 하 고 해당 스레드를 다시 시작한 후 종료 합니다.

     이 작업을 수행 C++ 하는 몇 가지 예제 코드는 다음과 같습니다. 오류 검사를 추가 해야 합니다.

    ```cpp
    int wmain(int argc, wchar_t* argv[])
    {
        // …
        // Parse command line here
        // …

        HANDLE hThread = OpenThread(THREAD_SUSPEND_RESUME,
                                                                  FALSE /* bInheritHandle */, nThreadID);
        ResumeThread(hThread);
        CloseHandle(hThread);
        return 0;
    }
    ```

     이 더미 디버거를 진단 도구 설치의 일부로 배포한 다음 `debuggerCommandLine` 매개 변수에서이 디버거의 경로를 지정 해야 합니다.

**Windows 스토어 앱 시작**

이제 Windows 스토어 앱을 시작 하는 순간에 도달 했습니다. 이미이 작업을 수행한 경우에는 [CreateProcess](/windows/desktop/api/processthreadsapi/nf-processthreadsapi-createprocessa) 가 Windows 스토어 앱 프로세스를 만드는 방법이 아니라는 것을 알게 되었을 것입니다. 대신 [IApplicationActivationManager:: 응용 프로그램](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-iapplicationactivationmanager-activateapplication) 메서드를 사용 해야 합니다. 이렇게 하려면 시작 중인 Windows 스토어 앱의 앱 사용자 모델 ID를 가져와야 합니다. 이는 매니페스트를 통해 약간의 작업을 수행 해야 함을 의미 합니다.

패키지를 반복 하는 동안 (이전 [시작 로드](#startup-load) 섹션의 "프로필에 대 한 Windows 스토어 앱 선택" 참조) 현재 패키지의 매니페스트에 포함 된 응용 프로그램 집합을 가져올 수 있습니다.

```csharp
string manifestPath = package.InstalledLocation.Path + "\\AppxManifest.xml";

AppxPackaging.IStream manifestStream;
SHCreateStreamOnFileEx(
                    manifestPath,
                    0x00000040,     // STGM_READ | STGM_SHARE_DENY_NONE
                    0,              // file creation attributes
                    false,          // fCreate
                    null,           // reserved
                    out manifestStream);

IAppxManifestReader manifestReader = appxFactory.CreateManifestReader(manifestStream);

IAppxManifestApplicationsEnumerator appsEnum = manifestReader.GetApplications();
```

예, 한 패키지에 여러 응용 프로그램이 있을 수 있으며, 각 응용 프로그램에는 고유한 응용 프로그램 사용자 모델 ID가 있습니다. 따라서 사용자에 게 프로 파일링 할 응용 프로그램을 요청 하 고 해당 특정 응용 프로그램에서 응용 프로그램 사용자 모델 ID를 가져올 수 있습니다.

```csharp
while (appsEnum.GetHasCurrent() != 0)
{
    IAppxManifestApplication app = appsEnum.GetCurrent();
    string appUserModelId = app.GetAppUserModelId();
    //...
}
```

마지막으로, 이제 Windows 스토어 앱을 시작 하는 데 필요한 항목이 있습니다.

```csharp
IApplicationActivationManager appActivationMgr = new ApplicationActivationManager();
appActivationMgr.ActivateApplication(appUserModelId, appArgs, ACTIVATEOPTIONS.AO_NONE, out pid);
```

**DisableDebugging을 호출 해야 합니다.**

[Ipackagedebugsettings:: EnableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-enabledebugging)호출 될 때 [ipackagedebugsettings::D isabledebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-disabledebugging) 메서드를 호출 하 여 사용자가 직접 정리 해야 하므로 프로 파일링 세션이 진행 될 때이 작업을 수행 해야 합니다.

### <a name="attach-load"></a>부하 연결

프로파일러 UI는 이미 실행 시작 된 응용 프로그램에 프로파일러 DLL을 연결 하려는 경우 [ICLRProfiling:: AttachProfiler](iclrprofiling-attachprofiler-method.md)를 사용 합니다. Windows 스토어 앱의 경우에도 마찬가지입니다. 그러나 앞에서 설명한 일반적인 고려 사항 외에도 대상 Windows 스토어 앱이 일시 중단 되지 않았는지 확인 합니다.

**EnableDebugging**

시작 로드와 마찬가지로 [Ipackagedebugsettings:: EnableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-enabledebugging) 메서드를 호출 합니다. 환경 블록을 전달 하는 데 필요 하지 않지만 자동 프로세스 일시 중단을 사용 하지 않도록 설정 하는 다른 기능 중 하나가 필요 합니다. 그렇지 않고 프로파일러 UI가 [AttachProfiler](iclrprofiling-attachprofiler-method.md)를 호출 하면 대상 Windows 스토어 앱이 일시 중단 될 수 있습니다. 실제로 사용자가 프로파일러 UI와 상호 작용 하 고 Windows 스토어 앱이 사용자의 화면에서 활성화 되지 않은 경우에이 문제가 발생할 수 있습니다. 그리고 Windows 스토어 앱이 일시 중단 된 경우 CLR이 프로파일러 DLL을 연결 하기 위해 보내는 신호에 응답할 수 없습니다.

따라서 다음과 같은 작업을 수행 합니다.

```csharp
IPackageDebugSettings pkgDebugSettings = new PackageDebugSettings();
pkgDebugSettings.EnableDebugging(packageFullName, null /* debuggerCommandLine */,
                                                                 IntPtr.Zero /* environment */);
```

이는 디버거 명령줄 또는 환경 블록을 지정 하지 않는 경우를 제외 하 고 시작 로드에 대해 수행 하는 것과 동일한 호출입니다.

**DisableDebugging**

프로 파일링 세션이 완료 되 면 항상 [Ipackagedebugsettings::D isableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-disabledebugging) 을 호출 해야 합니다.

## <a name="running-inside-the-windows-store-app"></a>Windows 스토어 앱 내에서 실행

따라서 Windows 스토어 앱은 마지막으로 프로파일러 DLL을 로드 했습니다. 이제 프로파일러 DLL은 허용 되는 Api 및 감소 된 권한으로 실행 하는 방법을 비롯 하 여 Windows 스토어 앱에 필요한 다양 한 규칙에 따라 재생 하는 방법을 잘 알아야 합니다.

### <a name="stick-to-the-windows-store-app-apis"></a>Windows 스토어 앱 Api에 집중

Windows API를 탐색할 때 모든 API는 데스크톱 앱, Windows 스토어 앱 또는 둘 다에 적용 되는 것으로 설명 됩니다. 예를 들어 [InitializeCriticalSectionAndSpinCount](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionandspincount) 함수 설명서의 **요구 사항** 섹션에서는 함수가 데스크톱 앱에만 적용 됨을 나타냅니다. 반면 [InitializeCriticalSectionEx](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionex) 함수는 데스크톱 앱과 Windows 스토어 앱 모두에 사용할 수 있습니다.

프로파일러 DLL을 개발할 때 Windows 스토어 앱 인 것 처럼 처리 하 고 Windows 스토어 앱에서 사용할 수 있는 것으로 문서화 된 Api만 사용 합니다. 종속성을 분석 하 고 (예를 들어, 프로파일러 DLL에 대 한 `link /dump /imports`을 실행 하 여 감사를) 문서를 검색 하 여 어떤 종속성이 확인 되 고 없는지 확인할 수 있습니다. 대부분의 경우 안전 하다 고 문서화 된 최신 형태의 API로 대체 하 여 위반을 수정할 수 있습니다 (예: [InitializeCriticalSectionAndSpinCount](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionandspincount) 를 [InitializeCriticalSectionEx](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionex)로 대체).

프로파일러 dll은 데스크톱 앱에만 적용 되는 Api를 호출 하지만 Windows 스토어 앱 내에서 프로파일러 DLL이 로드 된 경우에도 작동 하는 것 처럼 보일 수 있습니다. Windows 스토어 앱 프로세스에 로드 된 경우 프로파일러 DLL의 Windows 스토어 앱과 함께 사용 하기 위해 문서화 되지 않은 API를 사용 하는 것은 위험 합니다.

- 이러한 Api는 Windows 스토어 앱이 실행 되는 고유한 컨텍스트에서 호출 되는 경우 작동 하지 않을 수 있습니다.

- 이러한 Api는 다양 한 Windows 스토어 앱 프로세스 내에서 호출 될 경우 일관 되 게 작동 하지 않을 수 있습니다.

- 이러한 Api는 현재 버전의 windows에서 Windows 스토어 앱에서 제대로 작동 하는 것 처럼 보일 수 있지만 이후 버전의 Windows에서는 중단 되거나 사용 하지 않도록 설정할 수 있습니다.

가장 좋은 방법은 모든 위반을 해결 하 고 위험을 방지 하는 것입니다.

특정 API 없이는 절대 수행할 수 없으며 Windows 스토어 앱에 적합 한 대체 항목을 찾을 수 없습니다. 이 경우 최소한 다음 작업을 수행 합니다.

- 해당 API를 사용 하 여 살아있는 daylights 테스트, 테스트, 테스트 합니다.

- 이후 버전의 Windows에서 Windows 스토어 앱 내부에서 호출 하는 경우 API가 갑자기 중단 되거나 사라질 수 있음을 이해 합니다. 이는 Microsoft의 호환성 문제로 간주 되지 않으며 사용을 지 원하는 것은 우선 순위가 아닙니다.

### <a name="reduced-permissions"></a>권한 감소

Windows 스토어 앱 사용 권한이 데스크톱 앱과 다른 모든 방법을 나열 하기 위해이 항목의 범위를 벗어납니다. 그러나 프로파일러 DLL (데스크톱 앱과 비교 하 여 Windows 스토어 응용 프로그램에 로드 될 때)에서 모든 리소스에 액세스 하려고 시도 하는 경우에는 동작이 달라 집니다. 파일 시스템은 가장 일반적인 예입니다. 디스크에는 지정 된 Windows 스토어 앱에서 액세스할 수 있는 몇 가지 위치가 있습니다 ( [파일 액세스 및 사용 권한 (Windows 런타임 앱](https://docs.microsoft.com/previous-versions/windows/apps/hh967755(v=win.10))) 참조). 프로파일러 DLL은 동일한 제한이 적용 됩니다. 코드를 철저히 테스트 합니다.

### <a name="inter-process-communication"></a>프로세스 간 통신

이 문서의 시작 부분에 나오는 다이어그램에 표시 된 것 처럼 프로파일러 DLL (Windows 스토어 앱 프로세스 공간에 로드 됨)은 고유한 사용자 지정 프로세스를 통해 프로파일러 UI (별도의 데스크톱 앱 프로세스 공간에서 실행 됨)와 통신 해야 할 수 있습니다. 통신 (IPC) 채널 프로파일러 UI는 프로파일러 DLL로 신호를 전송 하 여 동작을 수정 하 고, 프로파일러 DLL은 분석 된 Windows 스토어 앱의 데이터를 사후 처리 및 프로파일러 사용자에 게 표시 하기 위해 프로파일러 UI로 다시 보냅니다.

대부분의 프로파일러는 이러한 방식으로 작업 해야 하지만 프로파일러 DLL이 Windows 스토어 앱에 로드 될 때 IPC 메커니즘에 대 한 선택은 더 제한적입니다. 예를 들어 명명 된 파이프는 Windows 스토어 앱 SDK에 포함 되지 않으므로 사용할 수 없습니다.

물론 파일은 더 제한 된 방식으로도 여전히에 있습니다. 이벤트를 사용할 수도 있습니다.

**파일을 통해 통신**

대부분의 데이터는 파일을 통해 프로파일러 DLL과 프로파일러 UI 사이에 전달 될 가능성이 높습니다. 핵심은 프로파일러 DLL (Windows 스토어 앱의 컨텍스트에서)과 Profiler UI 모두에 대 한 읽기 및 쓰기 권한이 있는 파일 위치를 선택 하는 것입니다. 예를 들어 임시 폴더 경로는 프로파일러 DLL과 프로파일러 UI 모두에 액세스할 수 있지만 다른 Windows 스토어 앱 패키지는 액세스할 수 없는 위치입니다. 따라서 다른 Windows 스토어 앱 패키지에서 로그 하는 모든 정보를 보호 합니다.

프로파일러 UI와 프로파일러 DLL 모두이 경로를 독립적으로 확인할 수 있습니다. 프로파일러 UI는 현재 사용자에 대해 설치 된 모든 패키지를 반복 하는 경우 (이전 샘플 코드 참조),이 코드 조각과 비슷한 코드를 사용 하 여 임시 폴더 경로를 파생할 수 있는 `PackageId` 클래스에 대 한 액세스를 가져옵니다. (언제나 처럼 간단 하 게 오류 검사가 생략 됩니다.)

```csharp
// C# code for the Profiler UI.
ApplicationData appData =
    ApplicationDataManager.CreateForPackageFamily(
        packageId.FamilyName);

tempDir = appData.TemporaryFolder.Path;
```

한편, 사용자의 프로파일러 DLL은 기본적으로 동일한 작업을 수행할 수 있지만 [Applicationdata. Current](xref:Windows.Storage.ApplicationData.Current%2A) 속성을 사용 하 여 <xref:Windows.Storage.ApplicationData> 클래스를 더욱 쉽게 얻을 수 있습니다.

**이벤트를 통해 통신**

프로파일러 UI와 프로파일러 DLL 간에 간단한 신호 의미 체계가 필요한 경우 Windows 스토어 앱 및 데스크톱 앱 내에서 이벤트를 사용할 수 있습니다.

프로파일러 DLL에서 [Createeventex](/windows/desktop/api/synchapi/nf-synchapi-createeventexa) 함수를 호출 하 여 원하는 이름을 가진 명명 된 이벤트를 만들 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

```cpp
// Profiler DLL in Windows Store app (C++).
CreateEventEx(
    NULL,  // Not inherited
    "MyNamedEvent"
    CREATE_EVENT_MANUAL_RESET, /* explicit ResetEvent() required; leave initial state unsignaled */
    EVENT_ALL_ACCESS);
```

그러면 프로파일러 UI가 Windows 스토어 응용 프로그램의 네임 스페이스에서 명명 된 이벤트를 찾아야 합니다. 예를 들어, 프로파일러 UI는 이벤트 이름을로 지정 하 여 [Createeventex](/windows/desktop/api/synchapi/nf-synchapi-createeventexa)를 호출할 수 있습니다.

`AppContainerNamedObjects\<acSid>\MyNamedEvent`

`<acSid>`은 Windows 스토어 앱의 AppContainer SID입니다. 이 항목의 이전 섹션에서는 현재 사용자에 대해 설치 된 패키지를 반복 하는 방법을 살펴보았습니다. 해당 샘플 코드에서 packageId를 가져올 수 있습니다. PackageId에서 다음과 유사한 코드를 사용 하 여 `<acSid>`을 얻을 수 있습니다.

```csharp
IntPtr acPSID;
DeriveAppContainerSidFromAppContainerName(packageId.FamilyName, out acPSID);

string acSid;
ConvertSidToStringSid(acPSID, out acSid);

string acDir;
GetAppContainerFolderPath(acSid, out acDir);
```

### <a name="no-shutdown-notifications"></a>종료 알림 없음

Windows 스토어 응용 프로그램 내에서 실행 하는 경우 프로파일러 DLL은 [ICorProfilerCallback:: Shutdown](icorprofilercallback-shutdown-method.md) 또는 [DllMain](/windows/desktop/Dlls/dllmain) (`DLL_PROCESS_DETACH`)을 사용 하 여 windows 스토어 앱이 종료 되었음을 프로파일러 dll에 알리기 위해 호출 되지 않아야 합니다. 실제로 호출 되지 않는 것으로 간주 됩니다. 지금까지 대부분의 프로파일러 Dll은 디스크에 캐시를 플러시하고, 파일을 닫고, 다시 프로파일러 UI로 알림을 보내는 등의 편리한 위치로 알림을 사용 했습니다. 그러나 이제 프로파일러 DLL을 약간 다르게 구성 해야 합니다.

프로파일러 DLL은 전달 될 때 정보를 기록 해야 합니다. 성능상의 이유로 일괄 처리의 크기가 일부 임계값을 초과 하 여 메모리에서 정보를 일괄 처리 하 고 디스크에 플러시하 려 할 수 있습니다. 그러나 디스크에 아직 플러시되지 않은 정보는 손실 될 수 있다고 가정 합니다. 즉, 임계값을 신중 하 게 선택 하 고 프로파일러 DLL에서 작성 된 불완전 한 정보를 처리 하기 위해 프로파일러 UI를 확정 해야 합니다.

## <a name="windows-runtime-metadata-files"></a>메타 데이터 파일 Windows 런타임

이 문서는이 문서의 범위를 벗어나므로 WinMD (Windows 런타임 metadata) 파일에 대 한 세부 정보를 제공 합니다. 이 섹션은 사용자의 프로파일러 DLL이 분석 하는 Windows 스토어 앱에서 WinMD 파일을 로드할 때 CLR 프로 파일링 API가 반응 하는 방법으로 제한 됩니다.

### <a name="managed-and-non-managed-winmds"></a>관리 및 관리 되지 않는 Winmd

개발자가 Visual Studio를 사용 하 여 새 Windows 런타임 구성 요소 프로젝트를 만드는 경우 해당 프로젝트의 빌드는 개발자가 작성 한 메타 데이터 (클래스, 인터페이스 등의 형식 설명)를 설명 하는 WinMD 파일을 생성 합니다. 이 프로젝트가 C# 또는 VB로 작성 된 관리 언어 프로젝트인 경우 동일한 WinMD 파일에도 이러한 형식의 구현이 포함 됩니다. 즉, 개발자의 소스 코드에서 컴파일된 모든 IL을 포함 합니다. 이러한 파일은 관리 되는 WinMD 파일 이라고 합니다. Windows 런타임 메타 데이터와 기본 구현이 모두 포함 되어 있기 때문에 흥미로운 점이 있습니다.

이와 대조적으로 개발자가에 대 한 C++Windows 런타임 구성 요소 프로젝트를 만드는 경우 해당 프로젝트의 빌드는 메타 데이터만 포함 된 WinMD 파일을 생성 하며 구현은 별도의 네이티브 DLL로 컴파일됩니다. 마찬가지로 Windows SDK에 제공 되는 WinMD 파일에는 메타 데이터만 포함 되며 구현은 Windows의 일부로 제공 되는 별도의 네이티브 Dll로 컴파일됩니다.

아래 정보는 메타 데이터 및 구현을 포함 하는 관리 되는 Winmd와 메타 데이터만 포함 하는 관리 되지 않는 Winmd에 모두 적용 됩니다.

### <a name="winmd-files-look-like-clr-modules"></a>WinMD 파일이 CLR 모듈과 유사 하 게 보입니다.

CLR이 염려 하는 한 모든 WinMD 파일은 모듈입니다. 따라서 CLR 프로 파일링 API는 다른 관리 되는 모듈에 대 한 것과 동일한 방식으로 WinMD 파일이 로드 될 때 프로파일러 DLL에 지시 하 고의 moduleid 합니다.

프로파일러 DLL은 [ICorProfilerInfo3:: GetModuleInfo2](icorprofilerinfo3-getmoduleinfo2-method.md) 메서드를 호출 하 고 [COR_PRF_MODULE_WINDOWS_RUNTIME](cor-prf-module-flags-enumeration.md) 플래그에 대 한 `pdwModuleFlags` 출력 매개 변수를 검사 하 여 다른 모듈의 WinMD 파일을 구분할 수 있습니다. ModuleID가 WinMD를 나타내는 경우에만 설정 됩니다.

### <a name="reading-metadata-from-winmds"></a>Winmd에서 메타 데이터 읽기

일반 모듈과 같은 WinMD 파일은 [메타 데이터 api](../../../../docs/framework/unmanaged-api/metadata/index.md)를 통해 읽을 수 있는 메타 데이터를 포함 합니다. 그러나 관리 코드에서 프로그램을 실행 하 고 WinMD 파일을 사용 하는 개발자가 보다 자연 스러운 프로그래밍 환경을 사용할 수 있도록 CLR은 WinMD 파일을 읽을 때 Windows 런타임 형식을 .NET Framework 형식에 매핑합니다. 이러한 매핑의 몇 가지 예는 [Windows 스토어 앱 및 Windows 런타임에 대 한 .NET Framework 지원](../../../standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)을 참조 하세요.

따라서 메타 데이터 Api를 사용할 때 프로파일러가 가져오는 뷰 (raw Windows 런타임 뷰 또는 매핑된 .NET Framework 뷰)  대답은 사용자에 게 있습니다.

WinMD에서 [ICorProfilerInfo:: GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md) 메서드를 호출 하 여 [IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)와 같은 메타 데이터 인터페이스를 가져오는 경우 `dwOpenFlags` 매개 변수에서 [ofnotransform](../../../../docs/framework/unmanaged-api/metadata/coropenflags-enumeration.md) 을 설정 하 여이 매핑을 해제할 수 있습니다. 그렇지 않으면 기본적으로 매핑이 사용 됩니다. 일반적으로 프로파일러는 매핑을 사용 하도록 설정 하 여 프로파일러 DLL이 WinMD 메타 데이터에서 가져오는 문자열 (예: 형식 이름)이 프로파일러 사용자에 게 친숙 하 고 자연스럽 게 보이도록 합니다.

### <a name="modifying-metadata-from-winmds"></a>Winmd에서 메타 데이터 수정

Winmd의 메타 데이터 수정은 지원 되지 않습니다. WinMD 파일에 대해 [ICorProfilerInfo:: GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md) 메서드를 호출 하 고 `dwOpenFlags` 매개 변수에 [ofwrite](../../../../docs/framework/unmanaged-api/metadata/coropenflags-enumeration.md) 를 지정 하거나 [IMetaDataEmit](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)와 같은 쓰기 가능 메타 데이터 인터페이스를 요청 하는 경우 [GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md) 가 실패 합니다. 이는 계측을 지원 하기 위해 메타 데이터를 수정 해야 하는 IL 재작성 프로파일러에 특히 중요 합니다. 예를 들어 AssemblyRefs 또는 새 메서드를 추가 합니다. 따라서 이전 섹션에서 설명한 대로 [COR_PRF_MODULE_WINDOWS_RUNTIME](cor-prf-module-flags-enumeration.md) 를 먼저 확인 하 고 이러한 모듈에 쓰기 가능한 메타 데이터 인터페이스를 묻지 않습니다.

### <a name="resolving-assembly-references-with-winmds"></a>Winmd를 사용 하 여 어셈블리 참조 확인

대부분의 프로파일러는 계측 또는 유형 검사를 지원 하기 위해 메타 데이터 참조를 수동으로 확인 해야 합니다. 이러한 프로파일러는 표준 어셈블리 참조와 완전히 다른 방식으로 확인 되므로 CLR에서 Winmd을 가리키는 어셈블리 참조를 확인 하는 방법을 알고 있어야 합니다.

## <a name="memory-profilers"></a>메모리 프로파일러

가비지 수집기 및 관리 되는 힙은 Windows 스토어 앱과 데스크톱 앱에서 근본적으로 다릅니다. 그러나 프로파일러 작성자가 알고 있어야 하는 약간의 차이점이 있습니다.

### <a name="forcegc-creates-a-managed-thread"></a>ForceGC에서 관리 되는 스레드를 만듭니다.

메모리 프로 파일링을 수행할 때 프로파일러 DLL은 일반적으로 [Forcegc 메서드](icorprofilerinfo-forcegc-method.md) 메서드를 호출할 개별 스레드를 만듭니다. 새 항목이 아닙니다. 그러나 Windows 스토어 앱 내에서 가비지 컬렉션을 수행 하는 작업은 스레드를 관리 되는 스레드로 변환할 수 있습니다. 예를 들어 해당 스레드에 대 한 프로 파일링 API ThreadID가 만들어집니다.

이에 대 한 결과를 이해 하려면 CLR 프로 파일링 API에서 정의한 동기 호출과 비동기 호출 간의 차이점을 이해 하는 것이 중요 합니다. 이는 Windows 스토어 앱의 비동기 호출 개념과 매우 다릅니다. 자세한 내용은 블로그 게시물 [CORPROF_E_UNSUPPORTED_CALL_SEQUENCE](https://blogs.msdn.microsoft.com/davbr/2008/12/23/why-we-have-corprof_e_unsupported_call_sequence/) 을 참조 하세요.

관련 점은 프로파일러에서 만든 스레드에 대해 수행 되는 호출은 프로파일러 DLL의 [ICorProfilerCallback](icorprofilercallback-interface.md) 메서드 중 하나를 구현 하는 외부에서 수행 되는 경우에도 항상 동기로 간주 됩니다. 이상 사용 되는 경우 이제 [Forcegc 메서드](icorprofilerinfo-forcegc-method.md)를 호출 하 여 CLR에서 프로파일러의 스레드를 관리 되는 스레드로 전환 했으므로 해당 스레드는 더 이상 프로파일러의 스레드로 간주 되지 않습니다. 따라서 CLR은 해당 스레드에 대해 동기로 한정 되는 항목에 대 한 보다 엄격한 정의를 적용 합니다. 즉, 호출이 프로파일러 DLL의 [ICorProfilerCallback](icorprofilercallback-interface.md) 메서드 중 하나에서 시작 되어야 동기로 한정 됩니다.

실제로는 무엇을 의미 하나요? 대부분의 [ICorProfilerInfo](icorprofilerinfo-interface.md) 메서드는 동기적으로 호출 되는 것이 안전 하며, 그렇지 않은 경우 즉시 실패 합니다. 따라서 프로파일러 DLL이 일반적으로 프로파일러 생성 스레드에 대해 수행 되는 다른 호출 (예: [RequestProfilerDetach](icorprofilerinfo3-requestprofilerdetach-method.md), [RequestReJIT](icorprofilerinfo4-requestrejit-method.md)또는 [Requestrevert](icorprofilerinfo4-requestrevert-method.md))에 대해 [forcegc 메서드](icorprofilerinfo-forcegc-method.md) 스레드를 다시 사용할 경우 문제가 발생할 수 있습니다. . [DoStackSnapshot](icorprofilerinfo2-dostacksnapshot-method.md) 와 같은 비동기 안전 함수에도 관리 되는 스레드에서 호출 될 때 특별 한 규칙이 있습니다. 자세한 내용은 블로그 게시물 [Profiler 스택 탐색을 참조 하세요. 자세한 내용은 기본 사항 및 @ no__t-0 이상입니다.

따라서 프로파일러 DLL이 [Forcegc 메서드](icorprofilerinfo-forcegc-method.md) 를 호출 하는 데 사용 하는 모든 스레드는 gc를 트리거하는 목적 *으로만* 사용 되 고 gc 콜백에 응답 하는 것이 좋습니다. 스택 샘플링 또는 분리와 같은 다른 작업을 수행 하기 위해 프로 파일링 API를 호출 해서는 안 됩니다.

### <a name="conditionalweaktablereferences"></a>ConditionalWeakTableReferences

.NET Framework 4.5부터 프로파일러에 *종속 핸들*에 대 한 자세한 정보를 제공 하는 새로운 GC 콜백 [ConditionalWeakTableElementReferences](icorprofilercallback5-conditionalweaktableelementreferences-method.md)이 있습니다. 이러한 핸들은 GC 수명 관리를 위해 소스 개체에서 대상 개체에 대 한 참조를 효과적으로 추가 합니다. 종속 핸들은 새로운 것은 아니지만 관리 코드에서 프로그래밍 하는 개발자는 Windows 8 및 .NET Framework 4.5 이전에도 <xref:System.Runtime.CompilerServices.ConditionalWeakTable%602?displayProperty=nameWithType> 클래스를 사용 하 여 고유한 종속 핸들을 만들 수 있었습니다.

그러나 관리 되는 XAML Windows 스토어 앱은 이제 종속 핸들을 많이 사용 합니다. 특히 CLR은 관리 되는 개체와 관리 되지 않는 Windows 런타임 개체 간의 참조 주기 관리를 지원 하기 위해이를 사용 합니다. 즉, 힙 그래프의 나머지 가장자리와 함께 시각화할 수 있도록 메모리 프로파일러에서 이러한 종속 핸들에 대 한 정보를 얻는 것 보다 더 중요 합니다. 프로파일러 DLL은 [RootReferences2](icorprofilercallback2-rootreferences2-method.md), [ObjectReferences](icorprofilercallback-objectreferences-method.md)및 [ConditionalWeakTableElementReferences](icorprofilercallback5-conditionalweaktableelementreferences-method.md) 를 함께 사용 하 여 힙 그래프의 전체 뷰를 구성 해야 합니다.

## <a name="conclusion"></a>결론

CLR 프로 파일링 API를 사용 하 여 Windows 스토어 응용 프로그램 내에서 실행 되는 관리 코드를 분석할 수 있습니다. 실제로 개발 중인 기존 프로파일러를 사용 하 여 Windows 스토어 앱을 대상으로 지정할 수 있도록 특정 변경 작업을 수행할 수 있습니다. 프로파일러 UI는 디버깅 모드에서 Windows 스토어 앱을 활성화 하기 위해 새 Api를 사용 해야 합니다. 프로파일러 DLL이 Windows 스토어 앱에 적용 가능한 Api만 사용 하는지 확인 합니다. 프로파일러 DLL과 프로파일러 UI 간의 통신 메커니즘은 windows 스토어 앱 API 제한을 염두에 둔 상태에서 Windows 스토어 앱에 대 한 제한 된 사용 권한을 인식 하 여 작성 해야 합니다. 프로파일러 DLL은 CLR이 Winmd를 처리 하는 방법과 관리 되는 스레드를 기준으로 가비지 수집기의 동작이 어떻게 다른가 무엇 인지 알고 있어야 합니다.

## <a name="resources"></a>리소스

**공용 언어 런타임**

- [프로 파일링 (관리 되지 않는 API 참조)](index.md)

- [메타 데이터 (관리 되지 않는 API 참조)](../metadata/index.md)

**CLR의 Windows 런타임 상호 작용**

- [Windows 스토어 앱 및 Windows 런타임에 대한 .NET Framework 지원](../../../standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)

**Windows 스토어 앱**

- [파일 액세스 및 사용 권한 (Windows 런타임 앱](https://docs.microsoft.com/previous-versions/windows/apps/hh967755%28v=win.10%29)

- [개발자 라이선스 얻기](https://docs.microsoft.com/previous-versions/windows/apps/hh974578%28v=win.10%29)

- [IPackageDebugSettings 인터페이스](/windows/desktop/api/shobjidl_core/nn-shobjidl_core-ipackagedebugsettings)
