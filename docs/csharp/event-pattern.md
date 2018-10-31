---
title: 표준 .NET 이벤트 패턴
description: 표준 이벤트 소스를 만들고 코드에서 표준 이벤트를 구독 및 처리하는 방법과 .NET 이벤트 패턴에 대해 알아봅니다.
ms.date: 06/20/2016
ms.assetid: 8a3133d6-4ef2-46f9-9c8d-a8ea8898e4c9
ms.openlocfilehash: 0b10c440f4d05533032aa94819ec879f6a1ca2a4
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48266771"
---
# <a name="standard-net-event-patterns"></a>표준 .NET 이벤트 패턴

[이전](events-overview.md)

.NET 이벤트는 일반적으로 몇 가지 알려진 패턴을 따릅니다. 이러한 패턴의 표준화는 개발자가 해당 표준 패턴에 대한 지식을 활용하여 모든 .NET 이벤트 프로그램에 적용할 수 있다는 의미입니다.

표준 이벤트 소스를 만들고 코드에서 표준 이벤트를 구독 및 처리하는 데 필요한 모든 정보를 얻을 수 있도록 이러한 표준 패턴을 살펴보겠습니다.

## <a name="event-delegate-signatures"></a>이벤트 대리자 시그니처

.NET 이벤트 대리자에 대한 표준 시그니처는 다음과 같습니다.

```csharp
void OnEventRaised(object sender, EventArgs args);
```

반환 형식은 void입니다. 이벤트는 대리자를 기반으로 하며 멀티캐스트 대리자입니다. 또한 모든 이벤트 소스에 대해 여러 구독자를 지원합니다. 메서드의 단일 반환 값은 여러 이벤트 구독자로 확장되지 않습니다. 이벤트 발생 후 이벤트 소스에 표시되는 반환 값은 무엇인가요? 이 문서의 뒷부분에서 이벤트 소스에 정보를 보고하는 이벤트 구독자를 지원하는 이벤트 프로토콜을 만드는 방법에 대해 살펴보겠습니다.

인수 목록에는 보낸 사람과 이벤트 인수의 두 인수가 포함됩니다. `sender`의 컴파일 시간 형식은 `System.Object`이지만 항상 올바른 더 많이 파생된 형식을 알고 있을 수도 있습니다. 규칙에 따라 `object`를 사용합니다.

두 번째 인수는 일반적으로 `System.EventArgs`에서 파생된 형식이었습니다. [다음 섹션](modern-events.md)에서 이 규칙이 더 이상 적용되지 않음을 확인할 수 있습니다. 이벤트 형식에 추가 인수가 필요하지 않은 경우 두 인수를 계속 제공합니다.
이벤트에 추가 정보가 포함되어 있지 않음을 나타낼 때 사용해야 하는 특수 값 `EventArgs.Empty`가 있습니다.

디렉터리 또는 패턴을 따르는 모든 하위 디렉터리의 파일을 나열하는 클래스를 만들어 보겠습니다. 이 구성 요소는 검색된 각 파일에 대해 패턴과 일치하는 이벤트를 발생시킵니다.

이벤트 모델을 사용하면 몇 가지 디자인 장점이 있습니다. 검색된 파일을 찾으면 다른 작업을 수행하는 여러 이벤트 수신기를 만들 수 있습니다. 서로 다른 수신기를 결합하면 더 강력한 알고리즘을 만들 수 있습니다.

검색된 파일을 찾기 위한 초기 이벤트 인수 선언은 다음과 같습니다. 

[!code-csharp[EventArgs](../../samples/csharp/events/Program.cs#EventArgsV1 "Define event arguments")]

이 형식은 작은 데이터 전용 형식처럼 보이지만 규칙을 따르고 참조(`class`) 형식으로 만들어야 합니다. 즉, 인수 개체가 참조로 전달되며 모든 구독자가 데이터에 대한 모든 업데이트를 볼 수 있습니다. 첫 번째 버전은 변경할 수 없는 개체입니다. 이벤트 인수 형식에서 속성을 변경할 수 없도록 하는 것이 좋습니다. 이런 방식으로 다른 구독자에게 값이 표시되기 전에는 한 구독자가 값을 변경할 수 없습니다. 여기에는 아래와 가은 예외가 있습니다.  

다음으로 FileSearcher 클래스에서 이벤트 선언을 만들어야 합니다. `EventHandler<T>` 형식을 활용하면 또 다른 형식 정의를 만들 필요가 없습니다. 제네릭 특수화를 사용하면 됩니다.

FileSearcher 클래스를 입력하여 패턴과 일치하는 파일을 검색하고 일치하는 항목이 검색되면 올바른 이벤트를 발생시켜 보겠습니다.

[!code-csharp[FileSearxcher](../../samples/csharp/events/Program.cs#FileSearcherV1 "Create the initial file searcher")]

## <a name="defining-and-raising-field-like-events"></a>필드와 유사한 이벤트 정의 및 발생

이벤트를 클래스에 추가하는 가장 간단한 방법은 이전 예제와 같이 해당 이벤트를 public 필드로 선언하는 것입니다.

[!code-csharp[DeclareEvent](../../samples/csharp/events/Program.cs#DeclareEvent "Declare the file found event")]

이 예제는 public 필드를 선언하는 것처럼 보이며, 잘못된 개체 지향 사례인 것 같습니다. 속성 또는 메서드를 통해 데이터 액세스를 보호하려고 합니다. 이렇게 하면 잘못된 사례처럼 보이지만 안전한 방식으로 이벤트 개체에만 액세스할 수 있도록 컴파일러에 의해 생성된 코드에서 래퍼를 만듭니다. 필드와 유사한 이벤트에서 사용 가능한 유일한 작업은 처리기 추가입니다.

[!code-csharp[DeclareEventHandler](../../samples/csharp/events/Program.cs#DeclareEventHandler "Declare the file found event handler")]

또한 처리기 제거도 가능합니다.

[!code-csharp[RemoveEventHandler](../../samples/csharp/events/Program.cs#RemoveHandler "Remove the event handler")]

처리기에 대한 지역 변수가 있어야 합니다. 람다 식의 본문을 사용한 경우 제거가 올바르게 작동하지 않습니다. 대리자의 다른 인스턴스가 되고 자동으로 아무 작업도 수행하지 않습니다.

클래스 외부의 코드는 이벤트를 발생시킬 수 없으며 다른 작업도 수행할 수 없습니다.

## <a name="returning-values-from-event-subscribers"></a>이벤트 구독자에서 값 반환

간단한 버전은 제대로 작동하고 있습니다. 이제 또 다른 기능인 취소를 추가해 보겠습니다.

찾은 이벤트를 발생시킬 때 이 파일이 마지막으로 검색된 파일인 경우 수신기에서 추가 처리를 중지할 수 있어야 합니다.

이벤트 처리기는 값을 반환하지 않으므로 다른 방식으로 값을 전달해야 합니다. 표준 이벤트 패턴은 EventArgs 개체를 사용하 여 이벤트 구독자가 취소를 전달하는 데 사용할 수 있는 필드를 포함합니다.

취소 계약의 의미 체계에 따라 두 가지 다른 패턴을 사용할 수 있습니다. 두 경우 모두 찾은 파일 이벤트에 대한 EventArguments에 부울 필드를 추가합니다. 

한 가지 패턴에서는 임의의 구독자 한 명이 작업을 취소할 수 있습니다.
이 패턴에서는 새 필드가 `false`로 초기화됩니다. 임의의 구독자가 이 값을 `true`로 변경할 수 있습니다. 모든 구독자가 발생된 이벤트를 확인하면 FileSearcher 구성 요소에서 부울 값을 검사하고 작업을 수행합니다.

두 번째 패턴에서는 모든 구독자가 작업 취소를 원하는 경우에만 작업을 취소합니다. 이 패턴에서는 작업이 취소되어야 함을 나타내도록 새 필드가 초기화되고 임의의 구독자는 작업이 계속되어야 함을 나타내도록 이 필드를 변경할 수 있습니다.
모든 구독자가 발생된 이벤트를 확인하면 FileSearcher 구성 요소에서 부울 값을 검사하고 작업을 수행합니다. 이 패턴에는 하나의 추가 단계가 있습니다. 구독자가 이벤트를 확인했는지 여부를 구성 요소에서 알고 있어야 합니다. 구독자가 없으면 필드는 취소를 잘못 나타내게 됩니다.

이 샘플에 대한 첫 번째 버전을 구현해 보겠습니다. `CancelRequested`라는 부울 필드를 `FileFoundArgs` 형식에 추가해야 합니다.

[!code-csharp[EventArgs](../../samples/csharp/events/Program.cs#EventArgs "Update event arguments")]

이 새 필드는 자동으로 부울 필드의 기본값인 `false`로 초기화되므로 실수로 취소될 가능성이 없습니다. 구성 요소에서 유일한 다른 변경 사항은 이벤트를 발생시킨 후 플래그를 확인하여 구독자가 취소를 요청했는지를 확인하는 것입니다.

```csharp
public void List(string directory, string searchPattern)
{
    foreach (var file in Directory.EnumerateFiles(directory, searchPattern))
    {
        var args = new FileFoundArgs(file);
        FileFound?.Invoke(this, args);
        if (args.CancelRequested)
            break;
    }
}
```

이 패턴의 한 가지 장점은 새로운 변경 사항이 아니라는 점입니다.
이전에 취소를 요청한 구독자가 없으며 여전히 요청하지 않습니다. 새로운 취소 프로토콜을 지원하려는 경우가 아니라면 구독자 코드를 업데이트할 필요가 없습니다. 이 경우 매우 느슨하게 결합되어 있습니다.

첫 번째 실행 파일을 찾으면 취소를 요청하도록 구독자를 업데이트해 보겠습니다.

```csharp
EventHandler<FileFoundArgs> onFileFound = (sender, eventArgs) =>
{
    Console.WriteLine(eventArgs.FoundFile);
    eventArgs.CancelRequested = true;
};
```

## <a name="adding-another-event-declaration"></a>다른 이벤트 선언 추가

기능을 하나 더 추가하고 이벤트에 대한 다른 언어 관용구를 보여 드리겠습니다. 파일 검색에서 모든 하위 디렉터리를 트래버스하는 `Search()` 메서드의 오버로드를 추가해 보겠습니다.

하위 디렉터리가 많은 디렉터리에서 이 작업은 시간이 오래 걸릴 수 있습니다. 각각의 새 디렉터리 검색이 시작될 때 발생되는 이벤트를 추가해 보겠습니다. 이렇게 하면 구독자가 진행률을 추적하고 진행률에 대해 사용자에게 업데이트할 수 있습니다. 지금까지 만든 모든 샘플은 public입니다. 이제 내부 이벤트로 만들어 보겠습니다. 즉, 인수에 사용된 형식을 내부 형식으로 설정할 수도 있습니다.

먼저 새 디렉터리 및 진행률을 보고하는 새 EventArgs 파생 클래스를 만듭니다. 

[!code-csharp[DirEventArgs](../../samples/csharp/events/Program.cs#SearchDirEventArgs "Define search directory event arguments")]

다시 권장 사항에 따라 이벤트 인수에 대해 변경할 수 없는 참조 형식을 만들 수 있습니다.

다음으로 이벤트를 정의합니다. 이번에는 다른 구문을 사용합니다. 필드 구문을 사용할 뿐만 아니라 추가 및 제거 처리기와 함께 속성을 명시적으로 만들 수도 있습니다. 이 샘플에서 해당 처리기에는 추가 코드가 필요하지 않지만 여기서는 만드는 방법을 보여 줍니다.

[!code-csharp[Declare event with add and remove handlers](../../samples/csharp/events/Program.cs#DeclareSearchEvent "Declare the event with add and remove handlers")]

여러 측면에서, 여기에서 작성하는 코드는 앞에서 살펴본 필드 이벤트 정의에 대해 컴파일러에서 생성하는 코드를 미러링합니다. [속성](properties.md)에 사용된 것과 매우 유사한 구문을 사용하여 이벤트를 만듭니다. 처리기의 이름은 `add`와 `remove`로 다릅니다. 이러한 처리기를 호출하여 이벤트를 구독하거나 이벤트에서 구독을 취소합니다. 또한 이벤트 변수를 저장하려면 private 지원 필드를 선언해야 합니다. 이 필드는 null로 초기화됩니다.

다음으로 하위 디렉터리를 트래버스하고 두 이벤트를 발생시키는 Search() 메서드의 오버로드를 추가해 보겠습니다. 이 작업을 수행하는 가장 쉬운 방법은 기본 인수를 사용하여 모든 디렉터리를 검색하도록 지정하는 것입니다.

[!code-csharp[SearchImplementation](../../samples/csharp/events/Program.cs#FinalImplementation "Implementation to search directories")]

이제 모든 하위 디렉터리를 검색하기 위해 오버로드를 호출하는 응용 프로그램을 실행할 수 있습니다. 새 `ChangeDirectory` 이벤트에는 구독자가 없지만 `?.Invoke()` 관용구를 사용하여 이 작업이 제대로 작동하도록 합니다.

 콘솔 창에 진행률을 표시하는 줄을 작성하는 처리기를 추가해 보겠습니다. 

[!code-csharp[Search](../../samples/csharp/events/Program.cs#Search "Declare event handler")]

.NET 에코시스템 전체에 적용되는 패턴을 살펴보았습니다.
이러한 패턴 및 규칙을 학습하면 자연스러운 C# 및 .NET을 신속하게 작성할 수 있습니다.

다음으로 .NET의 최신 릴리스에서 이러한 패턴의 일부 변경 내용을 확인합니다.

[다음](modern-events.md)
