---
title: .NET Framework 클래스 라이브러리의 사용되지 않는 기능
ms.custom: updateeachrelease
ms.date: 04/02/2019
helpviewer_keywords:
- obsolete [.NET Framework]
- what's obsolete [.NET Framework]
- deprecated [.NET Framework]
ms.assetid: d356a43a-73df-4ae2-a457-b9628074c7cd
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 810f49581d4cb28987ea41237645f75c50388084
ms.sourcegitcommit: d8ebe0ee198f5d38387a80ba50f395386779334f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66690481"
---
# <a name="whats-obsolete-in-the-net-framework-class-library"></a>.NET Framework 클래스 라이브러리의 사용되지 않는 기능

.NET Framework는 시간이 지남에 따라 변경됩니다. 새 버전이 나올 때마다 새로운 기능을 제공하는 새로운 형식 및 형식 멤버가 추가됩니다. 기존 형식과 해당 멤버도 시간이 지남에 따라 변경됩니다. 예를 들어 일부 형식은 지원하는 기술이 새로운 기술로 대체됨에 따라 덜 중요해지고 일부 메서드는 보다 편리하거나 보다 완전한 기능을 갖춘 최신 메서드로 대체됩니다.

.NET Framework 및 공용 언어 런타임은 이전 버전과의 호환성(특정 .NET Framework 버전으로 개발된 애플리케이션이 다음 버전의 .NET Framework에서 실행될 수 있도록 함)을 지원하기 위해 노력합니다. 이 때문에 형식 또는 형식 멤버를 단순히 제거하기 어렵습니다. 대신, .NET Framework는 사용되지 않음(obsolete) 또는 더 이상 사용되지 않음(deprecated)으로 표시하여 형식 또는 형식 멤버가 더 이상 사용되지 않음을 나타냅니다. 사용 중단의 일부로 형식 또는 멤버를 사용되지 않음으로 표시하면 개발자가 사용이 중단됨을 인식하고 제거에 대응할 시간을 가질 수 있습니다. 그러나 형식 또는 멤버를 사용하는 기존 코드는 새 버전의 .NET Framework에서 계속 실행됩니다.

> [!NOTE]
> *사용되지 않음(obsolete)* 및 *사용되지 않음(deprecated)* 용어는 .NET Framework의 형식 및 멤버에 적용될 경우 동일한 의미를 가집니다.

## <a name="the-obsoleteattribute-attribute"></a>ObsoleteAttribute 특성

.NET Framework는 <xref:System.ObsoleteAttribute> 특성으로 표시하여 형식 또는 형식 멤버가 사용되지 않음을 나타냅니다. 형식 또는 멤버에 이 특성을 적용하면 .NET Framework의 이후 버전에서 형식 또는 멤버가 해당 멤버를 사용하는 컴파일된 코드의 손상 없이 제거됨을 나타냅니다.

형식 또는 형식 멤버가 사용되지 않음을 나타낼 뿐 아니라 <xref:System.ObsoleteAttribute>는 컴파일러에서 해당 형식 또는 멤버를 포함하는 소스 코드를 처리하는 방법을 정의합니다. 컴파일러는 코드를 컴파일하지만 경고 메시지를 표시하거나, 형식 또는 멤버 사용을 오류로 처리할 수 있습니다. 첫 번째 경우에는 코드가 성공적으로 컴파일되지만 형식 또는 멤버가 사용되지 않는다는 경고 메시지가 표시됩니다. 두 번째 경우에는 컴파일이 실패합니다.

컴파일 시 경고 메시지 대신 오류가 생성되는 경우에도 <xref:System.ObsoleteAttribute>는 런타임 동작에 영향을 주지 않습니다. 즉, 형식 또는 멤버를 사용하며 성공적으로 컴파일된 애플리케이션은 항상 성공적으로 실행됩니다. 형식 또는 멤버를 사용하는 애플리케이션을 다시 컴파일하려는 시도만 실패합니다.

## <a name="how-to-handle-obsolete-types-and-members"></a>사용되지 않는 형식 및 멤버를 처리하는 방법

기존 코드를 업그레이드하고 다시 컴파일할 때 애플리케이션에서 컴파일러 경고를 생성하는 사용되지 않는 형식 또는 멤버를 사용하는 것은 완벽하게 허용됩니다. 그러나 컴파일러 경고 메시지를 검토하여 애플리케이션 코드를 변경해야 하는지 여부를 확인해야 합니다. 메시지에서 적절한 대안을 가리키지 않는 경우 다음 중 하나를 수행해야 합니다.

- 가능한 경우 형식 또는 멤버 사용을 제거하여 코드를 변경합니다.

     또는

- 이 기술 영역에 대한 설명서를 검토하여 사용 중단에 대응하는 방법을 확인합니다.

이후 버전의 .NET Framework에 대해 기존 코드를 다시 컴파일하지 않도록 선택할 수 있습니다. 대신, 기존의 컴파일된 코드가 실행되는 .NET Framework 버전을 지정할 수 있습니다. 예를 들어 .NET Framework 3.5에 대해 컴파일된 app1.exe라는 애플리케이션이 있지만 .NET Framework 4.5에 대해 애플리케이션을 실행하려 한다고 가정합니다. 이 경우 다음 단계를 수행해야 합니다.

1. 주 실행 파일에 대한 구성 파일을 만들고 이름을 *appName*.exe.config로 지정합니다. 여기서 *appName*은 애플리케이션 실행 파일의 이름입니다. 예제에서는 app1.exe라는 애플리케이션에 대해 app1.exe.config라는 구성 파일을 만듭니다.

2. 구성 파일에 다음 코드를 추가합니다.

    ```xml
    <configuration>
       <startup> 
          <supportedRuntime version="v4.0" />
       </startup>
    </configuration>
    ```

다음 표에서는 특정 버전의 .NET Framework를 대상으로 지정하기 위해 `version` 특성에 할당할 수 있는 문자열 값을 보여 줍니다.

|.NET Framework 버전|`version` 문자열|
|-|-|
|4.8|v4.0|
|4.7(4.7.1 및 4.7.2 포함)|v4.0|
|4.6(4.6.1 및 4.6.2 포함)|v4.0|
|4.5(4.5.1 및 4.5.2 포함)|v4.0|
|4|v4.0|
|3.5|v2.0.50727|
|2.0|v2.0.50727|
|1.1|v1.1.4322|
|1.0|v1.0.3705|

## <a name="obsolete-lists-for-the-net-framework-45-and-later-versions"></a>.NET Framework 4.5 이상 버전에서 사용되지 않는 항목 목록

- [사용되지 않는 형식](obsolete-types.md)
- [사용되지 않는 멤버](obsolete-members.md)

## <a name="obsolete-lists-for-previous-versions"></a>이전 버전에서 사용되지 않는 항목 목록

- [.NET Framework 4에서 사용되지 않는 형식](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ee461503(v=vs.100))

- [.NET Framework 4에서 사용되지 않는 멤버](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ee471421(v=vs.100))

- [.NET Framework 3.5에서 사용되지 않는 항목 목록](https://docs.microsoft.com/previous-versions/cc835481(v=msdn.10))

- [.NET Framework 2.0에서 사용되지 않는 항목 목록](https://docs.microsoft.com/previous-versions/aa497286(v=msdn.10))

## <a name="see-also"></a>참고 항목

- [\<supportedRuntime> 요소](../configure-apps/file-schema/startup/supportedruntime-element.md)
