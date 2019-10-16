---
title: 콘솔 애플리케이션
description: 이 자습서에서는 .NET Core 및 C# 언어의 다양한 기능에 대해 설명합니다.
ms.date: 03/06/2017
ms.assetid: 883cd93d-50ce-4144-b7c9-2df28d9c11a0
ms.openlocfilehash: 4324b25daa253b3d2446955ad9ca57c2f0294f0c
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70851013"
---
# <a name="console-application"></a>콘솔 애플리케이션

이 자습서에서는 .NET Core 및 C# 언어의 다양한 기능에 대해 설명합니다. 다음을 배울 수 있습니다.

- .NET Core CLI(명령줄 인터페이스)의 기본 사항
- C# 콘솔 애플리케이션의 구조
- 콘솔 I/O
- .NET에 포함된 파일 I/O API의 기본 사항
- .NET에 포함된 작업 비동기 프로그래밍의 기본 사항

텍스트 파일을 읽고 콘솔에 해당 텍스트 파일의 내용을 에코하는 애플리케이션을 빌드해 보겠습니다. 콘솔의 출력은 소리 내어 읽는 속도에 맞춰집니다. ‘<’(보다 작음) 또는 ‘>’(보다 큼) 키를 눌러 속도를 높이거나 낮출 수 있습니다.

이 자습서에는 많은 기능이 있습니다. 하나씩 빌드해 보겠습니다.

## <a name="prerequisites"></a>전제 조건

.NET Core를 실행하도록 컴퓨터에 설정해야 합니다. [.NET Core 다운로드](https://dotnet.microsoft.com/download) 페이지에서 설치 지침을 찾을 수 있습니다. Windows, Linux, macOS 또는 Docker 컨테이너에서 이 애플리케이션을 실행할 수 있습니다.
선호하는 코드 편집기를 설치해야 합니다.

## <a name="create-the-application"></a>애플리케이션 만들기

첫 번째 단계에서는 새 애플리케이션을 만듭니다. 명령 프롬프트를 열고 애플리케이션에 대한 새 디렉터리를 만듭니다. 해당 디렉터리를 현재 디렉터리로 지정합니다. 명령 프롬프트에 명령 `dotnet new console`을 입력합니다. 이렇게 하면 기본 "Hello World" 애플리케이션에 대한 시작 파일이 만들어집니다.

파일 수정을 시작하기 전에 간단한 Hello World 애플리케이션을 실행하는 단계를 진행해 보겠습니다. 애플리케이션을 만든 후에 명령 프롬프트에서 `dotnet restore`를 입력합니다. 이 명령은 NuGet 패키지 복원 프로세스를 실행합니다. NuGet은 .NET 패키지 관리자입니다. 이 명령은 프로젝트에 대한 누락된 종속성 중 하나를 다운로드합니다. 이 프로젝트는 새 프로젝트이므로 어떤 종속성도 없습니다. 따라서 처음 실행하면 .NET Core 프레임워크가 다운로드됩니다. 이 초기 단계 후에 새 종속 패키지를 추가하거나 종속성 버전을 업데이트할 때 `dotnet restore`를 실행하기만 하면 됩니다.

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

패키지를 복원한 후 `dotnet build`를 실행합니다. 이렇게 하면 빌드 엔진이 실행되고 애플리케이션 실행 파일이 만들어집니다. 마지막으로 `dotnet run`을 실행하여 애플리케이션을 실행합니다.

이 간단한 Hello World 애플리케이션 코드은 모두 Program.cs에 있습니다. 원하는 텍스트 편집기를 사용하여 해당 파일을 엽니다. 이제 첫 번째 변경을 수행해 보겠습니다.
파일 맨 위에서 using 문을 보세요.

```csharp
using System;
```

이 문은 `System` 네임스페이스의 모든 형식이 범위 내에 있음을 컴파일러에 알려줍니다. 사용해본 적이 있을 수 다른 개체 지향 언어와 마찬가지로 C#에서도 네임스페이스를 사용하여 형식을 구성합니다. 이 Hello World 프로그램도 다르지 않습니다. 프로그램이 현재 디렉터리의 이름에 기반한 이름으로 네임스페이스에 묶인 것을 볼 수 있습니다. 이 자습서에서는 네임스페이스 이름을 `TeleprompterConsole`로 변경해 보겠습니다.

```csharp
namespace TeleprompterConsole
```

## <a name="reading-and-echoing-the-file"></a>파일 읽기 및 에코

추가할 첫 번째 기능은 텍스트 파일을 읽고 콘솔에 해당 텍스트를 모두 표시하는 기능입니다. 먼저 텍스트 파일을 추가해 보겠습니다. 이 [샘플](https://github.com/dotnet/samples/tree/master/csharp/getting-started/console-teleprompter)에 대한 GitHub 리포지토리의 [sampleQuotes.txt](https://github.com/dotnet/samples/raw/master/csharp/getting-started/console-teleprompter/sampleQuotes.txt) 파일을 프로젝트 디렉터리로 복사합니다. 이 파일은 애플리케이션에 대한 스크립트로 작동합니다. 이 항목에 대한 샘플 앱을 다운로드하는 방법에 대한 정보를 원하는 경우 [샘플 및 자습서](../../samples-and-tutorials/index.md#viewing-and-downloading-samples) 항목의 지침을 참조하세요.

다음에는 다음 메서드를 `Program` 클래스에 추가합니다(`Main` 메서드 바로 아래).

```csharp
static IEnumerable<string> ReadFrom(string file)
{
    string line;
    using (var reader = File.OpenText(file))
    {
        while ((line = reader.ReadLine()) != null)
        {
            yield return line;
        }
    }
}
```

이 메서드는 두 개의 새 네임스페이스에 있는 형식을 사용합니다. 이를 컴파일하려면 파일 맨 위에 다음 두 줄을 추가해야 합니다.

```csharp
using System.Collections.Generic;
using System.IO;
```

<xref:System.Collections.Generic.IEnumerable%601> 인터페이스는 <xref:System.Collections.Generic> 네임스페이스에 정의되어 있습니다. <xref:System.IO.File> 클래스는 <xref:System.IO> 네임스페이스에 있습니다.

이 메서드는 *반복기 메서드*라는 특수한 형식의 C# 메서드입니다. 열거자 메서드는 지연 계산되는 시퀀스를 반환합니다. 즉, 시퀀스의 각 항목은 시퀀스를 사용하는 코드에서 요청된 것처럼 생성됩니다. 열거자 메서드는 하나 이상의 [`yield return`](../language-reference/keywords/yield.md) 문을 포함하는 메서드입니다. `ReadFrom` 메서드에서 반환된 개체는 시퀀스의 각 항목을 생성하는 코드를 포함합니다. 이 예제에서는 소스 파일에서 다음 텍스트 줄을 읽고 해당 문자열을 반환하는 코드에 해당합니다. 호출하는 코드가 시퀀스에서 다음 항목을 요청할 때마다 코드는 파일에서 다음 텍스트 줄을 읽고 반환합니다. 파일이 완전히 읽히면 시퀀스는 더 이상 항목이 없음을 나타냅니다.

여러분에게 생소할 수 있는 두 개의 다른 C# 구문 요소가 있습니다. 이 메서드의 [`using`](../language-reference/keywords/using-statement.md) 문은 리소스 정리를 관리합니다. `using` 문(이 예제의 `reader`)에서 초기화되는 변수는 <xref:System.IDisposable> 인터페이스를 구현해야 합니다. 이 인터페이스는 리소스를 해제해야 할 때 호출되어야 하는 단일 메서드 `Dispose`를 정의합니다. 컴파일러는 실행 중에 `using` 문의 닫는 중괄호에 도달하면 해당 호출을 생성합니다. 컴파일러에서 생성된 코드는 using 문으로 정의된 블록의 코드에서 예외가 throw되더라도 리소스가 해제되도록 합니다.

`reader` 변수는 `var` 키워드를 사용하여 정의됩니다. [`var`](../language-reference/keywords/var.md)은 *암시적으로 형식화한 지역 변수*를 정의합니다. 즉, 변수의 형식이 변수에 할당된 개체의 컴파일 시간 형식에 의해 결정됩니다. 여기서는 <xref:System.IO.StreamReader> 개체에 해당하는 <xref:System.IO.File.OpenText(System.String)> 메서드의 반환 값입니다.

이제 `Main` 메서드에서 파일을 읽는 코드를 채웁니다.

```csharp
var lines = ReadFrom("sampleQuotes.txt");
foreach (var line in lines)
{
    Console.WriteLine(line);
}
```

프로그램을 실행(`dotnet run` 사용)하면 모든 줄이 콘솔에 출력되는 것을 볼 수 있습니다.

## <a name="adding-delays-and-formatting-output"></a>지연 추가 및 출력 서식 지정

결과가 너무 빨리 표시되어 큰 표시로 읽을 수 없습니다. 이제 출력에 지연을 추가해야 합니다. 처음에는 비동기 처리를 가능하게 하는 일부 코어 코드를 빌드합니다. 그러나 이러한 첫 번째 단계는 몇 가지 안티 패턴을 따르게 됩니다. 안티 패턴은 코드를 추가할 때 주석에 표시되며 코드는 이후 단계에서 업데이트됩니다.

이 섹션에는 두 단계가 있습니다. 먼저 전체 줄이 아니라 단일 단어를 반환하는 반복기 메서드를 업데이트하게 됩니다. 이 작업은 다음과 같이 수정하면 수행됩니다. `yield return line;` 문을 다음 코드로 바꿉니다.

```csharp
var words = line.Split(' ');
foreach (var word in words)
{
    yield return word + " ";
}
yield return Environment.NewLine;
```

다음에는 해당 파일 줄을 사용하는 방법을 수정하고 각 단어를 쓴 후에 지연을 추가합니다. `Main` 메서드의 `Console.WriteLine(line)` 문을 다음 블록으로 바꿉니다.

```csharp
Console.Write(line);
if (!string.IsNullOrWhiteSpace(line))
{
    var pause = Task.Delay(200);
    // Synchronously waiting on a task is an
    // anti-pattern. This will get fixed in later
    // steps.
    pause.Wait();
}
```

<xref:System.Threading.Tasks.Task> 클래스는 <xref:System.Threading.Tasks> 네임스페이스에 있으므로 해당 `using` 문을 파일 맨 위에 추가해야 합니다.

```csharp
using System.Threading.Tasks;
```

샘플을 실행하고 출력을 확인합니다. 이제 개별 단어가 출력되고 200밀리초의 지연이 발생합니다. 그러나 표시된 출력은 소스 텍스트 파일이 줄 바꿈 없는 80자 이상을 포함하는 여러 줄로 구성되므로 몇 가지 문제를 나타냅니다. 스크롤하면서 읽기 어려울 수 있습니다. 이 문제는 쉽게 해결할 수 있습니다. 각 줄의 길이를 추적하고 줄 길이가 특정 임계값에 도달할 때마다 새 줄을 생성하도록 하면 됩니다. 줄 길이를 포함하는 `ReadFrom` 메서드의 `words` 선언 다음에 지역 변수를 선언합니다.

```csharp
var lineLength = 0;
```

그런 후 `yield return word + " ";` 문 뒤에(닫는 중괄호 이전) 다음 코드를 추가합니다.

```csharp
lineLength += word.Length + 1;
if (lineLength > 70)
{
    yield return Environment.NewLine;
    lineLength = 0;
}
```

샘플을 실행하면 미리 구성된 속도로 크게 읽을 수 있습니다.

## <a name="async-tasks"></a>비동기 작업

이 마지막 단계에서는 텍스트 표시 속도를 높이거나 낮추려는 경우 또는 텍스트 표시를 완전히 중지하려는 경우 사용자로부터 입력을 읽는 작업을 실행하면서 다른 작업에서 비동기적으로 출력을 쓰는 코드를 추가합니다. 이 과정은 몇 가지 단계로 진행되며 마지막에 필요한 모든 업데이트가 수행됩니다.
첫 번째 단계는 지금까지 파일을 읽고 표시하기 위해 만든 코드를 나타내는 비동기 <xref:System.Threading.Tasks.Task> 반환 메서드를 만드는 것입니다.

이 메서드를 `Program` 클래스(`Main` 메서드 본문에서 가져옴)에 추가합니다.

```csharp
private static async Task ShowTeleprompter()
{
    var words = ReadFrom("sampleQuotes.txt");
    foreach (var word in words)
    {
        Console.Write(word);
        if (!string.IsNullOrWhiteSpace(word))
        {
            await Task.Delay(200);
        }
    }
}
```

두 가지가 변경된 것을 알 수 있습니다. 첫째, 이 버전은 메서드 본문에서 <xref:System.Threading.Tasks.Task.Wait> 를 호출하여 작업이 완료되기를 동기식으로 대기하지 않고, `await` 키워드를 사용합니다. 이 작업을 수행하기 위해 메서드 시그니처에 `async` 한정자를 추가해야 합니다. 이 메서드는 `Task`를 반환합니다. `Task` 개체를 반환하는 Return 문은 없습니다. 대신, `Task` 개체는 `await` 연산자를 사용할 때 컴파일러가 생성하는 코드에 의해 만들어집니다. `await`에 도달하면 이 메서드가 반환되는 것을 상상할 수 있습니다. 반환된 `Task`는 작업이 완료되지 않았음을 나타냅니다.
이 메서드는 대기 중인 작업이 완료되면 다시 시작됩니다. 실행되어 완료되면 반환된 `Task`는 완료되었음을 나타냅니다.
호출하는 코드는 반환된 `Task`를 모니터링하여 완료되었는지 확인합니다.

`Main` 메서드에서 다음 새 메서드를 호출할 수 있습니다.

```csharp
ShowTeleprompter().Wait();
```

여기 `Main`에서 코드는 동기적으로 대기합니다. 가능한 경우 동기적으로 대기하는 대신 `await` 연산자를 사용하는 것이 좋습니다. 그러나 콘솔 애플리케이션의 `Main` 메서드에서는 `await` 연산자를 사용할 수 없습니다. 결과적으로 모든 작업을 완료하기 전에 애플리케이션이 종료됩니다.

> [!NOTE]
> C# 7.1 이상을 사용하는 경우 [`async``Main` 메서드](../whats-new/csharp-7-1.md#async-main)로 콘솔 애플리케이션을 만들 수 있습니다.

다음에는 콘솔에서 읽는 두 번째 비동기 메서드를 작성하고 ‘<’(보다 작음), ‘>’(보다 큼) 및 ‘X’ 또는 ‘x’ 키를 확인해야 합니다. 해당 작업에 대해 추가하는 메서드는 다음과 같습니다.

```csharp
private static async Task GetInput()
{
    var delay = 200;
    Action work = () =>
    {
        do {
            var key = Console.ReadKey(true);
            if (key.KeyChar == '>')
            {
                delay -= 10;
            }
            else if (key.KeyChar == '<')
            {
                delay += 10;
            }
            else if (key.KeyChar == 'X' || key.KeyChar == 'x')
            {
                break;
            }
        } while (true);
    };
    await Task.Run(work);
}
```

이 메서드는 콘솔에서 키를 읽고 사용자가 ‘<’(보다 작음) 또는 ‘>’(보다 큼) 키를 누를 때 지연을 나타내는 지역 변수를 수정하는 <xref:System.Action> 대리자를 나타내는 람다 식을 만듭니다. 사용자가 ‘X’ 또는 ‘x’ 키를 누를 때 대리자 메서드가 완료되면 사용자가 언제든지 텍스트 표시를 중지할 수 있습니다.
이 메서드는 <xref:System.Console.ReadKey> 를 사용하여 차단한 후 사용자가 키를 누를 때까지 기다립니다.

이 기능을 완료하려면 이러한 두 작업(`GetInput` 및 `ShowTeleprompter`)을 시작하고 이러한 두 작업 간에 공유 데이터를 관리하는 새 `async Task` 반환 메서드를 만들어야 합니다.

이러한 두 작업 간에 공유 데이터를 처리할 수 있는 클래스를 만들 차례입니다. 이 클래스에는 두 개의 공용 속성, 즉 지연과 파일이 완전히 읽혔음을 나타내는 `Done` 플래그가 포함됩니다.

```csharp
namespace TeleprompterConsole
{
    internal class TelePrompterConfig
    {
        public int DelayInMilliseconds { get; private set; } = 200;

        public void UpdateDelay(int increment) // negative to speed up
        {
            var newDelay = Min(DelayInMilliseconds + increment, 1000);
            newDelay = Max(newDelay, 20);
            DelayInMilliseconds = newDelay;
        }

        public bool Done { get; private set; }

        public void SetDone()
        {
            Done = true;
        }
    }
}
```

해당 클래스를 새 파일에 추가하고 위와 같이 `TeleprompterConsole` 네임스페이스에 클래스를 포함합니다. 또한 바깥쪽 클래스 또는 네임스페이스 이름 없이 `Min` 및 `Max` 메서드를 참조할 수 있도록 `using static` 문을 추가해야 합니다. [`using static`](../language-reference/keywords/using-static.md) 문은 하나의 클래스에서 메서드를 가져옵니다. 이것은 네임스페이스에서 모든 클래스를 가져오는 지금까지 사용했던 `using` 문과는 반대됩니다.

```csharp
using static System.Math;
```

다음에는 새 `config` 개체를 사용하도록 `ShowTeleprompter` 및 `GetInput` 메서드를 업데이트해야 합니다. 두 작업을 모두 시작한 다음 첫 번째 작업이 완료될 때 종료되는 하나의 최종 `Task` 반환 `async` 메서드를 작성합니다.

```csharp
private static async Task RunTeleprompter()
{
    var config = new TelePrompterConfig();
    var displayTask = ShowTeleprompter(config);

    var speedTask = GetInput(config);
    await Task.WhenAny(displayTask, speedTask);
}
```

여기서 한 가지 새로운 메서드가 <xref:System.Threading.Tasks.Task.WhenAny(System.Threading.Tasks.Task[])> 호출입니다. 그러면 인수 목록의 모든 작업이 완료되는 즉시 완료되는 `Task`가 만들어집니다.

다음에는 지연을 위해 `config` 개체를 사용하도록 `ShowTeleprompter` 및 `GetInput` 메서드를 모두 업데이트해야 합니다.

```csharp
private static async Task ShowTeleprompter(TelePrompterConfig config)
{
    var words = ReadFrom("sampleQuotes.txt");
    foreach (var word in words)
    {
        Console.Write(word);
        if (!string.IsNullOrWhiteSpace(word))
        {
            await Task.Delay(config.DelayInMilliseconds);
        }
    }
    config.SetDone();
}

private static async Task GetInput(TelePrompterConfig config)
{
    Action work = () =>
    {
        do {
            var key = Console.ReadKey(true);
            if (key.KeyChar == '>')
                config.UpdateDelay(-10);
            else if (key.KeyChar == '<')
                config.UpdateDelay(10);
            else if (key.KeyChar == 'X' || key.KeyChar == 'x')
                config.SetDone();
        } while (!config.Done);
    };
    await Task.Run(work);
}
```

이 새 버전의 `ShowTeleprompter`는 `TeleprompterConfig` 클래스에서 새 메서드를 호출합니다. 이제 `ShowTeleprompter` 대신 `RunTeleprompter`를 호출하도록 `Main`을 업데이트해야 합니다.

```csharp
RunTeleprompter().Wait();
```

## <a name="conclusion"></a>결론

이 자습서에서는 콘솔 애플리케이션 사용과 관련된 다양한 C# 언어 및 .NET Core 라이브러리 기능을 살펴보았습니다.
이 지식을 토대로 해당 언어 및 여기서 소개된 클래스에 대해 좀 더 자세히 알아볼 수 있습니다. 지금까지 파일 및 콘솔 I/O 기본 사항, 작업 기반 비동기 프로그래밍의 차단 및 비차단 사용, C# 언어 둘러보기, C# 프로그램이 구성되는 방식, .NET Core 명령줄 인터페이스 및 도구에 대해 살펴보았습니다.

파일 I/O에 대한 자세한 내용은 [파일 및 스트림 I/O](../../standard/io/index.md) 항목을 참조하세요. 이 자습서에서 사용된 비동기 프로그래밍 모델에 대한 자세한 내용은 [작업 기반 비동기 프로그래밍](../..//standard/parallel-programming/task-based-asynchronous-programming.md) 항목 및 [비동기 프로그래밍](../async.md) 항목을 참조하세요.
