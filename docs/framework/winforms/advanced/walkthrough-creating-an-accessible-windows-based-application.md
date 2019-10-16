---
title: '연습: 내게 필요한 옵션이 지원되는 Windows 기반 애플리케이션 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- accessibility [Windows Forms], Windows applications
- Windows applications [Windows Forms], accessibility
- applications [Windows Forms], accessibility
dev_langs:
- csharp
- vb
ms.assetid: 654c7f2f-1586-480b-9f12-9d9b8f5cc32b
ms.openlocfilehash: b8f0c7c4584505d382e78aca68e2e99c9fa7748f
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834623"
---
# <a name="walkthrough-creating-an-accessible-windows-based-application"></a>연습: 내게 필요한 옵션이 지원되는 Windows 기반 애플리케이션 만들기

액세스할 수 있는 애플리케이션을 만드는 것은 비즈니스에 중요한 영향을 줍니다. 많은 정부 기관에는 소프트웨어 구매와 관련된 접근성 규정이 있습니다. Certified for Windows 로고에는 접근성 요구 사항이 포함됩니다. 미국에만 3천만 명이 거주하는 것으로 추정되는 잠재 고객 중 많은 사람이 소프트웨어의 내게 필요한 옵션 기능에 따른 영향을 받습니다.

이 연습에서는 Certified for Windows 로고를 위한 5가지 접근성 요구 사항을 다룹니다. 이러한 요구 사항에 따라 액세스할 수 있는 애플리케이션은 다음을 수행합니다.

- 제어판 크기, 색, 글꼴 및 입력 설정을 지원합니다. 사용자가 제어판 설정을 변경하면 메뉴 모음, 제목 표시줄, 테두리 및 상태 표시줄의 크기가 자동으로 모두 조정됩니다. 이 애플리케이션에서 컨트롤 또는 코드를 추가로 변경할 필요가 없습니다.

- 고대비 모드를 지원합니다.

- 모든 기능에 대한 문서화된 키보드 액세스를 제공합니다.

- 키보드 포커스의 위치를 시각적으로 및 프로그래밍 방식으로 노출합니다.

- 중요한 정보를 소리로만 전달하지 마세요.

자세한 내용은 [내게 필요한 옵션을 제공하는 애플리케이션 설계를 위한 리소스](/visualstudio/ide/reference/resources-for-designing-accessible-applications)를 참조하세요.

다양한 자판 배열을 지원하는 방법에 대한 자세한 내용은 [지역화 대비 애플리케이션 개발을 위한 최선의 구현 방법](../../../standard/globalization-localization/best-practices-for-developing-world-ready-apps.md)을 참조하세요.

## <a name="creating-the-project"></a>프로젝트 만들기

이 연습에서는 피자 주문을 받는 애플리케이션용 사용자 인터페이스를 만듭니다. 고객 이름을 나타내는 <xref:System.Windows.Forms.TextBox>, 피자 크기를 선택하기 위한 <xref:System.Windows.Forms.RadioButton> 그룹, 토핑을 선택하기 위한 <xref:System.Windows.Forms.CheckedListBox>, Order 및 Cancel 레이블이 붙은 단추 컨트롤 2개 및 Exit 명령이 포함된 메뉴로 구성됩니다.

사용자가 고객 이름, 피자 크기 및 원하는 토핑을 입력합니다. 사용자가 Order 단추를 클릭하면 주문 요약과 비용이 메시지 상자에 표시되며 컨트롤이 선택 취소되고 다음 주문을 준비합니다. 사용자가 Cancel 단추를 클릭하면 컨트롤이 선택 취소되고 다음 주문을 준비합니다. 사용자가 Exit 메뉴 항목을 클릭하면 프로그램이 닫힙니다.

이 연습은 소매 주문 시스템의 코드가 아니라 사용자 인터페이스의 접근성을 강조합니다. 이 연습에서는 단추, 라디오 단추, 텍스트 상자 및 레이블을 포함하여 자주 사용하는 여러 컨트롤의 접근성 기능을 보여 줍니다.

#### <a name="to-begin-making-the-application"></a>애플리케이션 만들기를 시작하려면

- Visual Basic 또는 시각적 개체 C#에서 새 Windows 응용 프로그램을 만듭니다. 프로젝트 이름을 **PizzaOrder**로 지정합니다. 자세한 내용은 [새 솔루션 및 프로젝트 만들기](/visualstudio/ide/creating-solutions-and-projects)를 참조 하세요.

## <a name="adding-the-controls-to-the-form"></a>폼에 컨트롤 추가

폼에 컨트롤을 추가하는 경우 액세스할 수 있는 애플리케이션을 만들기 위한 다음 지침을 고려하세요.

- <xref:System.Windows.Forms.Control.AccessibleDescription%2A> 및 <xref:System.Windows.Forms.Control.AccessibleName%2A> 속성을 설정합니다. 이 예제에서는 <xref:System.Windows.Forms.Control.AccessibleRole%2A>에 대한 기본 설정만으로도 충분합니다. 내게 필요한 옵션 속성에 대한 자세한 내용은 [Windows Form의 컨트롤에 내게 필요한 옵션 정보 제공](../controls/providing-accessibility-information-for-controls-on-a-windows-form.md)을 참조하세요.

- 글꼴 크기를 10포인트 이상으로 설정합니다.

  > [!NOTE]
  > 시작할 때 폼의 글꼴 크기를 10으로 설정하면 이후에 폼에 추가된 모든 컨트롤도 글꼴 크기가 10입니다.

- TextBox 컨트롤을 설명하는 Label 컨트롤은 탭 순서에서 TextBox 컨트롤 바로 앞에 와야 합니다.

- 사용자가 탐색할 수 있는 모든 컨트롤의 <xref:System.Windows.Forms.Control.Text%2A> 속성에 "&" 문자를 사용 하 여 액세스 키를 추가 합니다.

- 사용자가 탐색할 수 있는 컨트롤 앞에 나오는 레이블의 <xref:System.Windows.Forms.Control.Text%2A> 속성에 "&" 문자를 사용 하 여 액세스 키를 추가 합니다. 사용자가 액세스 키를 누를 때 포커스가 탭 순서의 다음 컨트롤로 설정되도록 레이블의 <xref:System.Windows.Forms.Label.UseMnemonic%2A> 속성을 `true`로 설정합니다.

- 모든 메뉴 항목에 액세스 키를 추가합니다.

#### <a name="to-make-your-windows-application-accessible"></a>Windows 애플리케이션을 액세스할 수 있게 하려면

- 폼에 컨트롤을 추가하고 아래에 설명된 대로 속성을 설정합니다. 폼에 컨트롤을 정렬하는 방법에 대한 모델은 표 끝에 있는 그림을 참조하세요.

   |Object|속성|값|
   |------------|--------------|-----------|
   |Form1|AccessibleDescription|Order form|
   ||AccessibleName|Order form|
   ||글꼴 크기|10|
   ||텍스트|Pizza Order Form|
   |PictureBox|이름|로고|
   ||AccessibleDescription|A slice of pizza|
   ||AccessibleName|Company logo|
   ||이미지|임의 아이콘 또는 비트맵|
   |레이블|이름|companyLabel|
   ||텍스트|Good Pizza|
   ||TabIndex|1|
   ||AccessibleDescription|Company name|
   ||AccessibleName|Company name|
   ||Backcolor|파랑|
   ||Forecolor|노랑|
   ||글꼴 크기|18|
   |레이블|이름|customerLabel|
   ||텍스트|이름(&N)|
   ||TabIndex|2|
   ||AccessibleDescription|Customer name label|
   ||AccessibleName|Customer name label|
   ||UseMnemonic|True|
   |TextBox|이름|customerName|
   ||텍스트|(없음)|
   ||TabIndex|3|
   ||AccessibleDescription|Customer name|
   ||AccessibleName|Customer name|
   |GroupBox|이름|sizeOptions|
   ||AccessibleDescription|Pizza size options|
   ||AccessibleName|Pizza size options|
   ||텍스트|Pizza size|
   ||TabIndex|4|
   |RadioButton|이름|smallPizza|
   ||텍스트|&Small $6.00|
   ||선택한 상태|True|
   ||TabIndex|0|
   ||AccessibleDescription|Small pizza|
   ||AccessibleName|Small pizza|
   |RadioButton|이름|largePizza|
   ||텍스트|&Large $10.00|
   ||TabIndex|1|
   ||AccessibleDescription|Large pizza|
   ||AccessibleName|Large pizza|
   |레이블|이름|toppingsLabel|
   ||텍스트|&Toppings ($0.75 each)|
   ||TabIndex|5|
   ||AccessibleDescription|Toppings label|
   ||AccessibleName|Toppings label|
   ||UseMnemonic|True|
   |CheckedListBox|이름|toppings|
   ||TabIndex|6|
   ||AccessibleDescription|Available toppings|
   ||AccessibleName|Available toppings|
   ||항목|Pepperoni, Sausage, Mushrooms|
   |단추|이름|순서|
   ||텍스트|순서(&O)|
   ||TabIndex|7|
   ||AccessibleDescription|Total the order|
   ||AccessibleName|Total order|
   |단추|이름|cancel|
   ||텍스트|취소(&C)|
   ||TabIndex|8|
   ||AccessibleDescription|Cancel the order|
   ||AccessibleName|Cancel order|
   |MainMenu|이름|theMainMenu|
   |MenuItem|이름|fileCommands|
   ||텍스트|파일(&F)|
   |MenuItem|이름|exitApp|
   ||텍스트|끝내기(&X)|

   폼은 다음 이미지와 유사 하 게 표시 됩니다.

   ![이름 텍스트 상자와 크기 및 토 핑 선택이 있는 피자 주문 폼입니다.](./media/walkthrough-creating-an-accessible-windows-based-application/visual-basic-pizza-order-form.gif)

## <a name="supporting-high-contrast-mode"></a>고대비 모드 지원

고대비 모드는 시각 장애가 있는 사용자에게 도움이 되는 대비 색과 글꼴 크기를 사용하여 가독성을 향상시키는 Windows 시스템 설정입니다. <xref:System.Windows.Forms.SystemInformation.HighContrast%2A> 속성은 고대비 모드가 설정 되어 있는지 여부를 확인 하기 위해 제공 됩니다.

SystemInformation.HighContrast가 `true`이면 애플리케이션에서 다음을 수행해야 합니다.

- 시스템 색 구성표를 사용하여 모든 사용자 인터페이스 요소 표시

- 색을 통해 전달되는 모든 정보를 시각 신호나 소리로 전달합니다. 예를 들어 빨강 글꼴을 사용하여 특정 목록 항목이 강조 표시된 경우 해당 글꼴에 굵게 표시를 추가하여 항목이 강조 표시되었다는 색이 아닌 신호를 사용자에게 제공할 수도 있습니다.

- 텍스트 뒤에 있는 모든 이미지 또는 패턴 생략

애플리케이션이 시작되고 시스템 이벤트 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged>에 응답할 때 애플리케이션에서 <xref:System.Windows.Forms.SystemInformation.HighContrast%2A>의 설정을 확인해야 합니다. <xref:System.Windows.Forms.SystemInformation.HighContrast%2A>의 값이 변경되면 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged> 이벤트가 발생합니다.

이 애플리케이션에서 색 시스템 설정을 사용하지 않는 요소는 `lblCompanyName`뿐입니다. <xref:System.Drawing.SystemColors> 클래스는 레이블의 색 설정을 사용자가 선택한 시스템 색으로 변경 하는 데 사용 됩니다.

#### <a name="to-enable-high-contrast-mode-in-an-effective-way"></a>효과적인 방법으로 고대비 모드를 사용하도록 설정하려면

1. 레이블의 색을 시스템 색으로 설정하는 메서드를 만듭니다.

    ```vb
    Private Sub SetColorScheme()
        If SystemInformation.HighContrast Then
            companyLabel.BackColor = SystemColors.Window
            companyLabel.ForeColor = SystemColors.WindowText
        Else
            companyLabel.BackColor = Color.Blue
            companyLabel.ForeColor = Color.Yellow
        End If
    End Sub
    ```

    ```csharp
    private void SetColorScheme()
    {
        if (SystemInformation.HighContrast)
        {
            companyLabel.BackColor = SystemColors.Window;
            companyLabel.ForeColor = SystemColors.WindowText;
        }
        else
        {
            companyLabel.BackColor = Color.Blue;
            companyLabel.ForeColor = Color.Yellow;
        }
    }
    ```

2. 양식 생성자(Visual Basic의 `Public Sub New()`, Visual C#의 `public Form1()`)에서 `SetColorScheme` 프로시저를 호출합니다. Visual Basic에서 생성자에 액세스하려면 **Windows Form 디자이너에서 생성한 코드** 레이블이 지정된 영역을 확장해야 합니다.

    ```vb
    Public Sub New()
        MyBase.New()
        InitializeComponent()
        SetColorScheme()
    End Sub
    ```

    ```csharp
    public Form1()
    {
        InitializeComponent();
        SetColorScheme();
    }
    ```

3. 적절한 서명을 사용하여 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged> 이벤트에 응답하는 이벤트 프로시저를 만듭니다.

    ```vb
    Protected Sub UserPreferenceChanged(sender As Object, _
    e As Microsoft.Win32.UserPreferenceChangedEventArgs)
        SetColorScheme()
    End Sub
    ```

    ```csharp
    public void UserPreferenceChanged(object sender,
    Microsoft.Win32.UserPreferenceChangedEventArgs e)
    {
        SetColorScheme();
    }
    ```

4. 양식 생성자에서 `InitializeComponents` 호출 뒤에 이벤트 프로시저를 시스템 이벤트에 연결하는 코드를 추가합니다. 이 메서드는 `SetColorScheme` 프로시저를 호출합니다.

    ```vb
    Public Sub New()
        MyBase.New()
        InitializeComponent()
        SetColorScheme()
        AddHandler Microsoft.Win32.SystemEvents.UserPreferenceChanged, _
           AddressOf Me.UserPreferenceChanged
    End Sub
    ```

    ```csharp
    public Form1()
    {
        InitializeComponent();
        SetColorScheme();
        Microsoft.Win32.SystemEvents.UserPreferenceChanged
           += new Microsoft.Win32.UserPreferenceChangedEventHandler(
           this.UserPreferenceChanged);
    }
    ```

5. 폼 <xref:System.Windows.Forms.Control.Dispose%2A> 메서드에서 기본 클래스의 <xref:System.Windows.Forms.Control.Dispose%2A> 메서드 호출 앞에 코드를 추가하여 애플리케이션이 닫힐 때 이벤트를 해제합니다. Visual Basic에서 <xref:System.Windows.Forms.Control.Dispose%2A> 메서드에 액세스하려면 Windows Form 디자이너에서 생성한 코드 레이블이 지정된 영역을 확장해야 합니다.

    > [!NOTE]
    > 시스템 이벤트 코드는 주 애플리케이션과 별개인 스레드를 실행합니다. 이벤트를 해제하지 않으면 이벤트에 연결하는 코드가 프로그램이 닫힌 후에도 실행됩니다.

    ```vb
    Protected Overloads Overrides Sub Dispose(ByVal disposing As Boolean)
        If disposing AndAlso components IsNot Nothing Then
            components.Dispose()
        End If
        RemoveHandler Microsoft.Win32.SystemEvents.UserPreferenceChanged, _
           AddressOf Me.UserPreferenceChanged
        MyBase.Dispose(disposing)
    End Sub
    ```

    ```csharp
    protected override void Dispose(bool disposing)
    {
        if(disposing && components != null)
        {
            components.Dispose();
        }
        Microsoft.Win32.SystemEvents.UserPreferenceChanged
           -= new Microsoft.Win32.UserPreferenceChangedEventHandler(
           this.UserPreferenceChanged);
        base.Dispose( disposing );
    }
    ```

6. F5 키를 눌러 애플리케이션을 실행합니다.

## <a name="conveying-important-information-by-means-other-than-sound"></a>소리가 아닌 다른 수단으로 중요한 정보 전달

이 애플리케이션에서는 정보가 소리로만 전달되지 않습니다. 애플리케이션에서 소리를 사용하는 경우 다른 수단을 통해서도 정보를 제공해야 합니다.

#### <a name="to-supply-information-by-some-other-means-than-sound"></a>소리가 아닌 다른 수단으로 정보를 제공하려면

1. Windows API 함수 FlashWindow를 사용하여 제목 표시줄을 깜박이게 만듭니다. Windows API 함수를 호출 하는 방법에 대 한 예제 [를 보려면 연습: Windows Api](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)를 호출 합니다.

    > [!NOTE]
    > 사용자가 Windows 소리 탐지 서비스를 사용하도록 설정했을 수도 있습니다. 이 서비스는 컴퓨터의 기본 제공 스피커를 통해 시스템 소리가 재생될 때 창도 깜박이게 합니다.

2. 사용자가 응답할 수 있도록 비모달 창에 중요한 정보를 표시합니다.

3. 키보드 포커스를 획득하는 메시지 상자를 표시합니다. 사용자가 입력 중일 때는 이 메서드를 사용하지 마세요.

4. 작업 표시줄의 상태 알림 영역에 상태 표시기를 표시합니다. 자세한 내용은 [Windows Forms NotifyIcon 구성 요소를 사용하여 작업 표시줄에 애플리케이션 아이콘 추가](../controls/app-icons-to-the-taskbar-with-wf-notifyicon.md)를 참조하세요.

## <a name="testing-the-application"></a>응용 프로그램 테스트

애플리케이션을 배포하기 전에 구현한 접근성 기능을 테스트해야 합니다.

#### <a name="to-test-accessibility-features"></a>접근성 기능을 테스트하려면

1. 키보드 액세스를 테스트하려면 마우스를 분리하고 키보드만 사용하여 각 기능에 대한 사용자 인터페이스를 탐색합니다. 키보드만 사용하여 모든 작업을 수행할 수 있는지 확인합니다.

2. 고대비 지원을 테스트하려면 제어판의 내게 필요한 옵션 아이콘을 선택합니다. 표시 탭을 클릭하고 고대비 사용 확인란을 선택합니다. 모든 사용자 인터페이스 요소를 탐색하여 색 및 글꼴 변경 내용이 반영되었는지 확인합니다. 또한 텍스트 뒤에 그려진 이미지 또는 패턴이 생략되었는지 확인합니다.

    > [!NOTE]
    > Windows NT 4에서는 제어판에 내게 필요한 옵션 아이콘이 없습니다. 따라서 SystemInformation.HighContrast 설정을 변경하는 이 절차는 Windows NT 4에서 작동하지 않습니다.

3. 다른 도구는 애플리케이션의 접근성 테스트에 바로 사용할 수 있습니다.

4. 키보드 포커스 노출을 테스트하려면 돋보기를 실행합니다. 돋보기를 열려면 **시작** 메뉴를 클릭하고**프로그램**, **보조프로그램**, **내게 필요한 옵션**을 차례로 가리킨 다음 **돋보기**를 클릭합니다. 키보드 탭 이동 및 마우스를 사용하여 사용자 인터페이스를 탐색합니다. **돋보기**에서 모든 탐색이 제대로 추적되는지 확인합니다.

5. 화면 요소 노출을 테스트하려면 조사를 실행하고 마우스와 Tab 키를 둘 다 사용하여 각 요소에 접근합니다. 조사 창의 이름, 상태, 역할, 위치 및 값 필드에 제공된 정보가 UI의 각 개체에 대해 사용자에게 의미 있는 정보인지 확인합니다.
