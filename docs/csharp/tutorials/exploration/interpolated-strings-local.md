---
title: 문자열 보간 - C# 자습서
description: 이 자습서에서는 C# 문자열 보간 기능을 사용하여 더 큰 문자열에 형식이 지정된 식을 포함하는 방법을 보여 줍니다.
author: rpetrusha
ms.author: ronpet
ms.date: 10/23/2018
ms.openlocfilehash: e142c48cd944fd6119c697a299308dc9ce1203ca
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834130"
---
# <a name="use-string-interpolation-to-construct-formatted-strings"></a>문자열 보간을 사용하여 형식이 지정된 문자열 생성

이 자습서에서는 C# [문자열 보간](../../language-reference/tokens/interpolated.md)을 사용하여 단일 결과 문자열에 값을 삽입하는 방법을 설명합니다. C# 코드를 작성하고 컴파일 및 실행 결과를 확인합니다. 이 자습서는 문자열에 값을 삽입하고, 이러한 값을 다양한 방식으로 형식화하는 방법을 보여 주는 일련의 단원으로 구성됩니다.

이 자습서에서는 개발에 사용할 수 있는 머신이 있다고 예상합니다. .NET 자습서 [Hello World 10분 완성](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro)에는 Windows, Linux 또는 macOS의 로컬 개발 환경 설정에 대한 지침이 포함되어 있습니다. 브라우저에서 자습서의 [대화형 버전](interpolated-strings.yml)을 완료할 수도 있습니다.

## <a name="create-an-interpolated-string"></a>보간된 문자열 만들기

*interpolated*라는 디렉터리를 만듭니다. 현재 디렉터리로 만들고 콘솔 창에서 다음 명령을 실행합니다.

```dotnetcli
dotnet new console
```

이 명령은 현재 디렉터리에 새 .NET Core 콘솔 애플리케이션을 만듭니다.

원하는 편집기에서 *Program.cs*를 열고 `Console.WriteLine("Hello World!");` 줄을 다음 코드로 바꿉니다. 여기서 `<name>`을 사용자 이름으로 바꿉니다.

```csharp
var name = "<name>";
Console.WriteLine($"Hello, {name}. It's a pleasure to meet you!");
```

콘솔 창에 `dotnet run`을 입력하여 이 코드를 사용해 봅니다. 프로그램을 실행하면 인사말에 사용자 이름이 포함된 단일 문자열이 표시됩니다. <xref:System.Console.WriteLine%2A> 메서드 호출에 포함된 문자열은 *보간된 문자열 식*입니다. 이는 포함 코드가 들어있는 문자열에서 단일 문자열(*결과 문자열*이라고 함)을 생성할 수 있게 해주는 일종의 템플릿입니다. 보간된 문자열은 문자열에 값을 삽입하거나 문자열을 연결(함께 조인)하는 데 특히 유용합니다.

다음 간단한 예제에서는 모든 보간된 문자열이 포함해야 하는 두 가지 요소를 보여 줍니다.

- `$` 문자로 시작한 후 여는 따옴표 문자가 다음에 나오는 문자열 리터럴. `$` 기호와 따옴표 문자 사이에는 공백이 없어야 합니다. (공백을 포함하면 어떻게 되는지 확인하려면 `$` 문자 뒤에 공백을 삽입하고 파일을 저장한 후 콘솔 창에 `dotnet run`을 입력하여 프로그램을 다시 실행합니다. C# 컴파일러가 “오류 CS1056: 예기치 않은 문자 ‘$’”라는 오류 메시지를 표시합니다.)

- 하나 이상의 ‘보간 식’.  보간 식은 열기 및 닫기 중괄호(`{` 및 `}`)로 표시됩니다. 중괄호 안에 값을 반환(`null` 포함)하는 C# 식을 배치할 수 있습니다.

몇 가지 다른 데이터 형식을 포함하는 문자열 보간 예제를 더 살펴보겠습니다.

## <a name="include-different-data-types"></a>다양한 데이터 형식 포함

이전 섹션에서는 한 문자열을 다른 문자열 내에 삽입하는 데 문자열 보간을 사용했습니다. 보간 식의 결과는 모든 데이터 형식일 수 있습니다. 보간된 문자열에 다양한 데이터 형식의 값을 포함시켜 보겠습니다.

다음 예제에서는 먼저 `Name` [속성](../../properties.md)과 <xref:System.Object.ToString?displayProperty=nameWithType> 메서드의 동작을 [재정의](../../language-reference/keywords/override.md)하는 `ToString` [메서드](../../methods.md)가 있는 [클래스](../../programming-guide/classes-and-structs/classes.md) 데이터 형식 `Vegetable`을 정의합니다. [`public` 액세스 한정자](../../language-reference/keywords/public.md)를 지정하면 해당 메서드를 모든 클라이언트 코드에 사용하여 `Vegetable` 인스턴스의 문자열 표현을 가져올 수 있습니다. 예제에서 `Vegetable.ToString` 메서드는 `Vegetable` [생성자](../../programming-guide/classes-and-structs/constructors.md)에서 초기화된 `Name` 속성의 값을 반환합니다.

```csharp
public Vegetable(string name) => Name = name;
```

그런 다음, [`new` 연산자](../../language-reference/operators/new-operator.md)를 사용하고 생성자 `Vegetable`의 이름을 제공하여 `item`이라는 `Vegetable` 클래스의 인스턴스를 만듭니다.

```csharp
var item = new Vegetable("eggplant");
```

마지막으로 <xref:System.DateTime> 값, <xref:System.Decimal> 값 및 `Unit` [열거형](../../programming-guide/enumeration-types.md) 값을 포함하는 보간된 문자열에 `item` 변수를 포함시킵니다. 편집기에서 모든 C# 코드를 다음 코드로 바꾼 후 `dotnet run` 명령을 사용하여 실행합니다.

```csharp
using System;

public class Vegetable
{
   public Vegetable(string name) => Name = name;
   
   public string Name { get; }
   
   public override string ToString() => Name;
}

public class Program
{
   public enum Unit { item, kilogram, gram, dozen };

   public static void Main()
   {
      var item = new Vegetable("eggplant");
      var date = DateTime.Now;
      var price = 1.99m;
      var unit = Unit.item;
      Console.WriteLine($"On {date}, the price of {item} was {price} per {unit}.");
   }
}
```

보간된 문자열의 보간 식 `item`은 결과 문자열에 “eggplant”라는 텍스트로 확인됩니다. 이것은 식 결과의 형식이 문자열이 아닌 경우 다음과 같은 방식으로 결과가 문자열로 확인되기 때문입니다.

- 보간 식이 `null`로 평가되면 빈 문자열(“” 또는 <xref:System.String.Empty?displayProperty=nameWithType>)이 사용됩니다.

- 보간 식이 `null`로 계산되지 않고 결과 형식의 `ToString` 메서드가 호출됩니다. 이것은 `Vegetable.ToString` 메서드의 구현을 업데이트하여 테스트할 수 있습니다. 모든 형식에는 `ToString` 메서드가 구현되어 있으므로 이 메서드를 구현할 필요가 없을 수도 있습니다. 이것을 테스트하려면 예제에서 `Vegetable.ToString` 메서드 정의를 주석으로 처리합니다. (이렇게 하려면, 그 앞에 주석 기호 즉, `//`를 추가합니다.) 출력에서 "eggplant" 문자열은 정규화된 형식 이름(이 예제의 경우 "Vegetable")으로 바뀌며 이것이 <xref:System.Object.ToString?displayProperty=nameWithType> 메서드의 기본 동작입니다. 열거형 값에 대한 `ToString` 메서드의 기본 동작은 값의 문자열 표현을 반환하는 것입니다.

이 예제의 출력에서 날짜는 매우 정확하며(eggplant 가격은 초마다 변경되지 않음), 가격 값은 통화 단위를 나타내지 않습니다. 다음 섹션에서는 식 결과에 대한 문자열 표현의 형식을 제어하여 해당 문제를 해결하는 방법을 알아봅니다.

## <a name="control-the-formatting-of-interpolation-expressions"></a>보간 식의 서식 제어

이전 섹션에서는 형식이 잘못 지정된 두 개의 문자열을 결과 문자열에 삽입했습니다. 하나는 날짜만 적절한 날짜 및 시간 값이었습니다. 두 번째는 통화 단위를 나타내지 않는 가격이었습니다. 두 가지 문제는 쉽게 해결할 수 있습니다. 문자열 보간을 통해 특정 유형의 형식을 제어하는 *형식 문자열*을 지정할 수 있습니다. 다음 줄에 표시된 것처럼 이전 예제의 `Console.WriteLine`에 대한 호출을 수정하여 날짜 및 가격 식의 형식 문자열을 포함시킵니다.

```csharp
Console.WriteLine($"On {date:d}, the price of {item} was {price:C2} per {unit}.");
```

콜론(“:”)과 형식 문자열을 사용하여 보간 식에 따라 형식 문자열을 지정합니다. "d"는 간단한 날짜 형식을 나타내는 [표준 날짜 및 시간 형식 문자열](../../../standard/base-types/standard-date-and-time-format-strings.md#the-short-date-d-format-specifier)입니다. "C2"는 소수점 뒤 두 자릿수를 포함하는 통화 값으로 숫자를 나타내는 [표준 숫자 형식 문자열](../../../standard/base-types/standard-numeric-format-strings.md#the-currency-c-format-specifier)입니다.

.NET 라이브러리의 많은 형식은 미리 정의된 형식 문자열 집합을 지원합니다. 여기에는 모든 숫자 형식과 날짜 및 시간 형식이 포함됩니다. 형식 문자열을 지원하는 형식의 전체 목록을 보려면 [.NET의 서식 지정 형식](../../../standard/base-types/formatting-types.md) 문서의 [형식 문자열 및 .NET 클래스 라이브러리 형식](../../../standard/base-types/formatting-types.md#stringRef)을 참조하세요.

텍스트 편집기에서 형식 문자열을 수정하고, 변경할 때마다 프로그램을 다시 실행하여 날짜 및 시간의 서식과 숫자 값에 미치는 영향을 확인해 보세요. `{date:d}`의 "d"를 "t"(짧은 시간 형식 표시), "y"(연도 및 월 표시) 및 "yyyy"(연도를 4자리 숫자로 표시)로 변경합니다. `{price:C2}`의 "C2"를 "e"(지수 표기) 및 "F3"(소수점 뒤 세 자릿수의 숫자 값)으로 변경합니다.

형식을 제어하는 것 외에도, 결과 문자열에 포함된 형식이 지정된 문자열의 필드 너비와 맞춤을 제어할 수 있습니다. 다음 섹션에서 이 작업을 수행하는 방법을 알아봅니다.

## <a name="control-the-field-width-and-alignment-of-interpolation-expressions"></a>필드 너비와 보간 식의 맞춤을 제어합니다.

일반적으로 보간 식의 결과가 문자열로 형식이 지정되면 해당 문자열은 결과 문자열에 선행 또는 후행 공백 없이 포함됩니다. 특히 데이터 집합을 가지고 작업하는 경우 필드 너비와 텍스트 맞춤을 제어할 수 있으면 보다 읽기 쉬운 출력을 생성하는 데 도움이 됩니다. 이것을 확인하려면 텍스트 편집기에서 모든 코드를 다음 코드로 바꾼 후 `dotnet run`을 입력하여 프로그램을 실행합니다.

```csharp
using System;
using System.Collections.Generic;

public class Example
{
   public static void Main()
   {
      var titles = new Dictionary<string, string>()
      {
          ["Doyle, Arthur Conan"] = "Hound of the Baskervilles, The",
          ["London, Jack"] = "Call of the Wild, The",
          ["Shakespeare, William"] = "Tempest, The"
      };

      Console.WriteLine("Author and Title List");
      Console.WriteLine();
      Console.WriteLine($"|{"Author",-25}|{"Title",30}|");
      foreach (var title in titles)
         Console.WriteLine($"|{title.Key,-25}|{title.Value,30}|");
   }
}
```

작성자의 이름은 왼쪽 맞춤되며 이들이 작성한 제목은 오른쪽 맞춤됩니다. 보간 식 뒤에 쉼표(“,”)를 추가하고 ‘최소’ 필드 너비를 지정하여 맞춤을 지정합니다.  지정한 값이 양수이면 필드는 오른쪽 맞춤입니다. 음수이면 필드는 왼쪽 맞춤입니다.

다음 코드처럼 `{"Author",-25}` 및 `{title.Key,-25}` 코드에서 음수 기호를 제거하고 예제를 다시 실행해 보세요.

```csharp
Console.WriteLine($"|{"Author",25}|{"Title",30}|");
foreach (var title in titles)
   Console.WriteLine($"|{title.Key,25}|{title.Value,30}|");
```

이때 작성자 정보는 오른쪽 맞춤입니다.

하나의 보간 식에 대해 맞춤 지정자 및 형식 문자열을 결합할 수 있습니다. 이렇게 하려면 먼저 맞춤을 지정하고 콜론과 형식 문자열을 지정합니다. `Main` 메서드 내에 있는 모든 코드를 다음 코드로 바꾸면, 필드 너비가 정의된 세 가지 형식 지정된 문자열이 표시됩니다. 그런 다음 `dotnet run` 명령을 입력하여 프로그램을 실행합니다.

```csharp
Console.WriteLine($"[{DateTime.Now,-20:d}] Hour [{DateTime.Now,-10:HH}] [{1063.342,15:N2}] feet");
```

다음과 같은 출력을 얻을 수 있습니다.

```console
[04/14/2018          ] Hour [16        ] [       1,063.34] feet
```

문자열 보간 자습서를 완료했습니다.

자세한 내용은 [문자열 보간](../../language-reference/tokens/interpolated.md) 항목 및 [C#에서 문자열 보간](../../tutorials/string-interpolation.md) 자습서를 참조하세요.
