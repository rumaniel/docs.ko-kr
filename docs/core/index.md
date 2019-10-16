---
title: .NET Core 가이드
description: .NET Core는 Windows, Linux 및 Mac 앱을 만들기 위한 모듈식 고성능 .NET 구현입니다. 시작하려면 .NET Core에 관해 알아봅니다.
author: richlander
ms.date: 09/23/2019
ms.custom: updateeachrelease
ms.openlocfilehash: 95f18ca09852ce139a4b99ed7aef4802d4883e13
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216212"
---
# <a name="net-core-guide"></a>.NET Core 가이드

[.NET Core](about.md)는 Microsoft 및 [GitHub](https://github.com/dotnet/core)의 .NET 커뮤니티에서 유지 관리하는 [오픈 소스](https://github.com/dotnet/coreclr/blob/master/LICENSE.TXT) 범용 개발 플랫폼입니다. 플랫폼 간으로 Windows, macOS 및 Linux를 지원하며 디바이스, 클라우드 및 IoT 애플리케이션을 빌드하는 데 사용할 수 있습니다.

특성, 지원되는 언어 및 프레임워크, 키 API를 비롯한 .NET Core에 대한 자세한 내용은 [.NET Core 정보](about.md)를 참조하세요.

.NET Core 애플리케이션을 만드는 방법은 [.NET Core 자습서](tutorials/index.md)를 참조하세요. 첫 번째 앱을 만들고 실행하는 데 몇 분밖에 걸리지 않습니다. 브라우저에서 .NET Core를 사용하려면 [C#의 숫자](../csharp/tutorials/intro-to-csharp/numbers-in-csharp.yml) 온라인 자습서를 확인하세요.

## <a name="download-net-core"></a>.NET Core 다운로드

[.NET Core SDK](https://www.microsoft.com/net/download)를 다운로드하여 Windows, macOS 또는 Linux 머신에서 .NET Core를 사용해 보세요. Docker 컨테이너를 사용하려면 [.NET Core Docker Hub](https://hub.docker.com/_/microsoft-dotnet-core/)를 방문하세요.

다른 .NET Core 버전을 찾는 경우 [.NET Core 다운로드](https://dotnet.microsoft.com/download/dotnet-core)에서 모든 .NET Core 버전을 사용할 수 있습니다.

## <a name="net-core-30"></a>.NET Core 3.0

최신 버전은 .NET Core 3.0입니다. 새로운 기능에는 WPF(Windows Presentation Foundation) 및 Windows Forms를 사용한 Windows Desktop 지원, Blazor를 사용한 전체 스택 C# 웹 개발, SignalR 및 Azure SignalR Service의 새로운 기능 향상, C# 8의 새로운 C# 언어 기능 등이 포함됩니다. .NET Core 3.0의 새로운 기능에 대한 전체 목록은 [.NET Core 3.0의 새로운 기능](./whats-new/dotnet-core-3-0.md)을 참조하세요.

## <a name="create-your-first-application"></a>첫 애플리케이션 만들기

.NET Core SDK를 설치한 후 명령 프롬프트를 엽니다. 다음 `dotnet` 명령을 입력하여 C# 애플리케이션을 만들고 실행합니다.

```dotnetcli
dotnet new console
dotnet run
```

다음과 같은 내용이 출력됩니다.

```output
Hello World!
```

## <a name="support"></a>고객 지원팀

.NET Core는 [Microsoft에 의해](https://dotnet.microsoft.com/platform/support/policy) Windows, macOS 및 Linux에서 지원됩니다. 보안 및 품질을 위해 1년에 여러 번, 일반적으로 매월 업데이트됩니다.

.NET Core 이진 배포는 Azure의 Microsoft가 유지 관리하는 서버에서 빌드 및 테스트되고 Microsoft 제품처럼 지원됩니다.

RHEL(Red Hat Enterprise Linux)에서 [Red Hat이 .NET Core를 지원](http://redhatloves.net/)합니다. Red Hat은 소스에서 .NET Core를 빌드하여 [Red Hat 소프트웨어 컬렉션](https://developers.redhat.com/products/softwarecollections/overview/)에서 사용할 수 있게 합니다. Red Hat 및 Microsoft는 협력하여 RHEL에서 .NET Core가 잘 작동하도록 합니다.
