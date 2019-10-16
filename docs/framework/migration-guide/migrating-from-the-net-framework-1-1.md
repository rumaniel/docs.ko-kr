---
title: .NET Framework 1.1에서 마이그레이션
ms.date: 03/30/2017
helpviewer_keywords:
- .NET Framework 4.5, migrating from 1.1
- .NET Framework 1.1, migrating to .NET Framework 4.5
ms.assetid: 7ead0cb3-3b19-414a-8417-a1c1fa198d9e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7b15318ef38c407110c8d48d3e81977aa1b20df4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779466"
---
# <a name="migrating-from-the-net-framework-11"></a>.NET Framework 1.1에서 마이그레이션

[!INCLUDE[win7](../../../includes/win7-md.md)] 및 이후 버전의 Windows 운영 체제는 .NET Framework 1.1을 지원하지 않습니다. 따라서 [!INCLUDE[win7](../../../includes/win7-md.md)] 이상 운영 체제 버전에서 수정하지 않으면 .NET Framework 1.1을 대상으로 하는 애플리케이션이 실행되지 않습니다. 이 항목에서는 [!INCLUDE[win7](../../../includes/win7-md.md)] 및 이후 버전의 Windows 운영 체제에서 .NET Framework 1.1을 대상으로 하는 애플리케이션을 실행하는 데 필요한 단계에 대해 설명합니다. .NET Framework 1.1 및 [!INCLUDE[win8](../../../includes/win8-md.md)]에 대한 자세한 내용은 [Windows 8 이상 버전에서 .NET Framework 1.1 앱 실행](../install/run-net-framework-1-1-apps.md)을 참조하세요.

## <a name="retargeting-or-recompiling"></a>대상 변경 또는 다시 컴파일

.NET Framework 1.1을 사용하여 컴파일된 애플리케이션을 가져와서 [!INCLUDE[win7](../../../includes/win7-md.md)] 이상의 Windows 운영 체제에서 실행하는 방법에는 두 가지가 있습니다.

- .NET Framework 4 이상 버전에서 실행되는 애플리케이션 대상을 변경할 수 있습니다. 대상을 변경하려면 애플리케이션을 .NET Framework 4 이상 버전에서 실행하도록 허용하는 애플리케이션의 구성 파일에 [\<supportedRuntime&gt;](../configure-apps/file-schema/startup/supportedruntime-element.md) 요소를 추가해야 합니다. 이러한 구성 파일은 다음과 같은 형식을 사용합니다.

    ```xml
    <configuration>
       <startup>
          <supportedRuntime version="v4.0"/>
       </startup>
    </configuration>
    ```

- .NET Framework 4 이상 버전을 대상으로 하는 컴파일러를 사용하여 애플리케이션을 다시 컴파일할 수 있습니다. 처음에 Visual Studio 2003을 사용하여 솔루션을 개발하고 컴파일한 경우 Visual Studio 2010(가능하면 이상 버전)에서 솔루션을 열 수 있으며 **프로젝트 호환성** 대화 상자를 사용하여 Visual Studio 2003에서 사용된 형식의 솔루션 및 프로젝트 파일을 MSBuild(Microsoft Build Engine) 형식으로 변환합니다.

애플리케이션을 다시 컴파일하는지 또는 대상을 변경하는지에 관계 없이 애플리케이션이 해당 .NET Framework보다 최신 버전에 도입된 변경 사항에 영향을 받는지 여부를 확인해야 합니다. 이러한 변경 사항에는 두 가지 종류가 있습니다.

- .NET Framework 1.1 및 해당 .NET Framework보다 최신 버전 사이에서 발생된 호환성이 손상되는 변경.

- .NET Framework 1.1 및 해당 .NET Framework보다 최신 버전 사이에서 사용되지 않거나 더 이상 사용할 수 없게 표시된 형식 또는 형식 멤버.

애플리케이션을 다시 컴파일하거나 애플리케이션 대상을 변경할 때 .NET Framework 1.1 이후에 릴리스된 .NET Framework의 각 버전에 대해 주요 변경 사항 및 사용되지 않는 형식 및 멤버를 모두 검토해야 합니다.

## <a name="breaking-changes"></a>주요 변경 사항

주요 변경 사항이 발생하면 구체적인 변경 사항에 따라 대상이 변경되거나 다시 컴파일된 애플리케이션 모두에 대해 해결 방법을 사용할 수 있습니다. 이 경우 자식 요소를 애플리케이션의 구성 파일에 있는 [\<runtime&gt;](../configure-apps/file-schema/startup/supportedruntime-element.md) 요소에 추가하여 이전 동작을 복원할 수 있습니다. 예를 들어 다음 구성 파일에서는 .NET Framework 1.1에서 사용된 문자열 정렬 및 비교 동작을 복원하여 대상이 변경되거나 다시 컴파일된 애플리케이션에서 사용할 수 있습니다.

```xml
<configuration>
   <runtime>
      <CompatSortNLSVersion enabled="4096"/>
   </runtime>
</configuration>
```

그러나 경우에 따라 소스 코드를 수정하고 애플리케이션을 다시 컴파일해야 할 수도 있습니다.

애플리케이션의 가능한 주요 변경 사항의 영향을 평가하려면 다음 변경 사항 목록을 검토해야 합니다.

- [.NET Framework 2.0의 주요 변경 내용](https://go.microsoft.com/fwlink/?LinkId=125263) 문서의 .NET Framework 1.1을 대상으로 하는 애플리케이션에 영향을 줄 수 있는 .NET Framework 2.0 SP1의 변경 내용.

- [.NET Framework 3.5 SP1의 변경 내용](https://go.microsoft.com/fwlink/?LinkID=186989)에서는 .NET Framework 3.5와 .NET Framework 3.5 SP1 사이의 변경 내용을 문서화합니다.

- [.NET Framework 4 마이그레이션 문제](net-framework-4-migration-issues.md)에서는 .NET Framework 3.5 SP1과 .NET Framework 4 사이의 변경 내용을 문서화합니다.

## <a name="obsolete-types-and-members"></a>사용되지 않는 형식 및 멤버

사용되지 않는 형식 및 멤버의 영향은 대상이 변경된 애플리케이션 및 다시 컴파일된 애플리케이션에서 다르게 나타납니다. 사용되지 않는 형식 및 멤버를 사용하더라도 해당 어셈블리에서 해당 형식 및 멤버를 물리적으로 제거하지 않는 경우 대상이 변경된 애플리케이션에 영향을 주지 않습니다. 사용되지 않는 형식 및 멤버를 사용하는 애플리케이션을 다시 컴파일하면 일반적으로 컴파일러 오류가 아닌 컴파일러 경고가 발생합니다. 하지만 경우에 따라 컴파일러 오류가 발생되어 사용되지 않는 형식 및 멤버를 사용하는 코드가 성공적으로 컴파일되지 않습니다. 이 경우 애플리케이션을 다시 컴파일하기 전에 사용되지 않는 형식 및 멤버를 호출하는 소스 코드를 다시 작성해야 합니다. 사용되지 않는 형식 및 멤버에 대한 자세한 내용은 [클래스 라이브러리의 사용되지 않는 기능](../whats-new/whats-obsolete.md)을 참조하세요.

.NET Framework 2.0 SP1 릴리스 이후 사용되지 않는 형식 및 멤버의 영향을 평가하려면 [클래스 라이브러리의 사용되지 않는 기능](../whats-new/whats-obsolete.md)을 참조하세요. 사용되지 않는 형식 및 멤버 목록은 .NET Framework 2.0 SP1, .NET Framework 3.5 및 .NET Framework 4에서 검토합니다.
