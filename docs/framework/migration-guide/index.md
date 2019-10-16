---
title: '.NET Framework 4.8, 4.7, 4.6 및 4.5 마이그레이션 가이드 '
ms.custom: updateeachrelease
ms.date: 04/18/2019
helpviewer_keywords:
- .NET Framework, migrating applications to
- migration, .NET Framework
ms.assetid: 02d55147-9b3a-4557-a45f-fa936fadae3b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9b1cda82125a2d4a6eb3102b01bea639a4f3e3df
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65636081"
---
# <a name="migration-guide-to-the-net-framework-48-47-46-and-45"></a>.NET Framework 4.8, 4.7, 4.6 및 4.5 마이그레이션 가이드

이전 버전의 .NET Framework를 사용하여 앱을 만든 경우, 일반적으로 .NET Framework 4.5 및 해당 포인트 릴리스(4.5.1 및 4.5.2), .NET Framework 4.6 및 해당 포인트 릴리스(4.6.1 및 4.6.2), .NET Framework 4.7 및 해당 포인트 릴리스(4.7.1 및 4.7.2) 또는 .NET Framework 4.8로 쉽게 업그레이드할 수 있습니다. Visual Studio에서 프로젝트를 엽니다. 프로젝트가 이전 버전의 Visual Studio에서 만들어진 경우 **프로젝트 호환성** 대화 상자가 자동으로 열립니다. Visual Studio에서 프로젝트를 업그레이드하는 방법에 대한 자세한 내용은 [Visual Studio 프로젝트 포팅, 마이그레이션, 업그레이드](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects) 및 [Visual Studio 2019 플랫폼 대상 지정 및 호환성](/visualstudio/releases/2019/compatibility)을 참조하세요.

 그러나 .NET Framework에서 일부 사항을 변경하려면 코드를 변경해야 합니다. .NET Framework 4.5 및 해당 포인트 릴리스, .NET Framework 4.6 및 해당 포인트 릴리스, .NET Framework 4.7 및 해당 포인트 릴리스 또는 .NET Framework 4.8의 새로운 기능을 활용할 수도 있습니다. 새 버전의 .NET Framework용 으로 변경하는 이러한 유형의 작업을 일반적으로 *마이그레이션*이라고 합니다. 앱을 마이그레이션할 필요가 없는 경우 다시 컴파일하지 않고 .NET Framework 4.5 이상 버전에서 실행할 수 있습니다.

## <a name="migration-resources"></a>마이그레이션 리소스

이전 버전의 .NET Framework에서 버전 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2 또는 4.8로 앱을 마이그레이션하기 전에 다음 문서를 검토합니다.

- 각 버전의 .NET Framework 내부에 있는 CLR 버전을 파악하고 앱을 대상으로 지정하기 위한 지침을 검토하려면 [버전 및 종속성](versions-and-dependencies.md)을 참조하십시오.

- 앱에 영향을 줄 수 있는 런타임 및 대상 변경 관련 변경 내용과 이를 처리하는 방법을 알아보려면 [애플리케이션 호환성](application-compatibility.md)을 검토하십시오.

- 코드에서 더 이상 사용되지 않는 형식 또는 멤버와 권장되는 대체 항목을 확인하려면 [클래스 라이브러리의 사용되지 않는 기능](../whats-new/whats-obsolete.md)을 검토하십시오.

- 앱에 추가할 수 있는 새 기능에 대한 설명은 [새로운 기능](../whats-new/index.md)을 참조하십시오.

## <a name="see-also"></a>참고 항목

- [애플리케이션 호환성](application-compatibility.md)
- [.NET Framework 1.1에서 마이그레이션](migrating-from-the-net-framework-1-1.md)
- [버전 호환성](version-compatibility.md)
- [버전 및 종속성](versions-and-dependencies.md)
- [방법: .NET Framework 4 이상 버전을 지원하도록 앱 구성](how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)
- [새로운 기능](../whats-new/index.md)
- [클래스 라이브러리의 사용되지 않는 기능](../whats-new/whats-obsolete.md)
- [.NET Framework 버전 및 어셈블리 정보](https://go.microsoft.com/fwlink/?LinkId=201701)
- [Microsoft .NET Framework 지원 수명 주기 정책](https://go.microsoft.com/fwlink/?LinkId=196607)
- [.NET Framework 4 마이그레이션 문제](net-framework-4-migration-issues.md)
