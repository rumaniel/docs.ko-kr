---
title: Fuslogvw.exe(어셈블리 바인딩 로그 뷰어)
ms.date: 03/30/2017
helpviewer_keywords:
- failed assembly binds
- Fuslogvw.exe
- displaying failed assembly bind details
- assemblies [.NET Framework], failed assembly binds
- locating assemblies
- Assembly Binding Log Viewer
ms.assetid: e32fa443-0778-4cc3-bf36-5c8ea297d296
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6077acab533ecb755ae42b7c4359a6c77ff33449
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044673"
---
# <a name="fuslogvwexe-assembly-binding-log-viewer"></a>Fuslogvw.exe(어셈블리 바인딩 로그 뷰어)

어셈블리 바인딩 로그 뷰어는 어셈블리 바인딩에 대한 자세한 내용을 표시합니다. 이 정보를 검토하면 .NET Framework에서 런타임에 어셈블리를 찾지 못하는 이유를 진단할 수 있습니다. 이러한 오류는 일반적으로 어셈블리가 잘못된 위치에 배포되었거나 네이티브 이미지가 더 이상 유효하지 않거나 버전 번호 또는 문화권이 일치하지 않기 때문에 일어납니다. 공용 언어 런타임의 어셈블리 찾기 오류는 일반적으로 애플리케이션에서 <xref:System.TypeLoadException>으로 나타납니다.

> [!IMPORTANT]
> Fuslogvw.exe는 관리자 권한으로 실행해야 합니다.

이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 관리자 자격 증명과 함께 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.

명령 프롬프트에 다음을 입력합니다.

```console
fuslogvw
```

뷰어에서는 실패한 각 어셈블리 바인딩의 엔트리를 표시하고 실패한 각각의 경우에 대해 바인딩을 시작한 애플리케이션, 바인딩 대상 어셈블리(이름, 버전, 문화권, 공개 키 포함) 및 오류가 발생한 날짜와 시간 등에 대해 설명합니다.

### <a name="to-change-the-log-location-view"></a>로그 위치 보기를 변경하려면

1. **기본값** 옵션 단추를 선택하여 모든 애플리케이션 종류에 대한 바인딩 실패를 봅니다. 기본적으로 로그 항목은 디스크의 사용자별 디렉터리에서 wininet 캐시에 저장됩니다.

2. **사용자 지정** 옵션 단추를 선택하여 사용자 지정 디렉터리의 바인딩 오류를 봅니다. 유효한 디렉터리 이름을 위해 **로그 설정** 대화 상자에서 사용자 지정 로그 위치를 설정하여 런타임에 로그를 저장할 사용자 지정 위치를 지정해야 합니다. 이 디렉터리는 런타임에 생성되는 파일만 포함해야 합니다. 실패하여 로그를 남길 수 있는 실행 파일이 들어 있으면 도구에서 실행 파일과 같은 이름으로 디렉터리를 만들려고 시도하므로 실패한 경우 로그를 남길 수 없습니다. 또한 로그 위치에서 실행 파일을 실행할 수 없습니다.

    > [!NOTE]
    > 사용자 지정 바인딩 위치보다 기본 바인딩 위치를 사용하는 것이 좋습니다. 런타임은 기본 바인딩 위치를 wininet 캐시에 저장하기 때문에 자동으로 이 위치를 비웁니다. 그러나 사용자 지정 바인딩 위치를 지정하는 경우에는 사용자가 직접 비워야 합니다.

### <a name="to-view-details-about-a-specific-failure"></a>특정 오류에 대한 자세한 내용을 보려면

1. 뷰어에서 원하는 엔트리의 애플리케이션 이름을 선택합니다.

2. **로그 보기** 단추를 클릭합니다. 또는 선택한 엔트리를 두 번 클릭할 수도 있습니다.

    다음과 같이 선택한 바인딩 오류에 대한 자세한 내용이 표시됩니다.

    - "파일을 찾을 수 없습니다." 또는 "버전이 일치하지 않습니다." 등 바인딩이 실패한 특정 원인

    - 이름, 애플리케이션의 루트 디렉터리(AppBase) 및 개인 검색 경로(있는 경우)의 설명 등을 포함하여 바인딩을 시작한 애플리케이션에 대한 정보

    - 도구에서 찾고 있는 어셈블리의 ID

    - 적용된 애플리케이션, 게시자 또는 관리자 버전 정책 설명

    - [전역 어셈블리 캐시](../app-domains/gac.md)에 어셈블리가 있는지 여부

    - 검색하는 모든 URL 목록

다음 샘플 로그 엔트리는 실패한 어셈블리 바인딩에 대한 자세한 정보를 보여 줍니다.

```output
*** Assembly Binder Log Entry  (3/5/2007 @ 12:54:20 PM) ***

The operation failed.
Bind result: hr = 0x80070002. The system cannot find the file specified.

Assembly manager loaded from:  C:\WINNT\Microsoft.NET\Framework\v2.0.50727\fusion.dll
Running under executable  C:\Program Files\Microsoft.NET\FrameworkSDK\Samples\Tutorials\resourcesandlocalization\graphic\cs\graphicfailtest.exe
--- A detailed error log follows.

=== Pre-bind state information ===
LOG: DisplayName = graphicfailtest.resources, Version=0.0.0.0, Culture=en-US, PublicKeyToken=null
 (Fully-specified)
LOG: Appbase = C:\Program Files\Microsoft.NET\FrameworkSDK\Samples\Tutorials\resourcesandlocalization\graphic\cs\
LOG: Initial PrivatePath = NULL
LOG: Dynamic Base = NULL
LOG: Cache Base = NULL
LOG: AppName = NULL
Calling assembly : graphicfailtest, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null.
===

LOG: Processing DEVPATH.
LOG: DEVPATH is not set. Falling through to regular bind.
LOG: Policy not being applied to reference at this time (private, custom, partial, or location-based assembly bind).
LOG: Post-policy reference: graphicfailtest.resources, Version=0.0.0.0, Culture=en-US, PublicKeyToken=null
LOG: Attempting download of new URL file:///C:/Program Files/Microsoft.NET/FrameworkSDK/Samples/Tutorials/resourcesandlocalization/graphic/cs/graphicfailtest.resources.DLL.
LOG: Attempting download of new URL file:///C:/Program Files/Microsoft.NET/FrameworkSDK/Samples/Tutorials/resourcesandlocalization/graphic/cs/graphicfailtest.resources/graphicfailtest.resources.DLL.
LOG: Attempting download of new URL file:///C:/Program Files/Microsoft.NET/FrameworkSDK/Samples/Tutorials/resourcesandlocalization/graphic/cs/graphicfailtest.resources.EXE.
LOG: Attempting download of new URL file:///C:/Program Files/Microsoft.NET/FrameworkSDK/Samples/Tutorials/resourcesandlocalization/graphic/cs/graphicfailtest.resources/graphicfailtest.resources.EXE.
LOG: All probing URLs attempted and failed.
```

### <a name="to-delete-a-single-entry-from-the-log"></a>로그에서 단일 엔트리를 삭제하려면

1. 뷰어에서 엔트리를 선택합니다.

2. **항목 삭제** 단추를 클릭합니다.

### <a name="to-delete-all-entries-from-the-log"></a>로그에서 모든 엔트리를 삭제하려면

- **모두 삭제** 단추를 클릭합니다.

### <a name="to-refresh-the-user-interface"></a>사용자 인터페이스를 새로 고치려면

- **새로 고침** 단추를 클릭합니다. 뷰어는 실행 중인 동안에는 새 로그 엔트리를 자동으로 검색하지 않습니다. 새 항목을 표시하려면 **새로 고침** 단추를 사용해야 합니다.

### <a name="to-change-the-log-settings"></a>로그 설정을 변경하려면

- **설정** 단추를 클릭하여 **로그 설정** 대화 상자를 엽니다.

### <a name="to-view-the-about-dialog"></a>정보 상자를 보려면

- **정보** 단추를 클릭합니다.

## <a name="binding-logs-for-native-images"></a>네이티브 이미지에 대한 바인딩 로그

기본적으로 Fuslogvw.exe는 일반 어셈블리 바인딩 요청을 기록합니다. 또는 [Ngen.exe(네이티브 이미지 생성기)](ngen-exe-native-image-generator.md)를 사용하여 생성된 네이티브 이미지에 대한 어셈블리 바인딩을 기록할 수 있습니다.

#### <a name="to-log-assembly-binds-for-native-images"></a>네이티브 이미지에 대한 어셈블리 바인딩을 기록하려면

- **로그 범주** 그룹에서 **네이티브 이미지** 옵션 단추를 선택합니다.

다음 로그에서는 애플리케이션에 대한 네이티브 이미지가 생성되었을 때 종속성이 존재하지 않아 발생한 실패를 보여 줍니다. 런타임에서의 종속성과 Ngen.exe가 실행될 때의 종속성이 다른 경우 네이티브 이미지에 대한 바인딩을 사용할 수 없습니다.

```output
*** Assembly Binder Log Entry  (12/8/2006 @ 5:22:07 PM) ***

The operation failed.
Bind result: hr = 0x80070002. The system cannot find the file specified.

Assembly manager loaded from:  E:\Windows\Microsoft.NET\Framework64\v2.0.50727\mscorwks.dll
Running under executable  E:\test\App.exe
--- A detailed error log follows.

LOG: Start binding of native image App, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null.
LOG: IL assembly loaded from E:\test\App.exe.
LOG: Start validating native image App, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null.
LOG: Start validating all the dependencies.
LOG: [Level 1]Start validating native image dependency mscorlib, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089.
LOG: Dependency evaluation succeeded.
LOG: [Level 1]Start validating IL dependency b, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null.
WRN: Dependency assembly was not found at ngen time, but is found at binding time. Disallow using this native image.
WRN: No matching native image found.
LOG: Bind to native image assembly did not succeed. Use IL image.
```

다음 로그에서는 애플리케이션이 실행되었을 때의 컴퓨터 보안 설정이 네이티브 이미지가 생성되었을 때의 보안 설정과 달라 발생하는 네이티브 이미지 바인딩 실패를 보여 줍니다.

```output
*** Assembly Binder Log Entry  (12/8/2006 @ 5:29:09 PM) ***

The operation failed.
Bind result: hr = 0x80004005. Unspecified error

Assembly manager loaded from:  E:\Windows\Microsoft.NET\Framework64\v2.0.50727\mscorwks.dll
Running under executable  E:\test\Application101622.exe
--- A detailed error log follows.

LOG: Start binding of native image Application101622, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null.
LOG: IL assembly loaded from E:\test\Application101622.exe.
LOG: Start validating native image Application101622, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null.
LOG: Start validating all the dependencies.
LOG: [Level 1]Start validating native image dependency mscorlib, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089.
LOG: Dependency evaluation succeeded.
LOG: [Level 1]Start validating IL dependency Dependency101622, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null.
LOG: Dependency evaluation succeeded.
LOG: Validation of dependencies succeeded.
LOG: Start loading all the dependencies into load context.
LOG: Loading of dependencies succeeded.
LOG: Bind to native image succeeded.
Native image has correct version information.
Attempting to use native image E:\Windows\assembly\NativeImages_v2.0.50727_64\Application101622\1ac7fadabec4f72575d807501e9fdc72\Application101622.ni.exe.
Rejecting native image because it failed the security check. The assembly's permissions must have changed since the time it was ngenned, or it is running with a different security context.
Discarding native image.
```

## <a name="the-log-settings-dialog"></a>로그 설정 대화 상자

**로그 설정** 대화 상자를 사용하여 다음 작업을 수행할 수 있습니다.

#### <a name="to-disable-logging"></a>로깅을 사용하지 않으려면

- **로그 사용 안 함** 옵션 단추를 선택합니다.  이 옵션은 기본적으로 선택되어 있습니다.

#### <a name="to-log-assembly-binds-in-exceptions"></a>예외에 어셈블리 바인딩을 기록하려면

- **예외 텍스트로 기록** 옵션 단추를 선택합니다. 덜 자세한 fusion 로그 정보만 예외 텍스트로 기록됩니다. 전체 정보를 보려면 다른 설정 중 하나를 사용합니다.

  도메인 중립적으로 로드되는 어셈블리에 대한 중요 사항을 참조하세요.

#### <a name="to-log-assembly-bind-failures"></a>어셈블리 바인딩 실패를 기록하려면

- **디스크에 바인드 실패 기록** 옵션 단추를 선택합니다.

  도메인 중립적으로 로드되는 어셈블리에 대한 중요 사항을 참조하세요.

#### <a name="to-log-all-assembly-binds"></a>모든 어셈블리 바인딩을 기록하려면

- **디스크에 모든 바인드 기록** 옵션 단추를 선택합니다.

  도메인 중립적으로 로드되는 어셈블리에 대한 중요 사항을 참조하세요.

> [!IMPORTANT]
> 예를 들어 <xref:System.AppDomainSetup.LoaderOptimization%2A> 속성을 <xref:System.LoaderOptimization.MultiDomain?displayProperty=nameWithType> 또는 <xref:System.LoaderOptimization.MultiDomainHost?displayProperty=nameWithType>로 설정하여 어셈블리가 도메인 중립적으로 로드되는 경우 로깅을 설정하면 경우에 따라 메모리가 누수될 수 있습니다. 도메인 중립 모듈이 애플리케이션 도메인에 로드되었을 때 로그 엔트리가 만들어지고 나중에 애플리케이션 도메인이 언로드되면 이러한 누수가 발생할 수 있습니다. 프로세스가 끝날 때까지는 로그 엔트리가 해제되지 않을 수도 있습니다. 로깅이 자동으로 설정되는 디버거도 있습니다.

#### <a name="to-enable-a-custom-log-path"></a>사용자 지정 로그 경로를 사용하려면

1. **사용자 지정 로그 경로 사용** 옵션 단추를 선택합니다.

2. **사용자 지정 로그 경로** 텍스트 상자에 경로를 입력합니다.

> [!NOTE]
> [어셈블리 바인딩 로그 뷰어(Fuslogvw.exe)](fuslogvw-exe-assembly-binding-log-viewer.md)에서는 IE(Internet Explorer) 캐시를 사용하여 바인딩 로그를 저장합니다. 가끔 나타나는 IE 캐시 손상으로 인해 [어셈블리 바인딩 로그 뷰어(Fuslogvw.exe)](fuslogvw-exe-assembly-binding-log-viewer.md)에서는 보기 창에 새 바인딩 로그를 표시하지 않을 수도 있습니다. 이 손상으로 인해 .NET 바인딩 인프라(fusion)는 바인딩 로그에 쓰거나 바인딩 로그에서 읽을 수 없습니다. 사용자 지정 로그 경로를 사용하는 경우에는 이 문제가 발생하지 않습니다.  손상을 해결하고 fusion이 바인딩 로그를 다시 표시하도록 하려면 IE 옵션 대화 상자 내에서 임시 인터넷 파일을 삭제하여 IE 캐시를 지웁니다.
>
> 관리되지 않는 애플리케이션에서 `IHostAssemblyManager` 및 `IHostAssemblyStore` 인터페이스를 구현하여 공용 언어 런타임을 호스팅하는 경우 로그 엔트리를 wininet 캐시에 저장할 수 없습니다.  이러한 인터페이스를 구현하는 사용자 지정 호스트에 대한 로그 엔트리를 보려면 대체 로그 경로를 지정해야 합니다.

#### <a name="to-enable-logging-for-apps-running-in-the-windows-app-container"></a>Windows 앱 컨테이너에서 실행되는 앱에 대해 로깅을 사용하려면

1. 이전 절차에서 설명한 대로, 사용자 지정 로그 경로를 활성화시킵니다. 기본적으로, Windows 앱 컨테이너에서 실행되는 응용 프로그램은 하드 디스크에 대한 액세스가 제한됩니다. 지정한 디렉터리는 응용 프로그램 컨테이너에 있는 모든 응용 프로그램에 대한 읽기/쓰기 권한을 갖습니다.

2. **로깅 몰입 활성화** 확인란을 선택합니다.

    > [!NOTE]
    > Windows 8 이상에서만 상자가 활성화됩니다.

## <a name="see-also"></a>참고 항목

- <xref:System.TypeLoadException>
- [도구](index.md)
- [전역 어셈블리 캐시](../app-domains/gac.md)
- [런타임에서 어셈블리를 찾는 방법](../deployment/how-the-runtime-locates-assemblies.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
