---
title: 분기 및 루프 - C# 소개 자습서
description: 분기 및 루프에 관한 이 자습서에서는 C# 코드를 작성하여 문을 반복적으로 실행하기 위한 조건부 분기 및 루프를 지원하는 언어 구문을 살펴봅니다.
ms.date: 10/31/2017
ms.custom: mvc
ms.openlocfilehash: a0701a63d6c3aece6bac4263cbcf8a682a623cf7
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834119"
---
# <a name="learn-conditional-logic-with-branch-and-loop-statements"></a>분기 및 루프 문이 포함된 조건부 논리 알아보기

이 자습서에서는 변수를 검사하고 해당 변수에 따라 실행 경로를 변경하는 코드를 작성하는 방법에 대해 설명합니다. C# 코드를 작성하고 컴파일 및 실행 결과를 확인합니다. 이 자습서에는 C#에서 분기 및 루프 구문을 살펴보는 일련의 단원이 포함되어 있습니다. 이러한 단원에서는 C# 언어의 기본 사항을 설명합니다.

이 자습서에서는 개발에 사용할 수 있는 머신이 있다고 예상합니다. .NET 자습서 [Hello World 10분 완성](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro)에는 Windows, Linux 또는 macOS의 로컬 개발 환경 설정에 대한 지침이 포함되어 있습니다. 사용할 명령에 대한 간단한 개요는 [개발 도구 익히기](local-environment.md)에 자세한 정보의 링크와 함께 나와 있습니다.

## <a name="make-decisions-using-the-if-statement"></a>`if` 문을 사용하여 결정하기

*branches-tutorial*이라는 디렉터리를 만듭니다. 현재 디렉터리로 지정하고 `dotnet new console -n BranchesAndLoops -o .`을 실행합니다. 이 명령은 현재 디렉터리에 새 .NET Core 콘솔 애플리케이션을 만듭니다.

원하는 편집기에서 *Program.cs*를 열고 `Console.WriteLine("Hello World!");` 줄을 다음 코드로 바꿉니다.

```csharp
int a = 5;
int b = 6;
if (a + b > 10)
    Console.WriteLine("The answer is greater than 10.");
```

콘솔 창에 `dotnet run`을 입력하여 이 코드를 사용해 봅니다. “The answer is greater than 10.”(답은 10보다 큽니다.)이라는 메시지가 콘솔에 출력되어야 합니다.

합계가 10보다 작도록 `b`의 선언을 수정합니다.

```csharp
int b = 3;
```

`dotnet run`을 다시 입력합니다. 답이 10보다 작기 때문에 아무것도 출력되지 않습니다. 테스트하는 **조건**은 false입니다. `if` 문에 대해 가능한 분기 중 하나(true 분기)만 작성했기 때문에 실행할 코드가 없습니다.

> [!TIP]
> C# (또는 다른 프로그래밍 언어)를 살펴보면서 코드를 작성할 때 실수를 하게 될 것입니다. 컴파일러가 오류를 찾아 보고합니다. 오류 출력 및 오류를 생성한 코드를 자세히 살펴봅니다. 일반적으로 컴파일러 오류는 문제를 찾는 데 도움이 될 수 있습니다.

이 첫 번째 샘플에서는 `if`의 기능과 부울 형식을 보여 줍니다. *부울*은 `true` 또는 `false`의 두 값 중 하나를 가질 수 있는 변수입니다. C#은 부울 변수에 대한 특수 형식 `bool`을 정의합니다. `if` 문은 `bool`의 값을 확인합니다. 값이 `true`인 경우 `if` 뒤의 문이 실행됩니다. 그러하지 않으면 건너뜁니다.

조건을 확인하고 해당 조건에 따라 문을 실행하는 이 프로세스는 아주 강력합니다.

## <a name="make-if-and-else-work-together"></a>if와 else를 함께 사용하기

true 분기와 false 분기의 여러 코드를 실행하려면 조건이 false일 때 실행되는 `else` 분기를 생성합니다. 다음과 같이 해보세요. 아래 코드의 마지막 두 줄을 `Main` 메서드에 추가합니다(이미 처음 네 줄은 있음).

```csharp
int a = 5;
int b = 3;
if (a + b > 10)
    Console.WriteLine("The answer is greater than 10");
else
    Console.WriteLine("The answer is not greater than 10");
```

`else` 키워드 뒤의 문은 테스트하는 조건이 `false`인 경우에만 실행됩니다. `if` 및 `else`를 부울 조건과 결합하면 `true`와 `false` 조건을 모두 처리하는 데 필요한 모든 기능이 제공됩니다.

> [!IMPORTANT]
> `if` 및 `else` 문 아래의 들여쓰기는 사용자가 보기 편하도록 하기 위함입니다.
> C# 언어는 들여쓰기 또는 공백을 중요하게 취급하지 않습니다.
> `if` 또는 `else` 키워드 뒤의 문은 조건에 따라 실행됩니다. 이 자습서의 모든 샘플에서는 문의 제어 흐름을 기준으로 줄을 들여쓰는 일반적인 방법을 따릅니다.

들여쓰기는 중요하지 않기 때문에 `{` 및 `}`를 사용하여 두 개 이상의 문이 조건부로 실행되는 블록의 일부가 되는 시기를 나타내야 합니다. C# 프로그래머는 일반적으로 모든 `if` 및 `else` 절에서 중괄호를 사용합니다. 다음 예제는 방금 작성한 코드와 같습니다. 다음 코드와 일치하도록 위의 코드를 수정합니다.

```csharp
int a = 5;
int b = 3;
if (a + b > 10)
{
    Console.WriteLine("The answer is greater than 10");
}
else
{
    Console.WriteLine("The answer is not greater than 10");
}
```

> [!TIP]
> 이 자습서의 나머지 부분에서 코드 샘플에는 일반적인 방법에 따라 모두 중괄호가 포함되어 있습니다.

더 복잡한 조건을 테스트할 수 있습니다. `Main` 메서드에서 지금까지 작성한 코드 뒤에 다음 코드를 추가합니다.

```csharp
int c = 4;
if ((a + b + c > 10) && (a == b))
{
    Console.WriteLine("The answer is greater than 10");
    Console.WriteLine("And the first number is equal to the second");
}
else
{
    Console.WriteLine("The answer is not greater than 10");
    Console.WriteLine("Or the first number is not equal to the second");
}
```

`==` 기호는 같음을 테스트합니다.  `==`을 사용하면 같음 테스트가 `a = 5`에서 확인한 할당과 구분됩니다.

`&&`는 “and”를 나타냅니다. true 분기에서 문을 실행하려면 두 조건이 모두 true여야 합니다.  이러한 예제에서는 `{` 및 `}`로 문을 묶으면 각 조건부 분기에 여러 문을 가질 수 있음도 보여 줍니다.

`||`을 사용하여 “or”를 나타낼 수도 있습니다. 지금까지 작성한 코드 뒤에 다음 코드를 추가합니다.

```csharp
if ((a + b + c > 10) || (a == b))
{
    Console.WriteLine("The answer is greater than 10");
    Console.WriteLine("Or the first number is equal to the second");
}
else
{
    Console.WriteLine("The answer is not greater than 10");
    Console.WriteLine("And the first number is not equal to the second");
}
```

`a`, `b` 및 `c`의 값을 수정하고 `&&` 및 `||` 간에 전환하여 살펴봅니다. `&&` 및 `||` 연산자가 어떻게 작동하는지 더 잘 이해할 수 있습니다.

첫 번째 단계를 완료했습니다. 다음 섹션을 시작하기 전에 현재 코드를 별도의 메서드로 이동합니다. 이렇게 하면 새 예제 작업을 쉽게 시작할 수 있습니다. `Main` 메서드의 이름을 `ExploreIf`로 바꾸고 `ExploreIf`를 호출하는 새 `Main` 메서드를 작성합니다. 작업을 마치면 코드가 다음과 같이 됩니다.

```csharp
using System;

namespace BranchesAndLoops
{
    class Program
    {
        static void ExploreIf()
        {
            int a = 5;
            int b = 3;
            if (a + b > 10)
            {
                Console.WriteLine("The answer is greater than 10");
            }
            else
            {
                Console.WriteLine("The answer is not greater than 10");
            }

            int c = 4;
            if ((a + b + c > 10) && (a > b))
            {
                Console.WriteLine("The answer is greater than 10");
                Console.WriteLine("And the first number is greater than the second");
            }
            else
            {
                Console.WriteLine("The answer is not greater than 10");
                Console.WriteLine("Or the first number is not greater than the second");
            }

            if ((a + b + c > 10) || (a > b))
            {
                Console.WriteLine("The answer is greater than 10");
                Console.WriteLine("Or the first number is greater than the second");
            }
            else
            {
                Console.WriteLine("The answer is not greater than 10");
                Console.WriteLine("And the first number is not greater than the second");
            }
        }

        static void Main(string[] args)
        {
            ExploreIf();
        }
    }
}
```

`ExploreIf()`에 대한 호출을 주석으로 처리합니다. 그러면 이 섹션에서 작업할 때 출력이 덜 복잡해집니다.

```csharp
//ExploreIf();
```

`//`는 C#에서 **주석**을 시작합니다. 주석은 소스 코드에 유지하되 코드로 실행하지는 않으려는 모든 텍스트입니다. 컴파일러는 주석에서 실행 코드를 생성하지 않습니다.

## <a name="use-loops-to-repeat-operations"></a>루프를 사용하여 작업 반복

이 섹션에서는 **루프**를 사용하여 문을 반복합니다. `Main` 메서드에 다음 코드를 사용해 봅니다.

```csharp
int counter = 0;
while (counter < 10)
{
    Console.WriteLine($"Hello World! The counter is {counter}");
    counter++;
}
```

`while` 문은 조건을 검사하고 `while` 뒤에 있는 문 또는 문 블록을 실행합니다. 조건이 false가 될 때까지 반복적으로 조건을 확인하고 해당 문을 실행합니다.

이 예제에서는 다른 새 연산자가 하나 있습니다. `counter` 변수 뒤의 `++`는 **증가** 연산자입니다. 이 연산자는 `counter`의 값에 1을 더하고 해당 값을 `counter` 변수에 저장합니다.

> [!IMPORTANT]
> 코드를 실행할 때 `while` 루프 조건이 false로 바뀌는지 확인합니다. 그러하지 않으면 프로그램이 종료되지 않는 **무한 루프**를 생성합니다. 이러한 내용이 이 샘플에 설명되어 있지는 않은데, **CTRL-C** 또는 다른 방법을 사용하여 프로그램을 강제 종료해야 하기 때문입니다.

`while` 루프는 `while` 뒤에 코드를 실행하기 전에 조건을 테스트합니다. `do` ... `while` 루프는 코드를 먼저 실행한 후 조건을 확인합니다. do while 루프는 다음 코드에 나와 있습니다.

```csharp
int counter = 0;
do
{
    Console.WriteLine($"Hello World! The counter is {counter}");
    counter++;
} while (counter < 10);
```

이 `do` 루프 및 이전 `while` 루프는 같은 출력을 생성합니다.

## <a name="work-with-the-for-loop"></a>for 루프 작업

C#에서는 일반적으로 **for** 루프가 사용됩니다. Main() 메서드에 다음 코드를 사용해 봅니다.

```csharp
for (int index = 0; index < 10; index++)
{
    Console.WriteLine($"Hello World! The index is {index}");
}
```

`while` 루프 및 이미 사용한 `do` 루프와 동일한 작업을 수행합니다. `for` 문에는 작동 방식을 제어하는 세 부분이 있습니다.

첫 번째 부분은 **for 이니셜라이저입니다**. `int index = 0;`은 `index`가 루프 변수임을 선언하고 첫 번째 값을 `0`으로 설정합니다.

중간 부분은 **for 조건입니다**. `index < 10`은 이 `for` 루프가 카운터 값이 10보다 작으면 계속 실행됨을 선언합니다.

마지막 부분은 **for 반복기입니다**. `index++`는 `for` 문 다음의 블록을 실행한 후 루프 변수를 수정하는 방법을 지정합니다. 여기서 `index`는 블록이 실행될 때마다 1씩 증가하도록 지정합니다.

직접 실습해 보세요. 다음 각각을 시도해 보세요.

- 다른 값으로 시작하도록 이니셜라이저를 변경합니다.
- 다른 값에서 중지하도록 조건을 변경합니다.

완료하면, 학습한 내용을 토대로 직접 코드를 작성해 보겠습니다.

## <a name="combine-branches-and-loops"></a>분기 및 루프 결합

이제 C# 언어로 된 `if` 문과 루프 구조를 확인했습니다. C# 코드를 작성하여 3으로 나눌 수 있는, 1에서 20까지의 모든 정수의 합계를 찾을 수 있는지 확인해 보세요.  다음은 몇 가지 힌트입니다.

- `%` 연산자는 나누기 연산의 나머지를 제공합니다.
- `if` 문은 숫자가 합계의 일부여야 하는지를 확인하는 조건을 제공합니다.
- `for` 루프는 1에서 20까지의 모든 숫자에 대해 일련의 단계를 반복하는 데 도움이 됩니다.

직접 시도해 보세요. 그런 다음 어떻게 했는지 확인하세요. 답으로 63을 받아야 합니다. [GitHub에서 완성된 코드를 보고](https://github.com/dotnet/samples/tree/master/csharp/branches-quickstart/Program.cs#L46-L54) 가능한 한 가지 답을 확인할 수 있습니다.

“분기 및 루프” 자습서를 완료했습니다.

자체 개발 환경에서 [배열 및 컬렉션](arrays-and-collections.md) 자습서를 계속할 수 있습니다.

다음 항목에서는 해당 개념에 대해 더 자세히 알아볼 수 있습니다.

- [If 및 else 문](../../language-reference/keywords/if-else.md)
- [While 문](../../language-reference/keywords/while.md)
- [Do 문](../../language-reference/keywords/do.md)
- [For 문](../../language-reference/keywords/for.md)
