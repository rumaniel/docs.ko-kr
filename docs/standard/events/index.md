---
title: 이벤트 처리 및 발생
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- delegate model for events
- application development [.NET], events
- application development [.NET Framework], events
- application development [.NET Core], events
- events [.NET]
- events [.NET Core]
- events [.NET Framework]
ms.assetid: b6f65241-e0ad-4590-a99f-200ce741bb1f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b5e49e9d575ae2ec9b48b18f839d469632ffa769
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770411"
---
# <a name="handling-and-raising-events"></a>이벤트 처리 및 발생

.NET의 이벤트는 대리자 모델을 기반으로 합니다. 대리자 모델은 구독자가 공급자를 등록하고 공급자로부터 알림을 수신하는 데 사용할 수 있는 [관찰자 디자인 패턴](observer-design-pattern.md)을 따릅니다. 이벤트 전송자는 이벤트가 발생했음을 알리고, 이벤트 수신자는 해당 알림을 수신하고 그에 대한 응답을 정의합니다. 이 문서에서는 대리자 모델의 주요 구성 요소, 애플리케이션에서 이벤트를 사용하는 방법 및 코드에서 이벤트를 구현하는 방법에 대해 설명합니다.  
  
 Windows 8.x Store 앱에서의 이벤트 처리에 대한 자세한 내용은 [이벤트 및 라우트된 이벤트 개요](https://docs.microsoft.com/previous-versions/windows/apps/hh758286(v=win.10))를 참조하세요.  
  
## <a name="events"></a>이벤트

이벤트는 개체에서 작업 실행을 알리기 위해 보내는 메시지입니다. 이 작업은 단추 클릭과 같은 사용자 조작으로 발생하거나, 속성 값 변경 등의 다른 프로그램 논리에서 발생할 수 있습니다. 이벤트를 발생시키는 개체를 *이벤트 전송자*라고 하며 이벤트 전송자는 어떤 개체 또는 메서드가 발생되는 이벤트를 수신(처리)할지 모릅니다. 이벤트는 일반적으로 이벤트 전송자의 멤버입니다. 예를 들어 <xref:System.Web.UI.WebControls.Button.Click> 이벤트는 <xref:System.Web.UI.WebControls.Button> 클래스의 멤버이고, <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> 이벤트는 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스를 구현하는 클래스의 멤버입니다.  
  
이벤트를 정의하려면 C# [`event`](../../csharp/language-reference/keywords/event.md) 또는 Visual Basic [`Event`](../../visual-basic/language-reference/statements/event-statement.md) 키워드를 이벤트 클래스의 시그니처에서 사용하고 이벤트에 대한 대리자의 형식을 지정합니다. 대리자는 다음 섹션에 설명되어 있습니다.  
  
일반적으로 이벤트를 발생시키려면 `protected` 및 `virtual`(C#) 또는 `Protected` 및 `Overridable`(Visual Basic)이라고 표시된 메서드를 추가합니다. 이 메서드의 이름을 `On`*EventName*으로 지정합니다(예: `OnDataReceived`). 메서드에서 <xref:System.EventArgs> 형식이나 파생 형식의 개체인 이벤트 데이터 개체를 지정하는 하나의 매개 변수를 사용해야 합니다. 이 메서드를 사용하면 파생된 클래스를 이용해 이벤트를 발생시키는 논리를 재정의할 수 있습니다. 파생된 클래스는 등록된 대리자가 이벤트를 수신할 수 있도록 해주는 기본 클래스의 `On`*EventName* 메서드를 항상 호출해야 합니다.  

다음 예제에서는 `ThresholdReached`라는 이벤트를 선언하는 방법을 보여 줍니다. 이 이벤트는 <xref:System.EventHandler> 대리자와 연결되어 있고 `OnThresholdReached`라는 메서드에서 발생합니다.  
  
 [!code-csharp[EventsOverview#1](~/samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programtruncated.cs#1)]
 [!code-vb[EventsOverview#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1truncated.vb#1)]  
  
## <a name="delegates"></a>대리자

대리자는 메서드에 대한 참조를 가지는 형식입니다. 대리자는 참조하는 메서드의 반환 형식 및 매개 변수를 보여주는 시그니처를 사용하여 선언되며, 해당 시그니처와 일치하는 메서드에 대한 참조만 포함할 수 있습니다. 따라서 대리자는 형식이 안전한 함수 포인터나 콜백과 동일합니다. 대리자 선언은 대리자 클래스를 효율적으로 정의할 수 있습니다.  
  
대리자는 .NET에서 여러 용도로 사용됩니다. 이벤트의 컨텍스트에서 대리자는 이벤트 소스와 이벤트를 처리하는 코드 간의 매개자 (또는 포인터와 같은 메커니즘)입니다. 대리자와 이벤트의 연결은 이전 섹션의 예제에서와 같이 이벤트 선언에서 대리자 형식을 포함하는 방식으로 수행됩니다. 대리자에 대한 자세한 내용은 <xref:System.Delegate> 클래스를 참조하십시오.  
  
.NET에서는 <xref:System.EventHandler> 및 <xref:System.EventHandler%601> 대리자를 제공하여 대부분의 이벤트 시나리오를 지원합니다. 이벤트 데이터를 포함하지 않는 모든 이벤트에 대해 <xref:System.EventHandler> 대리자를 사용합니다. 이벤트에 대한 데이터를 포함하는 이벤트에 대해 <xref:System.EventHandler%601> 대리자를 사용합니다. 이러한 대리자는 반환 형식 값이 없으며, 두 개의 매개 변수(이벤트 소스 개체 및 이벤트 데이터 개체)를 사용합니다.  
  
대리자는 [멀티캐스트](xref:System.MulticastDelegate)로, 둘 이상의 이벤트 처리 메서드에 대한 참조를 포함할 수 있습니다. 자세한 내용은 <xref:System.Delegate> 참조 페이지를 참조하십시오. 대리자를 사용하면 유연하고 정밀하게 이벤트 처리를 제어할 수 있습니다. 대리자는 이벤트에 등록된 이벤트 처리기의 목록을 유지 관리하여 이벤트를 발생시키는 클래스의 이벤트 발송자 이벤트로서 작동합니다.  
  
<xref:System.EventHandler> 및 <xref:System.EventHandler%601> 대리자가 작동하지 않는 시나리오의 경우, 대리자를 정의할 수 있습니다. 대리자를 정의해야 하는 시나리오(예: 제네릭을 인식할 수 없는 코드를 사용하여 작업해야 하는 경우)는 매우 드뭅니다. 선언에서 대리자는 C# [`delegate`](../../csharp/language-reference/keywords/delegate.md) 및 Visual Basic [`Delegate`](../../visual-basic/language-reference/statements/delegate-statement.md) 키워드를 사용하여 표시합니다. 다음 예제에서는 `ThresholdReachedEventHandler`라는 대리자를 선언하는 방법을 보여 줍니다.  
  
[!code-csharp[EventsOverview#4](~/samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programtruncated.cs#4)]
[!code-vb[EventsOverview#4](~/samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1truncated.vb#4)]  
  
## <a name="event-data"></a>이벤트 데이터

이벤트와 관련된 데이터는 이벤트 데이터 클래스를 통해 제공할 수 있습니다. .NET에서는 애플리케이션에 사용할 수 있는 여러 이벤트 데이터 클래스를 제공합니다. 예를 들어, <xref:System.IO.Ports.SerialDataReceivedEventArgs> 클래스는 <xref:System.IO.Ports.SerialPort.DataReceived?displayProperty=nameWithType> 이벤트에 대한 이벤트 데이터 클래스에 해당합니다. .NET에서는 모든 이벤트 데이터 클래스를 `EventArgs`로 끝내는 명명 패턴을 따릅니다. 이벤트에 대한 대리자를 보는 것만으로 어떠한 이벤트 데이터 클래스가 이벤트에 연결되어 있는지 확인할 수 있습니다. 예를 들어, <xref:System.IO.Ports.SerialDataReceivedEventHandler> 대리자는 매개 변수 중 하나로 <xref:System.IO.Ports.SerialDataReceivedEventArgs> 클래스를 가집니다.  
  
<xref:System.EventArgs> 클래스는 모든 이벤트 데이터 클래스의 기본 형식입니다. <xref:System.EventArgs>는 이벤트에 연결된 데이터가 없을 때 사용하는 클래스이기도 합니다. 다른 클래스에게 어떤 일이 발생했으며 어떠한 데이터도 전달할 필요가 없다는 것을 알리기만 하는 이벤트를 만들려면 대리자에서 두 번째 매개 변수로 <xref:System.EventArgs> 클래스를 포함합니다. 어떠한 데이터도 제공되지 않은 경우 <xref:System.EventArgs.Empty?displayProperty=nameWithType> 값을 전달할 수 있습니다. <xref:System.EventHandler> 대리자는 매개 변수로 <xref:System.EventArgs> 클래스를 포함합니다.  
  
사용자 지정된 이벤트 데이터 클래스를 만들려면 <xref:System.EventArgs>로부터 파생된 클래스를 만든 후, 이벤트 관련 데이터를 전달하는 데 필요한 멤버를 제공합니다. 일반적으로 .NET과 동일한 명명 패턴을 사용하여 이벤트 데이터 클래스 이름을 `EventArgs`로 끝내야 합니다.  
  
다음 예제에서는 `ThresholdReachedEventArgs`라는 이벤트 데이터 클래스를 보여 줍니다. 발생한 이벤트와 관련된 속성도 포함됩니다.  
  
[!code-csharp[EventsOverview#3](~/samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programtruncated.cs#3)]
[!code-vb[EventsOverview#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1truncated.vb#3)]  
  
## <a name="event-handlers"></a>이벤트 처리기

이벤트에 응답하려면 이벤트 수신기에서 이벤트 처리기 메서드를 정의합니다. 이 메서드는 처리 중인 이벤트에 대한 대리자의 시그니처와 일치해야 합니다. 이벤트 처리기에서 사용자가 단추를 클릭한 후 사용자 입력 정보를 수집하는 등의 이벤트가 발생하는 경우 필요한 작업을 수행합니다. 이벤트가 발생할 때 알림을 받기 위해서는 이벤트 처리기 메서드에서 이벤트를 구독해야 합니다.  
  
다음 예제에서는 `c_ThresholdReached` 대리인에 대한 시그니처와 일치하는 <xref:System.EventHandler>라는 이벤트 처리기 메서드를 보여 줍니다. 이 메서드는 `ThresholdReached` 이벤트를 구독합니다.  
  
[!code-csharp[EventsOverview#2](~/samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programtruncated.cs#2)]
[!code-vb[EventsOverview#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1truncated.vb#2)]  
  
## <a name="static-and-dynamic-event-handlers"></a>정적 및 동적 이벤트 처리기  
 
.NET에서는 구독자가 정적이나 동적으로 이벤트 알림을 등록할 수 있습니다. 고정 이벤트 처리기는 해당 이벤트가 처리되는 클래스의 전체 수명 동안 적용됩니다. 동적 이벤트 처리기는 특정 조건부 프로그램 논리에 대한 응답에서 일반적으로 프로그램을 실행하는 동안 명시적으로 활성화되고 비활성화됩니다. 예를 들어 이벤트 알림이 특정 조건 하에서만 필요하거나 애플리케이션이 여러 이벤트 처리기를 제공하고 런타임 조건에서 사용할 적절한 이벤트 처리기를 정의하는 경우에 사용될 수 있습니다. 이전 섹션의 예제에서는 이벤트 처리기를 동적으로 추가하는 방법을 보여 줍니다. 자세한 내용은 [이벤트](../../visual-basic/programming-guide/language-features/events/index.md)(Visual Basic의 경우) 및 [이벤트](../../csharp/programming-guide/events/index.md)(C#의 경우)를 참조하세요.  
  
## <a name="raising-multiple-events"></a>여러 이벤트 발생  
 클래스에서 여러 이벤트를 발생시키는 경우, 컴파일러가 각 이벤트 대리자 인스턴스에 대해 하나의 필드를 생성합니다. 이벤트 수가 큰 경우 대리자당 하나의 필드의 스토리지 공간은 허용되지 않습니다. 이러한 경우를 위해 .NET에서는 이벤트 대리자를 저장하도록 선택한 다른 데이터 구조와 함께 사용할 수 있는 이벤트 속성을 제공합니다.  
  
 이벤트 속성은 이벤트 접근자와 함께 이벤트 선언으로 구성됩니다. 이벤트 접근자는 사용자가 정의하는 메서드로서, 스토리지 데이터 구조에서 이벤트 대리자 인스턴스를 추가하거나 제거할 수 있게 합니다. 각 이벤트 대리자는 호출되기 전에 검색되어야 하기 때문에 이벤트 속성은 이벤트 필드보다 속도가 느립니다. 메모리와 속도 간의 균형을 조정합니다. 클래스가 자주 발생하는 많은 이벤트를 정의하는 경우 이벤트 속성을 구현합니다. 자세한 내용은 [방법: 이벤트 속성을 사용하여 여러 이벤트 처리](how-to-handle-multiple-events-using-event-properties.md)를 참조하세요.  
  
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[방법: 이벤트 발생 및 사용](how-to-raise-and-consume-events.md)|이벤트의 발생 및 사용에 대한 예제를 포함합니다.|  
|[방법: 이벤트 속성을 사용하여 여러 이벤트 처리](how-to-handle-multiple-events-using-event-properties.md)|이벤트 속성을 사용하여 여러 이벤트를 처리하는 방법을 보여 줍니다.|  
|[관찰자 디자인 패턴](observer-design-pattern.md)|구독자가 공급자를 등록하고 공급자로부터 알림을 수신하는 데 사용할 수 있는 디자인 패턴에 대해 설명합니다.|  
|[방법: Web Forms 애플리케이션에서 이벤트 사용](how-to-consume-events-in-a-web-forms-application.md)|Web Forms 컨트롤에서 발생한 이벤트를 처리하는 방법을 보여 줍니다.|  
  
## <a name="see-also"></a>참고 항목

- <xref:System.EventHandler>
- <xref:System.EventHandler%601>
- <xref:System.EventArgs>
- <xref:System.Delegate>
- [이벤트(Visual Basic)](../../visual-basic/programming-guide/language-features/events/index.md)
- [이벤트(C# 프로그래밍 가이드)](../../csharp/programming-guide/events/index.md)
- [이벤트 및 라우팅 이벤트 개요(UWP 앱)](/windows/uwp/xaml-platform/events-and-routed-events-overview)
