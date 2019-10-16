---
title: '방법: 애플리케이션 설정 업데이트'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- validating application settings
- application settings [Windows Forms], Windows Forms
- application settings [Windows Forms], validating
ms.assetid: 9f145ada-4267-436a-aa4c-c4dcffd0afb7
ms.openlocfilehash: b3b2447b570f0635942183dcc62c0e4ed73800d1
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972253"
---
# <a name="how-to-validate-application-settings"></a>방법: 애플리케이션 설정 업데이트

이 항목에서는 애플리케이션 설정이 유지되기 전에 유효성을 검사하는 방법을 설명합니다.

애플리케이션 설정이 강력한 형식이기 때문에 사용자가 지정된 설정에 잘못된 형식의 데이터를 할당할 수 없다는 점이 어느 정도 보장됩니다. 그러나 사용자가 설정에 허용 가능한 범위 밖의 값을 할당하려고 시도할 수 있습니다(예: 미래의 생년월일 제공). <xref:System.Configuration.ApplicationSettingsBase>모든 응용 프로그램 설정 클래스의 부모 클래스인는 이러한 범위 검사를 사용 하도록 설정 하는 네 개의 이벤트를 노출 합니다. 이러한 이벤트를 처리하면 모든 유효성 검사 코드를 프로젝트 전체에 분산하지 않고 단일 위치에 배치합니다.

다음 표에 설명된 대로 사용할 이벤트는 설정의 유효성을 검사해야 하는 경우에 따라 다릅니다.

|이벤트(event)|발생 및 사용|
|-----------|------------------------|
|<xref:System.Configuration.ApplicationSettingsBase.SettingsLoaded>|설정 속성 그룹을 초기 로드한 이후에 발생합니다.<br /><br /> 이 이벤트를 사용하여 전체 속성 그룹 초기 값을 애플리케이션 내에서 사용하기 전에 유효성을 검사합니다.|
|<xref:System.Configuration.ApplicationSettingsBase.SettingChanging>|단일 설정 속성의 값이 변경되기 전에 발생합니다.<br /><br /> 이 이벤트를 사용하여 단일 속성을 변경하기 전에 유효성을 검사합니다. 해당 작업 및 선택 항목에 관한 즉각적인 피드백을 사용자에게 제공할 수 있습니다.|
|<xref:System.Configuration.ApplicationSettingsBase.PropertyChanged>|단일 설정 속성의 값이 변경된 후에 발생합니다.<br /><br /> 이 이벤트를 사용하여 단일 속성을 변경한 후에 유효성을 검사합니다. 이 이벤트는 시간이 오래 걸리는 비동기 유효성 검사 프로세스가 필요한 경우가 아니면 거의 유효성 검사에 사용되지 않습니다.|
|<xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>|설정 속성 그룹이 저장되기 전에 발생합니다.<br /><br /> 이 이벤트를 사용하여 전체 속성 그룹 값을 디스크에 유지하기 전에 유효성을 검사합니다.|

일반적으로 유효성을 검사하기 위해 동일한 애플리케이션 내에서 이러한 모든 이벤트를 사용하지 않습니다. 예를 들어 <xref:System.Configuration.ApplicationSettingsBase.SettingChanging> 이벤트를 처리 하 여 모든 유효성 검사 요구 사항을 충족할 수 있습니다.

이벤트 처리기가 잘못된 값을 감지하면 일반적으로 다음 작업 중 하나를 수행합니다.

- 기본 값과 같이 올바른 것으로 알려진 값을 자동으로 제공합니다.

- 정보에 대한 서버 코드의 사용자를 다시 쿼리합니다.

- 및 <xref:System.Configuration.ApplicationSettingsBase.SettingChanging> <xref:System.ComponentModel.CancelEventArgs> 와 같이 관련 된 작업 이전에 발생 한 이벤트의 경우 인수를 사용 하 여 작업을 취소 합니다. <xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>

이벤트를 처리하는 방법에 대한 자세한 내용은 [이벤트 처리기 개요](../event-handlers-overview-windows-forms.md)를 참조하세요.

다음 절차에서는 <xref:System.Configuration.ApplicationSettingsBase.SettingChanging> <xref:System.Configuration.ApplicationSettingsBase.SettingsSaving> 또는 이벤트를 사용 하 여 유효한 생년월일을 테스트 하는 방법을 보여 줍니다. 프로시저는 애플리케이션 설정을 이미 만들었다는 가정 하에서 작성되었습니다. 이 예제에서는 `DateOfBirth`라는 설정에 대한 범위 검사를 수행합니다. 설정을 [만드는 방법에 대 한 자세한 내용은 방법: 응용 프로그램 설정을](how-to-create-application-settings.md)만듭니다.

### <a name="to-obtain-the-application-settings-object"></a>애플리케이션 설정 개체를 가져오려면

- 다음 글머리 기호 항목 중 하나를 완료하여 애플리케이션 설정 개체(래퍼 인스턴스)에 대한 참조를 가져옵니다.

  - **속성 편집기**에서 Visual Studio 응용 프로그램 설정 대화 상자를 사용하여 설정을 만든 경우 다음 식을 통해 언어에 대해 생성된 기본 설정 개체를 검색할 수 있습니다.

    ```csharp
    Configuration.Settings.Default
    ```

    ```vb
    MySettings.Default
    ```

    -또는-

  - 사용자가 Visual Basic 개발자이며 프로젝트 디자이너를 사용하여 애플리케이션 설정을 만든 경우 [My.Settings 개체](../../../visual-basic/language-reference/objects/my-settings-object.md)를 사용하여 설정을 검색할 수 있습니다.

    -또는-

  - 에서 <xref:System.Configuration.ApplicationSettingsBase> 직접 파생 시켜 설정을 만든 경우 클래스를 수동으로 인스턴스화해야 합니다.

    ```csharp
    MyCustomSettings settings = new MyCustomSettings();
    ```

    ```vb
    Dim Settings as New MyCustomSettings()
    ```

다음 절차는 이 절차에서 마지막 글머리 기호 항목을 완료하여 애플리케이션 설정 개체를 가져왔다는 가정 하에서 작성되었습니다.

### <a name="to-validate-application-settings-when-a-setting-is-changing"></a>설정이 변경될 때 애플리케이션 설정 유효성을 검사하려면

1. 폼 이나 컨트롤의 C# `Load` 이벤트에서 개발자 인 경우 <xref:System.Configuration.ApplicationSettingsBase.SettingChanging> 이벤트에 대 한 이벤트 처리기를 추가 합니다.

    -또는-

    사용자가 Visual Basic 개발자인 경우 `WithEvents` 키워드를 사용하여 `Settings` 변수를 선언해야 합니다.

    ```csharp
    public void Form1_Load(Object sender, EventArgs e)
    {
        settings.SettingChanging += new SettingChangingEventHandler(MyCustomSettings_SettingChanging);
    }
    ```

    ```vb
    Public Sub Form1_Load(sender as Object, e as EventArgs)
        AddHandler settings.SettingChanging, AddressOf MyCustomSettings_SettingChanging
    End Sub
    ```

2. 이벤트 처리기를 정의하고 내부에 코드를 작성하여 생년월일에 대한 범위 검사를 수행합니다.

    ```csharp
    private void MyCustomSettings_SettingChanging(Object sender, SettingChangingEventArgs e)
    {
        if (e.SettingName.Equals("DateOfBirth"))
        {
            var newDate = (DateTime)e.NewValue;
            if (newDate > DateTime.Now)
            {
                e.Cancel = true;
                // Inform the user.
            }
        }
    }
    ```

    ```vb
    Private Sub MyCustomSettings_SettingChanging(sender as Object, e as SettingChangingEventArgs) Handles Settings.SettingChanging
        If (e.SettingName.Equals("DateOfBirth")) Then
            Dim NewDate as Date = CType(e.NewValue, Date)
            If (NewDate > Date.Now) Then
                e.Cancel = True
                ' Inform the user.
            End If
        End If
    End Sub
    ```

### <a name="to-validate-application-settings-when-a-save-occurs"></a>저장이 발생할 때 애플리케이션 설정의 유효성을 검사하려면

1. 양식이 나 컨트롤 `Load` 의 이벤트에서 이벤트 <xref:System.Configuration.ApplicationSettingsBase.SettingsSaving> 에 대 한 이벤트 처리기를 추가 합니다.

    ```csharp
    public void Form1_Load(Object sender, EventArgs e)
    {
        settings.SettingsSaving += new SettingsSavingEventHandler(MyCustomSettings_SettingsSaving);
    }
    ```

    ```vb
    Public Sub Form1_Load(Sender as Object, e as EventArgs)
        AddHandler settings.SettingsSaving, AddressOf MyCustomSettings_SettingsSaving
    End Sub
    ```

2. 이벤트 처리기를 정의하고 내부에 코드를 작성하여 생년월일에 대한 범위 검사를 수행합니다.

    ```csharp
    private void MyCustomSettings_SettingsSaving(Object sender, SettingsSavingEventArgs e)
    {
        if (this["DateOfBirth"] > Date.Now) {
            e.Cancel = true;
        }
    }
    ```

    ```vb
    Private Sub MyCustomSettings_SettingsSaving(Sender as Object, e as SettingsSavingEventArgs)
        If (Me["DateOfBirth"] > Date.Now) Then
            e.Cancel = True
        End If
    End Sub
    ```

## <a name="see-also"></a>참고자료

- [Windows Forms에서 이벤트 처리기 만들기](../creating-event-handlers-in-windows-forms.md)
- [방법: 응용 프로그램 설정 만들기](how-to-create-application-settings.md)
