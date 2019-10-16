---
title: 예외에 대한 모범 사례 - .NET
ms.date: 12/05/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- exceptions, best practices
ms.assetid: f06da765-235b-427a-bfb6-47cd219af539
ms.openlocfilehash: 6a165c3e0f41603ef7233669d7148dd44b1d3ce6
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696761"
---
# <a name="best-practices-for-exceptions"></a>예외에 대한 모범 사례

잘 설계된 응용 프로그램이 응용 프로그램 충돌을 방지하기 위해 예외와 오류를 처리합니다. 이 섹션에서는 예외를 처리하고 만들기 위한 모범 사례를 설명합니다.

## <a name="use-trycatchfinally-blocks-to-recover-from-errors-or-release-resources"></a>Try/catch/finally 블록을 사용하여 오류를 복구하거나 리소스를 해제합니다.

잠재적으로 예외를 생성***하고*** 코드가 해당 예외에서 복구될 수 있는 코드 주위에 `try`/`catch` 블록을 사용합니다. `catch` 블록에서 항상 가장 많이 파생된 것부터 가장 적게 파생된 것까지 예외를 정렬합니다. 모든 예외는 <xref:System.Exception>에서 파생됩니다. 더 많이 파생된 예외는 기본 예외 클래스에 대한 catch 절 앞에 오는 catch 절에 의해 처리되지 않습니다. 예외에서 코드를 복구할 수 없는 경우 해당 예외를 catch하지 마세요. 가능한 경우 메서드를 호출 스택 위에 추가하여 복구하세요.

`using` 문 또는 `finally` 블록으로 할당된 리소스를 정리하세요. 예외가 throw될 때 리소스를 자동으로 정리하려면 `using` 문을 사용하는 것이 좋습니다. `finally` 블록을 사용하여 <xref:System.IDisposable>을 구현하지 않는 리소스를 정리합니다. `finally` 절의 코드는 예외가 throw되더라도 거의 항상 실행됩니다.

## <a name="handle-common-conditions-without-throwing-exceptions"></a>예외를 throw하지 않고 일반적인 조건 처리

발생할 가능성이 높지만 예외를 트리거할 수도 있는 조건의 경우 예외를 방지하는 방식으로 조건을 처리하는 것이 좋습니다. 예를 들어 이미 닫혀 있는 연결을 닫으려고 하면 `InvalidOperationException`이 발생합니다. 닫기 전에 `if` 문을 사용하여 연결 상태를 확인하면 이 예외를 방지할 수 있습니다.

[!code-cpp[Conceptual.Exception.Handling#2](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#2)]
[!code-csharp[Conceptual.Exception.Handling#2](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#2)]
[!code-vb[Conceptual.Exception.Handling#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#2)]

닫기 전에 연결 상태를 확인하지 않을 경우 `InvalidOperationException` 예외를 catch할 수 있습니다.

[!code-cpp[Conceptual.Exception.Handling#3](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#3)]
[!code-csharp[Conceptual.Exception.Handling#3](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#3)]
[!code-vb[Conceptual.Exception.Handling#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#3)]

어떤 방법을 선택할 것인지는 해당 이벤트의 예상 발생 빈도에 따라 달라집니다.

- 이벤트가 그다지 자주 발생하지 않으면(즉, 예상치 못한 파일 끝과 같은 이벤트가 실제로 예외이고 오류를 나타내는 경우) 예외 처리를 사용합니다. 예외 처리를 사용하면 정상적인 조건에서 적은 수의 코드가 실행됩니다.

- 이벤트가 일상적으로 발생하고 정상적인 실행의 일부로 간주될 수 있는 경우 코드에서 오류 조건을 확인합니다. 일반적인 오류 조건을 확인하면 예외가 방지되기 때문에 실행되는 코드가 줄어듭니다.

## <a name="design-classes-so-that-exceptions-can-be-avoided"></a>예외를 방지할 수 있도록 클래스 디자인

클래스는 예외를 트리거하는 호출을 방지할 수 있도록 하는 메서드 또는 속성을 제공할 수 있습니다. 예를 들어, <xref:System.IO.FileStream> 클래스는 파일 끝에 도달했는지 확인하는 데 도움이 되는 메서드를 제공합니다. 이러한 메서드를 사용하면 파일의 끝을 지나서 읽을 경우 throw되는 예외를 방지할 수 있습니다. 다음 예제에서는 예외를 트리거하지 않고 파일의 끝까지 읽는 방법을 보여 줍니다.

[!code-cpp[Conceptual.Exception.Handling#5](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#5)]
[!code-csharp[Conceptual.Exception.Handling#5](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#5)]
[!code-vb[Conceptual.Exception.Handling#5](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#5)]

예외를 방지하는 또 다른 방법은 매우 일반적인 오류의 경우 예외를 throw하는 대신 null(또는 기본값)을 반환하는 것입니다. 매우 흔한 오류 사례는 정상적인 제어 흐름으로 간주할 수 있습니다. 이러한 경우에 null(또는 기본값)을 반환함으로써, 앱의 성능에 미치는 영향을 최소화합니다.

값 유형의 경우, 오류 표시기로 `Nullable<T>` 또는 기본값 중 무엇을 사용할지 여부는 특정 앱에서 고려해야 할 사항입니다. `Nullable<Guid>`를 사용하면 `default`는 `Guid.Empty` 대신 `null`이 됩니다. 값이 있거나 없는 경우 `Nullable<T>`을 추가하여 더 명확하게 만들 수도 있습니다. 또는 `Nullable<T>`을 추가하여 불필요한지를 확인하는 추가 사례를 만들고 오류의 잠재적 원인을 만드는 역할만 할 수도 있습니다. 

## <a name="throw-exceptions-instead-of-returning-an-error-code"></a>오류 코드를 반환하는 대신 예외 throw

예외는 호출하는 코드에서 반환 코드를 확인하지 않아 오류가 발견되지 않는 것을 방지합니다.

## <a name="use-the-predefined-net-exception-types"></a>미리 정의된 .NET 예외 형식 사용

새 예외 클래스는 미리 정의된 예외 클래스가 적용되지 않는 경우에만 도입합니다. 예:

- 개체의 현재 상태에서 속성 집합이나 메서드 호출이 적절하지 않을 경우 <xref:System.InvalidOperationException> 예외를 throw합니다.

- 잘못된 매개 변수가 전달되면 <xref:System.ArgumentException> 예외 또는 <xref:System.ArgumentException>에서 파생된 미리 정의된 클래스 중 하나를 throw합니다.

## <a name="end-exception-class-names-with-the-word-exception"></a>예외 클래스 이름 뒤에 단어 `Exception` 추가

사용자 지정 예외가 필요한 경우 적절한 이름을 지정하고 <xref:System.Exception> 클래스에서 파생합니다. 예:

[!code-cpp[Conceptual.Exception.Handling#4](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#4)]
[!code-csharp[Conceptual.Exception.Handling#4](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#4)]
[!code-vb[Conceptual.Exception.Handling#4](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#4)]

## <a name="include-three-constructors-in-custom-exception-classes"></a>사용자 지정 예외 클래스에 세 가지 생성자 포함

사용자 고유의 예외 클래스를 만들 때 최소한 다음 세 가지 일반 생성자를 사용합니다. 즉, 매개 변수 없는 생성자, 문자열 메시지를 사용하는 생성자, 문자열 메시지와 내부 예외를 사용하는 생성자입니다.

- 기본값을 사용하는 <xref:System.Exception.%23ctor>.

- 문자열 메시지를 수락하는 <xref:System.Exception.%23ctor%28System.String%29>.

- 문자열 메시지와 내부 예외를 허용하는 <xref:System.Exception.%23ctor%28System.String%2CSystem.Exception%29>.

예는 [방법: 사용자 정의 예외 만들기](how-to-create-user-defined-exceptions.md)를 참조하세요.

## <a name="ensure-that-exception-data-is-available-when-code-executes-remotely"></a>코드를 원격으로 실행하는 경우 예외 데이터를 사용할 수 있는지 확인

사용자 정의 예외를 만드는 경우 원격으로 실행하는 코드에서 예외에 대한 메타데이터를 사용할 수 있는지 확인합니다.

예를 들어 앱 도메인을 지원하는 .NET 구현에서 앱 도메인 간에 예외가 발생할 수 있습니다. 앱 도메인 A에서 앱 도메인 B를 만들고, 여기서 예외를 throw하는 코드를 실행한다고 가정해봅시다. 앱 도메인 A에서 예외를 정확하게 catch하고 처리하려면 앱 도메인 B에서 throw된 예외를 포함하는 어셈블리를 찾을 수 있어야 합니다. 앱 도메인 B에서 앱 도메인 A의 애플리케이션 기준 위치가 아니라 해당 애플리케이션 기준 위치 아래의 어셈블리에 포함된 예외를 throw할 경우 앱 도메인 A는 예외를 찾을 수 없으며 공용 언어 런타임에서 <xref:System.IO.FileNotFoundException> 예외를 throw합니다. 이러한 상황을 방지하기 위해 예외 정보가 포함된 어셈블리를 다음과 같은 두 가지 방법으로 배포할 수 있습니다.

- 해당 어셈블리를 두 애플리케이션 도메인이 공유하는 공통 애플리케이션 기본 구조에 넣습니다.

    \- 또는 -

- 도메인이 공통 애플리케이션 기반 구조를 공유하지 않을 경우, 예외 정보가 포함된 어셈블리를 강력한 이름으로 지정한 다음, 이 어셈블리를 전역 어셈블리 캐시에 배포합니다.

## <a name="use-grammatically-correct-error-messages"></a>문법적으로 올바른 오류 메시지 사용

명확한 문을 작성하고 종료 문장 부호를 포함합니다. <xref:System.Exception.Message?displayProperty=nameWithType> 속성에 할당된 문자열의 각 문장은 마침표로 끝나야 합니다. 예를 들어 “로그 테이블이 오버플로되었습니다.”는 적절한 메시지 문자열입니다.

## <a name="include-a-localized-string-message-in-every-exception"></a>모든 예외에 지역화된 문자열 메시지를 포함합니다.

사용자에게 표시되는 오류 메시지는 예외 클래스 이름에서 파생된 메시지가 아니라 throw된 예외의 <xref:System.Exception.Message?displayProperty=nameWithType> 속성에서 파생된 메시지입니다. 일반적으로 [예외 생성자](xref:System.Exception.%23ctor%2A)의 `message` 인수에 메시지 문자열을 전달하여 값을 <xref:System.Exception.Message?displayProperty=nameWithType> 속성에 할당합니다.

지역화된 애플리케이션의 경우 애플리케이션에서 throw할 수 있는 모든 예외에 대해 지역화된 메시지 문자열을 제공해야 합니다. 리소스 파일을 사용하여 지역화된 오류 메시지를 제공합니다. 애플리케이션을 지역화하고 지역화된 문자열을 검색하는 방법은 다음 문서를 참조하세요.

- [방법: 지역화된 예외 메시지를 사용하여 사용자 정의 예외 생성](how-to-create-localized-exception-messages.md)
- [데스크톱 앱의 리소스](../../framework/resources/index.md) 
- <xref:System.Resources.ResourceManager?displayProperty=nameWithType>

## <a name="in-custom-exceptions-provide-additional-properties-as-needed"></a>필요에 따라 사용자 지정 예외에서 추가 속성 제공

추가 정보가 유용한 프로그래밍 시나리오에 대해서만 예외에 사용자 지정 메시지 문자열 이외의 추가 속성을 제공합니다. 예를 들어, <xref:System.IO.FileNotFoundException>은 <xref:System.IO.FileNotFoundException.FileName> 속성을 제공합니다.

## <a name="place-throw-statements-so-that-the-stack-trace-will-be-helpful"></a>스택 추적이 도움이 되도록 throw 문 포함

스택 추적은 예외가 throw되는 문에서 시작하여 예외를 catch하는 `catch` 문까지 수행됩니다.

## <a name="use-exception-builder-methods"></a>예외 작성기 메서드 사용

클래스는 구현된 여러 위치에서 동일한 예외를 throw하는 것이 일반적입니다. 코드를 많이 사용하지 않으려면 예외를 만들어 반환하는 도우미 메서드를 사용합니다. 예:

[!code-cpp[Conceptual.Exception.Handling#6](~/samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#6)]
[!code-csharp[Conceptual.Exception.Handling#6](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#6)]
[!code-vb[Conceptual.Exception.Handling#6](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#6)]

예외의 생성자를 사용하여 예외를 작성하는 것이 더 적합한 경우도 있습니다. 예를 들어 <xref:System.ArgumentException>과 같은 전역 예외 클래스가 있습니다.

## <a name="restore-state-when-methods-dont-complete-due-to-exceptions"></a>예외로 인해 메서드가 완료되지 않을 때의 상태 복원

호출자가 메서드에서 예외가 throw될 때 의도하지 않은 결과가 발생하지 않는다고 가정할 수 있어야 합니다. 예를 들어 하나의 계좌에서 출금한 후 다른 계좌에 입금하여 돈을 이체하는 코드가 있고 입금을 실행하는 동안 예외가 발생할 경우 출금이 적용되기를 원하지 않을 것입니다.

```csharp
public void TransferFunds(Account from, Account to, decimal amount)
{
    from.Withdrawal(amount);
    // If the deposit fails, the withdrawal shouldn't remain in effect.
    to.Deposit(amount);
}
```

```vb
Public Sub TransferFunds(from As Account, [to] As Account, amount As Decimal)
    from.Withdrawal(amount)
    ' If the deposit fails, the withdrawal shouldn't remain in effect.
    [to].Deposit(amount)
End Sub
```

위의 메서드는 직접적으로 예외를 throw하지 않지만, 입금 작업이 실패하는 경우 출금이 취소되도록 방어적으로 작성해야 합니다.

이 상황을 처리하는 한 가지 방법은 입금 트랜잭션에서 throw된 예외를 catch하고 출금을 롤백하는 것입니다.

```csharp
private static void TransferFunds(Account from, Account to, decimal amount)
{
    string withdrawalTrxID = from.Withdrawal(amount);
    try
    {
        to.Deposit(amount);
    }
    catch
    {
        from.RollbackTransaction(withdrawalTrxID);
        throw;
    }
}
```

```vb
Private Shared Sub TransferFunds(from As Account, [to] As Account, amount As Decimal)
    Dim withdrawalTrxID As String = from.Withdrawal(amount)
    Try
        [to].Deposit(amount)
    Catch
        from.RollbackTransaction(withdrawalTrxID)
        Throw
    End Try
End Sub
```

이 예제에서는 `throw`를 사용하여 원래 예외를 다시 throw하는 방법을 보여 줍니다. 이렇게 하면 호출자가 <xref:System.Exception.InnerException> 속성을 검사하지 않아도 문제의 실제 원인을 쉽게 확인할 수 있습니다. 또는 새 예외를 throw하고 원래 예외를 내부 예외로 포함할 수 있습니다.

```csharp
catch (Exception ex)
{
    from.RollbackTransaction(withdrawalTrxID);
    throw new TransferFundsException("Withdrawal failed.", innerException: ex)
    {
        From = from,
        To = to,
        Amount = amount
    };
}
```

```vb
Catch ex As Exception
    from.RollbackTransaction(withdrawalTrxID)
    Throw New TransferFundsException("Withdrawal failed.", innerException:=ex) With
    {
        .From = from,
        .[To] = [to],
        .Amount = amount
    }
End Try
```

## <a name="see-also"></a>참고 항목

- [예외](index.md)
