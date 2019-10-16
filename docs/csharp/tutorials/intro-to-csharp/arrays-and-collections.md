---
title: 컬렉션 작업 - C# 소개 자습서
description: 이 자습서에서는 목록 컬렉션을 살펴보면서 C#에 대해 학습합니다.
ms.date: 10/13/2017
ms.custom: mvc
ms.openlocfilehash: b80225cf1614a7c25ac9011acd39e74032465ca3
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834144"
---
# <a name="learn-to-manage-data-collections-using-the-generic-list-type"></a>일반 목록 형식을 사용하여 데이터 컬렉션을 관리하는 방법 알아보기

이 소개 자습서에서는 C# 언어 및 <xref:System.Collections.Generic.List%601> 클래스의 기본 사항을 소개합니다.

이 자습서에서는 개발에 사용할 수 있는 머신이 있다고 예상합니다. .NET 자습서 [Hello World 10분 완성](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro)에는 Windows, Linux 또는 macOS의 로컬 개발 환경 설정에 대한 지침이 포함되어 있습니다. 사용할 명령에 대한 간단한 개요는 [개발 도구 익히기](local-environment.md)에 자세한 정보의 링크와 함께 나와 있습니다.

## <a name="a-basic-list-example"></a>기본 목록 예제

*list-tutorial*이라는 디렉터리를 만듭니다. 현재 디렉터리로 지정하고 `dotnet new console`을 실행합니다.

편집기에서 *Program.cs*를 열고 기존 코드를 다음으로 바꿉니다.

```csharp
using System;
using System.Collections.Generic;

namespace list_tutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            var names = new List<string> { "<name>", "Ana", "Felipe" };
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }
        }
    }
}
```

`<name>`을 사용자의 이름으로 바꿉니다. *Program.cs*를 저장합니다. 콘솔 창에 `dotnet run`을 입력하여 시도해 보세요.

문자열 목록을 만들고, 해당 목록에 3개의 이름을 추가하고, 이름을 모두 대문자로 출력했습니다. 이전 자습서에서 학습한 개념을 사용하여 목록을 반복합니다.

이름을 표시하는 코드는 [문자열 보간](../../language-reference/tokens/interpolated.md) 기능을 사용합니다.  `string` 앞에 `$` 문자를 넣으면 문자열 선언에 C# 코드를 포함할 수 있습니다. 실제 문자열은 C# 코드를 생성하는 값으로 바꿉니다. 이 예제에서는 <xref:System.String.ToUpper%2A> 메서드를 호출했기 때문에 `{name.ToUpper()}`를 대문자로 변환된 각 이름으로 바꿉니다.

계속해서 살펴보겠습니다.

## <a name="modify-list-contents"></a>목록 콘텐츠 수정

생성한 컬렉션은 <xref:System.Collections.Generic.List%601> 형식을 사용합니다. 이 형식은 요소의 시퀀스를 저장합니다. 꺾쇠 괄호 사이의 요소 형식을 지정합니다.

이 <xref:System.Collections.Generic.List%601> 형식은 늘리거나 줄일 수 있어 요소를 추가하거나 제거할 수 있습니다. `Main` 메서드에서 `}`를 닫기 전에 이 코드를 추가합니다.

```csharp
Console.WriteLine();
names.Add("Maria");
names.Add("Bill");
names.Remove("Ana");
foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

목록 끝에 이름을 두 개 더 추가했습니다. 또한 이름을 하나 제거했습니다. 파일을 저장하고 `dotnet run`을 입력하여 시도해 보세요.

<xref:System.Collections.Generic.List%601>를 사용하면 **인덱스**별로 각 항목을 참조할 수도 있습니다. 목록 이름 뒤 `[`와 `]` 토큰 사이에 인덱스를 배치합니다. C#은 첫 번째 인덱스에 0을 사용합니다. 방금 추가한 코드 바로 아래에 이 코드를 추가하여 시도합니다.

```csharp
Console.WriteLine($"My name is {names[0]}");
Console.WriteLine($"I've added {names[2]} and {names[3]} to the list");
```

목록의 끝을 벗어나는 인덱스에 액세스할 수 없습니다. 인덱스는 0부터 시작하므로, 가장 큰 유효 인덱스는 목록의 항목 수보다 하나 작습니다. <xref:System.Collections.Generic.List%601.Count%2A> 속성을 사용하여 목록의 길이를 확인할 수 있습니다. Main 메서드의 끝에 다음 코드를 추가합니다.

```csharp
Console.WriteLine($"The list has {names.Count} people in it");
 ```

파일을 저장하고 `dotnet run`을 다시 입력하여 결과를 확인합니다.

## <a name="search-and-sort-lists"></a>목록 검색 및 정렬

샘플에서는 상대적으로 작은 목록을 사용하지만 애플리케이션에서는 수천에 달하는 많은 요소가 포함된 목록을 작성할 수 있습니다. 이러한 큰 컬렉션에서 요소를 찾으려면 여러 항목의 목록을 검색해야 합니다. <xref:System.Collections.Generic.List%601.IndexOf%2A> 메서드는 항목을 검색하고 항목의 인덱스를 반환합니다. `Main` 메서드의 맨 아래에 이 코드를 추가합니다.

```csharp
var index = names.IndexOf("Felipe");
if (index == -1)
{
    Console.WriteLine($"When an item is not found, IndexOf returns {index}");
}
else
{
    Console.WriteLine($"The name {names[index]} is at index {index}");
}

index = names.IndexOf("Not Found");
if (index == -1)
{
    Console.WriteLine($"When an item is not found, IndexOf returns {index}");
}
else
{
    Console.WriteLine($"The name {names[index]} is at index {index}");

}
```

목록의 항목도 정렬할 수 있습니다. <xref:System.Collections.Generic.List%601.Sort%2A> 메서드는 일반적인 순서(문자열의 경우 사전순)로 목록의 모든 항목을 정렬합니다. `Main` 메서드의 맨 아래에 이 코드를 추가합니다.

```csharp
names.Sort();
foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

파일을 저장하고 `dotnet run`을 입력하여 이 최신 버전을 사용해 보세요.

다음 섹션을 시작하기 전에 현재 코드를 별도의 메서드로 이동합니다. 이렇게 하면 새 예제 작업을 쉽게 시작할 수 있습니다. `Main` 메서드의 이름을 `WorkingWithStrings`로 바꾸고 `WorkingWithStrings`를 호출하는 새 `Main` 메서드를 작성합니다. 작업을 마치면 코드가 다음과 같이 됩니다.

```csharp
using System;
using System.Collections.Generic;

namespace list_tutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            WorkingWithStrings();
        }

        public static void WorkingWithStrings()
        {
            var names = new List<string> { "<name>", "Ana", "Felipe" };
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }

            Console.WriteLine();
            names.Add("Maria");
            names.Add("Bill");
            names.Remove("Ana");
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }

            Console.WriteLine($"My name is {names[0]}");
            Console.WriteLine($"I've added {names[2]} and {names[3]} to the list");

            Console.WriteLine($"The list has {names.Count} people in it");

            var index = names.IndexOf("Felipe");
            Console.WriteLine($"The name {names[index]} is at index {index}");

            var notFound = names.IndexOf("Not Found");
            Console.WriteLine($"When an item is not found, IndexOf returns {notFound}");

            names.Sort();
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }
        }
    }
}
```

## <a name="lists-of-other-types"></a>다른 형식 목록

지금까지 목록에 `string` 형식을 사용했습니다. 다른 형식을 사용하여 <xref:System.Collections.Generic.List%601>를 만들어 보겠습니다. 숫자 집합을 빌드하겠습니다.

새 `Main` 메서드의 맨 아래에 다음을 추가합니다.

```csharp
var fibonacciNumbers = new List<int> {1, 1};
```

정수 목록을 만들고 처음 두 정수를 값 1로 설정합니다. 숫자 시퀀스인 *피보나치 시퀀스*의 첫 번째 두 값입니다. 다음 각 피보나치 수는 이전의 두 수의 합계를 사용하여 찾습니다. 이 코드를 추가합니다.

```csharp
var previous = fibonacciNumbers[fibonacciNumbers.Count - 1];
var previous2 = fibonacciNumbers[fibonacciNumbers.Count - 2];

fibonacciNumbers.Add(previous + previous2);

foreach (var item in fibonacciNumbers)
    Console.WriteLine(item);
```

파일을 저장하고 `dotnet run`을 입력하여 결과를 확인합니다.

> [!TIP]
> 이 섹션에만 집중하려면 `WorkingWithStrings();`를 호출하는 코드를 주석으로 처리할 수 있습니다. `// WorkingWithStrings();`처럼 호출 앞에 `/` 문자를 두 개 배치합니다.

## <a name="challenge"></a>과제

이 단원과 이전 단원에서 학습한 개념을 함께 적용할 수 있는지 확인하세요. 피보나치 수를 사용하여 지금까지 빌드한 내용을 확장합니다. 코드를 작성하여 시퀀스에서 처음 20개 수를 생성합니다. (힌트: 20번째 피보나치 수는 6765입니다.)

## <a name="complete-challenge"></a>과제 완료

[GitHub에서 완료된 샘플 코드를 보고](https://github.com/dotnet/samples/tree/master/csharp/list-quickstart/Program.cs#L13-L23) 예제 솔루션을 확인할 수 있습니다.

루프의 각 반복을 통해 목록의 마지막 두 정수를 사용하고, 더하고, 해당 값을 목록에 추가합니다. 목록에 20개의 항목이 추가될 때까지 루프가 반복됩니다.

축하합니다. 목록 자습서를 완료했습니다. 자체 개발 환경에서 [클래스 소개](introduction-to-classes.md) 자습서를 계속할 수 있습니다.

[.NET 가이드](../../../standard/index.md)의 [컬렉션](../../../standard/collections/index.md) 항목에서 `List` 형식에 대해 더 자세히 학습할 수 있습니다. 다른 많은 컬렉션 형식에 대해서도 학습합니다.
