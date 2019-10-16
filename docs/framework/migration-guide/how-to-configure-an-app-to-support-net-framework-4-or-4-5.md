---
title: '방법: .NET Framework 4 이상 버전을 지원하도록 앱 구성'
ms.date: 03/30/2017
helpviewer_keywords:
- configuring apps to support .NET Framework
- .NET Framework, configuring apps
ms.assetid: 63c6b9a8-0088-4077-9aa3-521ab7290f79
author: mairaw
ms.author: mairaw
ms.openlocfilehash: cd267de1e632fdc40dc50e8acdeba7d16bf8e61a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779488"
---
# <a name="how-to-configure-an-app-to-support-net-framework-4-or-later-versions"></a>방법: .NET Framework 4 이상 버전을 지원하도록 앱 구성

CLR(공용 언어 런타임)을 호스트하는 모든 응용 프로그램에서 관리 코드를 실행하기 위해서는 CLR을 시작하거나 *활성화*해야 합니다. 일반적으로 .NET Framework 애플리케이션은 빌드된 CLR 버전에서 실행되지만 애플리케이션 구성 파일(app.config 파일이라고도 함)을 사용하여 데스크톱 애플리케이션에 대해 이 동작을 변경할 수 있습니다. 그러나 애플리케이션 구성 파일을 사용하여 Windows 스토어 앱 또는 Windows Phone 앱에 대한 기본 활성화 동작을 변경할 수는 없습니다. 이 문서에서는 다른 버전의 .NET Framework에서 데스크톱 애플리케이션을 실행하도록 설정하는 방법을 설명하고 버전 4 이상을 대상으로 하는 방법에 대한 예제를 제공합니다.

 응용 프로그램을 실행하는 .NET Framework의 버전은 다음 순서로 결정됩니다.

- 구성 파일

     애플리케이션 구성 파일에 사용자 컴퓨터에 있는 하나 이상의 .NET Framework 버전 및 이러한 버전 중 하나를 지정하는 [\<supportedRuntime&gt;](../configure-apps/file-schema/startup/supportedruntime-element.md) 항목이 포함되어 있는 경우, 애플리케이션은 해당 버전에서 실행됩니다. 구성 파일은 나열된 순서대로 [\<supportedRuntime>](../configure-apps/file-schema/startup/supportedruntime-element.md) 항목을 읽고 사용자의 컴퓨터에 있는 목록의 첫 번째 .NET Framework 버전을 사용합니다. (버전 1.0용 [\<requiredRuntime> 요소](../configure-apps/file-schema/startup/requiredruntime-element.md) 사용)

- 컴파일 버전

     구성 파일은 없지만 응용 프로그램을 빌드한 .NET Framework 버전이 사용자의 컴퓨터에 있으면 응용 프로그램은 해당 버전에서 실행됩니다.

- 설치된 최신 버전

     응용 프로그램을 빌드한 .NET Framework 버전이 사용자 컴퓨터에 없고 구성 파일이 [\<supportedRuntime> element](../configure-apps/file-schema/startup/supportedruntime-element.md)의 버전을 지정하지 않으면 응용 프로그램은 사용자 컴퓨터에 있는 .NET Framework의 최신 버전에서 실행을 시도합니다.

     그러나 .NET Framework 1.0, 1.1, 2.0, 3.0 및 3.5 응용 프로그램은 .NET Framework 4 이상에서 자동으로 실행되지 않으며 경우에 따라 오류가 발생할 수 있고 .NET Framework 3.5를 설치하라는 메시지가 나타날 수 있습니다. 또한 다른 버전의 Windows 시스템에는 다른 버전의 .NET Framework가 포함되어 있으므로, 활성화 동작은 사용자의 운영 체제에 따라서도 달라질 수 있습니다. 응용 프로그램이 .NET Framework 3.5 및 4 이상을 모두 지원하는 경우 .NET Framework 초기화 오류를 방지하도록 구성 파일에 여러 항목을 사용하여 이를 표시하는 것이 좋습니다. 자세한 내용은 [버전 및 종속성](versions-and-dependencies.md)을 참조하세요.

 또한 버전 4 이상의 개선된 성능을 이용하기 위해 .NET Framework 3.5가 설치된 컴퓨터에서도 .NET Framework 4 이상 버전에서 .NET Framework 3.5 애플리케이션이 실행되도록 구성할 수 있습니다.

> [!IMPORTANT]
> 지원하는 .NET Framework 버전이 출시될 때마다 항상 응용 프로그램을 테스트하는 것이 좋습니다. .NET Framework의 이후 버전을 지원하도록 애플리케이션을 업그레이드하는 방법에 대한 자세한 내용은 [버전 호환성](version-compatibility.md)을 참조하세요.

 Windows 7 및 Windows 8을 지원하도록 .NET Framework 1.0 및 1.1 응용 프로그램을 수정하는 방법에 대한 자세한 내용은 [.NET Framework 1.1에서 마이그레이션](migrating-from-the-net-framework-1-1.md)을 참조하세요.

## <a name="to-configure-your-app-to-run-on-the-net-framework-4-or-later-versions"></a>.NET Framework 4 이상 버전에서 실행되도록 애플리케이션을 구성하려면

1. .NET Framework 프로젝트에 대한 구성 파일을 추가하거나 찾습니다. 응용 프로그램에 대한 구성 파일은 동일한 디렉터리에 있고 응용 프로그램과 동일한 이름이지만 확장명이 .config입니다. 예를 들어, MyExecutable.exe라는 애플리케이션의 경우 애플리케이션 구성 파일의 이름은 MyExecutable.exe.config입니다.

     Visual Studio 메뉴 모음에 구성 파일을 추가하려면 **프로젝트**, **새 항목 추가**를 차례로 선택합니다. 왼쪽 창에서 **일반**을 선택한 다음 **구성 파일**을 선택합니다. 구성 파일 이름을 *appName*.exe.config로 지정합니다. 해당 플랫폼에서 활성화 정책이 변경될 수 없으므로 이러한 메뉴 선택은 Windows 스토어 앱 또는 Windows Phone 앱 프로젝트에서 사용할 수 없습니다.

2. 다음과 같은 [\<supportedRuntime&gt;](../configure-apps/file-schema/startup/supportedruntime-element.md) 요소를 애플리케이션 구성 파일에 추가합니다.

    ```xml
    <configuration>
      <startup>
        <supportedRuntime version="<version>"/>
      </startup>
    </configuration>
    ```

     여기서 *\<version>* 은 앱이 지원하는 .NET Framework 버전에 맞는 CLR 버전을 지정합니다. 다음과 같은 문자열을 사용합니다.

    - .NET Framework 1.0: "v1.0.3705"

    - .NET Framework 1.1: "v1.1.4322"

    - .NET Framework 2.0, 3.0 및 3.5: "v2.0.50727"

    - .NET Framework 4 이상 버전: "v4.0"

     기본 설정 순서대로 나열된 여러 [\<supportedRuntime>](../configure-apps/file-schema/startup/supportedruntime-element.md) 요소를 추가하여 .NET Framework의 여러 버전에 대한 지원을 지정할 수 있습니다.

 다음 표에서는 컴퓨터에 설치된 애플리케이션 구성 파일 설정과 .NET Framework 버전으로 .NET Framework 3.5 애플리케이션이 실행 중인 버전을 결정하는 방법을 보여 줍니다. 이 예제는 .NET Framework 3.5 애플리케이션에 국한되지만 이전 .NET Framework 버전으로 빌드된 대상 애플리케이션에 이와 유사한 논리를 사용할 수 있습니다. .NET Framework 2.0 버전 번호(v2.0.50727)는 애플리케이션 구성 파일에서 .NET Framework 3.5를 지정하는 데 사용됩니다.

|App.config 파일 설정|버전 3.5가 설치된 컴퓨터|버전 3.5 및 4 이상이 설치된 컴퓨터|버전 4 이상이 설치된 컴퓨터|
|-|-|-|-|
|없음|3\.5에서 실행|3\.5에서 실행|사용자가 올바른 버전*을 설치하도록 요청하는 오류 메시지 표시|
|`<supportedRuntime version="v2.0.50727"/>`|3\.5에서 실행|3\.5에서 실행|사용자가 올바른 버전*을 설치하도록 요청하는 오류 메시지 표시|
|`<supportedRuntime version="v2.0.50727"/>` <br /> `<supportedRuntime version="v4.0"/>`|3\.5에서 실행|3\.5에서 실행|버전 4 이상에서 실행|
|`<supportedRuntime version="v4.0"/>` <br /> `<supportedRuntime version="v2.0.50727"/>`|3\.5에서 실행|버전 4 이상에서 실행|버전 4 이상에서 실행|
|`<supportedRuntime version="v4.0"/>`|사용자가 올바른 버전*을 설치하도록 요청하는 오류 메시지 표시|버전 4 이상에서 실행|버전 4 이상에서 실행|

 \* 이 오류 메시지와 이 오류를 방지하는 방법에 대한 자세한 내용은 [.NET Framework 초기화 오류: 사용자 환경 관리](../deployment/initialization-errors-managing-the-user-experience.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

- [.NET Framework 1.1에서 마이그레이션](migrating-from-the-net-framework-1-1.md)
- [마이그레이션 가이드](index.md)
