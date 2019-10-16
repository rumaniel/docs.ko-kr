---
title: 특성 - C#
description: C#에서 특성이 작동하는 방식을 알아봅니다.
author: mgroves
ms.date: 03/06/2017
ms.assetid: b152cf36-76e4-43a5-b805-1a1952e53b79
ms.openlocfilehash: 0037e8b2c5f50d1b8d0a950743f6eeb9145df414
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70851007"
---
# <a name="using-attributes-in-c"></a>C\#에서 특성 사용

특성은 선언적으로 정보를 코드와 연결하는 방법을 제공합니다. 다양한 대상에 적용할 수 있는 재사용 가능 요소를 제공할 수도 있습니다.

`[Obsolete]` 특성을 고려하세요. 이 특성은 클래스, 구조체, 메서드, 생성자 등에 적용될 수 있으며 요소가 더 이상 필요하지 않다는 사실을 _선언_합니다. 이 특성을 찾고 응답으로 특정 작업을 수행하는 것은 모두 C# 컴파일러가 진행합니다.

이 자습서에서는 코드에 특성을 추가하는 방법, 사용자 지정 특성을 만들고 사용하는 방법, .NET Core로 빌드되는 일부 특성을 사용하는 방법을 소개합니다.

## <a name="prerequisites"></a>전제 조건
.NET Core를 실행하도록 컴퓨터에 설정해야 합니다. [.NET Core 다운로드](https://dotnet.microsoft.com/download) 페이지에서 설치 지침을 찾을 수 있습니다.
Windows, Ubuntu Linux, macOS 또는 Docker 컨테이너에서 이 애플리케이션을 실행할 수 있습니다. 선호하는 코드 편집기를 설치해야 합니다. 아래 설명에서는 오픈 소스 플랫폼 간 편집기인 [Visual Studio Code](https://code.visualstudio.com/)를 사용합니다. 그러나 익숙한 어떤 도구도 사용 가능합니다.

## <a name="create-the-application"></a>애플리케이션 만들기

이제 모든 도구를 설치했으므로 새로운 .NET Core 애플리케이션을 만들어 보겠습니다. 명령줄 생성기를 사용하려면 즐겨 사용하는 셸에서 다음 명령을 실행합니다.

`dotnet new console`

이 명령은 기본 .NET Core 프로젝트 파일을 만듭니다. `dotnet restore`를 실행하여 이 프로젝트를 컴파일하는 데 필요한 종속성을 복원해야 합니다.

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

이 프로그램을 실행하려면 `dotnet run`을 사용합니다. 콘솔에 "Hello, World" 출력이 표시됩니다.

## <a name="how-to-add-attributes-to-code"></a>코드에 특성을 추가하는 방법

C#에서 특성은 `Attribute` 기본 클래스에서 상속되는 클래스입니다. `Attribute`에서 상속되는 모든 클래스는 코드의 다른 부분에서 일종의 "태그"로 사용될 수 있습니다.
예를 들어 `ObsoleteAttribute`라는 특성이 있습니다. 이 특성은 코드가 더 이상 사용되지 않으며 더 이상 사용할 수 없음을 알리기 위해 사용됩니다. 예를 들어 대괄호를 사용하여 클래스에 이 특성을 배치할 수 있습니다.

[!code-csharp[Obsolete attribute example](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#ObsoleteExample1)]  

이 클래스는 `ObsoleteAttribute`로 지칭되지만 코드에서 `[Obsolete]`를 사용하는 데만 필요합니다. 이것이 C#에서 준수하는 규칙입니다.
원할 경우 전체 이름 `[ObsoleteAttribute]`를 사용할 수 있습니다.

클래스를 더 이상 사용되지 않는 것으로 표시할 경우 더 이상 사용되지 않는 *이유* 및/또는 대싱 사용할 *항목*에 대한 정보를 제공하는 것이 좋습니다. 이 작업을 위해 Obsolete 특성에 문자열 매개 변수를 전달합니다.

[!code-csharp[Obsolete attribute example with parameters](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#ObsoleteExample2)]

이 문자열은 `var attr = new ObsoleteAttribute("some string")`를 작성하는 것처럼 `ObsoleteAttribute` 생성자에 인수로 전달됩니다.

특성 생성자에 대한 매개 변수는 단순 형식/리터럴인 `bool, int, double, string, Type, enums, etc` 및 해당 형식의 배열로 제한됩니다.
식 또는 변수는 사용할 수 없습니다. 위치 또는 명명된 매개 변수는 얼마든지 사용할 수 있습니다.

## <a name="how-to-create-your-own-attribute"></a>고유한 특성을 만드는 방법

특성을 만드는 과정은 `Attribute` 기본 클래스에서 상속하는 것만큼 간단합니다.

[!code-csharp[Create your own attribute](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#CreateAttributeExample1)]

위에 따라, 이제 코드베이스의 어디에서든지 `[MySpecial]`(또는 `[MySpecialAttribute]`)을 특성으로 사용할 수 있습니다.

[!code-csharp[Using your own attribute](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#CreateAttributeExample2)]

`ObsoleteAttribute` 트리거 같은 .NET 기본 클래스 라이브러리의 특성은 컴파일러 내에 특정 동작을 포함합니다. 그러나 만드는 특성은 메타데이터의 역할만 수행하며 특성 클래스 내의 코드는 실행되지 않습니다. 코드의 임의 위치에서 해당 메타데이터에 대해 작업을 수행할 수 있습니다(이 자습서의 뒷부분에 좀 더 자세히 설명되어 있음).

여기에는 확인해 볼만한 '과제'가 제공됩니다. 위에서 설명한 것처럼 특성을 사용할 때는 특정 형식만 인수로 전달되도록 허용됩니다. 그러나 특성 유형을 만들 때 C# 컴파일러는 사용자가 해당 매개 변수를 만들지 못하게 하지 않습니다. 아래 예제에서는 적절히 컴파일을 수행하는 생성자로 특성을 만들었습니다.

[!code-csharp[Valid constructor used in an attribute](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#AttributeGothca1)]

그러나 이 생성자를 특성 구문에서 사용할 수는 없습니다.

[!code-csharp[Invalid attempt to use the attribute constructor](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#AttributeGotcha2)]

위에서는 `Attribute constructor parameter 'myClass' has type 'Foo', which is not a valid attribute parameter type`과 같은 컴파일러 오류가 발생합니다.

## <a name="how-to-restrict-attribute-usage"></a>특성 사용을 제한하는 방법

특성은 다양한 "대상"에 사용할 수 있습니다. 위의 예제에서는 클래스에 대한 특성만 표시하지만 다음에도 사용될 수 있습니다.

* Assembly
* 클래스
* 생성자
* 대리자
* Enum
* 이벤트
* 필드
* GenericParameter
* 인터페이스
* 메서드
* Module
* 매개 변수
* 속성
* ReturnValue
* 구조체

특성 클래스를 만들 때 기본적으로 C#은 허용 가능한 특성 대상 중 하나에 대해 해당 특성을 사용할 수 있습니다. 특성을 특정 대상으로 제한하려는 경우 특성 클래스에 대해 `AttributeUsageAttribute`를 사용하면 됩니다. 맞습니다. 특성에 대한 특성입니다.

[!code-csharp[Using your own attribute](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#AttributeUsageExample1)]

클래스 또는 구조체 이외의 항목에 대해 위 특성을 적용하려고 하면 `Attribute 'MyAttributeForClassAndStructOnly' is not valid on this declaration type. It is only valid on 'class, struct' declarations`와 같은 컴파일러 오류가 발생합니다.

[!code-csharp[Using your own attribute](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#AttributeUsageExample2)]

## <a name="how-to-use-attributes-attached-to-a-code-element"></a>코드 요소에 연결된 특성을 사용하는 방법

특성는 메타데이터로 작동합니다. 외부 영향이 없으면 어떤 작업도 수행하지 않습니다.

특성을 찾아 작업을 수행하려면 일반적으로 [리플렉션](../programming-guide/concepts/reflection.md)이 필요합니다. 이 자습서에서는 리플렉션을 자세히 다루지 않겠지만, 기본 개념은 리플렉션을 사용하면 다른 코드를 검사하는 코드를 C#에서 작성할 수 있다는 것입니다.

예를 들어 리플렉션을 사용하여 클래스에 대한 정보(코드 헤드에 `using System.Reflection;` 추가)를 가져올 수 있습니다. 

[!code-csharp[Getting type information with Reflection](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#ReflectionExample1)]

다음과 같이 출력됩니다.`The assembly qualified name of MyClass is ConsoleApplication.MyClass, attributes, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`

`TypeInfo` 개체(또는 `MemberInfo`, `FieldInfo` 등)가 있으면 `GetCustomAttributes` 메서드를 사용할 수 있습니다. 그러면 `Attribute` 개체 컬렉션이 반환됩니다.
`GetCustomAttribute`를 사용하고 특성 유형을 지정할 수도 있습니다.

`MyClass`의 `MemberInfo` 인스턴스에 대해 `GetCustomAttributes`를 사용하는 예제는 다음과 같습니다(앞에서 살펴본 `[Obsolete]` 특성을 포함하는 예제).

[!code-csharp[Getting type information with Reflection](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#ReflectionExample2)]

해당 내용은 콘솔에 `Attribute on MyClass: ObsoleteAttribute`와 같이 표시됩니다. `MyClass`에 다른 특성을 추가해 보세요.

이러한 `Attribute` 개체가 지연되어 인스턴스화되는 것에 유의해야 합니다. 즉, `GetCustomAttribute` 또는 `GetCustomAttributes`를 사용해야만 인스턴스화됩니다.
또한 매번 인스턴스화되기도 합니다. `GetCustomAttributes`를 연속해서 2번 호출하면 2개의 다른 `ObsoleteAttribute` 인스턴스가 반환됩니다.

## <a name="common-attributes-in-the-base-class-library-bcl"></a>BCL(기본 클래스 라이브러리)의 공통 특성

특성은 많은 도구 및 프레임워크에서 사용됩니다. NUnit은 NUnit Test Runner에서 사용되는 `[Test]` 및 `[TestFixture]` 같은 특성을 사용합니다. ASP.NET MVC는 `[Authorize]`와 같은 특성을 사용하고 MVC 작업에 대해 크로스 커팅(Cross-Cutting) 문제를 해결하기 위한 작업 필터 프레임워크를 제공합니다. [PostSharp](https://www.postsharp.net)은 특성 구문을 사용하여 C#을 사용한 AOP(Aspect-Oriented Programming)를 허용합니다.

.NET Core 기본 클래스 라이브러리에 기본 제공되는 몇 가지 유의할 만한 특성은 다음과 같습니다.

* `[Obsolete]`. 이 특성은 위 예제에서 사용되었으며 `System` 네임스페이스에 있습니다. 기본 코드를 변경하는 방법에 대해 선언적 설명서를 제공하는 것이 유용합니다. 메시지는 문자열의 형태로 제공될 수 있으며 다른 부울 매개 변수가 컴파일러 경고를 컴파일러 오류로 에스컬레이션하는 데 사용될 수 있습니다.

* `[Conditional]`. 이 특성은 `System.Diagnostics` 네임스페이스에 있습니다. 이 특성은 메서드(또는 특성 클래스)에 적용할 수 있습니다. 생성자에는 문자열을 전달해야 합니다.
해당 문자열이 `#define` 지시문과 일치하지 않는 경우 해당 메서드에 대한 호출(메서드 자체는 아님)이 C# 컴파일러에 의해 제거됩니다. 일반적으로 이 특성은 디버깅(진단) 목적으로 사용됩니다.

* `[CallerMemberName]`. 이 특성은 매개 변수에 사용될 수 있으며 `System.Runtime.CompilerServices` 네임스페이스에 있습니다. 다른 메서드를 호출하는 메서드의 이름을 삽입하는 데 사용되는 특성입니다. 일반적으로 다양한 UI 프레임워크에서 INotifyPropertyChanged를 구현하는 경우 '매직 문자열'을 제거하는 방법으로 사용됩니다. 예제:

[!code-csharp[Using CallerMemberName when implementing INotifyPropertyChanged](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#CallerMemberName1)]

위의 코드에서는 리터럴 `"Name"` 문자열이 없어도 됩니다. 이 경우 입력 관련 버그가 방지되며 좀 더 매끄러운 리팩터링/이름 바꾸기가 가능해집니다.

## <a name="summary"></a>요약

특성은 C#에 선언적 기능을 제공하지만 코드의 메타데이터 형식이며 단독으로 동작하지 않습니다.
