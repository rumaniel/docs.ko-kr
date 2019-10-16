---
title: lock 문 - C# 참조
ms.custom: seodec18
description: C# lock 문을 사용하여 공유 리소스에 대한 스레드 액세스 동기화
ms.date: 10/01/2018
f1_keywords:
- lock_CSharpKeyword
- lock
helpviewer_keywords:
- lock keyword [C#]
ms.assetid: 656da1a4-707e-4ef6-9c6e-6d13b646af42
ms.openlocfilehash: 70fcd8041946f2b1db3b37de79318b87771ee676
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70168772"
---
# <a name="lock-statement-c-reference"></a>lock 문(C# 참조)

`lock` 문은 지정된 개체에 대한 상호 배제 잠금을 획득하여 명령문 블록을 실행한 다음, 잠금을 해제합니다. 잠금이 유지되는 동안 잠금을 보유하는 스레드는 잠금을 다시 획득하고 해제할 수 있습니다. 다른 스레드는 잠금을 획득할 수 없도록 차단되며 잠금이 해제될 때까지 대기합니다.

`lock` 문이 형식입니다.

```csharp
lock (x)
{
    // Your code...
}
```

여기서 `x`는 [참조 형식](reference-types.md)의 식입니다. 정확히 다음과 같은 경우

```csharp
object __lockObj = x;
bool __lockWasTaken = false;
try
{
    System.Threading.Monitor.Enter(__lockObj, ref __lockWasTaken);
    // Your code...
}
finally
{
    if (__lockWasTaken) System.Threading.Monitor.Exit(__lockObj);
}
```

코드에서 [try...finally](try-finally.md) 블록을 사용하므로 `lock` 문의 본문 내에서 예외가 throw되더라도 잠금이 해제됩니다.

`lock` 문의 본문에서 [await 연산자](../operators/await.md)를 사용할 수 없습니다.

## <a name="remarks"></a>설명

공유 리소스에 대한 스레드 액세스를 동기화하는 경우 전용 개체 인스턴스(예: `private readonly object balanceLock = new object();`) 또는 코드의 관련 없는 파트에서 잠금 개체로 사용되지 않을 가능성이 있는 다른 인스턴스를 잠급니다. 교착 상태 또는 잠금 경합이 발생할 수 있으므로 다른 공유 리소스에 대해 동일한 잠금 개체 인스턴스를 사용하지 마세요. 특히 다음을 잠금 개체로 사용하지 마세요.

- `this`(호출자가 잠금으로 사용할 수 있음).
- <xref:System.Type> 인스턴스([typeof](../operators/type-testing-and-cast.md#typeof-operator) 연산자 또는 리플렉션에서 획득할 수 있음).
- 문자열 인스턴스(문자열 리터럴 포함)([인터닝](/dotnet/api/system.string.intern#remarks)될 수 있음).

## <a name="example"></a>예제

다음 예제에서는 전용 `balanceLock` 인스턴스에 잠금을 설정하여 해당 개인 `balance` 필드에 대한 액세스를 동기화하는 `Account` 클래스를 정의합니다. 동일한 인스턴스를 잠금에 사용하면 `Debit` 또는 `Credit` 메서드를 동시에 호출하려는 두 스레드에 의해 `balance` 필드가 동시에 업데이트되지 않습니다.

[!code-csharp[lock-statement-example](~/samples/snippets/csharp/keywords/LockStatementExample.cs)]

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [lock 문](~/_csharplang/spec/statements.md#the-lock-statement) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- <xref:System.Threading.SpinLock?displayProperty=nameWithType>
- <xref:System.Threading.Interlocked?displayProperty=nameWithType>
- [C# 참조](../index.md)
- [C# 키워드](index.md)
- [동기화 기본 형식 개요](../../../standard/threading/overview-of-synchronization-primitives.md)
