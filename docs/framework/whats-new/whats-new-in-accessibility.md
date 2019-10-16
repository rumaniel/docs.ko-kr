---
title: .NET Framework에서 내게 필요한 옵션의 새로운 기능
ms.custom: updateeachrelease
ms.date: 04/18/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- what's new [.NET Framework]
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 22e1ae495276b0c474ad47f695d8410288289f83
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053730"
---
# <a name="whats-new-in-accessibility-in-the-net-framework"></a>.NET Framework에서 내게 필요한 옵션의 새로운 기능

.NET Framework는 애플리케이션을 사용자에게 더욱 액세스 가능하도록 만드는 것을 목표로 합니다. 내게 필요한 옵션 기능을 통해 애플리케이션은 사용자에게 보조 기술에 대한 적절한 환경을 제공할 수 있습니다. .NET Framework 4.7.1부터 .NET Framework에 개발자가 액세스 가능한 애플리케이션을 만들도록 허용하는 다수의 내게 필요한 옵션 개선 사항이 포함되어 있습니다.

## <a name="accessibility-switches"></a>내게 필요한 옵션 스위치

.NET Framework 4.7 이전 버전을 대상으로 하지만 .NET Framework 4.7.1 이상에서 실행되는 경우 내게 필요한 옵션 기능으로 옵트인하도록 앱을 구성할 수 있습니다. .NET Framework 4.7.1 이상을 대상으로 하는 경우 레거시 기능(및 내게 필요한 옵션 기능을 활용하지 못하도록)을 사용하도록 앱을 구성할 수도 있습니다. 내게 필요한 옵션 기능을 포함하는 .NET Framework의 각 버전에는 애플리케이션의 구성 파일의 [`<runtime>`](../configure-apps/file-schema/runtime/index.md) 섹션에서 [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 요소에 추가하는 버전별 내게 필요한 옵션 스위치가 있습니다. 다음은 지원되는 스위치입니다.

|버전|스위치|
|---|---|
|.NET Framework 4.7.1|"Switch.UseLegacyAccessibilityFeatures"|
|.NET Framework 4.7.2|"Switch.UseLegacyAccessibilityFeatures.2"|
|.NET Framework 4.8|"Switch.UseLegacyAccessibilityFeatures.3"|

### <a name="taking-advantage-of-accessibility-enhancements"></a>내게 필요한 옵션 개선 사항 활용

새로운 내게 필요한 옵션 기능은 .NET Framework 4.7.1 이상을 대상으로 하는 애플리케이션에 대해 기본적으로 활성화되어 있습니다. 또한 이전 버전의 .NET Framework를 대상으로 하지만 .NET Framework 4.7.1 이상에서 실행되는 애플리케이션은 애플리케이션의 구성 파일의 [`<runtime>`](../configure-apps/file-schema/runtime/index.md) 섹션에서 [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 요소에 스위치를 추가하고 해당 값을 `false`로 설정하여 레거시 내게 필요한 옵션 동작을 옵트아웃할 수 있습니다(따라서 내게 필요한 옵션 개선 사항 활용). 다음은 .NET Framework 4.7.1에 도입된 내게 필요한 옵션 개선 사항으로 옵트인하는 방법을 보여줍니다.

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false" />
</runtime>
```

.NET Framework의 이후 버전에서 내게 필요한 옵션 기능으로 옵트인하도록 선택한 경우 .NET Framework의 이전 버전에서도 기능으로 명시적으로 옵트인해야 합니다. .NET Framework 4.7.1 및 4.7.2 모두에서 내게 필요한 옵션 개선 사항을 활용하도록 앱을 구성하려면 다음 [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 요소가 필요합니다.

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false" />
</runtime>
```

.NET Framework 4.7.1 및 4.7.2 및 4.8에서 내게 필요한 옵션 개선 사항을 활용하도록 앱을 구성하려면 다음 [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 요소가 필요합니다.

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false" />
</runtime>
```

### <a name="restoring-legacy-behavior"></a>레거시 동작 복원

4\.7.1부터 시작하는 .NET Framework의 버전을 대상으로 하는 애플리케이션은 애플리케이션의 구성 파일의 [`<runtime>`](../configure-apps/file-schema/runtime/index.md) 섹션에서 [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 요소에 스위치를 추가하고 `true`로 해당 값을 설정하여 내게 필요한 옵션 기능을 비활성화할 수 있습니다. 예를 들어 다음 구성은 .NET Framework 4.7.2에 도입된 내게 필요한 옵션 기능을 옵트아웃합니다.

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures.2=true" />
</runtime>
```

## <a name="whats-new-in-accessibility-in-net-framework-48"></a>.NET Framework 4.8에서 내게 필요한 옵션의 새로운 기능

.NET Framework 4.8에는 다음과 같은 영역의 새로운 내게 필요한 옵션 기능이 포함됩니다.

- [Windows Forms](#winforms48)

- [WPF(Windows Presentation Foundation)](#wpf48)

- [Windows WF(Workflow Foundation) 워크플로 디자이너](#wf48)

<a name="winforms48" />

### <a name="windows-forms"></a>Windows Forms

.NET Framework 4.8에서 Windows Forms는 자주 사용되는 많은 컨트롤에 LiveRegions 및 알림 이벤트에 대한 지원을 추가합니다. 또한 사용자가 키보드를 사용하여 컨트롤로 이동할 때 도구 설명에 대한 지원을 추가합니다.

**레이블 및 StatusStrips에서 UIA LiveRegions 지원**

UIA LiveRegions를 사용하면 애플리케이션 개발자는 사용자가 작업하는 위치와 별도로 위치한 컨트롤의 텍스트 변경 내용을 화면 readers에 알릴 수 있습니다. 예를 들어 연결 상태를 표시하는 <xref:System.Windows.Forms.StatusStrip> 컨트롤에 유용합니다. 연결이 끊어지고 상태가 변경되면 개발자가 화면 reader에 알리기를 원할 수 있습니다.

.NET Framework 4.8부터 Windows Forms는 <xref:System.Windows.Forms.Label> 및 <xref:System.Windows.Forms.StatusStrip> 컨트롤 모두에 대해 UIA LiveRegions를 구현합니다. 예를 들어 다음 코드에서는 `label1`이라는 <xref:System.Windows.Forms.Label> 컨트롤에서 LiveRegion을 사용합니다.

```csharp
public Form1()
{
   InitializeComponent();
   label1.AutomationLiveSetting = AutomationLiveSetting.Polite;
}

…
Label1.Text = “Ready!”;
```

내레이터는 사용자가 애플리케이션과 상호 작용하는 위치에 관계없이 “준비”를 알립니다.

<xref:System.Windows.Forms.UserControl>을 LiveRegion으로 구현할 수 있습니다.

```csharp
using System;
using System.Windows.Forms;
using System.Windows.Forms.Automation;

namespace WindowsFormsApplication
{
   public partial class UserControl1 : UserControl, IAutomationLiveRegion
   {
      public UserControl1()
      {
         InitializeComponent();
      }

      public AutomationLiveSetting AutomationLiveSetting { get; set; }
      private AutomationLiveSetting IAutomationLiveRegion.GetLiveSetting()
      {
         return this.AutomationLiveSetting;
      }

      protected override void OnTextChanged(EventArgs e)
      {
         base.OnTextChanged(e);
         AutomationNotifications.UiaRaiseLiveRegionChangedEvent(this.AccessibilityObject);
      }
   }
}
```

**UIA 알림 이벤트**

Windows 10 Fall Creators Update에 도입된 UIA 알림 이벤트를 사용하면 앱에서 UIA 이벤트를 발생시킬 수 있습니다. 이로 인해 내레이터가 UI에서 해당 컨트롤을 사용할 필요 없이 이벤트와 함께 제공하는 텍스트를 기반으로 간단히 알림을 만듭니다. 일부 시나리오에서는 앱의 액세스 가능성을 크게 개선하는 간단한 방법입니다. 시간이 오래 걸릴 수 있는 일부 프로세스의 진행 상황을 알리는 데도 유용할 수 있습니다. UIA 알림 이벤트에 대한 자세한 내용은 [데스크톱 앱이 새 UI 알림 이벤트를 활용할 수 있나요?](https://blogs.msdn.microsoft.com/winuiautomation/2017/11/08/can-your-desktop-app-leverage-the-new-uia-notification-event-in-order-to-have-narrator-say-exactly-what-your-customers-need/)를 참조하세요.

다음 예제에서는 [알림 이벤트](xref:System.Windows.Forms.AccessibleObject.RaiseAutomationNotification%2A)를 발생시킵니다.

```csharp
MethodInfo raiseMethod = typeof(AccessibleObject).GetMethod("RaiseAutomationNotification");
if (raiseMethod != null) {
   raiseMethod.Invoke(progressBar1.AccessibilityObject, new object[3] {/*Other*/ 4, /*All*/ 2, "The progress is 50%." });
}
```

**키보드 액세스에 대한 도구 설명**

.NET Framework 4.7.2 및 이전 버전을 대상으로 하는 애플리케이션에서는 마우스 포인터를 컨트롤로 이동하여 컨트롤 [도구 설명](xref:System.Windows.Forms.ToolTip)이 팝업되도록 트리거할 수 있습니다. .NET Framework 4.8부터 키보드 사용자는 한정자 키의 유무와 상관없이 Tab 키 또는 화살표 키를 사용하여 컨트롤을 중심으로 도구 설명을 트리거할 수 있습니다. 이 특정 액세스 가능성 개선을 위해서는 [AppContext 스위치](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)가 필요합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
   <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6.1"/>
   </startup>
   <runtime>
      <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
      <!-- Please note that disabling Switch.UseLegacyAccessibilityFeatures, Switch.UseLegacyAccessibilityFeatures.2 and Switch.UseLegacyAccessibilityFeatures.3 is required to disable Switch.System.Windows.Forms.UseLegacyToolTipDisplay -->
      <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false;Switch.System.Windows.Forms.UseLegacyToolTipDisplay=false"/>
   </runtime>
</configuration>
```

다음 그림은 사용자가 키보드를 사용하여 단추를 선택한 경우의 도구 설명을 보여줍니다.

![사용자가 키보드를 사용하여 단추를 탐색할 때 도구 설명](./media/tooltip.png)

<a name="wpf48" />

### <a name="windows-presentation-foundation-wpf"></a>WPF(Windows Presentation Foundation)

.NET Framework 4.8부터 WPF에는 여러 가지 접근성 개선 사항이 포함되어 있습니다.

**화면 내레이터가 더 이상 축소되거나 숨겨긴 가시성이 있는 요소를 공지하지 않음**

축소되거나 숨겨진 가시성이 있는 요소는 더 이상 화면 reader에서 공지하지 않습니다. 가시성이 <xref:System.Windows.Visibility.Collapsed?displayProperty=nameWithType> 또는 <xref:System.Windows.Visibility.Hidden?displayProperty=nameWithType>인 요소가 포함된 사용자 인터페이스는 사용자에게 공지된 경우 화면 readers에 의해 잘못 전달될 수 있습니다. .NET Framework 4.8부터 WPF는 더 이상 UIAutomation 트리의 컨트롤 뷰에 축소되거나 숨겨진 요소를 포함하지 않기 때문에 화면 readers는 이러한 요소를 더 이상 공지할 수 없습니다.

**비표시기(Adorner) 기반 텍스트 선택 영역과 함께 사용할 SelectionTextBrush 속성**

.NET Framework 4.7.2에서 WPF는 표시기 계층을 사용하지 않고 <xref:System.Windows.Controls.TextBox> 및 <xref:System.Windows.Controls.PasswordBox> 텍스트 선택 영역을 그리는 기능을 추가했습니다. 이 시나리오에서 선택한 텍스트의 전경색은 <xref:System.Windows.SystemColors.HighlightTextBrush?displayProperty=nameWithType>에 의해 지정되었습니다.

.NET Framework 4.8은 개발자가 비표시기 기반 텍스트 선택 영역을 사용할 때 선택한 텍스트에 대한 특정 브러시를 선택할 수 있도록 하는 새 속성(`SelectionTextBrush`)을 추가합니다. 이 속성은 <xref:System.Windows.Controls.Primitives.TextBoxBase>에서 파생된 컨트롤과 비표시기 기반 텍스트 선택이 활성화된 WPF 애플리케이션의 <xref:System.Windows.Controls.PasswordBox> 컨트롤에서만 작동합니다. <xref:System.Windows.Controls.RichTextBox> 콘트롤에서는 작동하지 않습니다. 비표시기 기반 텍스트 선택 영역이 활성화되지 않은 경우 이 속성은 무시됩니다.

이 속성을 사용하려면 XAML 코드에 추가하고 적절한 브러시 또는 바인딩을 사용하기만 하면 됩니다. 결과 텍스트 선택 영역은 다음과 같습니다.

![사용자가 키보드를 사용하여 단추를 탐색할 때 도구 설명](./media/selectiontextbrush-property.png)

`SelectionBrush` 및 `SelectionTextBrush` 속성의 사용을 조합하여 적절한 것으로 간주되는 배경 및 전경색 조합을 생성할 수 있습니다.

**UIAutomation ControllerFor 속성 지원**

UIAutomation의 `ControllerFor` 속성은 이 속성을 지원하는 자동화 요소에 의해 조작되는 자동화 요소의 배열을 반환합니다. 이 속성은 자동 제안 접근성에 주로 사용됩니다. `ControllerFor`는 자동화 요소가 애플리케이션 UI 또는 데스크톱의 하나 이상의 세그먼트에 영향을 줄 때 사용됩니다. 그렇지 않으면 제어 작업의 영향을 UI 요소와 연결시키기가 어렵습니다. 이 기능은 컨트롤이 `ControllerFor` 속성 값을 제공하는 기능을 추가합니다.

.NET Framework 4.8에는 새로운 가상 메서드인 <xref:System.Windows.Automation.Peers.AutomationPeer.GetControlledPeersCore?displayProperty=nameWithType?displayProperty=nameWithType>이 추가됩니다. `ControllerFor` 속성에 대한 값을 제공하려면 이 메서드를 재정의하고 이 <xref:System.Windows.Automation.Peers.AutomationPeer>에 의해 조작되는 컨트롤에 대해 `List<AutomationPeer>`를 반환합니다.

```csharp
public class AutoSuggestTextBox: TextBox
{
   protected override AutomationPeer OnCreateAutomationPeer()
   {
      return new AutoSuggestTextBoxAutomationPeer(this);
   }

   public ListBox SuggestionListBox;
}

internal class AutoSuggestTextBoxAutomationPeer : TextBoxAutomationPeer
{
   public AutoSuggestTextBoxAutomationPeer(AutoSuggestTextBox owner) : base(owner)
   {
   }

   protected override List<AutomationPeer> GetControlledPeersCore()
   {
      List<AutomationPeer> controlledPeers = new List<AutomationPeer>();
      AutoSuggestTextBox owner = Owner as AutoSuggestTextBox;
      controlledPeers.Add(UIElementAutomationPeer.CreatePeerForElement(owner.SuggestionListBox));
      return controlledPeers;
   }
}
```

**키보드 액세스에 대한 도구 설명**

.NET Framework 4.7.2 및 이전 버전에서 도구 설명은 사용자가 마우스 커서를 컨트롤 위에 놓을 때만 표시됩니다. .NET Framework 4.8에서 도구 설명은 키보드 포커스뿐만 아니라 바로 가기 키를 통해서도 표시됩니다.

이 기능을 사용하려면 애플리케이션이 `Switch.UseLegacyAccessibilityFeatures.3` 및 `Switch.UseLegacyToolTipDisplay`[AppContext](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 스위치를 사용하여 .NET Framework 4.8을 대상으로 하거나 옵트인해야 합니다. 다음은 샘플 애플리케이션 구성 파일입니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
   <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
   </startup>
   <runtime>
      <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false;Switch.UseLegacyToolTipDisplay=false" />
   </runtime>
</configuration>
```

활성화되어 컨트롤이 키보드 포커스를 받으면 도구 설명이 포함된 모든 컨트롤이 표시됩니다. 도구 설명은 시간이 경과하거나 키보드 포커스가 변경될 때 해제할 수 있습니다. 사용자가 새로운 바로 가기 키인 Ctrl + Shift + F10을 사용하여 도구 설명을 수동으로 해제할 수도 있습니다. 도구 설명이 해제되면 동일한 바로 가기 키를 사용하여 다시 표시할 수 있습니다.

> [!NOTE]
> <xref:System.Windows.Controls.Ribbon.Ribbon> 컨트롤의 [리본 도구 설명](xref:System.Windows.Controls.Ribbon.RibbonToolTip)이 키보드 포커스에 표시되지 않습니다. 바로 가기 키를 통해서만 표시됩니다.

**SizeOfSet 및 PositionInSet UIAutomation 속성에 대한 지원 추가**

Windows 10에는 애플리케이션에서 집합의 항목 수를 설명하는 데 사용되는 두 개의 새로운 UIAutomation 속성(`SizeOfSet` 및 `PositionInSet`)이 도입되었습니다. 그런 다음, 화면 readers와 같은 UIAutomation 클라이언트 애플리케이션은 이러한 속성에 대한 애플리케이션을 쿼리하고 애플리케이션의 UI를 정확하게 표시할 수 있습니다.

.NET Framework 4.8부터 WPF 애플리케이션의 UIAutomation에 이러한 두 속성을 노출합니다. 이는 두 가지 방법으로 수행할 수 있습니다.

- 종속성 속성을 사용합니다.

  WPF는 두 개의 새 종속성 속성(<xref:System.Windows.Automation.AutomationProperties.SizeOfSet?displayProperty=nameWithType> 및 <xref:System.Windows.Automation.AutomationProperties.PositionInSet?displayProperty=nameWithType>)을 추가합니다. 개발자는 XAML을 사용하여 해당 값을 설정할 수 있습니다.

  ```xaml
  <Button AutomationProperties.SizeOfSet="3"
    AutomationProperties.PositionInSet="1">Button 1</Button>

  <Button AutomationProperties.SizeOfSet="3"
    AutomationProperties.PositionInSet="2">Button 2</Button>

  <Button AutomationProperties.SizeOfSet="3"
    AutomationProperties.PositionInSet="3">Button 3</Button>
  ```

- AutomationPeer 가상 메서드를 재정의합니다.

  <xref:System.Windows.Automation.Peers.AutomationPeer.GetSizeOfSetCore> 및 <xref:System.Windows.Automation.Peers.AutomationPeer.GetPositionInSetCore> 가상 메서드가 AutomationPeer 클래스에 추가되었습니다. 개발자는 다음 예제와 같이 이러한 메서드를 재정의하여 `SizeOfSet` 및 `PositionInSet`에 대한 값을 제공할 수 있습니다.

  ```csharp
  public class MyButtonAutomationPeer : ButtonAutomationPeer
  {
    protected override int GetSizeOfSetCore()
    {
        // Call into your own logic to provide a value for SizeOfSet
        return CalculateSizeOfSet();
    }

    protected override int GetPositionInSetCore()
    {
        // Call into your own logic to provide a value for PositionInSet
        return CalculatePositionInSet();
    }
  }
  ```

또한 <xref:System.Windows.Controls.ItemsControl> 인스턴스의 항목은 개발자의 추가 작업 없이 이러한 속성에 대한 값을 자동으로 제공합니다. <xref:System.Windows.Controls.ItemsControl>이 그룹화되면 그룹의 컬렉션이 집합으로 표시되고, 각 그룹은 별도의 집합으로 계산되며, 그룹 내의 각 항목은 해당 그룹 내에서의 위치뿐 아니라 그룹의 크기를 제공합니다. 자동 값은 가상화의 영향을 받지 않습니다. 항목이 실현되지 않더라도 여전히 집합의 전체 크기로 계산되며, 해당 형제 항목 세트의 위치에 영향을 줍니다.

자동 값은 애플리케이션이 .NET Framework 4.8을 대상으로 하는 경우에만 제공됩니다. 이전 버전의 .NET Framework를 대상으로 하는 애플리케이션의 경우 다음 App.config 파일에 표시된 것처럼 `Switch.UseLegacyAccessibilityFeatures.3` [AppContext 스위치](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)를 설정할 수 있습니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
   <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
   </startup>
   <runtime>
      <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false" />
   </runtime>
</configuration>
```

<a name="wf48" />

### <a name="windows-workflow-foundation-wf-workflow-designer"></a>Windows WF(Workflow Foundation) 워크플로 디자이너

워크플로 디자이너는 .NET Framework 4.8에서 다음과 같은 변경 내용을 포함합니다.

- 내레이터를 사용하는 사용자는 FlowSwitch 케이스 레이블의 개선 사항을 볼 수 있습니다.

- 내레이터를 사용하는 사용자는 단추 설명의 개선 사항을 볼 수 있습니다.

- 고대비 테마를 선택한 사용자는 워크플로 디자이너의 표시 유형에서 개선 사항 및 포커스 요소에 사용되는 요소와 더욱 분명한 선택 영역 상자 사이의 대조율과 같은 해당 컨트롤을 확인할 수 있습니다.

애플리케이션이 .NET Framework 4.7.2 또는 이전 버전을 대상으로 하는 경우 애플리케이션 구성 파일에서 `Switch.UseLegacyAccessibilityFeatures.3` [AppContext 스위치](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)를 `false`로 설정하여 이러한 변경 내용을 선택할 수 있습니다. 자세한 내용은 이 문서의 [내게 필요한 옵션 개선 사항 활용](#taking-advantage-of-accessibility-enhancements) 섹션을 참조하세요.

## <a name="whats-new-in-accessibility-in-net-framework-472"></a>.NET Framework 4.7.2에서 내게 필요한 옵션의 새로운 기능

.NET Framework 4.7.2에는 다음과 같은 영역의 새로운 내게 필요한 옵션 기능이 포함됩니다.

- [Windows Forms](#winforms472)

- [WPF(Windows Presentation Foundation)](#wpf472)

<a name="winforms472"></a>

### <a name="windows-forms"></a>Windows Forms

**고대비 테마에서 OS 정의 색**

.NET Framework 4.7.2부터 Windows Forms는 고대비 테마에서 운영 체제에 의해 정의된 색을 사용합니다. 이는 다음 컨트롤에 영향을 줍니다.

- <xref:System.Windows.Forms.ToolStripDropDownButton> 컨트롤의 드롭다운 화살표

- <xref:System.Windows.Forms.ButtonBase.FlatStyle>이 <xref:System.Windows.Forms.FlatStyle.Flat?displayProperty=nameWithType> 또는 <xref:System.Windows.Forms.FlatStyle.Popup?displayProperty=nameWithType>으로 설정된 <xref:System.Windows.Forms.Button>, <xref:System.Windows.Forms.RadioButton> 및 <xref:System.Windows.Forms.CheckBox> 컨트롤 이전에 선택한 텍스트 및 배경색이 대비되지 않았고 읽기가 어려웠습니다.

- 해당 <xref:System.Windows.Forms.Control.Enabled> 속성이 `false`로 설정된 <xref:System.Windows.Forms.GroupBox> 내부에 포함된 컨트롤

- 고대비 모드에서 명도 대비를 증가시킨 <xref:System.Windows.Forms.ToolStripButton>, <xref:System.Windows.Forms.ToolStripComboBox> 및 <xref:System.Windows.Forms.ToolStripDropDownButton> 컨트롤

- <xref:System.Windows.Forms.DataGridViewLinkCell>의 <xref:System.Windows.Forms.DataGridViewLinkCell.LinkColor> 속성입니다.

**내레이터 개선 사항**

.NET Framework 4.7.2부터 내레이터 지원이 다음과 같이 향상됩니다.

- <xref:System.Windows.Forms.ToolStripMenuItem>의 텍스트를 발표할 경우 <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys?displayProperty=nameWithType> 속성 값도 발표합니다.

- <xref:System.Windows.Forms.ToolStripMenuItem>이 해당 <xref:System.Windows.Forms.Control.Enabled> 속성을 `false`로 설정할 때를 지정합니다.

- <xref:System.Windows.Forms.ListView.CheckBoxes?displayProperty=nameWithType> 속성이 `true`로 설정될 경우 확인란의 상태에 대한 피드백을 제공합니다.

- 내레이터의 스캔 모드 포커스 순서는 ClickOnce 다운로드 대화 상자 창에서 컨트롤의 시각적 개체 순서와 일치합니다.

**DataGridView의 개선 사항**

.NET Framework 4.7.2부터 <xref:System.Windows.Forms.DataGridView> 컨트롤에는 다음과 같은 내게 필요한 옵션 개선 사항이 도입되었습니다.

- 행은 키보드를 사용하여 정렬할 수 있습니다. 현재 열로 정렬하기 위해 사용자는 F3 키를 사용할 수 있습니다.

- <xref:System.Windows.Forms.DataGridView.SelectionMode?displayProperty=nameWithType>이 <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect?displayProperty=nameWithType>으로 설정된 경우 열 헤더는 색을 변경하여 현재 행의 셀을 통해 현재 열을 사용자 탭으로 나타내게 됩니다.

- <xref:System.Windows.Forms.DataGridViewLinkCell.DataGridViewLinkCellAccessibleObject?displayProperty=nameWithType>의 <xref:System.Windows.Forms.AccessibleObject.Parent?displayProperty=nameWithType> 속성은 이제 올바른 부모 컨트롤을 반환합니다.

**개선된 시각적 표시**

- <xref:System.Windows.Forms.ButtonBase.Text> 속성이 빈 <xref:System.Windows.Forms.RadioButton> 및 <xref:System.Windows.Forms.CheckBox> 컨트롤은 포커스를 받을 때 포커스 표시기를 표시합니다.

**개선된 속성 표 지원**

- <xref:System.Windows.Forms.PropertyGrid> 컨트롤 자식 요소는 PropertyGrid 요소를 사용하도록 설정한 경우에만 <xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty> 속성에 대한 `true`를 반환합니다.

- <xref:System.Windows.Forms.PropertyGrid> 컨트롤 자식 요소는 PropertyGrid 요소를 사용자가 변경할 수 있는 경우에만 <xref:System.Windows.Automation.AutomationElement.IsEnabledProperty> 속성에 대한 `false`를 반환합니다.

**바로 가기 탐색 개선**

- <xref:System.Windows.Forms.ToolStripButton> 컨트롤은 <xref:System.Windows.Forms.ToolStripPanel.TabStop> 속성이 `true`로 설정된 <xref:System.Windows.Forms.ToolStripPanel>에 포함된 경우 포커스를 허용합니다.

<a name="wpf472"></a>

### <a name="windows-presentation-foundation-wpf"></a>WPF(Windows Presentation Foundation)

**CheckBox 및 RadioButton 컨트롤에 대한 변경**

.NET Framework 4.7.1 이전 버전에서 WPF <xref:System.Windows.Controls.CheckBox?displayProperty=nameWIthType> 및 <xref:System.Windows.Controls.RadioButton?displayProperty=nameWIthType> 컨트롤에는 일치하지 않는, 그리고 기본 및 고대비 테마에서는 잘못된 포커스 시각적 개체가 있습니다.  이러한 문제는 컨트롤에 아무 콘텐츠 집합도 없는 경우 발생합니다.  이렇게 하면 테마 혼동 및 포커스 시각적 개체 간 전환을 보기 어렵게 할 수 있습니다.

NET Framework 4.7.2에서 이러한 시각적 개체는 이제 테마에서 더욱 일관적이고 기본 및 고대비 테마에서 더욱 쉽게 볼 수 있습니다.

**WPF 애플리케이션에서 호스트되는 WinForms 컨트롤**

.NET Framework 4.7.1 이전 버전의 WPF 애플리케이션에서 호스팅되는 WinForms 컨트롤의 경우 사용자는 해당 계층의 첫 번째 또는 마지막 컨트롤이 WPF <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤이면 WinForms 계층을 탭아웃할 수 없습니다. .NET Framework 4.7.2에서 사용자는 이제 WinForms 계층을 탭아웃할 수 있습니다.

그러나 WinForms 계층을 이스케이프하지 않는 포커스를 사용하는 자동화된 애플리케이션은 더 이상 예상대로 작동하지 않을 수 있습니다.

## <a name="whats-new-in-accessibility-in-net-framework-471"></a>.NET Framework 4.7.1에서 내게 필요한 옵션의 새로운 기능

.NET Framework 4.7.1에는 다음과 같은 영역의 새로운 내게 필요한 옵션 기능이 포함됩니다.

- [WPF(Windows Presentation Foundation)](#wpf471)

- [Windows Forms](#winforms471)

- [ASP.NET 웹 컨트롤](#aspnet471)

- [.NET SDK Tools](#tools471)

- [Windows WF(Workflow Foundation) 워크플로 디자이너](#wf471)

<a name="wpf471"></a>

### <a name="windows-presentation-foundation-wpf"></a>WPF(Windows Presentation Foundation)

**화면 판독기 개선 사항**

내게 필요한 옵션 개선 사항이 활성화된 경우 .NET Framework 4.7.1에는 화면 판독기에 영향을 주는 다음과 같은 향상 기능이 포함되어 있습니다.

- .NET Framework 4.7 이전 버전에서 <xref:System.Windows.Controls.Expander> 컨트롤은 단추로 화면 readers에서 공지되었습니다. .NET Framework 4.7.1부터 확장/축소 가능한 그룹으로 올바르게 공지됩니다.

- .NET Framework 4.7 이전 버전에서 <xref:System.Windows.Controls.DataGridCell> 컨트롤은 “사용자 지정”으로 화면 readers에서 공지되었습니다. .NET Framework 4.7.1부터 이제 데이터 표 셸(지역화된)로 올바르게 공지됩니다.

- .NET Framework 4.7.1부터 화면 readers는 편집 가능한 <xref:System.Windows.Controls.ComboBox>의 이름을 공지합니다.

- .NET Framework 4.7 이전 버전에서 <xref:System.Windows.Controls.PasswordBox> 컨트롤은 "보기에 항목 없음"으로 공지되었거나 그렇지 않은 경우 잘못된 동작이 있었습니다. 이 문제는 .NET Framework 4.7.1부터 수정되었습니다.

**UIAutomation LiveRegion 지원**

내레이터와 같은 화면 판독기는 사용자가 일반적으로 포커스가 있는 UI 콘텐츠의 텍스트 음성 변환 출력에 의해 애플리케이션의 UI 콘텐츠를 읽는 데 도움을 줍니다. 그러나 UI 요소가 변경되고 포커스가 없는 경우 사용자는 알림을 받지 못하고 중요한 정보를 놓칠 수 있습니다. 라이브 영역은 이 문제를 해결하는 것을 목표로 합니다. 개발자는 화면 판독기 또는 다른 UIAutomation 클라이언트에게 UI 요소에 중요한 변경 내용이 만들어졌음을 알리는 데 사용할 수 있습니다. 화면 판독기는 사용자에게 이 변경 내용을 알리는 방법 및 시점을 결정할 수 있습니다.

라이브 영역을 지원하기 위해 다음과 같은 API가 WPF에 추가되었습니다.

- **LiveSetting** 속성 및 **LiveRegionChanged** 이벤트를 식별하는 <xref:System.Windows.Automation.AutomationElementIdentifiers.LiveSettingProperty?displayProperty=nameWithType> 및 <xref:System.Windows.Automation.AutomationElementIdentifiers.LiveRegionChangedEvent?displayProperty=nameWithType> 필드 XAML을 사용하여 설정할 수 있습니다.

- **AutomationProperties.LiveSetting** 연결된 속성으로, 화면 판독기에 사용자에 대한 UI 변경 내용의 중요성을 알려줍니다.

- **AutomationProperties.LiveSetting** 연결된 속성을 식별하는 <xref:System.Windows.Automation.AutomationProperties.LiveSettingProperty?displayProperty=nameWithType> 속성

- **LiveSetting** 값을 제공하도록 재정의될 수 있는 <xref:System.Windows.Automation.Peers.AutomationPeer.GetLiveSettingCore%2A?displayProperty=nameWithType> 메서드

- **LiveSetting** 값을 가져오고 설정하는 <xref:System.Windows.Automation.AutomationProperties.GetLiveSetting%2A?displayProperty=nameWithType> 및 <xref:System.Windows.Automation.AutomationProperties.SetLiveSetting%2A?displayProperty=nameWithType> 메서드

- 다음 가능한 **LiveSetting** 값을 정의하는 <xref:System.Windows.Automation.AutomationLiveSetting?displayProperty=nameWithType> 열거형

  - <xref:System.Windows.Automation.AutomationLiveSetting.Off?displayProperty=nameWithType>. 라이브 영역의 콘텐츠가 변경된 경우 요소는 알림을 보내지 않습니다.
  - <xref:System.Windows.Automation.AutomationLiveSetting.Polite?displayProperty=nameWithType>. 라이브 영역의 콘텐츠가 변경된 경우 요소는 비중단 알림을 보냅니다.

  - <xref:System.Windows.Automation.AutomationLiveSetting.Assertive?displayProperty=nameWithType>. 라이브 영역의 콘텐츠가 변경된 경우 요소는 중단 알림을 보냅니다.

다음 예제와 같이 관심 있는 요소에 **AutomationProperties.LiveSetting** 속성을 설정하여 LiveRegion을 만들 수 있습니다.

```xaml
<TextBlock Name="myTextBlock" AutomationProperties.LiveSetting="Assertive">announcement</TextBlock>
```

라이브 영역에 있는 데이터가 변경되고 화면 판독기에 알려야 하는 경우 다음 샘플과 같이 명시적으로 이벤트를 발생시킵니다.

```csharp
var peer = FrameworkElementAutomationPeer.FromElement(myTextBlock);

peer.RaiseAutomationEvent(AutomationEvents.LiveRegionChanged);
```

```vb
Dim peer = FrameworkElementAutomationPeer.FromElement(myTextBlock)
peer.RaiseAutomationEvent(AutomationEvents.LiveRegionChanged)

```

**고대비**

.NET Framework 4.7.1부터 다양한 WPF 컨트롤에 고대비의 개선 사항이 만들어졌습니다. <xref:System.Windows.SystemParameters.HighContrast%2A> 테마가 설정된 경우 이제 표시됩니다. 여기에는 다음이 포함됩니다.

- <xref:System.Windows.Controls.Expander> 컨트롤

  <xref:System.Windows.Controls.Expander> 컨트롤에 대한 포커스 시각적 개체는 이제 표시됩니다. <xref:System.Windows.Controls.ComboBox>, <xref:System.Windows.Controls.ListBox> 및 <xref:System.Windows.Controls.RadioButton> 컨트롤에 대한 키보드 시각적 개체도 표시됩니다. 예:

  이전: 

  ![내게 필요한 옵션 개선 사항 이전의 포커스가 있는 Expander 컨트롤](./media/expander-before.png)

  이후: 

  ![내게 필요한 옵션 개선 사항 이후의 포커스가 있는 Expander 컨트롤](./media/expander-after.png)

- <xref:System.Windows.Controls.CheckBox> 및 <xref:System.Windows.Controls.RadioButton> 컨트롤

  <xref:System.Windows.Controls.CheckBox> 및 <xref:System.Windows.Controls.RadioButton> 컨트롤의 텍스트는 이제 고대비 테마에서 선택하면 쉽게 볼 수 있습니다. 예:

  이전: 

  ![내게 필요한 옵션 개선 사항 이전의 포커스가 있는 고대비 라디오 단추](./media/radio-button-before.png)

  이후: 

  ![내게 필요한 옵션 개선 사항 이후의 포커스가 있는 고대비 라디오 단추](./media/radio-button-after.png)

- <xref:System.Windows.Controls.ComboBox> 컨트롤

  .NET Framework 4.7.1부터 비활성화된 <xref:System.Windows.Controls.ComboBox> 컨트롤의 테두리는 비활성화된 텍스트와 동일한 색입니다. 예:

  이전: 

  ![내게 필요한 옵션 개선 사항 이전의 콤보 상자 비활성화된 테두리 및 텍스트](./media/combo-disabled-before.png)

  이후:   

  ![내게 필요한 옵션 개선 사항 이후의 콤보 상자 비활성화된 테두리 및 텍스트](./media/combo-disabled-after.png)

  또한 비활성화되고 포커스가 있는 단추는 올바른 테마 색을 사용합니다.

  이전:

  ![내게 필요한 옵션 개선 사항 이전의 단추 테마 색](./media/button-themes-before.png) 

  이후: 

  ![내게 필요한 옵션 개선 사항 이후의 단추 테마 색](./media/button-themes-after.png) 

  마지막으로 .NET Framework 4.7 이전 버전에서 <xref:System.Windows.Controls.ComboBox> 컨트롤의 스타일을 `Toolbar.ComboBoxStyleKey`로 설정하면 드롭다운 화살표가 표시되지 않았습니다. 이 문제는 .NET Framework 4.7.1부터 수정되었습니다. 예:

  이전: 

  ![내게 필요한 옵션 개선 사항 이전의 Toolbar.ComboBoxStyleKey](./media/comboboxstylekey-before.png) 

  이후: 

  ![내게 필요한 옵션 개선 사항 이후의 Toolbar.ComboBoxStyleKey](./media/comboboxstylekey-after.png) 

- <xref:System.Windows.Controls.DataGrid> 컨트롤

  .NET Framework 4.7.1부터 <xref:System.Windows.Controls.DataGrid> 컨트롤의 정렬 표시기 화살표는 이제 올바른 테마 색을 사용합니다. 예:

  이전: 

  ![내게 필요한 옵션 개선 사항 이전의 정렬 표시기 화살표](./media/sort-indicator-before.png) 

  이후:   

  ![내게 필요한 옵션 개선 사항 이후의 정렬 표시기 화살표](./media/sort-indicator-after.png) 

  또한 .NET Framework 4.7 이전 버전에서 기본 링크 스타일은 고대비 모드의 마우스에서 잘못된 색으로 변경되었습니다. 이는 .NET Framework 4.7.1부터 해결되었습니다. 마찬가지로 <xref:System.Windows.Controls.DataGrid> 확인란 열은 .NET Framework 4.7.1부터 키보드 포커스 피드백에 대해 예상되는 색을 사용합니다.

  이전: 

  ![내게 필요한 옵션 개선 사항 이전의 DataGrid 기본 링크 스타일](./media/default-link-style-before.png) 

  이후:    

  ![내게 필요한 옵션 개선 사항 이후의 DataGrid 기본 링크 스타일](./media/default-link-style-after.png) 

.NET Framework 4.7.1에서 WPF 내게 필요한 옵션 개선 사항에 대한 자세한 내용은 [WPF의 내게 필요한 옵션 개선 사항](../migration-guide/retargeting/4.7-4.7.1.md#accessibility-improvements-in-wpf)을 참조하세요.

<a name="winforms471"></a>

### <a name="windows-forms-accessibility-improvements"></a>Windows Forms 내게 필요한 옵션 개선 사항

.NET Framework 4.7.1에서 WinForms(Windows Forms)는 다음 영역에서 내게 필요한 옵션 변경 내용을 포함합니다.

**고대비 모드에서 향상된 표시**

.NET Framework 4.7.1부터 다양한 WinForms 컨트롤은 운영 체제에서 사용할 수 있는 고대비 모드의 향상된 렌더링을 제공합니다. Windows 10은 일부 고대비 시스템 색에 대한 값을 변경했으며 Windows Forms는 Windows 10 Win32 프레임워크를 기반으로 합니다. 최상의 환경을 위해 최신 버전의 Windows를 실행하고 테스트 애플리케이션에 app.manifest 파일을 추가하여 최신 OS로 옵트인하고 다음과 같이 보이도록 Windows 10 지원 OS 줄에 대한 주석을 제거합니다.

```xml
<!-- Windows 10 -->
<supportedOS Id=”{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}” />
```

고대비 변경 내용의 몇 가지 예는 다음과 같습니다.

- <xref:System.Windows.Forms.MenuStrip> 항목의 확인 표시는 보기가 쉽습니다.

- 선택하면 비활성화된 <xref:System.Windows.Forms.MenuStrip> 항목이 보기가 쉽습니다.

- 선택된 <xref:System.Windows.Forms.Button> 컨트롤의 텍스트는 선택 영역 색과 대비됩니다.

- 비활성화된 텍스트는 읽기가 쉽습니다. 예:

  이전:

  ![내게 필요한 옵션 개선 사항 이전의 비활성화된 텍스트](./media/wf-disabled-before.png) 

  이후:

  ![내게 필요한 옵션 개선 사항 이후의 비활성화된 텍스트](./media/wf-disabled-after.png) 

- 스레드 예외 대화 상자의 고대비 개선 사항입니다.

**향상된 내레이터 지원**

.NET Framework 4.7.1에서 Windows Forms는 내레이터에 대한 다음과 같은 내게 필요한 옵션 개선 사항을 포함합니다.

- <xref:System.Windows.Forms.MonthCalendar> 컨트롤은 내레이터 및 다른 UI 자동화 도구로 액세스할 수 있습니다.

- <xref:System.Windows.Forms.CheckedListBox> 컨트롤은 항목의 선택 상태가 변경되어 목록 항목의 값을 변경했음을 사용자에게 알릴 때 내레이터에 알립니다.

- <xref:System.Windows.Forms.DataGridViewCell> 컨트롤은 올바른 읽기 전용 상태를 내레이터에 보고합니다.

- 내레이터는 이제 비활성화된 <xref:System.Windows.Forms.ToolStripMenuItem> 텍스트를 읽을 수 있는 반면 이전에는 비활성화된 메뉴 항목을 건너뛰었습니다.

**UIAutomation 내게 필요한 옵션 패턴에 대한 향상된 지원**

.NET Framework 4.7.1부터 내게 필요한 옵션 기술 도구의 개발자는 API 내게 필요한 옵션의 일반 패턴 및 여러 WinForms 컨트롤에 대한 속성을 활용할 수 있습니다. 이러한 내게 필요한 옵션 개선 사항은 다음을 포함합니다.

- <xref:System.Windows.Forms.ComboBox> 및 <xref:System.Windows.Forms.ToolStripSplitButton>은 이제 [확장/축소 패턴](../ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md)을 지원합니다.

- <xref:System.Windows.Forms.DataGridViewCheckBoxCell>은 이제 [토글 패턴](../ui-automation/implementing-the-ui-automation-toggle-control-pattern.md)을 지원합니다.

- <xref:System.Windows.Forms.ToolStripItem> 컨트롤은 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name> 속성 및 [확장/축소 패턴](../ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md)을 지원합니다.

- <xref:System.Windows.Forms.NumericUpDown> 및 <xref:System.Windows.Forms.DomainUpDown> 컨트롤은 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name> 속성을 지원합니다.

**향상된 속성 브라우저 환경**

.NET Framework 4.7.1부터 Windows Forms는 다음을 포함합니다.

- 다양한 드롭다운 선택 창을 통한 향상된 키보드 탐색
- 불필요한 탭 정지의 감소
- 컨트롤 형식의 향상된 보고
- 향상된 내레이터 동작

<a name="aspnet471"></a>

### <a name="aspnet-web-controls"></a>ASP.NET 웹 컨트롤

.NET Framework 4.7.1 및 Visual Studio 2017 15.3부터 ASP.NET은 ASP.NET 웹 컨트롤이 Visual Studio의 내게 필요한 옵션 기술과 연동하는 방식을 개선합니다. 변경 내용은 다음과 같습니다.

- **자세히 보기** 마법사의 **필드 추가** 대화 상자 또는 **ListView** 마법사의 **ListView 구성** 대화 상자와 같이 컨트롤에서 누락된 UI 액세스 가능성 패턴을 구현하도록 변경됨.

- **데이터 호출기 필드 편집기**와 같이 고대비 모드에서 디스플레이를 개선하도록 변경됨.

- DataPager 컨트롤의 **호출기 필드 편집** 마법사의 **필드** 대화 상자, **ObjectContext 구성** 대화 상자 또는 **데이터 원본 구성** 마법사의 **데이터 선택 구성** 대화 상자와 같은 컨트롤의 키보드 탐색 환경을 개선하도록 변경됨.

<a name="tools471"></a>

### <a name="net-sdk-tools"></a>.NET SDK Tools

[Configuration Editor 도구(SvcConfigEditor.exe)](../wcf/configuration-editor-tool-svcconfigeditor-exe.md) 및 [Service Trace Viewer 도구(SvcTraceViewer.exe)](../wcf/service-trace-viewer-tool-svctraceviewer-exe.md)는 다양한 액세스 가능성 문제를 수정하여 향상되었습니다. 이들 중 대부분은 정의되지 않은 이름이나 특정 UI 자동화 패턴이 올바르게 구현되지 않은 것과 같은 사소한 문제였습니다. 많은 사용자가 이러한 잘못된 값을 인식하지 못하지만, 화면 판독기와 같은 보조 기술을 사용하는 고객은 이러한 SDK 도구를 보다 쉽게 사용할 수 있습니다.

이러한 개선 사항은 키보드 포커스 순서 등의 일부 이전 동작을 변경합니다.

<a name="wf471"></a>

### <a name="windows-workflow-foundation-wf-workflow-designer"></a>Windows WF(Workflow Foundation) 워크플로 디자이너

워크플로 디자이너에서 내게 필요한 옵션 변경 내용은 다음과 같습니다.

- 일부 컨트롤에서 왼쪽에서 오른쪽으로, 위쪽에서 아래쪽으로 탭 순서를 변경합니다.

  - <xref:System.ServiceModel.Activities.InitializeCorrelation> 작업에 대한 상관 관계 데이터를 설정하는 초기화 상관 관계 창

  - <xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.SendReply> 및 <xref:System.ServiceModel.Activities.ReceiveReply> 작업에 대한 콘텐츠 정의 창

- 바로 가기를 통해 추가 함수가 지원됩니다.

  - 작업의 속성을 편집할 때 처음으로 포커스된 경우 바로 가기에서 속성 그룹을 축소할 수 있습니다.

  - 경고 아이콘은 바로 가기에서 액세스할 수 있습니다.

  - 바로 가기에서 **속성** 창의 **추가 속성** 단추에 액세스할 수 있습니다.

  - 바로 가기 사용자는 워크플로 디자이너의 **인수** 및 **변수** 창에 있는 헤더 항목에 액세스할 수 있습니다.

- 다음과 같은 경우 포커스가 있는 항목의 표시 유형 향상

  - 워크플로 디자이너 및 작업 디자이너에서 사용하는 데이터 그리드에 행 추가

  - <xref:System.ServiceModel.Activities.ReceiveReply> 및 <xref:System.ServiceModel.Activities.SendReply> 작업에서 필드 누름

  - 변수 또는 인수에 대한 기본값 설정

- 이제 화면 읽기 프로그램이 다음 항목을 올바르게 인식합니다.

  - 워크플로 디자이너에서 설정된 중단점

  - <xref:System.Activities.Statements.FlowSwitch%601>, <xref:System.Activities.Statements.FlowDecision> 및 <xref:System.ServiceModel.Activities.CorrelationScope> 작업
  - <xref:System.ServiceModel.Activities.Receive> 작업의 콘텐츠

  - <xref:System.Activities.Statements.InvokeMethod> 작업의 대상 유형

  - <xref:System.Activities.Statements.TryCatch> 작업의 예외 콤보 상자 및 마지막 섹션

  - 메시지 유형 콤보 상자, 상관 관계 이니셜라이저 추가 창의 분할기, 콘텐츠 정의 창 및 메시징 작업의 CorrelatesOn 정의 창(<xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.SendReply> 및 <xref:System.ServiceModel.Activities.ReceiveReply>)

  - 상태 컴퓨터 전환 및 전환 대상

  - <xref:System.Activities.Statements.FlowDecision> 작업의 주석 및 커넥터

  - 작업의 팝업(마우스 오른쪽 단추 클릭) 메뉴

  - 속성 값 편집기, 검색 정리 단추, 범주별으로 및 사전순 정렬 단추 및 속성 그리드의 식 편집기 대화 상자

  - 워크플로 디자이너의 확대/축소 백분율

  - <xref:System.Activities.Statements.Parallel> 및 <xref:System.Activities.Statements.Pick> 작업의 구분 기호

  - <xref:System.Activities.Statements.InvokeDelegate> 작업

  - 사전 작업의 형식 선택 창(`Microsoft.Activities.AddToDictionary<TKey,TValue>`, `Microsoft.Activities.RemoveFromDictionary<TKey,TValue>`등)

  - .NET 형식 찾아보기 및 선택 창

  - 워크플로 디자이너의 이동 경로

- 고대비 테마를 선택한 사용자는 워크플로 디자이너의 표시 유형에서 여러 개선 사항 및 포커스 요소에 사용되는 요소와 더욱 분명한 선택 영역 상자 사이의 대조율과 같은 해당 컨트롤을 확인합니다.

## <a name="see-also"></a>참고 항목

- [.NET Framework의 새로운 기능](whats-new.md)
