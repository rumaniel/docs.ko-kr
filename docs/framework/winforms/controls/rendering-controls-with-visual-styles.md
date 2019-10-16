---
title: 비주얼 스타일을 사용하여 컨트롤 렌더링
ms.date: 03/30/2017
helpviewer_keywords:
- professional appearance [Windows Forms], rendering Windows Forms controls
- themes [Windows Forms], XP visual styles in Window Forms
- custom controls [Windows Forms], rendering
- custom controls [Windows Forms], painting
- visual themes [Windows Forms], rendering Windows Forms controls
- user controls [Windows Forms], painting
- visual styles [Windows Forms], rendering Windows Forms controls
ms.assetid: a5b178ba-610e-46c4-a6c0-509c0886a744
ms.openlocfilehash: 32bcbab585c39be4a72150bf49820d4a16f1691f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968246"
---
# <a name="rendering-controls-with-visual-styles"></a>비주얼 스타일을 사용하여 컨트롤 렌더링
.NET Framework는 컨트롤을 지 원하는 운영 체제의 비주얼 스타일을 사용 하 여 컨트롤 및 기타 Windows UI (사용자 인터페이스) 요소를 렌더링 하는 기능을 제공 합니다. 이 항목에서는 운영 체제의 현재 비주얼 스타일을 사용 하 여 컨트롤 및 기타 UI 요소를 렌더링 하는 .NET Framework의 몇 가지 지원 수준에 대해 설명 합니다.  
  
## <a name="rendering-classes-for-common-controls"></a>공용 컨트롤의 클래스 렌더링  
 컨트롤 렌더링이란 컨트롤의 사용자 인터페이스를 그리는 것을 말합니다. <xref:System.Windows.Forms?displayProperty=nameWithType> 네임스페이스는 몇 가지 일반적인 Windows Forms 컨트롤 렌더링을 위한 <xref:System.Windows.Forms.ControlPaint> 클래스를 제공합니다. 그러나 이 클래스는 Windows 클래식 스타일로 컨트롤을 그립니다. 따라서 비주얼 스타일이 사용되는 애플리케이션에서 사용자 지정 컨트롤을 그릴 때 일관된 UI 환경을 유지하기가 어려울 수 있습니다.  
  
 .NET Framework 2.0에는 비주얼 스타일을 <xref:System.Windows.Forms?displayProperty=nameWithType> 사용 하 여 공용 컨트롤의 파트와 상태를 렌더링 하는 네임 스페이스의 클래스가 포함 되어 있습니다. 이러한 각 클래스에는 운영 체제의 현재 비주얼 스타일을 사용하여 특별한 상태의 컨트롤 또는 컨트롤의 일부를 그리기 위한 `static` 메서드가 포함되어 있습니다.  
  
 이러한 클래스 중 일부는 비주얼 스타일의 사용 가능 여부와 상관없이 관련 컨트롤을 그리도록 설계되어 있습니다. 비주얼 스타일을 사용할 수 있는 경우 클래스 멤버는 비주얼 스타일로 관련 컨트롤을 그립니다. 비주얼 스타일을 사용할 수 없는 경우 클래스 멤버는 Windows 클래식 스타일로 컨트롤을 그립니다. 이러한 클래스에는 다음이 포함됩니다.  
  
- <xref:System.Windows.Forms.ButtonRenderer>  
  
- <xref:System.Windows.Forms.CheckBoxRenderer>  
  
- <xref:System.Windows.Forms.GroupBoxRenderer>  
  
- <xref:System.Windows.Forms.RadioButtonRenderer>  
  
 다른 클래스는 비주얼 스타일을 사용할 수 있을 때에만 관련 컨트롤을 그릴 수 있으며, 비주얼 스타일을 사용할 수 없는 경우 해당 멤버는 예외를 throw합니다. 이러한 클래스에는 다음이 포함됩니다.  
  
- <xref:System.Windows.Forms.ComboBoxRenderer>  
  
- <xref:System.Windows.Forms.ProgressBarRenderer>  
  
- <xref:System.Windows.Forms.ScrollBarRenderer>  
  
- <xref:System.Windows.Forms.TabRenderer>  
  
- <xref:System.Windows.Forms.TextBoxRenderer>  
  
- <xref:System.Windows.Forms.TrackBarRenderer>  
  
 이러한 클래스를 사용 하 여 컨트롤 [을 그리는 방법에 대 한 자세한 내용은 방법: 컨트롤 렌더링 클래스](how-to-use-a-control-rendering-class.md)를 사용 합니다.  
  
## <a name="visual-style-element-and-rendering-classes"></a>비주얼 스타일 요소 및 렌더링 클래스  
 <xref:System.Windows.Forms.VisualStyles?displayProperty=nameWithType> 네임스페이스에는 그리기에 사용할 수 있고 비주얼 스타일에서 지원되는 컨트롤이나 UI 요소에 대한 정보를 가져올 수 있는 클래스가 포함되어 있습니다. 지원되는 컨트롤에는 <xref:System.Windows.Forms?displayProperty=nameWithType> 네임스페이스에 렌더링 클래스가 있는 공용 컨트롤(이전 섹션 참조) 및 탭 컨트롤과 rebar 컨트롤 같은 기타 컨트롤이 포함됩니다. 기타 지원되는 UI 요소에는 **시작** 메뉴의 일부, 작업 표시줄 및 창의 비클라이언트 영역이 있습니다.  
  
 <xref:System.Windows.Forms.VisualStyles?displayProperty=nameWithType> 네임스페이스의 주요 클래스는 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 및 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer>입니다. <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 는 비주얼 스타일에서 지원하는 컨트롤 또는 사용자 인터페이스 요소를 식별하기 위한 기본 클래스입니다. <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 자체 외에도 <xref:System.Windows.Forms.VisualStyles?displayProperty=nameWithType> 네임스페이스에는 컨트롤, 컨트롤 파트 또는 비주얼 스타일에서 지원하는 기타 UI 요소의 모든 상태에 대해 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement>를 반환하는 `static` 속성을 가지고 있는 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement>의 여러 중첩된 클래스가 포함되어 있습니다.  
  
 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 는 그리기를 수행하고 운영 체제의 현재 비주얼 스타일에 의해 정의된 각 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 에 대한 정보를 가져오는 메서드를 제공합니다. 요소에 대해 검색할 수 있는 정보에는 기본 크기, 배경 유형 및 색상 정의가 포함됩니다. <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 는 Windows Platform SDK의 Windows 셸 부분에서 비주얼 스타일(UxTheme) API의 기능을 래핑합니다. 자세한 내용은 [비주얼 스타일 사용](/windows/desktop/controls/cookbook-overview)을 참조 하세요.  
  
 및 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 사용에대한[자세한 내용은 방법: 비주얼 스타일 요소](how-to-render-a-visual-style-element.md)를 렌더링 합니다.  
  
## <a name="enabling-visual-styles"></a>비주얼 스타일 사용  
 .NET Framework 버전 1.0 용으로 작성 된 응용 프로그램에 대 한 비주얼 스타일을 사용 하도록 설정 하려면 프로그래머는 컨트롤을 그리기 위해 Comctl32.dll 버전 6 이상을 사용 하도록 지정 하는 응용 프로그램 매니페스트를 포함 해야 합니다. .NET Framework 버전 1.1 이상을 사용 하 여 빌드된 응용 프로그램은 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=nameWithType> <xref:System.Windows.Forms.Application> 클래스의 메서드를 사용할 수 있습니다.  
  
## <a name="checking-for-visual-styles-support"></a>비주얼 스타일 지원 확인  
 <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A> 클래스의 <xref:System.Windows.Forms.Application> 속성은 현재 응용 프로그램이 비주얼 스타일로 컨트롤을 그리는지 여부를 나타냅니다. 사용자 지정 컨트롤을 그릴 때 비주얼 스타일을 사용하거나 사용하지 않으면서 컨트롤을 렌더링할 지 여부를 판단하려면 <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A> 의 값을 확인할 수 있습니다. 다음 표에는 <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A> 를 반환하기 위해 `true`에 필요한 네 가지 조건이 나열되어 있습니다.  
  
|조건|노트|  
|---------------|-----------|  
|운영 체제에서 비주얼 스타일을 지원합니다.|이 조건을 별도로 확인하려면 <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation.IsSupportedByOS%2A> 클래스의 <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation> 속성을 사용하세요.|  
|사용자가 운영 체제에서 비주얼 스타일을 사용하도록 설정했습니다.|이 조건을 별도로 확인하려면 <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation.IsEnabledByUser%2A> 클래스의 <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation> 속성을 사용하세요.|  
|애플리케이션에서 비주얼 스타일이 사용 됩니다.|<xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=nameWithType> 메서드를 호출하여 또는 컨트롤 그리기에 ComCtl32.dll 버전 6 이상을 사용하도록 지정하는 응용 프로그램 매니페스트를 사용하여 응용 프로그램에서 비주얼 스타일을 사용하도록 설정할 수 있습니다.|  
|애플리케이션 창의 클라이언트 영역을 그리는 데 비주얼 스타일이 사용되고 있습니다.|이 조건을 별도로 확인하려면 <xref:System.Windows.Forms.Application> 클래스의 <xref:System.Windows.Forms.Application.VisualStyleState%2A> 속성을 사용하고 값이 <xref:System.Windows.Forms.VisualStyles.VisualStyleState.ClientAreaEnabled?displayProperty=nameWithType> 또는 <xref:System.Windows.Forms.VisualStyles.VisualStyleState.ClientAndNonClientAreasEnabled?displayProperty=nameWithType>인지 확인하세요.|  
  
 사용자가 비주얼 스타일을 사용하는지 여부 또는 한 비주얼 스타일에서 다른 비주얼 스타일로 전환하는지 여부를 확인하려면 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanging?displayProperty=nameWithType> 또는 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged?displayProperty=nameWithType> 이벤트에 대한 처리기에서 <xref:Microsoft.Win32.UserPreferenceCategory.VisualStyle?displayProperty=nameWithType> 값을 확인하세요.  
  
> [!IMPORTANT]
> 사용자가 비주얼 스타일을 사용할 때 또는 비주얼 스타일을 전환할 때 컨트롤 또는 UI 요소를 렌더링하기 위해 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 를 사용하려는 경우, <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged> 이벤트 대신 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanging> 이벤트를 처리할 때 이를 수행해야 합니다. <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 을 처리할 때 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanging>클래스를 사용하는 경우 예외가 throw됩니다.  
  
## <a name="see-also"></a>참고자료

- [사용자 지정 컨트롤 그리기 및 렌더링](custom-control-painting-and-rendering.md)
