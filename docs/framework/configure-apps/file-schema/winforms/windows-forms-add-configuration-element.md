---
title: 구성 요소 Windows Forms 추가
ms.date: 04/07/2017
helpviewer_keywords:
- Windows Forms Add configuration element
- configuring Windows Forms applications
ms.assetid: 3e3e04de-99d1-4658-b716-44cb669d9589
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cb607af0933ea64b7d67f8ed082ffce6e7d21f51
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69913058"
---
# <a name="windows-forms-add-configuration-element"></a>구성 요소 Windows Forms 추가

요소 `<add>` 는 Windows Form 앱이 .NET Framework 4.7 이상에서 Windows Forms 앱에 추가 된 기능을 지원 하는지 여부를 지정 하는 미리 정의 된 키를 추가 합니다.

## <a name="syntax"></a>구문

```xml
<System.Windows.Forms.ApplicationConfigurationSection>
  <add key="key-name" value="key-value" />
</System.Windows.Forms.ApplicationConfigurationSection>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

| 특성 | 설명 |
| --------- | ----------- |
| `key`     | 필수 특성입니다. 특정 Windows Forms 사용자 지정 가능 기능에 해당 하는 미리 정의 된 키 이름입니다. |
| `value`   | 필수 특성입니다. `key`에 할당할 값입니다. |

### <a name="key-attribute-names-and-associated-values"></a>`key`특성 이름 및 관련 값

| `key` 이름 | 값 | 설명 |
| ---------- | ------ | ----------- |
| "AnchorLayout.DisableSinglePassControlScaling" | "true"&#124;"false" | 앵커 된 컨트롤이 단일 패스에서 확장 되는지 여부를 나타냅니다. 단일 패스 크기 조정을 사용 하지 않도록 설정 하려면 "true"로 설정 합니다. 그렇지 않으면 false입니다. 자세한 내용은 [설명](#remarks) 의 "단일 패스 크기 조정" 섹션을 참조 하세요. |
| "DpiAwareness" | "PerMonitorV2"&#124;"false" | 응용 프로그램이 DPI를 인식 하는지 여부를 나타냅니다. Dpi 인식을 지원 하려면 키를 "PerMonitorV2"로 설정 합니다. 그렇지 않으면 "false"로 설정 합니다. DPI 인식은 옵트인 (opt in) 기능입니다. Windows Forms의 높은 DPI 지원 기능을 활용 하려면 해당 값을 "PerMonitorV2"로 설정 해야 합니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요. |
| "CheckedListBox.DisableHighDpiImprovements" | "true"&#124;"false" | 컨트롤에서 <xref:System.Windows.Forms.CheckedListBox> .NET Framework 4.7에 도입 된 크기 조정 및 레이아웃 향상 기능을 사용 하는지 여부를 나타냅니다. 크기 조정 및 레이아웃 개선을 옵트아웃 (opt in) 하려면 "true"로 설정 합니다. 그렇지 않으면 "false"입니다. |
| "DataGridView.DisableHighDpiImprovements" | "true"&#124;"false" | .NET Framework 4.7에 <xref:System.Windows.Forms.DataGridView> 컨트롤 크기 조정 및 레이아웃 향상 기능이 도입 되었는지 여부를 나타냅니다. DPI 인식에서 옵트아웃 (opt out) 하려면 "true"로 설정 합니다. 그렇지 않으면 "false"입니다. |
| "DisableDpiChangedMessageHandling" | "true"&#124;"false" | DPI 크기 조정 변경과 관련 된 메시지 수신을 옵트아웃 하려면 "true"로 설정 합니다. 그렇지 않으면 "false"입니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요. |
| "EnableWindowsFormsHighDpiAutoResizing" | "true"&#124;"false" | DPI 크기 조정 변경으로 인해 Windows Forms 응용 프로그램의 크기가 자동으로 조정 되는지 여부를 나타냅니다. 자동 크기 조정을 사용 하도록 설정 하려면 "true"로 설정 합니다. 그렇지 않으면 false입니다. |
| "Form.DisableSinglePassControlScaling" | "true"&#124;"false" | <xref:System.Windows.Forms.Form> 가 단일 패스로 확장 되는지 여부를 나타냅니다. 단일 패스 크기 조정을 사용 하지 않도록 설정 하려면 "true"로 설정 합니다. 그렇지 않으면 false입니다. 자세한 내용은 [설명](#remarks) 의 "단일 패스 크기 조정" 섹션을 참조 하세요. |
| "MonthCalendar.DisableSinglePassControlScaling" | "true"&#124;"false" | 단일 패스에서 <xref:System.Windows.Forms.MonthCalendar> 컨트롤의 크기를 조정할지 여부를 나타냅니다. 단일 패스 크기 조정을 사용 하지 않도록 설정 하려면 "true"로 설정 합니다. 그렇지 않으면 false입니다. 자세한 내용은 [설명](#remarks) 의 "단일 패스 크기 조정" 섹션을 참조 하세요. |
| "Toolstrip.DisableHighDpiImprovements" | "true"&#124;"false" | 컨트롤에서 <xref:System.Windows.Forms.ToolStrip> .NET Framework 4.7에 도입 된 크기 조정 및 레이아웃 향상 기능을 사용 하는지 여부를 나타냅니다. DPI 인식에서 옵트아웃 (opt out) 하려면 "true"로 설정 합니다. 그렇지 않으면 "false"입니다. |

### <a name="child-elements"></a>자식 요소

없음

### <a name="parent-elements"></a>부모 요소

| 요소 | 설명 |
| ------- | ----------- |
| [`<System.Windows.Forms.ApplicationConfigurationSection>`](index.md) | 새 Windows Forms 응용 프로그램 기능에 대 한 지원을 구성 합니다. |

## <a name="remarks"></a>설명

.NET Framework 4.7부터는 `<System.Windows.Forms.ApplicationConfigurationSection>` 요소를 사용하여 Windows Forms 애플리케이션을 구성해 최신 .NET Framework 릴리스에 추가된 기능을 활용할 수 있습니다.

요소를 사용 하면 각각 특정 구성 설정을 정의 하 `<add>` 는 하나 이상의 자식 요소를 추가할 수 있습니다. `<System.Windows.Forms.ApplicationConfigurationSection>`

Windows Forms 높은 DPI 지원에 대 한 개요는 [Windows Forms에서 높은 Dpi 지원](../../../winforms/high-dpi-support-in-windows-forms.md)을 참조 하세요.

### <a name="dpiawareness"></a>DpiAwareness

Windows 10 크리에이터 Edition 이상에서 실행 되는 Windows 버전에서 실행 되는 앱과 .NET Framework 4.7부터 시작 하는 .NET Framework의 대상 버전에서 실행 되는 Windows Forms 앱은에 도입 된 높은 DPI 향상 기능을 활용 하도록 구성 될 수 있습니다 .NET Framework 4.7. 여기에는 다음이 포함됩니다.

- 사용자가 Windows Forms 응용 프로그램이 시작 된 후 DPI 또는 배율 인수를 변경 하는 동적 DPI 시나리오에 대 한 지원.

- <xref:System.Windows.Forms.MonthCalendar> 컨트롤<xref:System.Windows.Forms.CheckedListBox> 및 컨트롤과 같은 여러 Windows Forms 컨트롤의 크기 조정 및 레이아웃이 개선 되었습니다.

높은 DPI 인식은 옵트인 (opt in) 기능입니다. 기본적으로의 `DpiAwareness` 값은 `false`입니다. 응용 프로그램 구성 파일에서이 키의 값을로 `PerMonitorV2` 설정 하 여 Windows Forms ' DPI 인식 지원을 옵트인 (opt in) 할 수 있습니다. DPI 인식을 사용 하는 경우 모든 개별 DPI 기능도 사용할 수 있습니다. 여기에는 다음이 포함됩니다.

- `DisableDpiChangedMessageHandling` 키로 제어 되는 DPI 변경 메시지입니다.

- `EnableWindowsFormsHighDpiAutoResizing` 키로 제어 되는 동적 DPI 지원

- `Form.DisableSinglePassControlScaling` 개별 `MonthCalendar.DisableSinglePassControlScaling` `AnchorLayout.DisableSinglePassControlScaling` 컨트롤에 대해, 고정 된<xref:System.Windows.Forms.MonthCalendar> 컨트롤의 키 및 컨트롤의 키로 제어 되는 단일 패스 컨트롤 크기 조정 <xref:System.Windows.Forms.Form>

- 컨트롤의 키, `CheckListBox.DisableHighDpiImprovements` `DataGridView.DisableHighDpiImprovements` `Toolstrip.DisableHighDpiImprovements` <xref:System.Windows.Forms.CheckedListBox> 컨트롤에 대 한 키 및<xref:System.Windows.Forms.ToolStrip> 컨트롤의 키로 제어 되는 높은 DPI 크기 조정 및 레이아웃 개선 <xref:System.Windows.Forms.DataGridView>

`DpiAwareness` 로`PerMonitorV2` 설정 하 여 제공 하는 단일 기본 옵트인 설정은 일반적으로 새 Windows Forms 응용 프로그램에 적합 합니다. 그러나 해당 하는 키를 응용 프로그램 구성 파일에 추가 하 여 개별 높은 DPI의 향상 된 기능을 옵트아웃 (opt out) 할 수 있습니다. 예를 들어 동적 DPI 지원을 제외 하 고 모든 새 DPI 기능을 활용 하려면 응용 프로그램 구성 파일에 다음을 추가 합니다.

```xml
<System.Windows.Forms.ApplicationConfigurationSection>
   <add key="DpiAwareness" value="PerMonitorV2" />
   <!-- Disable dynamic DPI support -->
   <add key="EnableWindowsFormsHighDpiAutoResizing" value="false" />
</System.Windows.Forms.ApplicationConfigurationSection>
```

일반적으로 프로그래밍 방식으로 처리 하도록 선택 했기 때문에 특정 기능을 옵트아웃 (opt out) 할 수 있습니다.

Windows Forms 응용 프로그램에서 높은 DPI 지원을 활용 하는 방법에 대 한 자세한 내용은 [Windows Forms의 높은 Dpi 지원](../../../winforms/high-dpi-support-in-windows-forms.md)을 참조 하세요.

### <a name="disabledpichangedmessagehandling"></a>DisableDpiChangedMessageHandling

.NET Framework 4.7부터 Windows Forms 컨트롤은 DPI 크기 조정의 변경과 관련 된 많은 이벤트를 발생 시킵니다. 여기에는 <xref:System.Windows.Forms.Control.DpiChangedAfterParent>, <xref:System.Windows.Forms.Control.DpiChangedBeforeParent>및 <xref:System.Windows.Forms.Form.DpiChanged> 이벤트가 포함 됩니다. `DisableDpiChangedMessageHandling` 키의 값은 Windows Forms 응용 프로그램에서 이러한 이벤트가 발생 하는지 여부를 결정 합니다.

### <a name="single-pass-scaling"></a>단일 패스 크기 조정

단일 또는 다중 패스 배율은 사용자 인터페이스의 인식 되는 응답성과 크기가 조정 될 때 사용자 인터페이스 요소의 시각적 모양에 영향을 미칩니다. .NET Framework 4.7부터 Windows Forms는 단일 패스 크기 조정을 사용 합니다. 이전 버전의 .NET Framework에서는 여러 패스를 통해 크기 조정을 수행 했습니다 .이로 인해 일부 컨트롤의 크기가 필요 이상으로 조정 되었습니다. 앱이 이전 동작에 종속 되는 경우에만 단일 패스 크기 조정을 사용 하지 않도록 설정 해야 합니다.

## <a name="see-also"></a>참고자료

- [Windows Forms 구성 섹션](index.md)
- [Windows Forms의 높은 DPI 지원](../../../winforms/high-dpi-support-in-windows-forms.md)
