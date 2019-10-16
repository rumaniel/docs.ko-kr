---
title: Memory<T> 및 Span<T> 사용 지침
ms.date: 10/01/2018
helpviewer_keywords:
- Memory&lt;T&gt; and Span&lt;T&gt; best practices
- using Memory&lt;T&gt; and Span&lt;T&gt;
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 171f6fd5a8b55d2e96a90a90d011a8166be6759d
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666407"
---
# <a name="memoryt-and-spant-usage-guidelines"></a>Memory\<T> 및 Span\<T> 사용 지침

.NET Core에는 메모리의 인접한 임의 영역을 나타내는 여러 형식이 포함되어 있습니다. .NET Core 2.0에서는 관리형 또는 비관리형 메모리로 지원할 수 있는 경량 메모리 버퍼인 <xref:System.Span%601> 및 <xref:System.ReadOnlySpan%601>이 도입되었습니다. 이러한 형식은 스택에만 저장될 수 있기 때문에 비동기 메서드 호출을 포함한 여러 시나리오에 적합하지 않습니다. .NET Core 2.1에서는 <xref:System.Memory%601>, <xref:System.ReadOnlyMemory%601>, <xref:System.Buffers.IMemoryOwner%601> 및 <xref:System.Buffers.MemoryPool%601>을 포함한 여러 형식이 추가되었습니다. <xref:System.Span%601>과 마찬가지로, <xref:System.Memory%601> 및 관련 형식은 관리형 및 비관리형 메모리 둘 다로 지원할 수 있습니다. <xref:System.Span%601>과 달리, <xref:System.Memory%601>는 관리형 힙에 저장할 수 있습니다.

<xref:System.Span%601> 및 <xref:System.Memory%601>는 둘 다 파이프라인에 사용할 수 있는 구조적 데이터의 버퍼입니다. 즉, 일부 또는 모든 데이터가 파이프라인의 구성 요소에 효율적으로 전달될 수 있도록 설계되었으며, 해당 구성 요소는 데이터를 처리하고 선택적으로 버퍼를 수정할 수 있습니다. <xref:System.Memory%601> 및 관련 형식은 여러 구성 요소나 여러 스레드에서 액세스할 수 있으므로 개발자가 몇 가지 표준 사용법 지침에 따라 강력한 코드를 생성하는 것이 중요합니다.

## <a name="owners-consumers-and-lifetime-management"></a>소유자, 소비자 및 수명 관리

API 간에 버퍼를 전달할 수 있으며, 때때로 여러 스레드에서 버퍼에 액세스할 수 있으므로 수명 관리를 고려하는 것이 중요합니다. 다음 세 가지 핵심 개념이 있습니다.

- **소유권**. 버퍼 인스턴스의 소유자는 더 이상 사용하지 않는 버퍼 삭제를 포함하여 수명 관리를 책임집니다. 모든 버퍼에 단일 소유자가 있습니다. 일반적으로 소유자는 버퍼를 만들었거나 팩터리에서 버퍼를 수신한 구성 요소입니다. 소유권을 양도할 수도 있습니다. **Component-A**가 버퍼 제어를 **Component-B**에 양도할 수 있으며, 이 시점부터 **Component-A**는 더 이상 버퍼를 사용할 수 없고 **Component-B**가 더 이상 사용하지 않는 버퍼 삭제를 책임집니다.

- **소비**. 버퍼 인스턴스의 소비자는 버퍼 인스턴스를 읽고 써서 사용할 수 있습니다. 외부 동기화 메커니즘을 제공하지 않으면 버퍼는 한 번에 하나의 소비자를 가질 수 있습니다. 버퍼의 활성 소비자는 버퍼의 소유자가 아니어도 됩니다.

- **임대 시간**. 임대 시간은 특정 구성 요소가 버퍼의 소비자가 될 수 있는 기간입니다.

다음 의사 코드 예제에서는 이러한 세 가지 개념을 보여 줍니다. <xref:System.Char> 형식의 <xref:System.Memory%601> 버퍼를 인스턴스화하는 `Main` 메서드를 포함하고, `WriteInt32ToBuffer` 메서드를 호출하여 정수의 문자열 표현을 버퍼에 쓴 다음, `DisplayBufferToConsole` 메서드를 호출하여 버퍼의 값을 표시합니다.

```csharp
using System;

class Program
{
    // Write 'value' as a human-readable string to the output buffer.
    void WriteInt32ToBuffer(int value, Buffer buffer);

    // Display the contents of the buffer to the console.
    void DisplayBufferToConsole(Buffer buffer);

    // Application code
    static void Main()
    {
        var buffer = CreateBuffer();
        try
        {
            int value = Int32.Parse(Console.ReadLine());
            WriteInt32ToBuffer(value, buffer);
            DisplayBufferToConsole(buffer);
        }
        finally
        {
            buffer.Destroy();
        }
    }
}
```

`Main` 메서드가 버퍼(이 경우 <xref:System.Span%601> 인스턴스)를 만들기 때문에 해당 소유자입니다. 따라서 `Main`이 더 이상 사용하지 않는 버퍼 삭제를 책임집니다. 이 메서드는 버퍼의 <xref:System.Span%601.Clear?displayProperty=nameWithType> 메서드를 호출하여 삭제 작업을 수행합니다. 여기서는 <xref:System.Span%601.Clear> 메서드가 실제로 메모리를 지웁니다. <xref:System.Span%601> 구조체에는 실제로 버퍼를 삭제하는 메서드가 없습니다.

버퍼에는 두 개의 소비자 `WriteInt32ToBuffer` 및 `DisplayBufferToConsole`이 있습니다. 한 번에 하나의 소비자만 있고(`WriteInt32ToBuffer`, `DisplayBufferToConsole` 순), 두 소비자 모두 버퍼를 소유하지 않습니다. 또한 이 컨텍스트의 “소비자”는 버퍼의 읽기 전용 보기를 암시하지 않습니다. 버퍼의 읽기/쓰기 보기가 제공되면 `WriteInt32ToBuffer`와 같이 소비자가 버퍼 내용을 수정할 수 있습니다.

`WriteInt32ToBuffer` 메서드는 메서드 호출 시작과 메서드가 반환되는 시간 사이에 버퍼를 임대합니다(사용할 수 있음). 마찬가지로, `DisplayBufferToConsole`은 버퍼가 실행되는 동안 버퍼를 임대하고, 메서드가 해제되면 임대가 해제됩니다. 임대 관리에 대한 API는 없습니다. “임대”는 개념적 용어입니다.

## <a name="memoryt-and-the-ownerconsumer-model"></a>Memory\<T> 및 소유자/소비자 모델

[소유자, 소비자 및 수명 관리](#owners-consumers-and-lifetime-management) 섹션에 설명된 대로, 버퍼에는 항상 하나의 소유자가 있습니다. .NET Core는 다음 두 가지 소유권 모델을 지원합니다.

- 단일 소유권을 지원하는 모델. 전체 수명 동안 버퍼에 단일 소유자가 있습니다.

- 소유권 이전을 지원하는 모델. 버퍼의 소유권을 원래 소유자(생성자)에서 다른 구성 요소로 양도할 수 있으며, 그 후에는 해당 구성 요소가 버퍼의 수명 관리를 책임집니다. 이 소유자는 다시 소유권을 다른 구성 요소에 이전할 수 있습니다.

<xref:System.Buffers.IMemoryOwner%601?displayProperty=nameWithType> 인터페이스를 사용하여 버퍼의 소유권을 명시적으로 관리합니다. <xref:System.Buffers.IMemoryOwner%601>는 두 소유권 모델을 모두 지원합니다. <xref:System.Buffers.IMemoryOwner%601> 참조가 있는 구성 요소가 버퍼를 소유합니다. 다음 예제에서는 <xref:System.Buffers.IMemoryOwner%601?> 인스턴스를 사용하여 <xref:System.Memory%601> 버퍼의 소유권을 반영합니다.

[!code-csharp[ownership](~/samples/snippets/standard/buffers/memory-t/owner/owner.cs)]

[`using`](../../csharp/language-reference/keywords/using-statement.md)을 사용하여 이 예제를 작성할 수도 있습니다.

[!code-csharp[ownership-using](~/samples/snippets/standard/buffers/memory-t/owner-using/owner-using.cs)]

이 코드에서는 다음과 같습니다.

- `Main` 메서드에 <xref:System.Buffers.IMemoryOwner%601> 인스턴스에 대한 참조가 있으므로 `Main` 메서드가 버퍼의 소유자입니다.

- `WriteInt32ToBuffer` 및 `DisplayBufferToConsole` 메서드는 공용 API로 <xref:System.Memory%601>를 수락합니다. 따라서 버퍼의 소비자가 됩니다. 또한 한 번에 하나씩 버퍼를 사용합니다.

`WriteInt32ToBuffer` 메서드는 버퍼에 값을 쓰기 위한 것이지만 `DisplayBufferToConsole` 메서드는 그렇지 않습니다. 이를 반영하기 위해 <xref:System.ReadOnlyMemory%601> 형식의 인수를 허용했을 수 있습니다. <xref:System.ReadOnlyMemory%601>에 대한 자세한 내용은 [규칙 #2: 버퍼가 읽기 전용이어야 하는 경우 ReadOnlySpan\<T> 또는 ReadOnlyMemory\<T> 사용](#rule-2)을 참조하세요.

### <a name="ownerless-memoryt-instances"></a>“소유자가 없는” Memory\<T> 인스턴스

<xref:System.Buffers.IMemoryOwner%601>를 사용하지 않고 <xref:System.Memory%601> 인스턴스를 만들 수 있습니다. 이 경우 버퍼의 소유권은 명시적이 아니라 암시적이며 단일 소유자 모델만 지원됩니다. 이렇게 하려면 다음을 수행합니다.

- 다음 예제와 같이 `T[]`를 전달하여 <xref:System.Memory%601> 생성자 중 하나를 직접 호출합니다.

- [String.AsMemory](xref:System.MemoryExtensions.AsMemory(System.String)) 확장 메서드를 호출하여 `ReadOnlyMemory<char>` 인스턴스를 생성합니다.

[!code-csharp[ownerless-memory](~/samples/snippets/standard/buffers/memory-t/ownerless/ownerless.cs)]

처음에 <xref:System.Memory%601> 인스턴스를 만드는 메서드가 버퍼의 암시적 소유자입니다. 이전을 지원하는 <xref:System.Buffers.IMemoryOwner%601> 인스턴스가 없으므로 소유권을 다른 구성 요소에 이전할 수 없습니다. 또는 런타임의 가비지 수집기가 버퍼를 소유하고, 모든 메서드는 버퍼를 사용하기만 한다고 가정할 수도 있습니다.

## <a name="usage-guidelines"></a>사용 지침

메모리 블록은 소유되지만 여러 구성 요소에 전달되고, 이 중에서 일부가 특정 메모리 블록에서 동시에 작업할 수 있기 때문에 <xref:System.Memory%601> 및 <xref:System.Span%601> 사용 방법에 대한 지침을 설정하는 것이 중요합니다.  지침이 필요한 이유는 다음과 같습니다.

- 소유자가 해제한 후에도 구성 요소가 메모리 블록에 대한 참조를 유지할 수 있습니다.

- 다른 구성 요소가 작업 중인 버퍼에 대해 구성 요소가 동시에 작업하여 버퍼의 데이터가 손상될 수 있습니다.

- <xref:System.Span%601>의 스택 할당 특성은 성능을 최적화하고 <xref:System.Span%601>을 메모리 블록에서 작업하는 기본 형식으로 설정하는 반면, <xref:System.Span%601>에 몇 가지 주요 제한 사항이 적용되게도 합니다. <xref:System.Span%601>을 사용해야 하는 경우와 <xref:System.Memory%601>를 사용해야 하는 경우를 아는 것이 중요합니다.

다음은 <xref:System.Memory%601> 및 관련 형식을 성공적으로 사용하기 위한 권장 사항입니다. <xref:System.Memory%601> 및 <xref:System.Span%601>에 적용되는 지침은 명시적으로 달리 언급되지 않는 한 <xref:System.ReadOnlyMemory%601> 및 <xref:System.ReadOnlySpan%601>에도 적용됩니다.

**규칙 #1: 동기 API의 경우 가능하면 Memory\<T> 대신 Span\<T>를 매개 변수로 사용합니다.**

<xref:System.Span%601>은 <xref:System.Memory%601>보다 유연하며 더 광범위한 인접한 메모리 버퍼를 나타낼 수 있습니다. 또한 <xref:System.Span%601>은 <xref:System.Memory%601>보다 나은 성능을 제공합니다. 마지막으로, <xref:System.Memory%601.Span?displayProperty=nameWithType> 속성을 사용하여 <xref:System.Memory%601> 인스턴스를 <xref:System.Span%601>으로 변환할 수 있습니다. 단, Span\<T>-Memory\<T> 변환은 불가능합니다. 따라서 호출자에게 <xref:System.Memory%601> 인스턴스가 있는 경우 <xref:System.Span%601> 매개 변수를 사용하여 메서드를 호출할 수 있습니다.

<xref:System.Memory%601> 형식 대신 <xref:System.Span%601> 형식의 매개 변수를 사용하면 올바른 소비 메서드 구현을 작성하는 데에도 도움이 됩니다. 메서드의 임대 기간을 지나서 버퍼에 액세스를 시도하지 않는지 확인하기 위해 자동으로 컴파일 시간 검사가 수행됩니다(뒷부분에서 자세히 설명).

때로는 완전히 동기인 경우에도 <xref:System.Span%601> 매개 변수 대신 <xref:System.Memory%601> 매개 변수를 사용해야 합니다. 사용하는 API가 <xref:System.Memory%601> 인수만 허용하는 경우도 있습니다. 이 동작은 정상적이지만, <xref:System.Memory%601>를 동기적으로 사용하는 경우 관련된 절충에 유의해야 합니다.

<a name="rule-2" />

**규칙 #2: 버퍼가 읽기 전용이어야 하는 경우 ReadOnlySpan\<T> 또는 ReadOnlyMemory\<T>를 사용합니다.**

앞의 예제에서 `DisplayBufferToConsole` 메서드는 버퍼에서 읽기만 하고 버퍼 내용을 수정하지 않습니다. 메서드 시그니처를 다음으로 변경해야 합니다.

```csharp
void DisplayBufferToConsole(ReadOnlyMemory<char> buffer);
```

실제로 이 규칙과 규칙 #1을 결합하면 더 나은 결과를 얻을 수 있으며, 다음과 같이 메서드 시그니처를 다시 작성할 수 있습니다.

```csharp
void DisplayBufferToConsole(ReadOnlySpan<char> buffer);
```

이제 `DisplayBufferToConsole` 메서드는 `T[]`, [stackalloc](../../csharp/language-reference/operators/stackalloc.md)로 할당된 스토리지 등 거의 모든 버퍼 형식에서 작동합니다. 이 메서드에 <xref:System.String>을 직접 전달할 수도 있습니다.

**규칙 #3: 메서드가 Memory\<T>를 사용하고 `void`를 반환하는 경우 메서드가 반환된 후에는 Memory\<T> 인스턴스를 사용하면 안 됩니다.**

이 내용은 앞에서 언급한 “임대 기간” 개념과 관련이 있습니다. <xref:System.Memory%601> 인스턴스에 대한 void 반환 메서드의 임대 기간은 메서드가 시작될 때 시작되고 메서드가 종료될 때 종료됩니다. 콘솔의 입력에 따라 루프에서 `Log`를 호출하는 다음 예제를 고려해 보세요.

[!code-csharp[void-returning](~/samples/snippets/standard/buffers/memory-t/void-returning/void-returning.cs#1)]

`Log`가 완전히 동기 메서드인 경우에는 메모리 인스턴스의 활성 소비자가 항상 하나뿐이므로 이 코드가 예상대로 작동합니다.
그러나 `Log`에 이 구현이 있다고 가정해 보겠습니다.

```csharp
// !!! INCORRECT IMPLEMENTATION !!!
static void Log(ReadOnlyMemory<char> message)
{
    // Run in background so that we don't block the main thread while performing IO.
    Task.Run(() =>
    {
        StreamWriter sw = File.AppendText(@".\input-numbers.dat");
        sw.WriteLine(message);
    });
}
```

이 구현에서 `Log`는 원래 메서드가 반환된 후에도 백그라운드에서 <xref:System.Memory%601> 인스턴스를 계속 사용하려고 시도하기 때문에 해당 임대 기간을 위반합니다. `Log`가 읽는 동안 `Main` 메서드가 버퍼를 변경할 수 있으며, 이로 인해 데이터가 손상될 수 있습니다.

이 문제를 해결하는 몇 가지 방법은 다음과 같습니다.

- 다음과 같은 `Log` 메서드 구현처럼, `Log` 메서드가 `void` 대신 <xref:System.Threading.Tasks.Task>를 반환할 수 있습니다.

   [!code-csharp[task-returning](~/samples/snippets/standard/buffers/memory-t/task-returning2/task-returning2.cs#1)]

- 다음과 같이 `Log`를 구현할 수 있습니다.

   [!code-csharp[defensive-copy](~/samples/snippets/standard/buffers/memory-t/task-returning/task-returning.cs#1)]

**규칙 #4: 메서드가 Memory\<T>를 사용하고 Task를 반환하는 경우, Task가 터미널 상태로 전환된 후에는 Memory\<T> 인스턴스를 사용하면 안 됩니다.**

이 규칙은 단순히 규칙 #3의 비동기 변형입니다. 이 규칙을 준수하기 위해 이전 예제의 `Log` 메서드를 다음과 같이 작성할 수 있습니다.

[!code-csharp[task-returning-async](~/samples/snippets/standard/buffers/memory-t/void-returning-async/void-returning-async.cs#1)]

여기서 “터미널 상태”는 Task가 완료됨, 오류 또는 취소됨 상태로 전환됨을 의미합니다. 즉, “터미널 상태”는 “await에서 throw하거나 실행을 계속하게 하는 모든 것”을 의미합니다.

이 지침은 <xref:System.Threading.Tasks.Task>, <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.ValueTask%601> 또는 유사한 형식을 반환하는 메서드에 적용됩니다.

**규칙 #5: 생성자가 Memory\<T>를 매개 변수로 사용하는 경우 생성된 개체의 인스턴스 메서드가 Memory\<T> 인스턴스의 소비자로 간주됩니다.**

다음 예제를 참조하세요.

```csharp
class OddValueExtractor
{
    public OddValueExtractor(ReadOnlyMemory<int> input);
    public bool TryReadNextOddValue(out int value);
}

void PrintAllOddValues(ReadOnlyMemory<int> input)
{
    var extractor = new OddValueExtractor(input);
    while (extractor.TryReadNextOddValue(out int value))
    {
      Console.WriteLine(value);
    }
}
```

여기서 `OddValueExtractor` 생성자는 `ReadOnlyMemory<int>`를 생성자 매개 변수로 사용하므로 생성자 자체는 `ReadOnlyMemory<int>` 인스턴스의 소비자이며, 반환된 값의 모든 인스턴스 메서드도 원래 `ReadOnlyMemory<int>` 인스턴스의 소비자입니다. 즉, 인스턴스가 `TryReadNextOddValue` 메서드에 직접 전달되지 않더라도 `TryReadNextOddValue`가 `ReadOnlyMemory<int>` 인스턴스를 사용합니다.

**규칙 #6: 설정 가능한 Memory\<T> 형식의 속성(또는 동등한 인스턴스 메서드)이 형식에 있는 경우 해당 개체의 인스턴스 메서드는 Memory\<T> 인스턴스의 소비자로 간주됩니다.**

이 규칙은 단순히 규칙 #5의 변형입니다. 이 규칙이 필요한 이유는 속성 setter 또는 이와 동등한 메서드가 해당 입력을 캡처하고 유지한다고 가정되므로 동일한 개체의 인스턴스 메서드가 캡처된 상태를 활용할 수 있기 때문입니다.

다음 예제는 이 규칙을 트리거합니다.

```csharp
class Person
{
    // Settable property.
    public Memory<char> FirstName { get; set; }

    // alternatively, equivalent "setter" method
    public SetFirstName(Memory<char> value);

    // alternatively, a public settable field
    public Memory<char> FirstName;
}
```

**규칙 #7: IMemoryOwner\<T> 참조가 있는 경우 일정 시점에서 삭제하거나 해당 소유권을 이전해야 합니다(둘 다는 아님).**

관리형 또는 비관리형 메모리에서 <xref:System.Memory%601> 인스턴스를 지원할 수 있으므로 <xref:System.Memory%601> 인스턴스에서 수행된 작업이 완료되면 소유자가 <xref:System.Buffers.MemoryPool%601.Dispose%2A?displayProperty=nameWithType>을 호출해야 합니다. 또는 소유자가 <xref:System.Buffers.IMemoryOwner%601> 인스턴스의 소유권을 다른 구성 요소에 이전할 수 있습니다. 이 시점에서 획득하는 구성 요소는 적절한 시점에 <xref:System.Buffers.MemoryPool%601.Dispose%2A?displayProperty=nameWithType>을 호출할 책임이 있습니다(뒷부분에서 자세히 설명).

<xref:System.Buffers.MemoryPool%601.Dispose%2A> 메서드를 호출하지 않으면 비관리형 메모리 누수 또는 기타 성능 저하가 발생할 수 있습니다.

이 규칙은 <xref:System.Buffers.MemoryPool%601.Rent%2A?displayProperty=nameWithType> 등의 팩터리 메서드를 호출하는 코드에도 적용됩니다. 호출자는 반환된 <xref:System.Buffers.IMemoryOwner%601>의 소유자가 되며, 인스턴스가 완료되면 삭제할 책임이 있습니다.

**규칙 #8: API 노출 영역에 IMemoryOwner\<T> 매개 변수가 있는 경우 해당 인스턴스의 소유권을 허용하는 것입니다.**

이 형식의 인스턴스를 허용하면 해당 구성 요소가 이 인스턴스를 소유하려고 함을 나타냅니다. 해당 구성 요소가 규칙 #7에 따라 적절하게 삭제할 책임이 있습니다.

<xref:System.Buffers.IMemoryOwner%601> 인스턴스의 소유권을 다른 구성 요소에 이전하는 구성 요소는 메서드 호출이 완료된 후 해당 인스턴스를 더 이상 사용하면 안 됩니다.

> [!IMPORTANT]
> 생성자가 <xref:System.Buffers.IMemoryOwner%601>를 매개 변수로 사용하는 경우 해당 형식이 <xref:System.IDisposable>을 구현해야 하며, <xref:System.IDisposable.Dispose%2A> 메서드가 <xref:System.Buffers.MemoryPool%601.Dispose%2A?displayProperty=nameWithType>을 호출해야 합니다.

**규칙 #9: 동기 P/Invoke 메서드를 래핑하는 경우 API가 Span\<T>를 매개 변수로 사용해야 합니다.**

규칙 #1에 따라 <xref:System.Span%601>은 일반적으로 동기 API에 사용할 올바른 형식입니다. 다음 예제와 같이 [`fixed`](../../csharp/language-reference/keywords/fixed-statement.md) 키워드를 통해 <xref:System.Span%601> 인스턴스를 고정할 수 있습니다.

```csharp
using System.Runtime.InteropServices;

[DllImport(...)]
private static extern unsafe int ExportedMethod(byte* pbData, int cbData);

public unsafe int ManagedWrapper(Span<byte> data)
{
    fixed (byte* pbData = &MemoryMarshal.GetReference(data))
    {
        int retVal = ExportedMethod(pbData, data.Length);

        /* error checking retVal goes here */

        return retVal;
    }
}
```

앞의 예제에서, 입력 범위가 비어 있는 경우 `pbData`는 Null일 수 있습니다. 내보낸 메서드에서 `pbData`가 Null이 아니어야 하는 경우 `cbData`가 0이더라도 메서드를 다음과 같이 구현할 수 있습니다.

```csharp
public unsafe int ManagedWrapper(Span<byte> data)
{
    fixed (byte* pbData = &MemoryMarshal.GetReference(data))
    {
        byte dummy = 0;
        int retVal = ExportedMethod((pbData != null) ? pbData : &dummy, data.Length);

        /* error checking retVal goes here */

        return retVal;
    }
}
```

**규칙 #10: 비동기 P/Invoke 메서드를 래핑하는 경우 API가 Memory\<T>를 매개 변수로 사용해야 합니다.**

비동기 작업에서는 [`fixed`](../../csharp/language-reference/keywords/fixed-statement.md) 키워드를 사용할 수 없으므로 인스턴스가 나타내는 인접한 메모리 종류와 관계없이 <xref:System.Memory%601.Pin%2A?displayProperty=nameWithType> 메서드를 사용하여 <xref:System.Memory%601> 인스턴스를 고정합니다. 다음 예제에서는 이 API를 사용하여 비동기 P/Invoke 호출을 수행하는 방법을 보여 줍니다.

```csharp
using System.Runtime.InteropServices;

[UnmanagedFunctionPointer(...)]
private delegate void OnCompletedCallback(IntPtr state, int result);

[DllImport(...)]
private static extern unsafe int ExportedAsyncMethod(byte* pbData, int cbData, IntPtr pState, IntPtr lpfnOnCompletedCallback);

private static readonly IntPtr _callbackPtr = GetCompletionCallbackPointer();

public unsafe Task<int> ManagedWrapperAsync(Memory<byte> data)
{
    // setup
    var tcs = new TaskCompletionSource<int>();
    var state = new MyCompletedCallbackState
    {
        Tcs = tcs
    };
    var pState = (IntPtr)GCHandle.Alloc(state);

    var memoryHandle = data.Pin();
    state.MemoryHandle = memoryHandle;

    // make the call
    int result;
    try
    {
        result = ExportedAsyncMethod((byte*)memoryHandle.Pointer, data.Length, pState, _callbackPtr);
    }
    catch
    {
        ((GCHandle)pState).Free(); // cleanup since callback won't be invoked
        memoryHandle.Dispose();
        throw;
    }

    if (result != PENDING)
    {
        // Operation completed synchronously; invoke callback manually
        // for result processing and cleanup.
        MyCompletedCallbackImplementation(pState, result);
    }

    return tcs.Task;
}

private static void MyCompletedCallbackImplementation(IntPtr state, int result)
{
    GCHandle handle = (GCHandle)state;
    var actualState = (MyCompletedCallbackState)state;
    handle.Free();
    actualState.MemoryHandle.Dispose();

    /* error checking result goes here */

    if (error)
    {
        actualState.Tcs.SetException(...);
    }
    else
    {
        actualState.Tcs.SetResult(result);
    }
}

private static IntPtr GetCompletionCallbackPointer()
{
    OnCompletedCallback callback = MyCompletedCallbackImplementation;
    GCHandle.Alloc(callback); // keep alive for lifetime of application
    return Marshal.GetFunctionPointerForDelegate(callback);
}

private class MyCompletedCallbackState
{
    public TaskCompletionSource<int> Tcs;
    public MemoryHandle MemoryHandle;
}
```

## <a name="see-also"></a>참고 항목

- <xref:System.Memory%601?displayProperty=nameWithType>
- <xref:System.Buffers.IMemoryOwner%601?displayProperty=nameWithType>
- <xref:System.Span%601?displayProperty=nameWithType>
