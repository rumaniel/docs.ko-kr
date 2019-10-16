---
title: ‘이 애플리케이션을 시작할 수 없음’ 문제 해결
description: "'이 애플리케이션을 시작할 수 없음' 대화 상자가 표시되면 어떻게 해야 하는지 알아보세요."
author: rpetrusha
ms.author: ronpet
ms.date: 09/05/2019
ms.openlocfilehash: 2534979e8dea886c2d7298c57e12b66d7a962c69
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401283"
---
# <a name="troubleshooting-a-this-application-could-not-be-started-error-message"></a>‘이 애플리케이션을 시작할 수 없음’ 오류 메시지 문제 해결

.NET Framework용으로 개발된 애플리케이션에서는 일반적으로 특정 버전의 .NET Framework를 시스템에 설치해야 합니다. 경우에 따라 설치된 버전이나 필요한 .NET Framework 버전 없이 애플리케이션을 실행하려고 할 수 있습니다. 이 경우 다음과 같은 오류 대화 상자가 생성됩니다.

![이 애플리케이션을 시작할 수 없습니다.](media/application-not-started/app-could-not-be-started.png)

이것은 일반적으로 다음 조건 중 하나를 나타냅니다.

- 시스템의 .NET Framework 설치가 손상되었습니다.

- 애플리케이션에 필요한 .NET Framework 버전을 검색할 수 없습니다.

애플리케이션을 실행할 수 있도록 이 문제를 해결하려면 다음을 수행합니다.

1. [.NET Framework 복구 도구(NetFxRepairTool.exe)](https://www.microsoft.com/download/details.aspx?id=30135)를 다운로드합니다. 다운로드가 완료되면 도구가 자동으로 실행됩니다.

1. .NET Framework 복구 도구에서 다음 그림에 표시된 것과 같은 추가 작업을 권장하는 경우 **다음**을 선택합니다.

   ![권장 변경 내용](media/application-not-started/repair-tool-recommended-changes.png)

1. .NET Framework 복구 도구는 다음 그림에 표시된 대화 상자를 표시하여 변경이 완료되었음을 나타냅니다. 애플리케이션을 다시 실행하는 동안 이 대화 상자를 열어 둡니다. .NET Framework 복구 도구에서 손상된 .NET Framework 설치를 확인하고 해결한 경우 이 작업은 성공입니다.

   ![권장 변경 내용](media/application-not-started/repair-tool-changes-complete.png)

1. 애플리케이션이 성공적으로 실행되는 경우 **마침** 단추를 선택합니다. 그렇지 않으면 **다음** 단추를 선택합니다.

1. **다음** 단추를 선택한 경우 .NET Framework 복구 도구는 다음과 같은 대화 상자를 표시합니다. **마침** 단추를 선택하여 진단 정보를 Microsoft에 보냅니다.

   ![이 문제를 해결할 수 없음](media/application-not-started/repair-tool-no-resolution.png)

1. 애플리케이션을 여전히 실행할 수 없는 경우 다음 표에 표시된 것처럼 사용 중인 Windows에서 지원하는 최신 버전의 .NET Framework를 설치합니다.

   |Windows 버전|.NET Framework 설치|
   |---|---|
   |Windows 10 1주년 업데이트 이상 버전|[.NET Framework 4.8 런타임](https://dotnet.microsoft.com/download/dotnet-framework/net48)|
   |Windows 10, Windows 10 11월 업데이트|[.NET Framework 4.6.2](https://www.microsoft.com/download/details.aspx?id=53345)|
   |Windows 8.1|[.NET Framework 4.8 런타임](https://dotnet.microsoft.com/download/dotnet-framework/net48)|
   |Windows 8|[.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981)|
   |Windows 7 SP1|[.NET Framework 4.8 런타임](https://dotnet.microsoft.com/download/dotnet-framework/net48)|
   |Windows Vista SP2|[.NET Framework 4.6](https://www.microsoft.com/download/details.aspx?id=48130)|

   > [!NOTE]
   >  Windows 10 2019년 5월 업데이트에는 .NET Framework 4.8이 미리 설치되어 있습니다.

1. 애플리케이션을 시작하려고 합니다.

1. 경우에 따라 .NET Framework 3.5를 설치하도록 요구하는 다음과 같은 대화 상자가 나타날 수 있습니다. **이 기능 다운로드 및 설치**를 선택하여 .NET Framework 3.5를 설치한 다음, 애플리케이션을 다시 시작합니다.

   ![이 문제를 해결할 수 없음](media/application-not-started/install-3-5.png)

## <a name="see-also"></a>참고 항목

- [.NET Framework 시스템 요구 사항](../get-started/system-requirements.md)
- [.NET Framework 설치 가이드](index.md)
- [차단된 .NET Framework 설치 및 제거 문제 해결](troubleshoot-blocked-installations-and-uninstallations.md)
