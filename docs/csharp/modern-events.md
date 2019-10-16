---
title: 업데이트된 .NET Core 이벤트 패턴
description: .NET Core 이벤트 패턴을 통해 이전 버전과의 호환성을 유연하게 사용하는 방법 및 비동기 구독자로 안전한 이벤트 처리를 구현하는 방법을 알아봅니다.
ms.date: 06/20/2016
ms.assetid: 9aa627c3-3222-4094-9ca8-7e88e1071e06
ms.openlocfilehash: 158295215932f54c75afdf1e96d48453434129fe
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64751777"
---
# <a name="the-updated-net-core-event-pattern"></a>업데이트된 .NET Core 이벤트 패턴

[이전](event-pattern.md)

이전 문서에서는 가장 일반적인 이벤트 패턴을 설명했습니다. .NET Core에는 보다 완화된 패턴이 있습니다. 이 버전에서는 `EventHandler<TEventArgs>` 정의에 `TEventArgs`가 `System.EventArgs`에서 파생된 클래스여야 한다는 제약 조건이 더 이상 없습니다.

이 때문에 유연성이 증가하고 이전 버전과 호환됩니다. 유연성부터 살펴보겠습니다. System.EventArgs 클래스는 개체의 부분 복사본을 만드는 `MemberwiseClone()` 메서드 하나를 소개합니다.
이 메서드는 `EventArgs`에서 파생된 클래스에 대해 해당 기능을 구현하기 위해 리플렉션을 사용해야 합니다. 특정 파생 클래스에서는 해당 기능을 더 쉽게 만들 수 있습니다. 이는 System.EventArgs에서 파생되는 것이 디자인을 제한하는 제약 조건이지만 추가적인 혜택은 없음을 의미합니다.
실제로 `EventArgs`에서 파생되지 않도록 `FileFoundArgs` 및 `SearchDirectoryArgs`의 정의를 변경할 수 있습니다.
프로그램은 동일하게 작동합니다.

한 가지 더 변경하는 경우 `SearchDirectoryArgs`를 구조체로 변경할 수 있습니다.

```csharp
internal struct SearchDirectoryArgs
{
    internal string CurrentSearchDirectory { get; }
    internal int TotalDirs { get; }
    internal int CompletedDirs { get; }

    internal SearchDirectoryArgs(string dir, int totalDirs, int completedDirs) : this()
    {
        CurrentSearchDirectory = dir;
        TotalDirs = totalDirs;
        CompletedDirs = completedDirs;
    }
}
```

추가 변경은 모든 필드를 초기화하는 생성자를 입력하기 전에 매개 변수 없는 생성자를 호출하는 것입니다. 해당 코드를 추가하지 않으면 C#의 규칙에서 속성이 할당되기 전에 액세스된다고 보고합니다.

`FileFoundArgs`를 클래스(참조 형식)에서 구조체(값 형식)로 변경하면 안 됩니다. 이는 취소를 처리하기 위한 프로토콜에서 이벤트 인수가 참조로 전달되도록 요구하기 때문입니다. 동일한 변경을 수행하면 파일 검색 클래스가 이벤트 구독자의 변경 내용을 관찰할 수 없습니다. 구조체의 새 복사본이 각 구독자에 사용되며, 해당 복사본은 파일 검색 개체에 표시되는 것과는 다른 복사본입니다.

다음으로, 이러한 변경 내용이 이전 버전과 호환될 수 방법을 살펴보겠습니다.
제약 조건을 제거해도 기존 코드에는 영향을 주지 않습니다. 기존 이벤트 인수 형식은 여전히 `System.EventArgs`에서 파생됩니다.
이전 버전과의 호환성은 `System.EventArgs`에서 계속 파생되는 한 가지 주요 이유입니다. 기존 이벤트 구독자는 클래식 패턴을 따르는 이벤트의 구독자가 됩니다.

유사한 논리에 따라 이제 생성되는 이벤트 인수 형식은 기존 코드베이스에 구독자가 없습니다. `System.EventArgs`에서 파생되지 않는 새 이벤트 유형은 이러한 코드베이스를 중단하지 않습니다.

## <a name="events-with-async-subscribers"></a>비동기 구독자가 포함된 이벤트

학습할 하나의 최종 패턴이 있습니다. 비동기 코드를 호출하는 이벤트 구독자를 올바르게 작성하는 방법입니다. 이 과제는 [async 및 await](async.md)에 대한 문서에서 설명합니다. 비동기 메서드의 반환 형식이 void일 수도 있지만 권장되지는 않습니다. 이벤트 구독자 코드에서 비동기 메서드를 호출하는 경우 `async void` 메서드를 만들 수밖에 없습니다. 이벤트 처리기 시그니처에 이 메서드가 필요합니다.

이 반대 지침을 조정해야 합니다. 어떻게 해서든 안전한 `async void` 메서드를 만들어야 합니다. 구현해야 하는 패턴의 기본 사항은 아래와 같습니다.

```csharp
worker.StartWorking += async (sender, eventArgs) =>
{
    try 
    {
        await DoWorkAsync();
    }
    catch (Exception e)
    {
        //Some form of logging.
        Console.WriteLine($"Async task failure: {e.ToString()}");
        // Consider gracefully, and quickly exiting.
    }
};
```

첫째, 처리기는 비동기 처리기로 표시됩니다. 이벤트 처리기 대리자 형식에 할당되므로 void 반환 형식을 갖습니다. 즉, 처리기에 표시된 패턴을 따르고 비동기 처리기의 컨텍스트 외부에서 예외가 throw되지 않도록 해야 합니다. 작업을 반환하지 않으므로 오류 상태를 입력하여 오류를 보고할 수 있는 작업이 없습니다. 메서드가 비동기이므로 메서드에서 단순히 예외를 throw할 수 없습니다. 호출하는 메서드가 `async`이므로 실행을 계속했습니다. 실제 런타임 동작은 각 환경마다 다르게 정의됩니다. 스레드를 종료하거나, 프로그램을 종료하거나, 프로그램을 결정되지 않은 상태로 둘 수 있습니다. 모두 좋은 결과는 아닙니다.

이 때문에 비동기 작업에 대한 await 문을 고유한 try 블록에 래핑해야 합니다. 오류 작업이 발생하는 경우 오류를 기록할 수 있습니다. 애플리케이션이 복구할 수 없는 오류인 경우 빠르고 정상적으로 프로그램을 종료할 수 있습니다.

이러한 기능은 .NET 이벤트 패턴에 대한 주요 업데이트입니다. 작업할 라이브러리에 이전 버전의 예제가 많이 표시됩니다. 그러나 최신 패턴이 무엇인지도 이해해야 합니다.

이 시리즈의 다음 문서는 디자인에 `delegates`를 사용하는 경우와 `events`를 사용하는 경우를 구분하는 데 도움이 됩니다. 비슷한 개념이며 해당 문서를 통해 프로그램에 대한 최상의 결정을 내릴 수 있습니다.

[다음](distinguish-delegates-events.md)
