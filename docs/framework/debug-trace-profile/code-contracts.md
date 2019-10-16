---
title: 코드 계약
ms.date: 09/05/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Code contracts
ms.assetid: 84526045-496f-489d-8517-a258cf76f040
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9e40f93be7f2dad4a80a4f4d23f61f3c93061751
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61874941"
---
# <a name="code-contracts"></a>코드 계약

코드 계약을 통해 코드에서 사전 조건, 사후 조건 및 개체 고정을 지정할 수 있습니다. 사전 조건은 메서드 또는 속성을 입력할 때 충족해야 하는 요구 사항입니다. 사후 조건은 메서드 또는 속성 코드가 종료될 때의 예상을 설명합니다. 개체 고정은 양호한 상태인 클래스의 예상 상태를 설명합니다.

코드 계약에는 코드 표시를 위한 클래스, 컴파일 타임 분석을 위한 정적 분석기 및 런타임 분석기가 포함됩니다. 코드 계약에 대한 클래스는 <xref:System.Diagnostics.Contracts> 네임스페이스에서 확인할 수 있습니다.

코드 계약의 이점은 다음과 같습니다.

- 테스트 향상: 코드 계약은 정적 계약 검증, 런타임 검사 및 문서 생성 합니다.

- 자동 테스트 도구: 사전 조건을 충족 하지 않는 의미 없는 테스트 인수를 필터링 하 여 보다 의미 있는 단위 테스트를 생성할 코드 계약을 사용할 수 있습니다.

- 정적 검증: 정적 검사기는 프로그램을 실행 하지 않고 계약 위반이 있는지 여부를 결정할 수 있습니다. null 역참조 및 배열 범위와 같은 암시적 계약 및 명시적 계약을 검사합니다.

- 참조 설명서: 설명서 생성기 계약 정보를 사용 하 여 기존 XML 문서 파일을 보강합니다. 생성된 설명서 페이지에 계약 섹션이 포함되도록 [Sandcastle](https://github.com/EWSoftware/SHFB)과 함께 사용할 수 있는 스타일시트도 있습니다.

모든 .NET Framework 언어는 계약을 즉시 활용할 수 있습니다. 특별한 파서 또는 컴파일러를 작성할 필요가 없습니다. Visual Studio 추가 기능을 통해 수행할 코드 계약 분석 수준을 지정할 수 있습니다. 분석기는 계약이 제대로 구성되었는지 확인할 수 있으며(형식 검사 및 이름 확인) 컴파일된 계약 형태를 MSIL(Microsoft Intermediate Language) 형식으로 생성할 수 있습니다. Visual Studio에서 계약을 작성하는 경우 도구에서 제공하는 표준 IntelliSense를 활용할 수 있습니다.

계약 클래스에 있는 대부분의 메서드는 조건부로 컴파일됩니다. 즉, `#define` 지시문을 사용하여 특수 기호 CONTRACTS_FULL을 정의하는 경우에만 컴파일러가 이러한 메서드 호출을 내보냅니다. CONTRACTS_FULL을 사용하면 `#ifdef` 지시문을 사용하지 않고 코드에서 계약을 작성할 수 있습니다. 일부는 계약을 포함하고 일부는 계약을 포함하지 않는 다양한 빌드를 생성할 수 있습니다.

코드 계약을 사용하기 위한 도구 및 자세한 지침은 MSDN DevLabs 웹 사이트의 [코드 계약](https://go.microsoft.com/fwlink/?LinkId=152461)을 참조하세요.

## <a name="preconditions"></a>전제 조건

<xref:System.Diagnostics.Contracts.Contract.Requires%2A?displayProperty=nameWithType> 메서드를 사용하여 사전 조건을 표현할 수 있습니다. 사전 조건은 메서드가 호출될 때의 상태를 지정합니다. 일반적으로 유효한 매개 변수 값을 지정하는 데 사용됩니다. 사전 조건에 언급된 모든 멤버는 최소한 메서드 자체만큼 액세스 가능해야 합니다. 그러지 않으면 메서드의 일부 호출자가 사전 조건을 이해하지 못할 수 있습니다. 조건에 파생 작업이 없어야 합니다. 실패한 사전 조건의 런타임 동작은 런타임 분석기에 의해 결정됩니다.

예를 들어 다음 사전 조건은 `x` 매개 변수가 null이 아니어야 한다고 표현합니다.

```csharp
Contract.Requires(x != null);
```

사전 조건이 실패할 때 코드에서 특정 예외를 발생시켜야 하는 경우 다음과 같이 <xref:System.Diagnostics.Contracts.Contract.Requires%2A>의 제네릭 오버로드를 사용할 수 있습니다.

```csharp
Contract.Requires<ArgumentNullException>(x != null, "x");
```

### <a name="legacy-requires-statements"></a>레거시 Requires 문

대부분의 코드에는 `if`-`then`-`throw` 코드 형태의 일부 매개 변수 유효성 검사가 포함되어 있습니다. 다음과 같은 경우 계약 도구는 이러한 문을 사전 조건으로 인식합니다.

- 문이 메서드에서 다른 문 앞에 표시됩니다.

- 이러한 문의 전체 집합 뒤에는 <xref:System.Diagnostics.Contracts.Contract.Requires%2A>, <xref:System.Diagnostics.Contracts.Contract.Ensures%2A>, <xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A> 또는 <xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A> 메서드 호출과 같은 명시적 <xref:System.Diagnostics.Contracts.Contract> 메서드 호출이 나옵니다.

`if`-`then`-`throw` 문이 이 형태로 나타나는 경우 도구에서 레거시 `requires` 문으로 인식합니다. `if`-`then`-`throw` 시퀀스 뒤에 나오는 다른 계약이 없는 경우 <xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A?displayProperty=nameWithType> 메서드를 사용하여 코드를 끝냅니다.

```csharp
if (x == null) throw new ...
Contract.EndContractBlock(); // All previous "if" checks are preconditions
```

앞의 테스트에 있는 조건은 부정된 사전 조건입니다. 실제 사전 조건은 `x != null`입니다. 부정 된 사전 조건은 매우 제한적입니다. 이전 예에서 같이 작성 해야 합니다. 즉, 포함 하지 않아야 `else` 절 및 본문에는 `then` 절은 단일 되어야 합니다 `throw` 문입니다. `if` 테스트에는 순수성 및 표시 유형 규칙이 둘 다 적용되지만([사용 지침](#usage_guidelines) 참조) `throw` 식에는 순수성 규칙만 적용됩니다. 그러나 발생한 예외 형식은 계약이 발생하는 메서드와 동일한 표시 유형이어야 합니다.

## <a name="postconditions"></a>사후 조건

사후 조건은 종료될 때의 메서드 상태에 대한 계약입니다. 사후 조건은 메서드를 종료하기 직전에 검사됩니다. 실패한 사후 조건의 런타임 동작은 런타임 분석기에 의해 결정됩니다.

사전 조건과 달리 사후 조건은 표시 수준이 낮은 멤버를 참조할 수 있습니다. 클라이언트가 전용 상태를 사용하여 사후 조건에서 표현된 일부 정보를 이해 또는 사용하지 못할 수도 있지만 메서드를 올바르게 사용할 수 있는 클라이언트의 기능에는 영향을 주지 않습니다.

### <a name="standard-postconditions"></a>표준 사후 조건

<xref:System.Diagnostics.Contracts.Contract.Ensures%2A> 메서드를 사용하여 표준 사후 조건을 표현할 수 있습니다. 사후 조건은 메서드가 정상 종료될 때 `true`여야 하는 조건을 표현합니다.

```csharp
Contract.Ensures(this.F > 0);
```

### <a name="exceptional-postconditions"></a>예외 사후 조건

예외 사후 조건은 메서드에서 특정 예외가 발생할 때 `true`여야 하는 사후 조건입니다. 다음 예제에 같이 <xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A?displayProperty=nameWithType> 메서드를 사용하여 이러한 사후 조건을 지정할 수 있습니다.

```csharp
Contract.EnsuresOnThrow<T>(this.F > 0);
```

인수는 `T`의 하위 형식인 예외가 발생할 때마다 `true`여야 하는 조건입니다.

예외 사후 조건에서 사용하기 어려운 일부 예외 형식이 있습니다. 예를 들어 `T`에 대해 <xref:System.Exception> 형식을 사용하면 스택 오버플로 또는 제어하기 어려운 다른 예외인 경우에도 발생한 예외 형식에 관계없이 메서드가 조건을 보장해야 합니다. 예외 사후 조건은 멤버 호출 시 발생할 수 있는 특정 예외(예: <xref:System.TimeZoneInfo> 메서드 호출에 대해 <xref:System.InvalidTimeZoneException>이 발생하는 경우)에 대해서만 사용해야 합니다.

### <a name="special-postconditions"></a>특수 사후 조건

다음 메서드는 사후 조건 내에서만 사용할 수 있습니다.

- `T`가 메서드의 반환 형식으로 대체되는 `Contract.Result<T>()` 식을 사용하여 사후 조건에서 메서드 반환 값을 참조할 수 있습니다. 컴파일러가 형식을 유추할 수 없는 경우 명시적으로 제공해야 합니다. 예를 들어는 C# 컴파일러는 인수를 사용 하지 않는 메서드에 대 한 형식을 유추할 수 없습니다. `Contract.Ensures(0 <Contract.Result<int>())` 반환 형식이 있는 메서드에 `void` 참조할 수 없습니다. `Contract.Result<T>()` 는 사후 조건에서.

- 사후 조건의 사전 상태 값은 메서드 또는 속성의 시작 부분에 있는 식의 값을 참조합니다. `Contract.OldValue<T>(e)` 식을 사용합니다. 여기서 `T`는 `e`의 형식입니다. 컴파일러가 형식을 유추할 수 있는 경우 언제든지 제네릭 형식 인수를 생략할 수 있습니다. 예를 들어 C# 컴파일러는 인수를 사용하기 때문에 항상 형식을 유추합니다. `e`에서 발생할 수 있는 사항 및 이전 식이 나타날 수 있는 컨텍스트에 대한 몇 가지 제한 사항이 있습니다. 이전 식은 다른 이전 식을 포함할 수 없습니다. 무엇보다도 이전 식은 메서드의 사전 조건 상태에 있던 값을 참조해야 합니다. 즉, 메서드의 사전 조건이 `true`이기만 하면 평가할 수 있는 식이어야 합니다. 다음은 해당 규칙의 여러 인스턴스입니다.

  - 값은 메서드의 사전 조건 상태에 있어야 합니다. 개체의 필드를 참조 하려면 사전 개체는 null이 아닌 항상 보장 해야 합니다.

  - 이전 식에서는 메서드의 반환 값을 참조할 수 없습니다.

      ```csharp
      Contract.OldValue(Contract.Result<int>() + x) // ERROR
      ```

  - 이전 식에서는 `out` 매개 변수를 참조할 수 없습니다.

  - 수량자 범위가 메서드의 반환 값에 종속된 경우 이전 식은 수량자의 바인딩된 변수에 종속될 수 없습니다.

      ```csharp
      Contract.ForAll(0, Contract.Result<int>(), i => Contract.OldValue(xs[i]) > 3); // ERROR
      ```

  - 이전 식이 메서드 호출의 인덱서 또는 인수로 사용되지 않는 한 <xref:System.Diagnostics.Contracts.Contract.ForAll%2A> 또는 <xref:System.Diagnostics.Contracts.Contract.Exists%2A> 호출에서 익명 대리자의 매개 변수를 참조할 수 없습니다.

      ```csharp
      Contract.ForAll(0, xs.Length, i => Contract.OldValue(xs[i]) > 3); // OK
      Contract.ForAll(0, xs.Length, i => Contract.OldValue(i) > 3); // ERROR
      ```

  - 익명 대리자가 <xref:System.Diagnostics.Contracts.Contract.ForAll%2A> 또는 <xref:System.Diagnostics.Contracts.Contract.Exists%2A> 메서드에 대한 인수가 아니면 이전 식의 값이 익명 대리자의 매개 변수 중 하나에 종속된 경우 익명 대리자의 본문에서 이전 식이 발생할 수 없습니다.

      ```csharp
      Method(... (T t) => Contract.OldValue(... t ...) ...); // ERROR
      ```

  - 계약이 메서드 본문 앞에 나타나고 대부분의 컴파일러가 사후 조건에서 `out` 매개 변수를 허용하지 않으므로 `Out` 매개 변수는 문제를 일으킵니다. 이 문제를 해결하기 위해 <xref:System.Diagnostics.Contracts.Contract> 클래스는 `out` 매개 변수를 기준으로 사후 조건을 허용하는 <xref:System.Diagnostics.Contracts.Contract.ValueAtReturn%2A> 메서드를 제공합니다.

      ```csharp
      public void OutParam(out int x)
      {
          Contract.Ensures(Contract.ValueAtReturn(out x) == 3);
          x = 3;
      }
      ```

      <xref:System.Diagnostics.Contracts.Contract.OldValue%2A> 메서드와 마찬가지로, 컴파일러가 형식을 유추할 수 있는 경우 언제든지 제네릭 형식 매개 변수를 생략할 수 있습니다. 계약 재작성기는 메서드 호출을 `out` 매개 변수의 값으로 대체합니다. <xref:System.Diagnostics.Contracts.Contract.ValueAtReturn%2A> 메서드는 사후 조건에서만 나타날 수 있습니다. 메서드에 대한 인수는 `out` 매개 변수 또는 구조체 필드 `out` 매개 변수여야 합니다. 후자는 구조체 생성자의 사후 조건에서 필드를 참조할 때에도 유용합니다.

      > [!NOTE]
      > 코드 계약 분석 도구는 현재 `out` 매개 변수가 올바르게 초기화되었는지 여부를 확인하지 않으며 사후 조건에서 해당 내용을 무시합니다. 따라서 앞의 예제에서 계약 뒤의 줄이 정수를 할당하는 대신 `x`의 값을 사용한 경우 컴파일러가 올바른 오류를 실행하지 않습니다. 그러나 CONTRACTS_FULL 전처리기 기호가 정의되지 않은 빌드(예: 릴리스 빌드)에서는 컴파일러가 오류를 실행합니다.

## <a name="invariants"></a>고정

개체 고정은 해당 개체가 클라이언트에 표시될 때마다 클래스의 각 인스턴스에 대해 true여야 하는 조건입니다. 개체가 올바른 것으로 간주되는 조건을 표현합니다.

고정 메서드는 <xref:System.Diagnostics.Contracts.ContractInvariantMethodAttribute> 특성 표시로 식별됩니다. 고정 메서드는 다음 예제와 같이 각각 개별 고정을 지정하는 <xref:System.Diagnostics.Contracts.Contract.Invariant%2A> 메서드 호출 시퀀스를 제외하고 코드를 포함하면 안 됩니다.

```csharp
[ContractInvariantMethod]
protected void ObjectInvariant ()
{
    Contract.Invariant(this.y >= 0);
    Contract.Invariant(this.x > this.y);
    ...
}
```

고정은 CONTRACTS_FULL 전처리기 기호에 의해 조건부로 정의됩니다. 런타임 검사 중에 고정은 각 public 메서드의 끝에서 검사됩니다. 고정이 동일한 클래스의 public 메서드를 언급하는 경우 일반적으로 해당 public 메서드의 끝에서 발생하는 고정 검사를 사용할 수 없습니다. 대신, 해당 클래스에 대한 가장 바깥쪽 메서드 호출의 끝에서만 검사가 발생합니다. 이 검사는 다른 클래스의 메서드 호출로 인해 클래스에 재진입하는 경우에도 발생합니다. 고정 된 개체 종료자에 대 한 확인 되지 않습니다 및 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 구현 합니다.

<a name="usage_guidelines"></a>

## <a name="usage-guidelines"></a>사용 지침

### <a name="contract-ordering"></a>계약 순서 지정

다음 표에서는 메서드 계약을 쓸 때 사용해야 하는 요소의 순서를 보여 줍니다.

|`If-then-throw statements`|이전 버전과 호환되는 공용 사전 조건|
|-|-|
|<xref:System.Diagnostics.Contracts.Contract.Requires%2A>|모든 공용 사전 조건|
|<xref:System.Diagnostics.Contracts.Contract.Ensures%2A>|모든 공용(일반) 사후 조건|
|<xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A>|모든 공용 예외 사후 조건|
|<xref:System.Diagnostics.Contracts.Contract.Ensures%2A>|모든 전용/내부(일반) 사후 조건|
|<xref:System.Diagnostics.Contracts.Contract.EnsuresOnThrow%2A>|모든 전용/내부 예외 사후 조건|
|<xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A>|다른 계약 없이 `if`-`then`-`throw` 스타일 사전 조건을 사용하는 경우 <xref:System.Diagnostics.Contracts.Contract.EndContractBlock%2A> 호출을 배치하여 이전의 모든 if 검사가 사전 조건임을 나타냅니다.|

<a name="purity"></a>

### <a name="purity"></a>순수성

계약 내에서 호출되는 모든 메서드는 순수해야 합니다. 즉, 기존 상태를 업데이트하면 안 됩니다. 순수 메서드는 순수 메서드에 진입한 후 생성된 개체를 수정할 수 있습니다.

코드 계약 도구는 현재 다음과 같은 코드 요소를 순수하다고 가정합니다.

- <xref:System.Diagnostics.Contracts.PureAttribute>로 표시된 메서드

- <xref:System.Diagnostics.Contracts.PureAttribute>로 표시된 형식(형식의 모든 메서드에 특성이 적용됨)

- 속성 get 접근자

- 연산자(이름이 "op"로 시작하고 한두 개의 매개 변수와 void가 아닌 반환 형식을 가진 static 메서드)

- 정규화된 이름이 "System.Diagnostics.Contracts.Contract", "System.String", "System.IO.Path" 또는 "System.Type"으로 시작하는 모든 메서드

- 호출된 대리자(대리자 형식 자체가 <xref:System.Diagnostics.Contracts.PureAttribute> 특성을 가진 경우) 대리자 형식 <xref:System.Predicate%601?displayProperty=nameWithType> 및 <xref:System.Comparison%601?displayProperty=nameWithType>은 순수하다고 간주됩니다.

<a name="visibility"></a>

### <a name="visibility"></a>표시 유형

계약에 언급된 모든 멤버는 최소한 멤버가 표시되는 메서드와 동일한 표시 유형이어야 합니다. 예를 들어 전용 필드는 public 메서드에 대한 사전 조건에서 언급할 수 없습니다. 클라이언트가 메서드를 호출하기 전에 이러한 계약의 유효성을 검사할 수 없습니다. 그러나 필드가 <xref:System.Diagnostics.Contracts.ContractPublicPropertyNameAttribute>로 표시된 경우에는 이러한 규칙에서 제외됩니다.

## <a name="example"></a>예제

다음 예제에서는 코드 계약을 사용하는 방법을 보여 줍니다.

[!code-csharp[ContractExample#1](../../../samples/snippets/csharp/VS_Snippets_CLR/contractexample/cs/program.cs#1)]
[!code-vb[ContractExample#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/contractexample/vb/program.vb#1)]
