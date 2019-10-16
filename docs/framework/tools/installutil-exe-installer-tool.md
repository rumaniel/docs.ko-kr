---
title: Installutil.exe(설치 관리자 도구)
ms.date: 03/30/2017
helpviewer_keywords:
- uninstalling server resources
- removing server resources
- status information for installation
- installation progress reports
- installing server resources
- Installer tool
- Installutil.exe
- files, Installer tool
- progress information for installation
- reporting installation progress
ms.assetid: 3f9d0533-f895-4897-b4ea-528284e0241d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5ad0497bd5303dc4113dbb7b8078c70cb044cc95
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044535"
---
# <a name="installutilexe-installer-tool"></a>Installutil.exe(설치 관리자 도구)

설치 관리자 도구는 특정 어셈블리에서 설치 관리자 구성 요소를 실행하는 방법으로 서버 리소스를 설치하고 제거하는 데 사용할 수 있는 명령줄 유틸리티입니다. 이 도구는 <xref:System.Configuration.Install> 네임스페이스의 클래스와 함께 사용됩니다.

이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.

명령 프롬프트에 다음을 입력합니다.

## <a name="syntax"></a>구문

```console
installutil [/u[ninstall]] [options] assembly [[options] assembly] ...
```

## <a name="parameters"></a>매개 변수

|인수|설명|
|--------------|-----------------|
|`assembly`|설치 관리자 구성 요소를 실행할 어셈블리의 파일 이름을 나타냅니다. `/AssemblyName` 옵션을 사용하여 어셈블리의 강력한 이름을 지정하려면 이 매개 변수를 생략합니다.|

<a name="options"></a>

## <a name="options"></a>옵션

|옵션|설명|
|------------|-----------------|
|`/h[elp]`<br /><br /> 또는<br /><br /> `/?`|이 도구의 명령 구문 및 옵션을 표시합니다.|
|`/help` *assembly*<br /><br /> 또는<br /><br /> `/?` *assembly*|InstallUtil.exe에 대한 명령 구문 및 옵션과 함께 지정된 어셈블리 내의 개별 설치 프로그램에서 재구성한 추가 옵션을 표시합니다. 이 옵션은 각 설치 관리자 구성 요소의 <xref:System.Configuration.Install.Installer.HelpText%2A?displayProperty=nameWithType> 속성에서 반환되는 텍스트를 InstallUtil.exe의 도움말 텍스트에 추가합니다.|
|`/AssemblyName` "*assemblyName*<br /><br /> ,Version=*major.minor.build.revision*<br /><br /> ,Culture=*locale*<br /><br /> ,PublicKeyToken=*publicKeyToken*"|전역 어셈블리 캐시에 등록해야 하는 어셈블리의 이름 또는 강력한 이름을 지정합니다. 어셈블리의 버전, 문화권 및 공개 키 토큰을 사용하여 어셈블리 이름을 정규화해야 합니다. 정규화된 어셈블리 이름은 따옴표로 묶어야 합니다.<br /><br /> 예를 들어, "myAssembly, Culture=neutral, PublicKeyToken=0038abc9deabfle5, Version=4.0.0.0"은 정규화된 어셈블리 이름입니다.|
|`/InstallStateDir=[` *directoryName* `]`|어셈블리를 제거하는 데 사용한 데이터가 포함된 .InstallState 파일의 디렉터리를 지정합니다. 기본 디렉터리는 어셈블리가 들어 있는 디렉터리입니다.|
|`/LogFile=`[*filename*]|설치 진행 정보가 기록되는 로그 파일의 이름을 지정합니다. 기본적으로 `/LogFile` 옵션을 생략하면 *assemblyname*.InstallLog라는 로그 파일이 생성됩니다. *filename*을 생략하면 로그 파일이 생성되지 않습니다.|
|`/LogToConsole`={`true`&#124;`false`}|`true`인 경우 출력을 콘솔에 표시합니다. `false`(기본값)이면 출력 내용을 콘솔에 표시하지 않습니다.|
|`/ShowCallStack`|설치 도중 어느 한 지점에서 예외가 발생하면 호출 스택을 로그 파일에 출력합니다.|
|`/u`[`ninstall`]|지정된 어셈블리를 제거합니다. 다른 옵션과 달리, `/u`는 명령줄에서 옵션이 표시되는 위치에 관계없이 모든 어셈블리에 적용됩니다.|

<a name="cmdline"></a>

## <a name="additional-installer-options"></a>추가 설치 관리자 옵션

어셈블리 내에서 사용되는 개별 설치 관리자는 [옵션](#options) 섹션에서 나열한 옵션 이외의 옵션도 인식할 수 있습니다. 이 옵션에 대해 자세히 알아보려면 InstallUtil.exe를 `/?` 또는 `/help` 옵션에 따라 명령줄에서 어셈블리 경로와 함께 실행합니다. 이러한 옵션을 지정하려면 InstallUtil.exe에서 인식하는 옵션과 함께 명령줄에 이 옵션을 포함합니다.

> [!NOTE]
> 개별 설치 관리자 구성 요소에서 지원하는 옵션에 대한 도움말 텍스트는 <xref:System.Configuration.Install.Installer.HelpText%2A?displayProperty=nameWithType> 속성에서 반환됩니다. 명령줄에 입력한 개별 옵션은 <xref:System.Configuration.Install.Installer.Context%2A?displayProperty=nameWithType> 속성에서 프로그래밍 방식으로 액세스할 수 있습니다.

모든 옵션 및 명령줄 매개 변수는 설치 로그 파일에 기록됩니다. 그러나 일부 설치 관리자 구성 요소에서 인식되는 `/Password` 매개 변수를 사용하는 경우 암호 정보는 8개의 별표(*)로 대체되며 로그 파일에는 나타나지 않습니다.

> [!IMPORTANT]
> 경우에 따라 설치 관리자에 전달되는 매개 변수는 중요하거나 개인적으로 식별할 수 있는 정보를 포함할 수 있으며 기본적으로 일반 텍스트 파일로 작성됩니다. 이 동작을 방지하려면 명령줄에서 Installutil.exe를 실행한 후 `/LogFile=`(*filename* 인수 없음)을 지정하여 로그 파일을 표시하지 않을 수 있습니다.

## <a name="remarks"></a>설명

.NET Framework 애플리케이션은 일반적인 프로그램 파일과 애플리케이션 배포 시 만들어야 하는 메시지 큐, 이벤트 로그 및 성능 카운터 등의 관련 리소스로 구성됩니다. 어셈블리의 설치 관리자 구성 요소를 사용하면 애플리케이션 설치 시에는 이러한 리소스를 만들고, 애플리케이션 제거 시에는 이러한 리소스를 제거할 수 있습니다. Installutil.exe를 사용하여 이러한 설치 관리자 구성 요소를 감지하고 실행할 수 있습니다.

동일한 명령줄에서 여러 개의 어셈블리를 지정할 수 있습니다. 어셈블리 이름 앞에 나타나는 모든 옵션은 해당 어셈블리의 설치에 적용됩니다. `/u` 및 `/AssemblyName`을 제외한 옵션은 누적되지만 재정의할 수 있습니다. 즉, 한 어셈블리에 대해 지정된 옵션은 이 옵션이 새 값으로 지정되지 않는 한 모든 후속 어셈블리에도 적용됩니다.

아무 옵션도 지정하지 않고 어셈블리에 대해 Installutil.exe를 실행하면 다음 세 개의 파일이 해당 어셈블리의 디렉터리에 놓입니다.

- InstallUtil.InstallLog - 설치 진행에 대한 일반적인 설명이 들어 있습니다.

- *assemblyname*.InstallLog - 설치 프로세스의 커밋 단계와 관련된 정보가 포함되어 있습니다. 커밋 단계에 대한 자세한 내용은 <xref:System.Configuration.Install.Installer.Commit%2A> 메서드를 참조하십시오.

- *assemblyname*.InstallState - 어셈블리를 제거하는 데 사용되는 데이터가 포함되어 있습니다.

Installutil.exe에서 리플렉션을 사용하여 지정된 어셈블리를 검사하고 <xref:System.Configuration.Install.Installer>에 대한 <xref:System.ComponentModel.RunInstallerAttribute?displayProperty=nameWithType> 특성 집합을 가지는 모든 `true` 형식을 찾습니다. 그런 다음 도구는 <xref:System.Configuration.Install.Installer.Install%2A?displayProperty=nameWithType> 형식의 각 인스턴스에서 <xref:System.Configuration.Install.Installer.Uninstall%2A?displayProperty=nameWithType> 또는 <xref:System.Configuration.Install.Installer> 메서드를 실행합니다. Installutil.exe를 사용하면 트랜잭션 방식으로 설치를 수행할 수도 있습니다. 즉, 어셈블리가 하나라도 설치되지 않으면 다른 모든 어셈블리의 설치도 롤백됩니다. 그러나 제거 시에는 트랜잭션 방식이 사용되지 않습니다.

Installutil.exe를 사용하면 서명이 연기된 어셈블리를 설치하거나 제거할 수 없지만 강력한 이름의 어셈블리는 설치하거나 제거할 수 있습니다.

.NET Framework 버전 2.0부터는 32비트 버전의 CLR(공용 언어 런타임)이 32비트 버전의 설치 관리자 도구에만 제공되며, 64비트 버전의 CLR은 32비트 및 64비트 버전의 설치 관리자 도구 모두에 제공됩니다. 64비트 CLR을 사용할 경우에는 32비트 설치 관리자 도구를 사용하여 32비트 어셈블리를 설치하고, 64비트 설치 관리자 도구를 사용하여 64비트 및 MSIL(Microsoft Intermediate Language) 어셈블리를 설치하십시오. 두 버전의 설치 관리자 도구가 동일하게 동작합니다.

Installutil.exe는 C++ 컴파일러에 의해 생성되는 포함된 네이티브 코드를 인식할 수 없으므로 C++를 사용하여 만든 Windows 서비스를 배포할 수 없습니다. Installutil.exe로 만든 C++ Windows 서비스를 배포하려고 시도하면 <xref:System.BadImageFormatException>과 같은 예외가 throw됩니다. 이 시나리오를 사용하여 작업하려면 C++ 모듈로 서비스 코드를 이동한 후 설치 관리자 개체를 C# 또는 Visual Basic에 씁니다.

## <a name="examples"></a>예

다음 명령은 InstallUtil.exe에 대한 옵션 및 명령 구문에 대한 설명을 표시합니다.

```console
installutil /?
```

다음 명령은 InstallUtil.exe에 대한 옵션 및 명령 구문에 대한 설명을 표시합니다. 도움말 텍스트가 설치 관리자의 <xref:System.Configuration.Install.Installer.HelpText%2A?displayProperty=nameWithType> 속성에 지정된 경우 `myAssembly.exe`의 설치 관리자 구성 요소에 의해 지원되는 옵션 목록 및 설명도 표시됩니다.

```console
installutil /? myAssembly.exe
```

다음 명령을 사용하여 어셈블리 `myAssembly.exe`에서 설치 관리자 구성 요소를 실행합니다.

```console
installutil myAssembly.exe
```

다음 명령은 `/AssemblyName` 스위치와 정규화된 이름을 사용하여 어셈블리에서 설치 관리자 구성 요소를 실행합니다.

```console
installutil /AssemblyName "myAssembly, Culture=neutral, PublicKeyToken=0038abc9deabfle5, Version=4.0.0.0"
```

다음 명령은 파일 이름으로 지정된 어셈블리와 강력한 이름으로 지정된 어셈블리에서 설치 관리자 구성 요소를 실행합니다. 파일 이름에서 지정한 모든 어셈블리는 `/AssemblyName` 옵션을 재정의할 수 없으므로 명령줄에서 강력한 이름으로 지정된 어셈블리보다 앞에 와야 합니다.

```console
installutil myAssembly.exe /AssemblyName "myAssembly, Culture=neutral, PublicKeyToken=0038abc9deabfle5, Version=4.0.0.0"
```

다음 명령을 사용하여 어셈블리 `myAssembly.exe`에서 설치 제거 관리자 구성 요소를 실행합니다.

```console
installutil /u myAssembly.exe
```

다음 명령은 어셈블리 `myAssembly1.exe` 및 `myAssembly2.exe`에서 제거 프로그램 구성 요소를 실행합니다.

```console
installutil myAssembly1.exe /u myAssembly2.exe
```

명령줄에서 `/u` 옵션의 위치는 중요하지 않기 때문에 다음 명령과 동일합니다.

```console
installutil /u myAssembly1.exe myAssembly2.exe
```

다음 명령을 사용하여 어셈블리 `myAssembly.exe`에서 설치 관리자를 실행하고 진행 정보가 `myLog.InstallLog`에 기록되도록 지정합니다.

```console
installutil /LogFile=myLog.InstallLog myAssembly.exe
```

다음 명령은 `myAssembly.exe` 어셈블리에서 설치 관리자를 실행하며 진행 정보를 `myLog.InstallLog`에 작성하도록 지정하며 설치 관리자의 사용자 지정 `/reg` 옵션을 통해 시스템 레지스트리로 업데이트하도록 지정합니다.

```console
installutil /LogFile=myLog.InstallLog /reg=true myAssembly.exe
```

다음 명령은 `myAssembly.exe` 어셈블리에서 설치 관리자를 실행하고 설치 관리자의 사용자 지정 `/email` 옵션을 사용하여 사용자의 전자 메일 주소를 지정하고 로그 파일에 대한 출력을 표시하지 않습니다.

```console
installutil /LogFile= /email=admin@mycompany.com myAssembly.exe
```

다음 명령은 `myAssembly.exe`에 대한 설치 진행률을 `myLog.InstallLog`에 쓰고, `myTestAssembly.exe`에 대한 설치 진행률을 `myTestLog.InstallLog`에 씁니다.

```console
installutil /LogFile=myLog.InstallLog myAssembly.exe /LogFile=myTestLog.InstallLog myTestAssembly.exe
```

## <a name="see-also"></a>참고 항목

- <xref:System.Configuration.Install>
- [도구](index.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
