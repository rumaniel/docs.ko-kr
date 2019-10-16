---
title: '완화: WPF 창 렌더링'
ms.date: 03/30/2017
ms.assetid: 28ed6bf8-141b-4b73-a4e3-44a99fae5084
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 13091c06561da24d2fc03f810fd8b8687b21d9a4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70789797"
---
# <a name="mitigation-wpf-window-rendering"></a>완화: WPF 창 렌더링

Windows 8 이상에서 실행되는 .NET Framework 4.6에서, 다중 모니터 시나리오에서 전체 창이 단일 디스플레이를 벗어나 확장되는 경우 잘림 없이 렌더링됩니다.

## <a name="impact"></a>영향

일반적으로 다중 모니터에서 클리핑 없이 전체 창이 렌더링되는 것은 예상된 동작입니다. 그러나 Windows 7 및 이전 버전에서 WPF 창이 단일 디스플레이를 벗어나 확장되면 두 번째 모니터 창의 일부를 렌더링할 때 성능에 큰 영향을 주기 때문에 WPF 창이 클리핑됩니다.

Windows 8 이상에서 모니터 간의 WPF 창을 렌더링하는 작업에 미치는 영향은 수많은 요인에 따라 달라질 수 있으므로 정확하게 측정할 수 없습니다. 경우에 따라서, 특히 그래픽 위주 애플리케이션을 실행하고 여러 모니터에 걸친 창을 사용하는 경우 성능에 원하지 않는 영향이 계속 나타날 수 있습니다. 다른 경우에는 여러 .NET Framework 버전에서 일관된 동작이 발생하기를 원할 수 있습니다.

## <a name="mitigation"></a>완화

이 변경을 사용하지 않도록 설정하고 단일 디스플레이를 벗어나 확장될 때 WPF 창을 클리핑하는 이전 동작으로 되돌릴 수 있습니다. 여기에는 두 가지 방법이 있습니다.

- 애플리케이션 구성 파일의 `<appSettings>` 섹션에 `<EnableMultiMonitorDisplayClipping>` 요소를 추가하여 Windows 8 이상에서 실행되는 앱에서 이 동작을 사용하지 않거나 사용하도록 설정할 수 있습니다. 예를 들어 다음 구성 섹션은 클리핑 없이 렌더링을 사용하지 않도록 설정합니다.

  ```xml
  <appSettings>
      <add key="EnableMultiMonitorDisplayClipping" value="true"/>
    </appSettings>
  ```

  `<EnableMultiMonitorDisplayClipping>` 구성 설정에 다음 두 값 중 하나를 적용할 수 있습니다.

  - `true`, 렌더링하는 동안 창의 클리핑이 범위를 모니터링하도록 설정합니다.

  - `false`, 렌더링하는 동안 창의 클리핑이 범위를 모니터링하지 않도록 설정합니다.

- 앱을 시작할 때 <xref:System.Windows.CoreCompatibilityPreferences.EnableMultiMonitorDisplayClipping%2A> 속성을 `true`로 설정합니다.

## <a name="see-also"></a>참고 항목

- [런타임 변경 내용](runtime-changes-in-the-net-framework-4-6.md)
