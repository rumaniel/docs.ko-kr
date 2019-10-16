---
title: '방법: 코드에서 마우스 및 키보드 이벤트 시뮬레이션'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- keyboards [Windows Forms], event simulation
- user input [Windows Forms], simulating
- SendKeys [Windows Forms], using
- mouse clicks [Windows Forms], simulating
- mouse [Windows Forms], event simulation
ms.assetid: 6abcb67e-3766-4af2-9590-bf5dabd17e41
ms.openlocfilehash: 1a7a0fa6295cd8332313a983ca78345bfbac393e
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046389"
---
# <a name="how-to-simulate-mouse-and-keyboard-events-in-code"></a>방법: 코드에서 마우스 및 키보드 이벤트 시뮬레이션

Windows Forms는 프로그래밍 방식으로 마우스 및 키보드 입력을 시뮬레이션하기 위한 여러 가지 옵션을 제공합니다. 이 항목에서는 이러한 옵션에 대해 간략하게 설명합니다.

## <a name="simulating-mouse-input"></a>마우스 입력 시뮬레이션

마우스 이벤트를 시뮬레이션하는 가장 좋은 방법은 시뮬레이션하려는 마우스 이벤트를 발생시키는 `On`*EventName* 메서드를 호출하는 것입니다. 이벤트를 발생시키는 메서드는 보호되며 컨트롤이나 폼 외부에서 액세스할 수 없기 때문에 이 옵션은 일반적으로 사용자 지정 컨트롤 및 폼 내에서만 가능합니다. 예를 들어 다음 단계에서는 코드에서 마우스 오른쪽 단추를 클릭하여 시뮬레이션하는 방법을 보여 줍니다.

#### <a name="to-programmatically-click-the-right-mouse-button"></a>프로그래밍 방식으로 마우스 오른쪽 단추를 클릭하려면

1. <xref:System.Windows.Forms.MouseEventArgs.Button%2A> 속성이 <xref:System.Windows.Forms.MouseButtons.Right?displayProperty=nameWithType> 값으로 설정된 <xref:System.Windows.Forms.MouseEventArgs>를 만듭니다.

2. 이 <xref:System.Windows.Forms.Control.OnMouseClick%2A> 를 인수로 사용하여 <xref:System.Windows.Forms.MouseEventArgs> 메서드를 호출합니다.

사용자 지정 컨트롤에 대한 자세한 내용은 [디자인 타임에 Windows Forms 컨트롤 개발](./controls/developing-windows-forms-controls-at-design-time.md)을 참조하세요.

마우스 입력을 시뮬레이션하는 다른 방법이 있습니다. 예를 들어 일반적으로 마우스 입력을 통해 설정되는 상태를 나타내는 컨트롤 속성(예: <xref:System.Windows.Forms.CheckBox.Checked%2A> 컨트롤의 <xref:System.Windows.Forms.CheckBox> 속성)을 프로그래밍 방식으로 설정하거나 시뮬레이션하려는 이벤트에 연결된 대리자를 직접 호출할 수 있습니다.

## <a name="simulating-keyboard-input"></a>키보드 입력 시뮬레이션

마우스 입력에 대해 위에서 설명한 전략을 사용하여 키보드 입력을 시뮬레이션할 수도 있지만 Windows Forms에서는 활성 애플리케이션에 키 입력을 전송하기 위한 <xref:System.Windows.Forms.SendKeys> 클래스도 제공합니다.

> [!CAUTION]
> 다양한 키보드를 통해 전 세계에서 사용하기 위한 응용 프로그램인 경우 <xref:System.Windows.Forms.SendKeys.Send%2A?displayProperty=nameWithType>를 사용하면 예기치 않은 결과가 발생할 수 있으며 피해야 합니다.

> [!NOTE]
> <xref:System.Windows.Forms.SendKeys> 클래스는 Windows Vista에서 실행되는 응용 프로그램에서 사용할 수 있도록 .NET Framework 3.0에서 업데이트되었습니다. Windows Vista의 향상된 보안(사용자 계정 컨트롤 또는 UAC라고 함) 때문에 이전 구현이 예상대로 작동하지 않습니다.
>
> <xref:System.Windows.Forms.SendKeys> 클래스는 타이밍 문제에 취약하며, 이를 해결하기 위해 일부 개발자가 노력해야 했습니다. 업데이트된 구현도 타이밍 문제에 취약하지만 약간 더 빠르며 해결 방법에 대한 변경이 필요할 수도 있습니다. <xref:System.Windows.Forms.SendKeys> 클래스는 먼저 이전 구현을 사용하려고 시도하며, 실패할 경우 새 구현을 사용합니다. 따라서 <xref:System.Windows.Forms.SendKeys> 클래스는 운영 체제마다 다르게 동작할 수 있습니다. 또한 <xref:System.Windows.Forms.SendKeys> 클래스가 새 구현을 사용하는 경우 <xref:System.Windows.Forms.SendKeys.SendWait%2A> 메서드는 다른 프로세스로 전송된 메시지가 처리될 때까지 기다리지 않습니다.
>
> 애플리케이션이 운영 체제와 관계없이 일관된 동작에 의존하는 경우 app.config 파일에 다음 애플리케이션 설정을 추가하여 <xref:System.Windows.Forms.SendKeys> 클래스에서 새 구현을 사용하도록 강제할 수 있습니다.
>
> ```xml
> <appSettings>
>  <add key="SendKeys" value="SendInput"/>
> </appSettings>
> ```
>
> <xref:System.Windows.Forms.SendKeys> 클래스에서 이전 구현을 사용하도록 강제하려면 `"JournalHook"` 값을 대신 사용합니다.

#### <a name="to-send-a-keystroke-to-the-same-application"></a>동일한 애플리케이션에 키 입력을 보내려면

1. <xref:System.Windows.Forms.SendKeys.Send%2A> 클래스의 <xref:System.Windows.Forms.SendKeys.SendWait%2A> 또는 <xref:System.Windows.Forms.SendKeys> 메서드를 호출합니다. 애플리케이션의 활성 컨트롤이 지정된 키 입력을 받습니다. 다음 코드 예제에서는 <xref:System.Windows.Forms.SendKeys.Send%2A> 를 사용하여 사용자가 폼의 화면을 두 번 클릭할 때 Enter 키 누름을 시뮬레이션합니다. 이 예제에서는 탭 인덱스가 0인 단일 <xref:System.Windows.Forms.Form> 컨트롤이 있는 <xref:System.Windows.Forms.Button> 을 가정합니다.

    [!code-cpp[System.Windows.Forms.SimulateKeyPress#10](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/cpp/form1.cpp#10)]
    [!code-csharp[System.Windows.Forms.SimulateKeyPress#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/CS/form1.cs#10)]
    [!code-vb[System.Windows.Forms.SimulateKeyPress#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/VB/form1.vb#10)]

#### <a name="to-send-a-keystroke-to-a-different-application"></a>다른 애플리케이션에 키 입력을 보내려면

1. 키 입력을 수신할 애플리케이션 창을 활성화한 다음 <xref:System.Windows.Forms.SendKeys.Send%2A> 또는 <xref:System.Windows.Forms.SendKeys.SendWait%2A> 메서드를 호출합니다. 다른 애플리케이션을 활성화할 관리되는 메서드가 없으므로 네이티브 Windows 메서드를 사용하여 다른 애플리케이션에 포커스를 강제로 설정해야 합니다. 다음 코드 예제에서는 플랫폼 호출을 통해 `FindWindow` 및 `SetForegroundWindow` 메서드를 호출하여 계산기 애플리케이션 창을 활성화한 다음 <xref:System.Windows.Forms.SendKeys.SendWait%2A> 를 호출하여 계산기 애플리케이션에 일련의 계산을 실행합니다.

    > [!NOTE]
    > 계산기 애플리케이션을 찾는 `FindWindow` 호출의 올바른 매개 변수는 Windows 버전에 따라 달라집니다.  다음 코드에서는 [!INCLUDE[win7](../../../includes/win7-md.md)]에서 계산기 애플리케이션을 찾습니다. [!INCLUDE[windowsver](../../../includes/windowsver-md.md)]에서 첫 번째 매개 변수를 "SciCalc"로 변경합니다. Visual Studio에 포함된 Spy++ 도구를 사용하여 올바른 매개 변수를 확인할 수 있습니다.

    [!code-cpp[System.Windows.Forms.SimulateKeyPress#5](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/cpp/form1.cpp#5)]
    [!code-csharp[System.Windows.Forms.SimulateKeyPress#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/CS/form1.cs#5)]
    [!code-vb[System.Windows.Forms.SimulateKeyPress#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/VB/form1.vb#5)]

## <a name="example"></a>예제

다음 코드 예제는 이전 코드 예제에 대한 전체 애플리케이션입니다.

[!code-cpp[System.Windows.Forms.SimulateKeyPress#0](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/cpp/form1.cpp#0)]
[!code-csharp[System.Windows.Forms.SimulateKeyPress#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/CS/form1.cs#0)]
[!code-vb[System.Windows.Forms.SimulateKeyPress#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/VB/form1.vb#0)]

## <a name="compiling-the-code"></a>코드 컴파일

이 예제에는 다음 사항이 필요합니다.

- System, System.Drawing 및 System.Windows.Forms 어셈블리에 대한 참조

## <a name="see-also"></a>참고자료

- [Windows Forms에 사용자 입력](user-input-in-windows-forms.md)
