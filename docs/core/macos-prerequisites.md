---
title: Mac에서 .NET Core의 필수 구성 요소
description: macOS 컴퓨터에서.NET Core 응용 프로그램을 개발, 배포 및 실행하기 위해 지원되는 macOS 버전 및 .NET Core 종속성입니다.
author: guardrex
ms.author: mairaw
ms.date: 10/03/2018
ms.openlocfilehash: b5b3c6ea90a2cc4487e849af468d324b645834af
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48584080"
---
# <a name="prerequisites-for-net-core-on-macos"></a>macOS에서 .NET Core의 필수 구성 요소

이 문서에서는 macOS 컴퓨터에서.NET Core 응용 프로그램을 개발, 배포 및 실행하기 위해 필요한 지원되는 macOS 버전 및 .NET Core 종속성을 보여 줍니다. 다음에 나오는 지원되는 OS 버전 및 종속성은 Mac에서 .NET Core 앱을 개발하기 위한 세 가지 방법, 즉 [즐겨 사용하는 편집기를 통한 명령줄](tutorials/using-with-xplat-cli.md), [Visual Studio Code](https://code.visualstudio.com/) 및 [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/visual-studio-mac/)에 적용됩니다.

## <a name="supported-macos-versions"></a>지원되는 macOS 버전

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

.NET Core 2.x는 다음 macOS 버전에서 지원됩니다.

* macOS 10.12 "Sierra" 이상 버전

지원 OS 버전 중 .NET Core 2.x를 지원하는 운영 체제 및 수명 주기 정책 링크는 [.NET Core 2.x Supported OS Versions](https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md)(.NET Core 2.x가 지원되는 OS 버전)를 참조하세요.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

.NET Core 1.x는 다음 macOS 버전에서 지원됩니다.

* macOS 10.12 "Sierra"
* macOS 10.11 "El Capitan"

지원 OS 버전 중 .NET Core 1.x를 지원하는 운영 체제 및 수명 주기 정책 링크는 [.NET Core 1.x Supported OS Versions](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0-supported-os.md)(.NET Core 1.x가 지원되는 OS 버전)를 참조하세요.

---

## <a name="net-core-dependencies"></a>.NET Core 종속성

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

[.NET 다운로드](https://www.microsoft.com/net/download/core)에서 .NET Core SDK를 다운로드하여 설치합니다. macOS에 설치하는 데 문제가 있는 경우 설치된 버전에 해당하는 [알려진 문제](https://github.com/dotnet/core/tree/master/release-notes/2.1) 항목을 참조하세요.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

**.NET Core 1.x**

.NET Core 1.x를 macOS에서 실행할 때는 OpenSSL이 필요합니다. OpenSSL을 획득하는 쉬운 방법은 macOS용 [Homebrew("brew")](https://brew.sh/) 패키지 관리자를 사용하는 것입니다. *brew*를 설치한 후 터미널(명령) 프롬프트에서 다음 명령을 실행하여 OpenSSL을 설치합니다.

```console
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

[.NET 다운로드](https://www.microsoft.com/net/download/core)에서 .NET Core SDK를 다운로드하여 설치합니다. macOS에 설치하는 데 문제가 있는 경우 [1.0.0 알려진 문제](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0-known-issues.md) 및 [1.0.1 알려진 문제](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.1-known-issues.md) 항목을 참조하세요.

---

## <a name="increase-the-maximum-open-file-limit-net-core-versions-before-net-core-sdk-202"></a>열려 있는 최대 파일 제한 늘리기(.NET Core SDK 2.0.2 이전 .NET Core 버전) 

.NET Core 버전(.NET Core SDK 2.0.2 이전)에서 macOS에서 열려 있는 기본 파일 제한은 프로젝트를 복원하거나 단위 테스트를 실행하는 등 일부 .NET Core 작업에 충분하지 않을 수 있습니다.

다음 단계를 수행하여 이 제한을 늘릴 수 있습니다.

1. 텍스트 편집기를 사용하여 새 파일 _/Library/LaunchDaemons/limit.maxfiles.plist_를 만들고 이 콘텐츠로 파일을 저장합니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN"
        "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>limit.maxfiles</string>
    <key>ProgramArguments</key>
    <array>
      <string>launchctl</string>
      <string>limit</string>
      <string>maxfiles</string>
      <string>2048</string>
      <string>4096</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>ServiceIPC</key>
    <false/>
  </dict>
</plist>
```

2. 터미널 창에서 다음 명령을 실행합니다.

```console
echo 'ulimit -n 2048' | sudo tee -a /etc/profile
```

3. Mac을 다시 부팅하여 이 설정을 적용합니다.

## <a name="visual-studio-for-mac"></a>Visual Studio for Mac

.NET Core SDK를 사용하여 .NET Core 응용 프로그램을 개발하기 위해 원하는 편집기를 사용할 수 있습니다. 그러나 통합 개발 환경의 Mac에서 .NET Core 응용 프로그램을 개발하려는 경우 [Mac용 Visual Studio](https://visualstudio.microsoft.com/vs/visual-studio-mac/)를 사용할 수 있습니다. 

Visual Studio for Mac을 사용하여 macOS에서 .NET Core로 개발하려면 다음이 필요합니다.

* 지원되는 macOS 운영 체제 버전
* OpenSSL(.NET Core 1.x 전용, .NET Core 2.x는 macOS에서 기본적으로 제공되는 보안 서비스를 사용함)
* .NET Core SDK for Mac
* [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/visual-studio-mac/)
