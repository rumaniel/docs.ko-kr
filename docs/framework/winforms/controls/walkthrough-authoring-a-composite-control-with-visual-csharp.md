---
title: '연습: Visual C#에서 복합 컨트롤 제작'
ms.date: 03/30/2017
dev_langs:
- CSharp
helpviewer_keywords:
- custom controls [C#]
- user controls [Windows Forms], creating with Visual C#
- UserControl class [Windows Forms], walkthroughs
- user controls [C#]
- custom controls [Windows Forms], creating
ms.assetid: f88481a8-c746-4a36-9479-374ce5f2e91f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d1af6c0e013f82569eed8d085df0249f4fb991bb
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015687"
---
# <a name="walkthrough-author-a-composite-control-with-c"></a>연습: C를 사용 하 여 복합 컨트롤 작성\#

복합 컨트롤은 사용자 지정 그래픽 인터페이스를 만들고 재사용할 수 있는 방법을 제공합니다. 복합 컨트롤은 기본적으로 시각적 표현이 있는 구성 요소입니다. 따라서 사용자 입력의 유효성을 검사하고 표시 속성을 수정하거나 작성자가 요구하는 다른 작업을 수행하여 기능을 확장할 수 있는 하나 이상의 Windows Forms 컨트롤, 구성 요소 또는 코드 블록으로 구성할 수 있습니다. 복합 컨트롤은 다른 컨트롤과 동일한 방식으로 Windows Forms에 배치할 수 있습니다. 이 연습의 첫 번째 부분에서는 `ctlClock`이라는 간단한 복합 컨트롤을 만듭니다. 두 번째 부분에서는 상속을 통해 `ctlClock`의 기능을 확장합니다.

## <a name="create-the-project"></a>프로젝트 만들기

새 프로젝트를 만들 때는 이에 대한 이름을 지정하여 루트 네임스페이스, 어셈블리 이름 및 프로젝트 이름을 설정하고 기본 구성 요소가 올바른 네임스페이스에 있는지 확인합니다.

### <a name="to-create-the-ctlclocklib-control-library-and-the-ctlclock-control"></a>ctlClockLib 컨트롤 라이브러리 및 ctlClock 컨트롤을 만들려면

1. Visual Studio에서 새 **Windows Forms 컨트롤 라이브러리** 프로젝트를 만들고 이름을 **ctlClockLib**로 표시 합니다.

     프로젝트 이름, `ctlClockLib`는 기본적으로 루트 네임스페이스에도 할당됩니다. 루트 네임스페이스는 어셈블리에서 구성 요소의 이름을 정규화하는 데 사용됩니다. 예를 들어 두 어셈블리에서 `ctlClock`이라는 구성 요소를 제공하면 `ctlClockLib.ctlClock.`을 사용하여 `ctlClock` 구성 요소를 지정할 수 있습니다.

2. **솔루션 탐색기**에서 **UserControl1.cs**을 마우스 오른쪽 단추로 클릭 한 다음 **이름 바꾸기**를 클릭 합니다. 파일 이름을 `ctlClock.cs`로 변경합니다. 코드 요소 “UserControl1”에 대한 모든 참조 이름을 변경할지 묻는 메시지가 표시되면 **예** 단추를 클릭합니다.

    > [!NOTE]
    > 기본적으로 복합 컨트롤은 시스템에서 제공 하 <xref:System.Windows.Forms.UserControl> 는 클래스에서 상속 됩니다. 클래스 <xref:System.Windows.Forms.UserControl> 는 모든 복합 컨트롤에 필요한 기능을 제공 하 고 표준 메서드 및 속성을 구현 합니다.

3. **파일** 메뉴에서 **모두 저장**을 클릭하여 프로젝트를 저장합니다.

## <a name="add-windows-controls-and-components-to-the-composite-control"></a>복합 컨트롤에 Windows 컨트롤 및 구성 요소 추가

시각적 인터페이스는 복합 컨트롤의 필수적인 부분입니다. 이 시각적 인터페이스는 하나 이상의 Windows 컨트롤을 디자이너 화면에 추가하여 구현합니다. 다음 데모에서는 Windows 컨트롤을 복합 컨트롤에 통합하고 기능을 구현하는 코드를 작성합니다.

### <a name="to-add-a-label-and-a-timer-to-your-composite-control"></a>복합 컨트롤에 레이블 및 타이머를 추가하려면

1. **솔루션 탐색기**에서 **ctlClock.cs**을 마우스 오른쪽 단추로 클릭 한 다음 **뷰 디자이너**를 클릭 합니다.

2. **도구 상자**에서 **공용 컨트롤** 노드를 확장한 후 **레이블**을 두 번 클릭합니다.

     <xref:System.Windows.Forms.Label> 이라는`label1` 컨트롤은 디자이너 화면에서 컨트롤에 추가 됩니다.

3. 디자이너에서 **label1**을 클릭합니다. 속성 창에서 다음 속성을 설정합니다.

    |속성|다음으로 변경|
    |--------------|---------------|
    |**이름**|`lblDisplay`|
    |**텍스트**|`(blank space)`|
    |**TextAlign**|`MiddleCenter`|
    |**Font.Size**|`14`|

4. **도구 상자**에서 **구성 요소** 노드를 확장한 후 **타이머**를 두 번 클릭합니다.

     는 <xref:System.Windows.Forms.Timer> 구성 요소 이므로 런타임에 시각적으로 표시 되지 않습니다. 따라서 디자이너 화면에 컨트롤과 함께 나타나지 않으며 **구성 요소 디자이너**(디자이너 화면 맨 아래 트레이)에 나타납니다.

5. **구성 요소 디자이너**에서 **timer1**을 클릭 하 고 속성을로 <xref:System.Windows.Forms.Timer.Interval%2A> 설정 하 `1000` 고 <xref:System.Windows.Forms.Timer.Enabled%2A> 속성을로 `true`설정 합니다.

     속성 <xref:System.Windows.Forms.Timer.Interval%2A> 은 <xref:System.Windows.Forms.Timer> 구성 요소가 틱 하는 빈도를 제어 합니다. `timer1`이 틱할 때마다 `timer1_Tick` 이벤트에 있는 코드를 실행합니다. 간격은 틱 사이에 시간(밀리초)을 나타냅니다.

6. **구성 요소 디자이너**에서 **timer1**을 두 번 클릭하여 `ctlClock`에 대한 `timer1_Tick` 이벤트로 이동합니다.

7. 다음 코드 샘플과 비슷하도록 코드를 수정합니다. `private`에서 `protected`로 액세스 한정자를 변경해야 합니다.

    ```csharp
    protected void timer1_Tick(object sender, System.EventArgs e)
    {
        // Causes the label to display the current time.
        lblDisplay.Text = DateTime.Now.ToLongTimeString();
    }
    ```

     이 코드를 통해 `lblDisplay`에 현재 시간이 표시됩니다. `timer1`의 간격은 `1000`으로 설정되었으므로 이 이벤트는 천 밀리초마다 발생하므로 현재 시간이 1초마다 업데이트됩니다.

8. 메서드를 `virtual` 키워드로 재정의 가능하도록 수정합니다. 자세한 내용은 아래의 “사용자 컨트롤에서 상속” 섹션을 참조하세요.

    ```csharp
    protected virtual void timer1_Tick(object sender, System.EventArgs e)
    ```

9. **파일** 메뉴에서 **모두 저장**을 클릭하여 프로젝트를 저장합니다.

## <a name="add-properties-to-the-composite-control"></a>복합 컨트롤에 속성 추가

이제 클록 컨트롤이 <xref:System.Windows.Forms.Label> 컨트롤과 <xref:System.Windows.Forms.Timer> 구성 요소를 캡슐화 하며 각각 고유한 속성 집합이 있습니다. 이러한 컨트롤의 개별 속성은 이후 컨트롤 사용자가 액세스할 수 없지만 적절한 코드 블록을 작성하여 사용자 지정 속성을 만들고 노출할 수 있습니다. 다음 프로시저에서 사용자가 배경 및 텍스트 색을 변경할 수 있도록 컨트롤에 속성을 추가합니다.

### <a name="to-add-a-property-to-your-composite-control"></a>복합 컨트롤에 속성을 추가하려면

1. **솔루션 탐색기**에서 **ctlClock.cs**을 마우스 오른쪽 단추로 클릭 한 다음 **코드 보기**를 클릭 합니다.

     컨트롤에 대한 **코드 편집기**가 열립니다.

2. `public partial class ctlClock` 문을 찾습니다. 여는 중괄호 (`{)` 아래에 다음 코드를 입력합니다.

    ```csharp
    private Color colFColor;
    private Color colBColor;
    ```

     이러한 문은 작성하려는 속성에 대한 값을 저장하는 데 사용할 private 변수를 만듭니다.

3. 2 단계에서 변수 선언 아래에 다음 코드를 입력 하거나 붙여 넣습니다.

    ```csharp
    // Declares the name and type of the property.
    public Color ClockBackColor
    {
        // Retrieves the value of the private variable colBColor.
        get
        {
            return colBColor;
        }
        // Stores the selected value in the private variable colBColor, and
        // updates the background color of the label control lblDisplay.
        set
        {
            colBColor = value;
            lblDisplay.BackColor = colBColor;
        }
    }
    // Provides a similar set of instructions for the foreground color.
    public Color ClockForeColor
    {
        get
        {
            return colFColor;
        }
        set
        {
            colFColor = value;
            lblDisplay.ForeColor = colFColor;
        }
    }
    ```

     위의 코드는 `ClockForeColor` 및 `ClockBackColor`라는 두 사용자 지정 속성을 만들며 이 속성은 이 컨트롤의 후속 사용자에게 제공됩니다. `get` 및 `set` 문은 속성 값의 저장 및 검색과 속성에 맞는 기능을 구현하는 코드를 위해 제공됩니다.

4. **파일** 메뉴에서 **모두 저장**을 클릭하여 프로젝트를 저장합니다.

## <a name="test-the-control"></a>컨트롤 테스트

컨트롤은 독립 실행형 애플리케이션이 아니며 컨테이너에서 호스팅해야 합니다. 컨트롤의 런타임 동작을 테스트하고 **UserControl 테스트 컨테이너**로 해당 속성을 실행합니다. 자세한 내용은 [방법: UserControl](how-to-test-the-run-time-behavior-of-a-usercontrol.md)의 런타임 동작을 테스트 합니다.

### <a name="to-test-your-control"></a>컨트롤을 테스트하려면

1. **F5** 키를 눌러 프로젝트를 빌드하고 **UserControl 테스트 컨테이너**에서 컨트롤을 실행 합니다.

2. 테스트 컨테이너의 속성 눈금에서 `ClockBackColor` 속성을 찾은 후 해당 속성을 선택하여 색상표를 표시합니다.

3. 클릭하여 색을 선택합니다.

   컨트롤의 배경색이 선택한 색으로 바뀝니다.

4. 유사한 이벤트 시퀀스를 사용하여 `ClockForeColor` 속성이 예상대로 작동하는지 확인합니다.

   이 섹션과 이전 섹션에서는 구성 요소 및 Windows 컨트롤을 코드와 결합하고 패키징하여 복합 컨트롤 형태로 사용자 지정 기능을 제공하는 방법을 살펴보았습니다. 복합 컨트롤에 속성을 노출하고 완료한 후에는 컨트롤을 테스트하는 방법도 알아보았습니다. 다음 섹션에서는 `ctlClock`을 기본으로 사용하여 상속된 복합 컨트롤을 생성하는 방법에 대해 알아봅니다.

## <a name="inherit-from-a-composite-control"></a>복합 컨트롤에서 상속

이전 섹션에서는 Windows 컨트롤, 구성 요소 및 코드를 재사용 가능한 복합 컨트롤에 결합하는 방법을 알아보았습니다. 이제 복합 컨트롤을 다른 컨트롤을 작성하기 위한 기본으로 활용할 수 있습니다. 기본 클래스에서 클래스를 파생시키는 과정을 *상속*이라고 합니다. 이 섹션에서는 `ctlAlarmClock`이라는 복합 컨트롤을 만듭니다. 이 컨트롤은 부모 컨트롤인 `ctlClock`에서 파생됩니다. 부모 메서드를 재정의하고 새 메서드 및 속성을 추가하여 `ctlClock`의 기능을 확장하는 방법을 알아보겠습니다.

상속된 컨트롤을 만드는 첫 번째 단계는 부모에서 파생시키는 것입니다. 이 작업은 속성, 메서드 및 부모 컨트롤의 그래픽 특성을 모두 포함하는 새 컨트롤을 만들지만 신규 또는 수정된 기능 추가를 위한 기본으로도 활용할 수 있습니다.

### <a name="to-create-the-inherited-control"></a>상속된 컨트롤을 만들려면

1. **솔루션 탐색기**에서 **ctlClockLib**을 마우스 오른쪽 단추로 클릭 하 고 **추가**를 가리킨 다음 **사용자 정의 컨트롤**을 클릭 합니다.

     **새 항목 추가** 대화 상자가 열립니다.

2. **상속된 사용자 정의 컨트롤** 템플릿을 선택합니다.

3. **이름** 상자에 `ctlAlarmClock.cs`를 입력한 다음 **추가**를 클릭합니다.

     **상속 선택** 대화 상자가 나타납니다.

4. **구성 요소 이름** 아래에서 **ctlClock**을 두 번 클릭합니다.

5. **솔루션 탐색기**에서 현재 프로젝트를 찾습니다.

    > [!NOTE]
    > **ctlAlarmClock.cs**라는 파일이 현재 프로젝트에 추가되었습니다.

### <a name="add-the-alarm-properties"></a>경보 속성 추가

속성은 복합 컨트롤에 추가된 것과 같은 방식으로 상속된 컨트롤에 추가됩니다. 이제 속성 선언 구문을 사용하여 컨트롤에 두 가지 속성, 즉 경보가 꺼지는 날짜와 시간 값을 저장하는 `AlarmTime`과 경보가 설정되는지 여부를 나타내는 `AlarmSet`을 추가합니다.

#### <a name="to-add-properties-to-your-composite-control"></a>복합 컨트롤에 속성을 추가하려면

1. **솔루션 탐색기**에서 **ctlAlarmClock**을 마우스 오른쪽 단추로 클릭 한 다음 **코드 보기**를 클릭 합니다.

2. `public class` 문을 찾습니다. 컨트롤은 `ctlClockLib.ctlClock`에서 상속됩니다. 여는 중괄호 (`{)` 문 아래에 다음 코드를 입력합니다.

    ```csharp
    private DateTime dteAlarmTime;
    private bool blnAlarmSet;
    // These properties will be declared as public to allow future
    // developers to access them.
    public DateTime AlarmTime
    {
        get
        {
            return dteAlarmTime;
        }
        set
        {
            dteAlarmTime = value;
        }
    }
    public bool AlarmSet
    {
        get
        {
            return blnAlarmSet;
        }
        set
        {
            blnAlarmSet = value;
        }
    }
    ```

### <a name="add-to-the-graphical-interface-of-the-control"></a>컨트롤의 그래픽 인터페이스에 추가

상속된 컨트롤에는 상속 원본 컨트롤과 동일한 시각적 인터페이스가 있습니다. 부모 컨트롤과 동일한 구성 요소 컨트롤을 소유하지만, 구체적으로 노출되지 않는 한, 구성 요소 컨트롤의 속성을 사용할 수 없습니다. 복합 컨트롤에 추가하는 것과 같은 방법으로 상속된 복합 컨트롤의 그래픽 인터페이스에 추가할 수 있습니다. 알람 시계의 시각적 인터페이스에 계속 추가하려면 경보가 울릴 때 깜박거리는 레이블 컨트롤을 추가합니다.

#### <a name="to-add-the-label-control"></a>레이블 컨트롤을 추가하려면

1. **솔루션 탐색기**에서 **ctlAlarmClock**을 마우스 오른쪽 단추로 클릭 한 다음 **뷰 디자이너**를 클릭 합니다.

     `ctlAlarmClock`에 대한 디자이너가 주 창에 열립니다.

2. 컨트롤의 표시 부분을 클릭하고 속성 창을 확인합니다.

    > [!NOTE]
    > 모든 속성이 표시되는 동안 흐리게 표시됩니다. 이것은 이러한 속성이 `lblDisplay`의 기본 속성이며 속성 창에서 수정하거나 액세스할 수 없음을 나타냅니다. 기본적으로 복합 컨트롤에 포함된 컨트롤은 `private`이며 해당 속성은 어떤 방법으로도 액세스할 수 없습니다.

    > [!NOTE]
    > 복합 컨트롤의 후속 사용자가 내부 컨트롤에 액세스할 수 있도록 하려면 이를 `public` 또는 `protected`로 선언합니다. 이렇게 하면 적절한 코드를 사용하여 복합 컨트롤 내에 포함된 컨트롤의 속성을 설정 및 수정할 수 있습니다.

3. 복합 컨트롤에 컨트롤을 추가 합니다. <xref:System.Windows.Forms.Label>

4. 마우스를 사용 하 여 <xref:System.Windows.Forms.Label> 컨트롤을 표시 상자 바로 아래로 끕니다. 속성 창에서 다음 속성을 설정합니다.

    |속성|설정|
    |--------------|-------------|
    |**이름**|`lblAlarm`|
    |**텍스트**|**Alarm!**|
    |**TextAlign**|`MiddleCenter`|
    |**Visible**|`false`|

### <a name="add-the-alarm-functionality"></a>알람 기능 추가

이전 프로시저에서는 복합 컨트롤에서 경보 기능을 설정하는 속성 및 컨트롤을 추가했습니다. 이 프로시저에서는 현재 시간을 경보 시간과 비교하여 같으면 깜박이는 코드를 추가합니다. `ctlClock`의 `timer1_Tick` 메소드를 재정의하고 코드를 더 추가하여 `ctlClock`의 모든 고유 기능을 유지하면서 `ctlAlarmClock`의 기능을 확장합니다.

#### <a name="to-override-the-timer1_tick-method-of-ctlclock"></a>ctlClock의 timer1_Tick 메서드를 재정의하려면

1. **코드 편집기**에서 `private bool blnAlarmSet;` 문을 찾습니다. 바로 아래에서 다음 문을 추가합니다.

    ```csharp
    private bool blnColorTicker;
    ```

2. **코드 편집기**에서 클래스 끝에 있는 닫는 중괄호 (`})`를 찾습니다. 중괄호 바로 앞에 다음 코드를 추가합니다.

    ```csharp
    protected override void timer1_Tick(object sender, System.EventArgs e)
    {
        // Calls the Timer1_Tick method of ctlClock.
        base.timer1_Tick(sender, e);
        // Checks to see if the alarm is set.
        if (AlarmSet == false)
            return;
        else
            // If the date, hour, and minute of the alarm time are the same as
            // the current time, flash an alarm.
        {
            if (AlarmTime.Date == DateTime.Now.Date && AlarmTime.Hour ==
                DateTime.Now.Hour && AlarmTime.Minute == DateTime.Now.Minute)
            {
                // Sets lblAlarmVisible to true, and changes the background color based on
                // the value of blnColorTicker. The background color of the label
                // will flash once per tick of the clock.
                lblAlarm.Visible = true;
                if (blnColorTicker == false)
                {
                    lblAlarm.BackColor = Color.Red;
                    blnColorTicker = true;
                }
                else
                {
                    lblAlarm.BackColor = Color.Blue;
                    blnColorTicker = false;
                }
            }
            else
            {
                // Once the alarm has sounded for a minute, the label is made
                // invisible again.
                lblAlarm.Visible = false;
            }
        }
    }
    ```

     이 코드를 추가하려면 여러 작업을 수행할 수 있습니다. `override` 문은 기본 컨트롤에서 상속된 메서드 대신, 이 메서드를 사용하도록 컨트롤에 지시합니다. 이 메서드가 호출되면 `base.timer1_Tick` 문을 호출하여 이를 재정의하는 메서드를 호출하여 원래 컨트롤에 통합된 모든 기능이 이 컨트롤에서 재현되도록 합니다. 그런 다음 경보 기능을 통합하는 추가 코드를 실행합니다. 경보가 발생하면 깜박이는 레이블 컨트롤이 나타납니다.

     알람 시계 컨트롤이 거의 완료되었습니다. 이제 해제하는 방법을 구현하는 것만 남았습니다. 이를 위해서는 `lblAlarm_Click` 메서드에 코드를 추가합니다.

#### <a name="to-implement-the-shutoff-method"></a>shutoff 메서드를 구현하려면

1. **솔루션 탐색기**에서 **ctlAlarmClock.cs**을 마우스 오른쪽 단추로 클릭 한 다음 **뷰 디자이너**를 클릭 합니다.

     디자이너가 열립니다.

2. 단추를 폼에 추가합니다. 단추의 속성을 다음과 같이 설정합니다.

    |속성|값|
    |--------------|-----------|
    |**이름**|`btnAlarmOff`|
    |**텍스트**|**경보 사용 안 함**|

3. 디자이너에서 **btnAlarmOff**를 두 번 클릭합니다.

     **코드 편집기**에 `private void btnAlarmOff_Click` 행이 열립니다.

4. 이 메서드를 다음 코드와 비슷하도록 수정합니다.

    ```csharp
    private void btnAlarmOff_Click(object sender, System.EventArgs e)
    {
        // Turns off the alarm.
        AlarmSet = false;
        // Hides the flashing label.
        lblAlarm.Visible = false;
    }
    ```

5. **파일** 메뉴에서 **모두 저장**을 클릭하여 프로젝트를 저장합니다.

### <a name="use-the-inherited-control-on-a-form"></a>폼에서 상속 된 컨트롤 사용

기본 클래스 컨트롤을 테스트 한 것과 같은 방법으로 상속 된 컨트롤을 `ctlClock`테스트할 수 있습니다. **F5** 키를 눌러 프로젝트를 빌드하고 **UserControl 테스트 컨테이너**에서 컨트롤을 실행 합니다. 자세한 내용은 [방법: UserControl](how-to-test-the-run-time-behavior-of-a-usercontrol.md)의 런타임 동작을 테스트 합니다.

사용할 컨트롤을 배치하려면 폼에서 컨트롤을 호스트해야 합니다. 표준 복합 컨트롤과 마찬가지로 상속된 복합 컨트롤은 독립 실행형으로 사용할 수 없으며 폼 또는 다른 컨테이너에서 호스트해야 합니다. `ctlAlarmClock`은 보다 심도 있는 기능을 포함하므로 테스트하려면 추가 코드가 필요합니다. 이 프로시저에서는 `ctlAlarmClock`의 기능을 테스트하는 간단한 프로그램을 작성합니다. `ctlAlarmClock`의 `AlarmTime` 속성을 설정하고 표시하는 코드를 작성하고 고유한 기능을 테스트합니다.

#### <a name="to-build-and-add-your-control-to-a-test-form"></a>컨트롤을 빌드하고 테스트 폼에 추가하려면

1. **솔루션 탐색기**에서 **ctlClockLib**을 마우스 오른쪽 단추로 클릭 한 다음 **빌드**를 클릭 합니다.

2. 새 **Windows 응용 프로그램** 프로젝트를 솔루션에 추가 하 고 이름을 **Test**로 만듭니다.

3. **솔루션 탐색기**에서 테스트 프로젝트에 대 한 **참조** 노드를 마우스 오른쪽 단추로 클릭 합니다. **참조 추가** 대화 상자를 표시하려면 **참조 추가**를 클릭합니다. **프로젝트**로 레이블이 지정된 탭을 클릭합니다. `ctlClockLib` 프로젝트가 **프로젝트 이름** 아래에 나열됩니다. 프로젝트를 두 번 클릭하여 테스트 프로젝트에 참조를 추가합니다.

4. **솔루션 탐색기**에서 **Test**를 마우스 오른쪽 단추로 클릭 한 다음 **빌드**를 클릭 합니다.

5. **도구 상자**에서 **ctlClockLib 구성 요소** 노드를 확장합니다.

6. **ctlAlarmClock**을 두 번 클릭하여 `ctlAlarmClock`의 복사본을 폼에 추가합니다.

7. **도구 상자**에서 **DateTimePicker** <xref:System.Windows.Forms.DateTimePicker> 를 찾아 두 번 클릭 하 여 <xref:System.Windows.Forms.Label> 폼에 컨트롤을 추가한 다음 **레이블을**두 번 클릭 하 여 컨트롤을 추가 합니다.

8. 마우스를 사용하여 폼의 편리한 위치에 컨트롤을 배치합니다.

9. 다음 방식으로 이러한 컨트롤의 속성을 설정합니다.

    |컨트롤|속성|값|
    |-------------|--------------|-----------|
    |`label1`|**텍스트**|`(blank space)`|
    ||**이름**|`lblTest`|
    |`dateTimePicker1`|**이름**|`dtpTest`|
    ||**Format**|<xref:System.Windows.Forms.DateTimePickerFormat.Time>|

10. 디자이너에서 **dtpTest**를 두 번 클릭합니다.

     **코드 편집기**에 `private void dtpTest_ValueChanged`가 열립니다.

11. 다음과 비슷하도록 코드를 수정합니다.

    ```csharp
    private void dtpTest_ValueChanged(object sender, System.EventArgs e)
    {
        ctlAlarmClock1.AlarmTime = dtpTest.Value;
        ctlAlarmClock1.AlarmSet = true;
        lblTest.Text = "Alarm Time is " +
            ctlAlarmClock1.AlarmTime.ToShortTimeString();
    }
    ```

12. **솔루션 탐색기**에서 **Test**를 마우스 오른쪽 단추로 클릭 한 다음 **시작 프로젝트로 설정**을 클릭 합니다.

13. **디버그** 메뉴에서 **디버깅 시작**을 클릭합니다.

     테스트 프로그램이 시작됩니다. `ctlAlarmClock` 컨트롤에서 현재 시간을 업데이트 하 고 시작 시간이 <xref:System.Windows.Forms.DateTimePicker> 컨트롤에 표시 되는지 확인 합니다.

14. 시간의 분 <xref:System.Windows.Forms.DateTimePicker> 이 표시 되는 위치를 클릭 합니다.

15. 키보드를 사용하여 `ctlAlarmClock`으로 표시된 현재 시간보다 1분 큰 값(분)을 설정합니다.

     경보 설정 시간이 `lblTest`에 표시됩니다. 표시된 시간이 경보 설정 시간에 도달할 때까지 기다립니다. 표시된 시간이 경보 설정 시간에 도달하면 `lblAlarm`이 깜박입니다.

16. `btnAlarmOff`을 클릭하여 경보를 해제합니다. 이제 경보를 다시 설정할 수 있습니다.

이 문서에서는 몇 가지 주요 개념에 대해 설명 했습니다. 컨트롤 및 구성 요소를 복합 컨트롤 컨테이너에 결합하여 복합 컨트롤을 만드는 방법을 배웠습니다. 컨트롤에 속성을 추가하고 사용자 지정 기능을 작성하는 코드를 작성하는 방법도 알아봤습니다. 마지막 섹션에서는 상속성을 통해 지정된 복합 컨트롤의 기능을 확장하고 해당 메서드를 재정의하여 호스트 메서드의 기능을 수정해보았습니다.

## <a name="see-also"></a>참고자료

- [사용자 지정 컨트롤의 종류](varieties-of-custom-controls.md)
- [방법: 도구 상자 항목 선택 대화 상자에 컨트롤 표시](how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)
- [연습: 시각적 개체를 사용 하 여 Windows Forms 컨트롤에서 상속C#](walkthrough-inheriting-from-a-windows-forms-control-with-visual-csharp.md)
