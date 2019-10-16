---
title: 이벤트
description: 이벤트를 F# 사용 하 여 함수 호출을 GUI 프로그래밍에서 중요 한 사용자 동작에 연결 하는 방법을 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: e581d9c31c1b8f3c114b86c898011dec3bd52535
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216465"
---
# <a name="events"></a>이벤트

> [!NOTE]
> 이 문서의 API 참조 링크를 통해 MSDN으로 이동됩니다.  docs.microsoft.com API 참조가 완전하지 않습니다.

이벤트를 사용하면 함수 호출을 사용자 동작에 연결할 수 있습니다. 이벤트는 GUI 프로그래밍에서 중요한 부분을 차지합니다. 응용 프로그램이나 운영 체제에서 이벤트를 트리거할 수도 있습니다.

## <a name="handling-events"></a>이벤트 처리

Windows Forms 또는 WPF(Windows Presentation Foundation) 같은 GUI 라이브러리를 사용하는 경우 응용 프로그램의 코드 대부분은 라이브러리에 미리 정의되어 있는 이벤트에 대한 응답으로 실행됩니다. 이렇게 미리 정의되어 있는 이벤트는 폼과 컨트롤 같은 GUI 클래스의 멤버입니다. 다음 코드에서 볼 수 있는 것처럼 `Click` 클래스의 `Form` 이벤트 같이 명명된 특정 이벤트를 참조하고 `Add` 메서드를 호출하여 단추 클릭 같은 기존 이벤트에 사용자 지정 동작을 추가할 수 있습니다. F# Interactive에서 이를 실행할 경우에는 `System.Windows.Forms.Application.Run(System.Windows.Forms.Form)`에 대한 호출을 생략합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3601.fs)]

`Add` 메서드의 형식은 `('a -> unit) -> unit`입니다. 따라서 이벤트 처리기 메서드는 매개 변수 하나를 사용하고 `unit`을 반환합니다. 이 메서드에 사용되는 매개 변수는 일반적으로 이벤트 인수입니다. 위 예제에서는 이벤트 처리기가 람다 식으로 나와 있습니다. 이벤트 처리기는 다음 코드 예제에서와 같이 함수 값일 수도 있습니다. 다음 코드 예제에서는 이벤트 처리기 매개 변수를 사용하여 이벤트의 형식에 맞는 특정 정보를 제공하는 방법도 보여 줍니다. 시스템에서는 `MouseMove` 이벤트에 대해 `System.Windows.Forms.MouseEventArgs` 개체를 전달합니다. 이 개체에는 포인터의 `X` 및 `Y` 위치가 포함됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3602.fs)]

## <a name="creating-custom-events"></a>사용자 지정 이벤트 만들기

F#이벤트는 [IEvent](https://msdn.microsoft.com/library/8dbca0df-f8a1-40bd-8d50-aa26f6a8b862) 인터페이스를 F# 구현 하는 [이벤트](https://msdn.microsoft.com/library/f3b47c8a-4ee5-4ce8-9a72-ad305a17c4b9) 클래스로 표현됩니다. `IEvent`자체는 다른 두 인터페이스 `System.IObservable<'T>` 및 [IDelegateEvent](https://msdn.microsoft.com/library/3d849465-6b8e-4fc5-b36c-2941d734268a)의 기능을 결합 하는 인터페이스입니다. 따라서 `Event`에는 다른 언어의 대리자와 동등한 기능에 더해 `IObservable`의 기능이 추가로 포함됩니다. 즉, F# 이벤트는 이벤트 필터링을 지원하며 F# 고급 함수와 람다 식을 이벤트 처리기로 사용할 수 있습니다. 이 기능은 [이벤트 모듈](https://msdn.microsoft.com/library/8b883baa-a460-4840-9baa-de8260351bc7)에서 제공 됩니다.

클래스에 대해 다른 .NET Framework 이벤트와 같은 방식으로 작동하는 이벤트를 만들려면 클래스의 필드로 `let` 를 정의하는 `Event` 바인딩을 클래스에 추가하면 됩니다. 원하는 이벤트 인수 형식을 형식 인수로 지정하거나, 인수 형식을 비워 두고 컴파일러가 적합한 형식을 유추하도록 할 수 있습니다. 또한 이벤트를 노출하는 이벤트 멤버를 CLI이벤트로 정의해야 합니다. 이 멤버에는 [Clievent](https://msdn.microsoft.com/library/d359f1dd-ffa5-42fb-8808-b4c8131a0333) 특성이 있어야 합니다. 이 클래스는 속성으로 선언 되며, 해당 구현은 이벤트의 [게시](https://msdn.microsoft.com/library/b0fdaad5-25e5-43d0-9c0c-ce37c4aeb68e) 속성에 대 한 호출 일 뿐입니다. 클래스 사용자는 게시된 이벤트의 `Add` 메서드를 사용하여 처리기를 추가할 수 있습니다. `Add` 메서드에 대한 인수는 람다 식일 수 있습니다. 이벤트의 `Trigger` 속성을 사용하여 이벤트를 발생시키고 인수를 처리기 함수에 전달할 수 있습니다. 다음 코드 예제에서는 그 구체적인 방법을 보여 줍니다. 이 예에서 이벤트에 대해 유추된 형식 인수는 람다 식의 인수를 나타내는 튜플입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3605.fs)]

출력은 다음과 같습니다.

```console
Event1 occurred! Object data: Hello World!
```

여기서는 `Event` 모듈을 통해 추가로 제공되는 기능을 보여 줍니다. 다음 코드 예제에서는 `Event.create`를 사용하여 이벤트와 트리거 메서드를 만들고 이벤트 처리기 두 개를 람다 식 형태로 추가한 다음 이벤트를 트리거하여 두 람다 식을 실행하는 기본적인 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3603.fs)]

위 코드는 다음과 같이 출력됩니다.

```console
Event occurred.
Given a value: Event occurred.
```

## <a name="processing-event-streams"></a>이벤트 스트림 처리

Event [. add](https://msdn.microsoft.com/library/10670d3b-8d47-4f6e-b8df-ebc6f64ef4fd) 함수를 사용 하 여 이벤트에 대 한 이벤트 처리기를 추가 하는 대신 `Event` 모듈의 함수를 사용 하 여 고도로 사용자 지정 된 방식으로 이벤트 스트림을 처리할 수 있습니다. 이를 위해서는 일련의 함수 호출에서 첫째 값으로 이벤트를 사용하고 이후의 함수 호출로는 `|>` 모듈 함수를 사용하면서 전달 파이프(`Event`)를 사용해야 합니다.

다음 코드 예제에서는 특정 조건이 충족될 때만 처리기가 호출되는 이벤트를 설정하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3604.fs)]

[관찰 가능한 모듈](https://msdn.microsoft.com/library/16b8610b-b30a-4df7-aa99-d9d352276227) 은 관찰 가능한 개체에서 작동 하는 유사한 함수를 포함 합니다. 관찰 가능한 개체는 이벤트와 비슷하지만 개체 자체가 구독 대상인 경우에만 능동적으로 이벤트를 구독합니다.

## <a name="implementing-an-interface-event"></a>인터페이스 이벤트 구현

UI 구성 요소를 개발할 때 종종 기존 폼 또는 컨트롤에서 상속하는 새 컨트롤 또는 새 폼을 만들어 시작합니다. 이벤트는 인터페이스에서 자주 정의되며, 그럴 경우 이벤트를 구현하려면 인터페이스를 구현해야 합니다. `System.ComponentModel.INotifyPropertyChanged` 인터페이스는 단일 `System.ComponentModel.INotifyPropertyChanged.PropertyChanged` 이벤트를 정의합니다. 다음 코드에서는 이 상속된 인터페이스가 정의한 이벤트를 구현하는 방법을 보여줍니다.

```fsharp
module CustomForm

open System.Windows.Forms
open System.ComponentModel

type AppForm() as this =
    inherit Form()

    // Define the propertyChanged event.
    let propertyChanged = Event<PropertyChangedEventHandler, PropertyChangedEventArgs>()
    let mutable underlyingValue = "text0"

    // Set up a click event to change the properties.
    do
        this.Click |> Event.add(fun evArgs -> this.Property1 <- "text2"
        this.Property2 <- "text3")

    // This property does not have the property-changed event set.
    member val Property1 : string = "text" with get, set

    // This property has the property-changed event set.
    member this.Property2
        with get() = underlyingValue
        and set(newValue) =
            underlyingValue <- newValue
            propertyChanged.Trigger(this, new PropertyChangedEventArgs("Property2"))

    // Expose the PropertyChanged event as a first class .NET event.
    [<CLIEvent>]
    member this.PropertyChanged = propertyChanged.Publish

    // Define the add and remove methods to implement this interface.
    interface INotifyPropertyChanged with
        member this.add_PropertyChanged(handler) = propertyChanged.Publish.AddHandler(handler)
        member this.remove_PropertyChanged(handler) = propertyChanged.Publish.RemoveHandler(handler)

    // This is the event-handler method.
    member this.OnPropertyChanged(args : PropertyChangedEventArgs) =
        let newProperty = this.GetType().GetProperty(args.PropertyName)
        let newValue = newProperty.GetValue(this :> obj) :?> string
        printfn "Property %s changed its value to %s" args.PropertyName newValue

// Create a form, hook up the event handler, and start the application.
let appForm = new AppForm()
let inpc = appForm :> INotifyPropertyChanged
inpc.PropertyChanged.Add(appForm.OnPropertyChanged)
Application.Run(appForm)
```

생성자에서 이벤트를 후크하려는 경우 다음 예제에서처럼 이벤트 연결이 추가 생성자의 `then` 블록에 있어야 하기 때문에 코드가 조금 더 복잡합니다.

```fsharp
module CustomForm

open System.Windows.Forms
open System.ComponentModel

// Create a private constructor with a dummy argument so that the public
// constructor can have no arguments.
type AppForm private (dummy) as this =
    inherit Form()

    // Define the propertyChanged event.
    let propertyChanged = Event<PropertyChangedEventHandler, PropertyChangedEventArgs>()
    let mutable underlyingValue = "text0"

    // Set up a click event to change the properties.
    do
        this.Click |> Event.add(fun evArgs -> this.Property1 <- "text2"
        this.Property2 <- "text3")

    // This property does not have the property changed event set.
    member val Property1 : string = "text" with get, set

    // This property has the property changed event set.
    member this.Property2
        with get() = underlyingValue
        and set(newValue) =
            underlyingValue <- newValue
            propertyChanged.Trigger(this, new PropertyChangedEventArgs("Property2"))

    [<CLIEvent>]
    member this.PropertyChanged = propertyChanged.Publish

    // Define the add and remove methods to implement this interface.
    interface INotifyPropertyChanged with
        member this.add_PropertyChanged(handler) = this.PropertyChanged.AddHandler(handler)
        member this.remove_PropertyChanged(handler) = this.PropertyChanged.RemoveHandler(handler)

    // This is the event handler method.
    member this.OnPropertyChanged(args : PropertyChangedEventArgs) =
        let newProperty = this.GetType().GetProperty(args.PropertyName)
        let newValue = newProperty.GetValue(this :> obj) :?> string
        printfn "Property %s changed its value to %s" args.PropertyName newValue

    new() as this =
        new AppForm(0)
        then
            let inpc = this :> INotifyPropertyChanged
            inpc.PropertyChanged.Add(this.OnPropertyChanged)

// Create a form, hook up the event handler, and start the application.
let appForm = new AppForm()
Application.Run(appForm)
```

## <a name="see-also"></a>참고자료

- [멤버](index.md)
- [이벤트 처리 및 발생](../../../standard/events/index.md)
- [람다 식: `fun` 키워드](../functions/lambda-expressions-the-fun-keyword.md)
- [Control. 이벤트 모듈](https://msdn.microsoft.com/visualfsharpdocs/conceptual/control.event-module-%5bfsharp%5d)
- [Control. Event&#60;&#62; 클래스](https://msdn.microsoft.com/visualfsharpdocs/conceptual/control.event%5b%27t%5d-class-%5bfsharp%5d)
- [Control. Event&#60;' Delegate, ' Args&#62; 클래스](https://msdn.microsoft.com/visualfsharpdocs/conceptual/control.event%5b%27delegate%2c%27args%5d-class-%5bfsharp%5d)
