---
title: Windows Forms의 높은 DPI 지원
ms.date: 05/16/2017
helpviewer_keywords:
- High DPI in Windows Forms
- Dynamic rescaling in Windows Forms
- Windows Forms layout
- Windows Forms dynamic resizing
ms.assetid: 075ea4c3-900c-4f8a-9dd2-13ea6804346b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1641702c7b1c3d3b0e83c59a96529de70f699d17
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61966969"
---
# <a name="high-dpi-support-in-windows-forms"></a>Windows Forms의 높은 DPI 지원

.NET Framework 4.7부터 Windows Forms 일반적인 높은 DPI 및 동적 DPI 시나리오에 대 한 향상 된 기능을 포함 합니다. 여기에는 다음이 포함됩니다.

- 와 같은 크기 조정 및 레이아웃의 다양 한 Windows Forms의 향상 된 컨트롤을 <xref:System.Windows.Forms.MonthCalendar> 컨트롤 및 <xref:System.Windows.Forms.CheckedListBox> 제어 합니다.

- 단일 패스 크기 조정 합니다.  .NET Framework 4.6 및 이전 버전에서 크기 조정 필요 하는 것 보다 몇 가지 컨트롤 확장을 발생 하는 여러 패스를 통해 수행 되었습니다.

- 사용자가 변경할 DPI 또는 확장 비율을 Windows Forms 응용 프로그램을 실행 된 후 동적 DPI 시나리오를 지원 합니다.

.NET Framework 4.7 이상의.NET Framework의 버전에서 향상 된 높은 DPI 지원 옵트인 기능입니다. 활용 하도록 응용 프로그램을 구성 해야 합니다.

## <a name="configuring-your-windows-forms-app-for-high-dpi-support"></a>높은 DPI 지원에 대 한 Windows Forms 앱 구성

새 Windows Forms를 지 원하는 높은 DPI 인식 기능은.NET Framework 4.7을 대상 Windows 10 크리에이터 스 업데이트 이상 Windows 운영 체제에서 실행 되는 응용 프로그램 에서만 사용할 수 있습니다.

또한 Windows Forms 응용 프로그램의 높은 DPI 지원을 구성 하려면는 다음을 수행 해야 합니다.

- Windows 10과의 호환성을 선언 합니다.

  이렇게 하려면 다음 매니페스트 파일에 추가 합니다.

  ```xml
  <compatibility xmlns="urn:schemas-microsoft-com:compatibility.v1">
    <application>
      <!-- Windows 10 compatibility -->
      <supportedOS Id="{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}" />
    </application>
  </compatibility>
  ```

- 모니터별 DPI 인식을 사용 하도록 설정 합니다 *app.config* 파일입니다.

  새 Windows Forms 소개 [ `<System.Windows.Forms.ApplicationConfigurationSection>` ](../configure-apps/file-schema/winforms/index.md) 요소를 새 기능을 추가 하는 사용자 지정.NET Framework 4.7부터 지원 합니다. 높은 DPI를 지 원하는 새 기능을 활용 하려면 다음 응용 프로그램 구성 파일을 추가 합니다.

  ```xml
  <System.Windows.Forms.ApplicationConfigurationSection>
    <add key="DpiAwareness" value="PerMonitorV2" />
  </System.Windows.Forms.ApplicationConfigurationSection>
  ```

  > [!IMPORTANT]
  > .NET Framework의 이전 버전에서는 높은 DPI 지원 추가 매니페스트를 사용 합니다. App.config 파일에 정의 된 설정을 재정의 하므로이 방법은 더 이상 권장 됩니다.

- 정적 호출 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> 메서드.

  이 응용 프로그램 진입점의 첫 번째 메서드 호출 해야 합니다. 예를 들어:

  ```csharp
  static void Main()
  {
      Application.EnableVisualStyles();
      Application.SetCompatibleTextRenderingDefault(false);
      Application.Run(new Form2());
  }
  ```

## <a name="opting-out-of-individual-high-dpi-features"></a>개별 높은 DPI 기능을 옵트아웃

설정 된 `DpiAwareness` 값을 `PerMonitorV2` .NET Framework 4.7 이상의.NET Framework 버전에서 지 원하는 모든 높은 DPI 인식 기능을 사용 하도록 설정 합니다. 일반적으로이 대부분의 Windows Forms 응용 프로그램에 적합 합니다. 그러나 다음 하나 이상의 개별 기능을 옵트아웃 하는 것이 좋습니다. 이 작업을 수행 하는 것에 대 한 가장 중요 한 이유는 해당 기능에 기존 응용 프로그램 코드는 이미 처리 합니다.  예를 들어, 자동 크기 조정을 처리 하는 응용 프로그램을 하는 경우 다음과 같이 자동 크기 조정 기능을 해제 하는 것이 좋습니다.

```xml
<System.Windows.Forms.ApplicationConfigurationSection>
  <add key="DpiAwareness" value="PerMonitorV2" />
  <add key="EnableWindowsFormsHighDpiAutoResizing" value="false" />
</System.Windows.Forms.ApplicationConfigurationSection>
```

개별 키와 값 목록은 참조 하세요 [Windows Forms 구성 요소 추가](../configure-apps/file-schema/winforms/windows-forms-add-configuration-element.md)합니다.

## <a name="new-dpi-change-events"></a>새 DPI 변경 이벤트

세 개의 새 이벤트를.NET Framework 4.7부터 프로그래밍 방식으로 동적 DPI 변경을 처리할 수 있도록 합니다.

- <xref:System.Windows.Forms.Control.DpiChangedAfterParent>에 부모 컨트롤에 대 한 DPI 변경 이벤트가 컨트롤의 DPI 설정이 프로그래밍 방식으로 변경 되거나 폼 발생 하는 경우 발생 합니다.
- <xref:System.Windows.Forms.Control.DpiChangedBeforeParent>에 부모 컨트롤에 대 한 DPI 변경 이벤트가 하기 전에 컨트롤의 DPI 설정이 프로그래밍 방식으로 변경 되거나 폼 발생 하는 경우 발생 합니다.
- <xref:System.Windows.Forms.Form.DpiChanged>에 폼이 표시 현재 디스플레이 장치의 DPI 설정이 변경 될 때 발생 합니다.

## <a name="new-helper-methods-and-properties"></a>새로운 도우미 메서드 및 속성

또한.NET Framework 4.7 DPI 배율 정보를 제공 하 고 DPI 조정을 수행할 수는 새로운 도우미 메서드 및 속성의 숫자를 추가 합니다. 여기에는 다음이 포함됩니다.

- <xref:System.Windows.Forms.Control.LogicalToDeviceUnits%2A>을 장치 픽셀에 논리적 좌표에서 값을 변환 합니다.

- <xref:System.Windows.Forms.Control.ScaleBitmapLogicalToDevice%2A>에서 확장 되는 비트맵 이미지를 장치에 대 한 논리적 DPI입니다.

- <xref:System.Windows.Forms.Control.DeviceDpi%2A>에 현재 장치에 대 한 DPI를 반환 합니다.

## <a name="versioning-considerations"></a>버전 관리 고려 사항

.NET Framework 4.7 및 Windows 10 크리에이터 스 업데이트를 실행 하는 것 외에도 응용 프로그램도는 호환 되지 않으므로 높은 DPI 향상 된 환경에서 실행할 수 있습니다. 이 경우 응용 프로그램에 대 한 대체를 개발 해야 합니다. 하는 데이 수행할 수 있습니다 [사용자 지정 그리기](./controls/user-drawn-controls.md) 에 크기 조정을 처리 합니다.

이렇게 하려면 앱이 실행 되는 운영 체제를 확인 해야 합니다. 다음과 같은 코드를 사용 하 여 수행할 수 있습니다.

```csharp
// Create a reference to the OS version of Windows 10 Creators Update.
Version OsMinVersion = new Version(10, 0, 15063, 0);

// Access the platform/version of the current OS.
Console.WriteLine(Environment.OSVersion.Platform.ToString());
Console.WriteLine(Environment.OSVersion.VersionString);

// Compare the current version to the minimum required version.
Console.WriteLine(Environment.OSVersion.Version.CompareTo(OsMinVersion));
```

응용 프로그램 응용 프로그램 매니페스트에서 지원 되는 운영 체제로 나열 되지 않은 경우 Windows 10 감지 했습니다. 않습니다 참고 합니다.

또한 응용 프로그램을 빌드한.NET Framework의 버전을 확인할 수 있습니다.

```csharp
Console.WriteLine(AppDomain.CurrentDomain.SetupInformation.TargetFrameworkName);
```

## <a name="see-also"></a>참고자료

- [Windows Forms 구성 요소를 추가합니다.](../configure-apps/file-schema/winforms/windows-forms-add-configuration-element.md)
- [Windows Forms의 크기 및 배율 조정](adjusting-the-size-and-scale-of-windows-forms.md)
