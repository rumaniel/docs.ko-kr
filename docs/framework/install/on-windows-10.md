---
title: Windows 10에 .NET Framework 설치
description: Windows 10 또는 Windows Server 2016에서 .NET Framework를 설치하는 방법을 알아봅니다.
author: rlander
ms.author: mairaw
ms.date: 04/18/2019
ms.custom: updateeachrelease
ms.openlocfilehash: 0de48e14f11d3763ee239b28b40bdb809dbeb433
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70853947"
---
# <a name="install-the-net-framework-on-windows-10-and-windows-server-2016-and-later"></a>Windows 10 및 Windows Server 2016 이상에 .NET Framework 설치

Windows에서 많은 애플리케이션을 실행하는 데 .NET Framework가 필요합니다. 이 문서의 지침은 필요한 .NET Framework 버전을 설치하는 데 도움이 됩니다. [.NET Framework 4.8](https://github.com/Microsoft/dotnet/tree/master/releases/net48)은 사용 가능한 최신 버전입니다.

애플리케이션을 실행한 후 컴퓨터에 다음과 같은 대화 상자가 표시되어 이 페이지를 방문했을 수 있습니다.

![이 애플리케이션을 시작할 수 없습니다.](./media/this-application-could-not-be-started.png)

## <a name="net-framework-48"></a>.NET Framework 4.8

.NET Framework 4.8에는 다음이 포함되어 있습니다.

- [Windows 10 2019년 5월 업데이트](https://support.microsoft.com/help/4028685/windows-10-get-the-update)

> [!div class="button"]
> [.NET Framework 4.8 다운로드](https://dotnet.microsoft.com/download/dotnet-framework/net48)

[.NET Framework 4.8](https://dotnet.microsoft.com/download/dotnet-framework/net48)은 .NET Framework 4.0~4.7.2용으로 빌드된 애플리케이션을 실행하는 데 사용될 수 있습니다.

다음에 [.NET Framework 4.8](https://dotnet.microsoft.com/download/dotnet-framework/net48)을 설치할 수 있습니다.

- Windows 10 2018년 10월 업데이트(버전 1809)
- Windows 10 2018년 4월 업데이트(버전 1803)
- Windows 10 가을 작성자 업데이트(버전 1709)
- Windows 10 Creators Update(버전 1703)
- Windows 10 1주년 업데이트(버전 1607)
- Windows Server 2019
- Windows Server, 버전 1809
- Windows Server, 버전 1803
- Windows Server 2016

.NET Framework 4.8은 다음에서 지원되지 않습니다.

- Windows 10 1507
- Windows 10 1511

Windows 10 1507 또는 1511을 사용 중인 경우 .NET Framework 4.8을 설치하려면 먼저 이후 Windows 10 버전으로 업그레이드해야 합니다.

## <a name="net-framework-462"></a>.NET Framework 4.6.2

[.NET Framework 4.6.2](https://www.microsoft.com/download/details.aspx?id=53345)는 Windows 10 1507 및 1511에서 지원되는 최신 .NET Framework 버전입니다.

.NET Framework 4.6.2는 .NET Framework 4.0~4.6.2용으로 빌드된 앱을 지원합니다.

## <a name="net-framework-35"></a>.NET Framework 3.5

지침에 따라 [.NET Framework 3.5를 Windows 10에](dotnet-35-windows-10.md) 설치합니다.

.NET Framework 3.5는 .NET Framework 1.0~3.5용으로 빌드된 앱을 지원합니다.

## <a name="additional-information"></a>추가 정보

.NET Framework 4.x 버전은 이전 버전에 대한 내부 업데이트입니다. 이는 다음을 의미합니다.

- 컴퓨터에는 하나의 .NET Framework 4.x 버전만 설치할 수 있습니다.

- 이후 버전이 이미 설치되어 있으면 컴퓨터에 이전 버전의 .NET Framework를 설치할 수 없습니다.

- .NET Framework 4.x 버전은 .NET Framework 4.0~해당 버전용으로 빌드된 애플리케이션을 실행하는 데 사용할 수 있습니다. 예를 들어 .NET Framework 4.7은 .NET Framework 4.0~4.7용으로 빌드된 애플리케이션을 실행하는 데 사용할 수 있습니다. 최신 버전(.NET Framework 4.8)은 4.0으로 시작되는 모든 .NET Framework 버전으로 빌드된 애플리케이션을 실행하는 데 사용할 수 있습니다.

다운로드할 수 있는 모든 .NET Framework 버전 목록은 [.NET 다운로드](https://dotnet.microsoft.com/download) 페이지를 참조하세요.

## <a name="help"></a>도움말

설치된 .NET Framework의 정확한 버전을 확인할 수 없는 경우 [Microsoft에 지원을 문의](mailto:dotnet-install-help@service.microsoft.com?subject=Install-Help)할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [.NET 다운로드](https://dotnet.microsoft.com/download)
- [차단된 .NET Framework 설치 및 제거 문제 해결](troubleshoot-blocked-installations-and-uninstallations.md)
- [개발자용 .NET Framework 설치](guide-for-developers.md)
