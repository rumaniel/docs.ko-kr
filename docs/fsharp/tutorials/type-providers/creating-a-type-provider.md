---
title: '자습서: 형식 공급자 만들기'
description: 몇 가지 간단한 형식 공급자를 F# 검사 하 여 F# 기본 개념을 보여 주는 3.0에서 고유한 형식 공급자를 만드는 방법에 대해 알아봅니다.
ms.date: 02/02/2019
ms.openlocfilehash: 8d1a1fedf03437ccbacd40616cc7dc3e1da435b2
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71214266"
---
# <a name="tutorial-create-a-type-provider"></a>자습서: 형식 공급자 만들기

의 F# 형식 공급자 메커니즘은 정보 기능이 풍부한 프로그래밍에 대 한 지원의 중요 한 부분입니다. 이 자습서에서는 기본 개념을 설명 하기 위해 몇 가지 간단한 형식 공급자를 개발 하는 과정을 통해 사용자 고유의 형식 공급자를 만드는 방법을 설명 합니다. 의 F#형식 공급자 메커니즘에 대 한 자세한 내용은 [형식 공급자](index.md)를 참조 하십시오.

F# 에코 시스템에는 일반적으로 사용 되는 인터넷 및 엔터프라이즈 데이터 서비스에 대 한 다양 한 형식 공급자가 포함 되어 있습니다. 예:

- [Fsharp.core](https://fsharp.github.io/FSharp.Data/) 에는 JSON, XML, CSV 및 HTML 문서 형식에 대 한 형식 공급자가 포함 되어 있습니다.

- [Sqlprovider](https://fsprojects.github.io/SQLProvider/) 는 이러한 데이터 원본에 대 한 개체 매핑과 F# LINQ 쿼리를 통해 SQL database에 대 한 강력한 형식의 액세스를 제공 합니다.

- [Fsharp.core](https://fsprojects.github.io/FSharp.Data.SqlClient/) 에는의 F#t-sql을 확인 하는 컴파일 시간에 대 한 형식 공급자 집합이 있습니다.

- [Fsharp.core 공급자](https://fsprojects.github.io/FSharp.Data.TypeProviders/) 는 SQL, Entity Framework, ODATA 및 WSDL Data services에 액세스 하기 위한 .NET Framework 프로그래밍에만 사용할 수 있는 이전 형식 공급자 집합입니다.

필요한 경우 사용자 지정 형식 공급자를 만들거나 다른 사용자가 만든 형식 공급자를 참조할 수 있습니다. 예를 들어 조직에는 각각 자체의 안정적인 데이터 스키마를 포함 하는 많은 수의 명명 된 데이터 집합을 제공 하는 데이터 서비스가 있을 수 있습니다. 스키마를 읽고 강력한 형식의 방식으로 프로그래머에 게 현재 데이터 집합을 제공 하는 형식 공급자를 만들 수 있습니다.

## <a name="before-you-start"></a>시작하기 전에

형식 공급자 메커니즘은 주로 안정적인 데이터 및 서비스 정보 공간을 F# 프로그래밍 환경에 삽입 하도록 디자인 되었습니다.

이 메커니즘은 프로그램 논리와 관련 된 방식으로 프로그램 실행 중에 스키마가 변경 되는 정보 공간을 삽입 하기 위한 것이 아닙니다. 또한이 메커니즘은 도메인에 일부 유효한 사용이 포함 되어 있는 경우에도 언어 간 메타 프로그래밍을 위해 디자인 되지 않았습니다. 필요한 경우에만이 메커니즘을 사용 하 고 형식 공급자의 개발에서 매우 높은 값을 생성 해야 합니다.

스키마를 사용할 수 없는 형식 공급자를 작성 하지 않아야 합니다. 마찬가지로 일반적인 (또는 기존) .NET 라이브러리에서 충분 한 형식 공급자를 작성 하지 않아야 합니다.

시작 하기 전에 다음 질문을 할 수 있습니다.

- 정보 소스에 대 한 스키마가 있나요? 그렇다면 .NET 형식 시스템에 대 F# 한 매핑은 무엇입니까?

- 기존 (동적으로 형식화 된) API를 구현에 대 한 시작 지점으로 사용할 수 있나요?

- 사용자와 조직에서 형식 공급자를 충분히 사용 하 여 it를 효율적으로 작성할 수 있나요? 정상적인 .NET 라이브러리가 사용자의 요구를 충족 하나요?

- 스키마가 얼마나 변경 되나요?

- 코딩 중에 변경 됩니까?

- 코딩 세션 간에 변경 됩니까?

- 프로그램 실행 중에 변경 됩니까?

형식 공급자는 런타임에 그리고 컴파일된 코드의 수명 동안 안정적으로 작동 하는 상황에 가장 적합 합니다.

## <a name="a-simple-type-provider"></a>단순 형식 공급자

이 샘플은 `examples` [ F# 형식 공급자 SDK](https://github.com/fsprojects/FSharp.TypeProviders.SDK/)의 디렉터리에 있는 샘플과 유사한 HelloWorldTypeProvider입니다. 공급자는 서명 구문을 사용 F# 하 고 모든를 제외 `Type1`하 고 세부 정보를 생략 하 여 다음 코드와 같이, 100 지워진 형식을 포함 하는 "형식 공간"을 사용할 수 있도록 합니다. 지워진 형식에 대 한 자세한 내용은이 항목의 뒷부분에 나오는 [지워진 제공 형식에 대 한 세부](#details-about-erased-provided-types) 정보를 참조 하세요.

```fsharp
namespace Samples.HelloWorldTypeProvider

type Type1 =
    /// This is a static property.
    static member StaticProperty : string

    /// This constructor takes no arguments.
    new : unit -> Type1

    /// This constructor takes one argument.
    new : data:string -> Type1

    /// This is an instance property.
    member InstanceProperty : int

    /// This is an instance method.
    member InstanceMethod : x:int -> char

    nested type NestedType =
        /// This is StaticProperty1 on NestedType.
        static member StaticProperty1 : string
        …
        /// This is StaticProperty100 on NestedType.
        static member StaticProperty100 : string

type Type2 =
…
…

type Type100 =
…
```

제공 된 형식 및 멤버 집합은 정적으로 알려져 있습니다. 이 예제에서는 공급자의 기능을 활용 하 여 스키마에 종속 된 형식을 제공 하지 않습니다. 형식 공급자의 구현은 다음 코드에서 간략하게 설명 하 고 세부 정보는이 항목의 이후 섹션에서 설명 합니다.

> [!WARNING]
> 이 코드와 온라인 샘플 간에는 차이점이 있을 수 있습니다.

```fsharp
namespace Samples.FSharp.HelloWorldTypeProvider

open System
open System.Reflection
open ProviderImplementation.ProvidedTypes
open FSharp.Core.CompilerServices
open FSharp.Quotations

// This type defines the type provider. When compiled to a DLL, it can be added
// as a reference to an F# command-line compilation, script, or project.
[<TypeProvider>]
type SampleTypeProvider(config: TypeProviderConfig) as this =

  // Inheriting from this type provides implementations of ITypeProvider
  // in terms of the provided types below.
  inherit TypeProviderForNamespaces(config)

  let namespaceName = "Samples.HelloWorldTypeProvider"
  let thisAssembly = Assembly.GetExecutingAssembly()

  // Make one provided type, called TypeN.
  let makeOneProvidedType (n:int) =
  …
  // Now generate 100 types
  let types = [ for i in 1 .. 100 -> makeOneProvidedType i ]

  // And add them to the namespace
  do this.AddNamespace(namespaceName, types)

[<assembly:TypeProviderAssembly>]
do()
```

이 공급자를 사용 하려면 별도의 Visual Studio 인스턴스를 열고, F# 스크립트를 만든 다음, 다음 코드에 표시 된 대로 #r를 사용 하 여 스크립트의 공급자에 대 한 참조를 추가 합니다.

```fsharp
#r @".\bin\Debug\Samples.HelloWorldTypeProvider.dll"

let obj1 = Samples.HelloWorldTypeProvider.Type1("some data")

let obj2 = Samples.HelloWorldTypeProvider.Type1("some other data")

obj1.InstanceProperty
obj2.InstanceProperty

[ for index in 0 .. obj1.InstanceProperty-1 -> obj1.InstanceMethod(index) ]
[ for index in 0 .. obj2.InstanceProperty-1 -> obj2.InstanceMethod(index) ]

let data1 = Samples.HelloWorldTypeProvider.Type1.NestedType.StaticProperty35
```

그런 다음 형식 공급자가 생성 한 `Samples.HelloWorldTypeProvider` 네임 스페이스에서 형식을 찾습니다.

공급자를 다시 컴파일하기 전에 공급자 DLL을 사용 하는 Visual Studio 및 F# 대화형의 모든 인스턴스를 닫았는지 확인 합니다. 그렇지 않으면 출력 DLL이 잠기므로 빌드 오류가 발생 합니다.

Print 문을 사용 하 여이 공급자를 디버깅 하려면 공급자와 관련 된 문제를 노출 하는 스크립트를 만든 후 다음 코드를 사용 합니다.

```console
fsc.exe -r:bin\Debug\HelloWorldTypeProvider.dll script.fsx
```

Visual Studio를 사용 하 여이 공급자를 디버깅 하려면 관리자 자격 증명을 사용 하 여 Visual Studio에 대 한 개발자 명령 프롬프트를 열고 다음 명령을 실행 합니다.

```console
devenv.exe /debugexe fsc.exe -r:bin\Debug\HelloWorldTypeProvider.dll script.fsx
```

또는 Visual Studio를 열고, 디버그 메뉴를 열고,를 선택 `Debug/Attach to process…`하 고, 스크립트를 편집 하는 다른 `devenv` 프로세스에 연결 합니다. 이 메서드를 사용 하 여 두 번째 인스턴스 (전체 IntelliSense 및 기타 기능 사용)에 식을 대화형으로 입력 하 여 형식 공급자에서 특정 논리를 보다 쉽게 대상으로 지정할 수 있습니다.

내 코드만 디버깅을 사용 하지 않도록 설정 하 여 생성 된 코드에서 오류를 더 잘 식별할 수 있습니다. 이 기능을 사용 하거나 사용 하지 않도록 설정 하는 방법에 대 한 자세한 내용은 [디버거를 사용 하 여 코드 탐색](/visualstudio/debugger/navigating-through-code-with-the-debugger)을 참조 하세요. 또한 `Debug` 메뉴를 연 `Exceptions` 다음 Ctrl + Alt + `Exceptions` E 키를 선택 하 여 대화 상자를 열면 첫 번째 예외 catch를 설정할 수도 있습니다. 이 대화 상자의 아래 `Common Language Runtime Exceptions`에서 `Thrown` 확인란을 선택 합니다.

### <a name="implementation-of-the-type-provider"></a>형식 공급자 구현

이 섹션에서는 형식 공급자 구현의 주요 섹션을 안내 합니다. 먼저 사용자 지정 형식 공급자 자체에 대 한 형식을 정의 합니다.

```fsharp
[<TypeProvider>]
type SampleTypeProvider(config: TypeProviderConfig) as this =
```

이 형식은 public 이어야 하며, 다른 F# 프로젝트에서 해당 형식을 포함 하는 어셈블리를 참조할 때 컴파일러가 형식 공급자를 인식할 수 있도록 [typeprovider](https://msdn.microsoft.com/library/bdf7b036-7490-4ace-b79f-c5f1b1b37947) 특성으로 표시 해야 합니다. *Config* 매개 변수는 선택 사항이 며, 있는 경우 컴파일러에서 F# 생성 하는 형식 공급자 인스턴스에 대 한 컨텍스트 구성 정보를 포함 합니다.

다음으로 [ITypeProvider](https://msdn.microsoft.com/library/2c2b0571-843d-4a7d-95d4-0a7510ed5e2f) 인터페이스를 구현 합니다. 이 경우 `TypeProviderForNamespaces` `ProvidedTypes` API의 형식을 기본 형식으로 사용 합니다. 이 도우미 형식은 적극적으로 제공 되는 네임 스페이스의 한정 된 컬렉션을 제공할 수 있습니다. 각 네임 스페이스는 고정 된 수의 고정 된 형식을 직접 포함 합니다. 이 컨텍스트에서 공급자는 필요 하거나 사용 하지 않더라도 형식을 *적극적* 으로 생성 합니다.

```fsharp
inherit TypeProviderForNamespaces(config)
```

그런 다음 제공 된 형식에 대 한 네임 스페이스를 지정 하는 로컬 전용 값을 정의 하 고 형식 공급자 어셈블리 자체를 찾습니다. 이 어셈블리는 나중에 제공 된 지워진 형식의 논리적 부모 형식으로 사용 됩니다.

```fsharp
let namespaceName = "Samples.HelloWorldTypeProvider"
let thisAssembly = Assembly.GetExecutingAssembly()
```

다음에는 각 형식 Type1을 제공 하는 함수를 만듭니다. Type100. 이 기능에 대해서는이 항목의 뒷부분에서 자세히 설명 합니다.

```fsharp
let makeOneProvidedType (n:int) = …
```

다음으로 100 제공 유형을 생성 합니다.

```fsharp
let types = [ for i in 1 .. 100 -> makeOneProvidedType i ]
```

다음으로 형식을 제공 된 네임 스페이스로 추가 합니다.

```fsharp
do this.AddNamespace(namespaceName, types)
```

마지막으로, 형식 공급자 DLL을 만드는 중임을 나타내는 어셈블리 특성을 추가 합니다.

```fsharp
[<assembly:TypeProviderAssembly>]
do()
```

### <a name="providing-one-type-and-its-members"></a>한 형식 및 해당 멤버 제공

함수 `makeOneProvidedType` 는 형식 중 하나를 제공 하는 실제 작업을 수행 합니다.

```fsharp
let makeOneProvidedType (n:int) =
…
```

이 단계에서는이 함수를 구현 하는 방법을 설명 합니다. 먼저 제공 된 형식 (예: Type1, when n = 1, Type57, n = 57 인 경우)을 만듭니다.

```fsharp
// This is the provided type. It is an erased provided type and, in compiled code,
// will appear as type 'obj'.
let t = ProvidedTypeDefinition(thisAssembly, namespaceName,
                               "Type" + string n,
                               baseType = Some typeof<obj>)
```

다음 사항에 유의 해야 합니다.

- 제공 된 형식이 지워집니다.  기본 형식이 `obj`임을 나타내므로 인스턴스는 컴파일된 코드에서 [obj](https://msdn.microsoft.com/library/dcf2430f-702b-40e5-a0a1-97518bf137f7) 형식의 값으로 표시 됩니다.

- 중첩 되지 않은 형식을 지정 하는 경우 어셈블리와 네임 스페이스를 지정 해야 합니다. 지워진 형식의 경우 어셈블리는 형식 공급자 어셈블리 자체 여야 합니다.

그런 다음 형식에 XML 문서를 추가 합니다. 이 설명서는 지연 됩니다. 즉, 호스트 컴파일러에 필요한 경우에는 요청 시에 계산 됩니다.

```fsharp
t.AddXmlDocDelayed (fun () -> sprintf "This provided type %s" ("Type" + string n))
```

다음에는 제공 된 정적 속성을 형식에 추가 합니다.

```fsharp
let staticProp = ProvidedProperty(propertyName = "StaticProperty",
                                  propertyType = typeof<string>,
                                  isStatic = true,
                                  getterCode = (fun args -> <@@ "Hello!" @@>))
```

이 속성을 가져오면 항상 문자열 "Hello!"로 평가 됩니다. 속성 `GetterCode` 의는 호스트 컴파일러가 속성 F# 을 가져오기 위해 생성 하는 코드를 나타내는 따옴표를 사용 합니다. 인용구에 대 한 자세한 내용은 [코드 인용 (F#)](https://msdn.microsoft.com/library/6f055397-a1f0-4f9a-927c-f0d7c6951155)을 참조 하세요.

속성에 XML 문서를 추가 합니다.

```fsharp
staticProp.AddXmlDocDelayed(fun () -> "This is a static property")
```

이제 제공 된 속성을 제공 된 형식에 연결 합니다. 제공 된 멤버를 한 형식에만 연결 해야 합니다. 그렇지 않은 경우에는 멤버에 액세스할 수 없습니다.

```fsharp
t.AddMember staticProp
```

이제 매개 변수를 사용 하지 않는 제공 된 생성자를 만듭니다.

```fsharp
let ctor = ProvidedConstructor(parameters = [ ],
                               invokeCode = (fun args -> <@@ "The object data" :> obj @@>))
```

생성자 `InvokeCode` 의는 생성자가 호출 F# 될 때 호스트 컴파일러가 생성 하는 코드를 나타내는 따옴표를 반환 합니다. 예를 들어 다음 생성자를 사용할 수 있습니다.

```fsharp
new Type10()
```

제공 된 형식의 인스턴스는 기본 데이터 "the object data"를 사용 하 여 생성 됩니다. 따옴표 붙은 코드는 제공 된 형식을 선언할 때 지정한 대로이 형식이 제공 된 형식을 모두 지우기 때문에 [obj](https://msdn.microsoft.com/library/dcf2430f-702b-40e5-a0a1-97518bf137f7) 로의 변환을 포함 합니다.

생성자에 XML 문서를 추가 하 고 제공 된 형식에 제공 된 생성자를 추가 합니다.

```fsharp
ctor.AddXmlDocDelayed(fun () -> "This is a constructor")

t.AddMember ctor
```

하나의 매개 변수를 사용 하는 제공 된 두 번째 생성자를 만듭니다.

```fsharp
let ctor2 =
ProvidedConstructor(parameters = [ ProvidedParameter("data",typeof<string>) ],
                    invokeCode = (fun args -> <@@ (%%(args.[0]) : string) :> obj @@>))
```

생성자 `InvokeCode` 에 대 한는 호스트 컴파일러가 F# 메서드를 호출 하기 위해 생성 한 코드를 나타내는 따옴표를 다시 반환 합니다. 예를 들어 다음 생성자를 사용할 수 있습니다.

```fsharp
new Type10("ten")
```

제공 된 형식의 인스턴스는 기본 데이터 "10"을 사용 하 여 생성 됩니다. `InvokeCode` 함수가 따옴표를 반환 한다는 것을 이미 알고 있을 수 있습니다. 이 함수에 대 한 입력은 생성자 매개 변수 별로 하나씩 식의 목록입니다. 이 경우 단일 매개 변수 값을 나타내는 식은에서 `args.[0]`사용할 수 있습니다. 생성자를 호출 하는 코드는 반환 값을 지워진 형식 `obj`으로 강제 변환 합니다. 제공 된 두 번째 생성자를 형식에 추가한 후에는 제공 된 인스턴스 속성을 만듭니다.

```fsharp
let instanceProp =
    ProvidedProperty(propertyName = "InstanceProperty",
                     propertyType = typeof<int>,
                     getterCode= (fun args ->
                        <@@ ((%%(args.[0]) : obj) :?> string).Length @@>))
instanceProp.AddXmlDocDelayed(fun () -> "This is an instance property")
t.AddMember instanceProp
```

이 속성을 가져오면 표시 개체인 문자열의 길이가 반환 됩니다. 속성 `GetterCode` 은 호스트 컴파일러가 F# 속성을 얻기 위해 생성 하는 코드를 지정 하는 따옴표를 반환 합니다. 와 `InvokeCode`같이 함수 `GetterCode` 는 따옴표를 반환 합니다. 호스트 컴파일러는 인수 목록을 사용 하 여이 함수를 호출 합니다. 이 경우 인수는를 사용 `args.[0]`하 여 액세스할 수 있는 getter가 호출 되는 인스턴스를 나타내는 단일 식만 포함 합니다. 그런 다음의 `GetterCode` 구현은 지운 형식의 `obj`결과 따옴표로 스플라이스, 캐스팅은 개체가 문자열인 형식을 확인 하는 컴파일러의 메커니즘을 충족 하는 데 사용 됩니다. 의 `makeOneProvidedType` 다음 부분에서는 하나의 매개 변수를 사용 하는 인스턴스 메서드를 제공 합니다.

```fsharp
let instanceMeth =
    ProvidedMethod(methodName = "InstanceMethod",
                   parameters = [ProvidedParameter("x",typeof<int>)],
                   returnType = typeof<char>,
                   invokeCode = (fun args ->
                       <@@ ((%%(args.[0]) : obj) :?> string).Chars(%%(args.[1]) : int) @@>))

instanceMeth.AddXmlDocDelayed(fun () -> "This is an instance method")
// Add the instance method to the type.
t.AddMember instanceMeth
```

마지막으로 100 중첩 된 속성을 포함 하는 중첩 형식을 만듭니다. 이 중첩 된 형식과 해당 속성의 생성은 지연 됩니다. 즉, 요청 시 계산 됩니다.

```fsharp
t.AddMembersDelayed(fun () ->
  let nestedType = ProvidedTypeDefinition("NestedType", Some typeof<obj>)

  nestedType.AddMembersDelayed (fun () ->
    let staticPropsInNestedType =
      [ for i in 1 .. 100 do
          let valueOfTheProperty = "I am string "  + string i

          let p =
            ProvidedProperty(propertyName = "StaticProperty" + string i,
              propertyType = typeof<string>,
              isStatic = true,
              getterCode= (fun args -> <@@ valueOfTheProperty @@>))

          p.AddXmlDocDelayed(fun () ->
              sprintf "This is StaticProperty%d on NestedType" i)

          yield p ]

    staticPropsInNestedType)

  [nestedType])
```

### <a name="details-about-erased-provided-types"></a>지워진 제공 유형에 대 한 세부 정보

이 섹션의 예제에서는 다음과 같은 경우에 특히 유용한 *지워진 제공 형식만*제공 합니다.

- 데이터 및 메서드만 포함 하는 정보 공간에 대 한 공급자를 작성 하는 경우

- 정확한 런타임 형식 의미 체계가 중요 하지 않은 공급자를 작성 하는 경우 정보 공간을 실제로 사용 하는 것이 중요 합니다.

- 정보 공간에 대 한 공급자를 작성 하는 경우 해당 정보 공간에 대 한 실제 .NET 형식을 생성 하는 것은 기술적으로는 불가능 합니다.

이 예제에서 제공 된 각 형식은 형식 `obj`으로 지워지고 형식의 모든 사용은 컴파일된 코드에서 형식 `obj` 으로 표시 됩니다. 실제로 이러한 예제의 기본 개체는 문자열 이지만 형식은 .net 컴파일 코드에서로 `System.Object` 표시 됩니다. 형식 지우기를 사용할 때와 마찬가지로 명시적 boxing, unboxing 및 캐스트를 사용 하 여 방해할 지워진 형식을 사용할 수 있습니다. 이 경우 개체를 사용할 때 유효 하지 않은 캐스트 예외가 발생할 수 있습니다. 공급자 런타임은 고유한 개인 표현 형식을 정의 하 여 가양성을 방지할 수 있습니다. 지워진 형식을 자체적으로 F# 정의할 수는 없습니다. 제공 된 유형만 지울 수 있습니다. 형식 공급자에 대해 지워진 유형을 사용 하거나 지워진 유형을 제공 하는 공급자를 사용 하는 경우의 실제 및 의미 체계를 이해 해야 합니다. 지워진 유형에는 실제 .NET 유형이 없습니다. 따라서 형식에 대해 정확한 리플렉션을 수행할 수 없으며, 런타임 캐스트를 사용 하는 경우와 정확한 런타임 형식 의미 체계를 사용 하는 기타 기술을 사용 하는 경우에는 지워진 형식을 방해할 수 있습니다. 지워진 형식의 Subversion은 런타임에 형식 캐스팅 예외가 발생 합니다.

### <a name="choosing-representations-for-erased-provided-types"></a>지워진 제공 형식에 대 한 표현 선택

지워진 제공 형식의 일부 사용에는 표현이 필요 하지 않습니다. 예를 들어, 지워진 제공 된 형식에는 정적 속성 및 멤버만 포함 되 고 생성자는 포함 되지 않을 수 있으며, 메서드나 속성은 형식의 인스턴스를 반환 하지 않습니다. 지워진 제공 된 유형의 인스턴스에 도달할 수 있는 경우 다음 질문을 고려해 야 합니다.

**제공 된 형식의 지우기는 무엇 인가요?**

- 제공 된 형식을 지울 때 형식이 컴파일된 .NET 코드에 표시 되는 방식입니다.

- 제공 된 지워진 클래스 형식을 삭제 하는 것은 항상 형식의 상속 체인에서 삭제 되지 않은 첫 번째 기본 형식입니다.

- 제공 된 지워진 인터페이스 형식은 항상 `System.Object`지워집니다.

**제공 된 형식의 표현은 무엇입니까?**

- 지워진 제공 된 형식에 대해 가능한 개체 집합을 해당 표현 이라고 합니다. 이 문서의 예제에서 모든 지워진 제공 된 형식의 `Type1..Type100` 표현은 항상 문자열 개체입니다.

제공 된 형식의 모든 표현은 제공 된 형식의 지우기와 호환 되어야 합니다. 그렇지 않으면 컴파일러에서 F# 형식 공급자 사용에 대 한 오류를 제공 하거나, 유효 하지 않은 비안정형 .net 코드가 생성 됩니다. 형식 공급자는 유효하지 않은 표현을 제공하는 코드를 반환하는 경우 사용할 수 없습니다.)

다음 방법 중 하나를 사용 하 여 제공 된 개체에 대 한 표현을 선택할 수 있습니다 .이 두 가지 방법 모두 매우 일반적입니다.

- 기존 .NET 형식에 대 한 강력한 형식의 래퍼를 제공 하는 경우 형식에서 해당 형식을 지우거 나, 해당 형식의 인스턴스를 표현으로 사용 하거나, 두 가지 방법을 모두 사용 하는 것이 적합 합니다. 이 방법은 강력한 형식의 버전을 사용할 때 해당 형식에 대 한 대부분의 기존 메서드가 여전히 적합 한 경우에 적합 합니다.

- 기존 .NET API와 크게 다른 API를 만들려는 경우 제공 된 형식에 대 한 형식 지우기 및 표현이 되는 런타임 형식을 만드는 것이 좋습니다.

이 문서의 예제에서는 문자열을 제공 된 개체의 표현으로 사용 합니다. 다른 개체를 사용 하 여 표현 하는 것이 적합할 수도 있습니다. 예를 들어 사전을 속성 모음으로 사용할 수 있습니다.

```fsharp
ProvidedConstructor(parameters = [],
    invokeCode= (fun args -> <@@ (new Dictionary<string,obj>()) :> obj @@>))
```

또는 형식 공급자에서 런타임에 사용 되는 형식을 정의 하 여 하나 이상의 런타임 작업과 함께 표현을 만들 수 있습니다.

```fsharp
type DataObject() =
    let data = Dictionary<string,obj>()
    member x.RuntimeOperation() = data.Count
```

제공 된 멤버는이 개체 형식의 인스턴스를 생성할 수 있습니다.

```fsharp
ProvidedConstructor(parameters = [],
    invokeCode= (fun args -> <@@ (new DataObject()) :> obj @@>))
```

이 경우에는 `baseType` `ProvidedTypeDefinition`를 생성할 때이 형식을로 지정 하 여 형식 지우기로이 형식을 사용할 수 있습니다 (옵션).

```fsharp
ProvidedTypeDefinition(…, baseType = Some typeof<DataObject> )
…
ProvidedConstructor(…, InvokeCode = (fun args -> <@@ new DataObject() @@>), …)
```

### <a name="key-lessons"></a>주요 단원

이전 단원에서는 다양 한 형식, 속성 및 메서드를 제공 하는 간단한 지우기 형식 공급자를 만드는 방법을 설명 했습니다. 또한이 섹션에서는 형식 공급자에서 지워진 형식을 제공 하는 경우의 장점과 단점을 비롯 하 여 형식 지우기의 개념에 대해 설명 하 고, 지워진 형식의 표현에 대해 설명 했습니다.

## <a name="a-type-provider-that-uses-static-parameters"></a>정적 매개 변수를 사용 하는 형식 공급자입니다.

공급자가 로컬 또는 원격 데이터에 액세스할 필요가 없는 경우에도 정적 데이터를 사용 하 여 형식 공급자를 매개 변수화 하는 기능이 많은 흥미로운 시나리오를 가능 하 게 합니다. 이 섹션에서는 이러한 공급자를 통합 하기 위한 몇 가지 기본 기술에 대해 알아봅니다.

### <a name="type-checked-regex-provider"></a>선택 된 Regex 공급자 유형

다음 컴파일 시간을 제공 하는 인터페이스에서 .net <xref:System.Text.RegularExpressions.Regex> 라이브러리를 래핑하는 정규식에 대 한 형식 공급자를 구현 한다고 가정 합니다.

- 정규식이 유효한 지 여부를 확인 하는 중입니다.

- 정규식의 그룹 이름을 기반으로 하는 일치 항목에 명명 된 속성을 제공 합니다.

이 섹션에서는 형식 공급자를 사용 하 여 이러한 혜택을 `RegexTyped` 제공 하기 위해 정규식 패턴에서 매개 변수화 하는 형식을 만드는 방법을 보여 줍니다. 제공 된 패턴이 유효 하지 않을 경우 컴파일러에서 오류를 보고 하 고, 형식 공급자가 패턴에서 그룹을 추출 하 여 일치 하는 명명 된 속성을 사용 하 여 액세스할 수 있습니다. 형식 공급자를 디자인할 때 노출 되는 API가 최종 사용자에 게 표시 되는 방법 및이 디자인을 .NET 코드로 변환 하는 방법을 고려해 야 합니다. 다음 예제에서는 이러한 API를 사용 하 여 지역 코드의 구성 요소를 가져오는 방법을 보여 줍니다.

```fsharp
type T = RegexTyped< @"(?<AreaCode>^\d{3})-(?<PhoneNumber>\d{3}-\d{4}$)">
let reg = T()
let result = T.IsMatch("425-555-2345")
let r = reg.Match("425-555-2345").Group_AreaCode.Value //r equals "425"
```

다음 예제에서는 형식 공급자가 이러한 호출을 변환 하는 방법을 보여 줍니다.

```fsharp
let reg = new Regex(@"(?<AreaCode>^\d{3})-(?<PhoneNumber>\d{3}-\d{4}$)")
let result = reg.IsMatch("425-123-2345")
let r = reg.Match("425-123-2345").Groups.["AreaCode"].Value //r equals "425"
```

다음 사항에 유의 하세요.

- 표준 Regex 형식은 매개 변수가 `RegexTyped` 있는 형식을 나타냅니다.

- 생성자 `RegexTyped` 는 Regex 생성자를 호출 하 여 패턴에 대 한 정적 형식 인수를 전달 합니다.

- `Match` 메서드의 결과는 표준 <xref:System.Text.RegularExpressions.Match> 형식으로 표현 됩니다.

- 각 명명 된 그룹은 제공 된 속성을 생성 하 고 속성에 액세스 하면 일치 `Groups` 하는 컬렉션에 대해 인덱서가 사용 됩니다.

다음 코드는 이러한 공급자를 구현 하는 논리의 핵심 이며,이 예제에서는 제공 된 형식에 대 한 모든 멤버의 추가를 생략 합니다. 추가 된 각 멤버에 대 한 자세한 내용은이 항목의 뒷부분에 있는 해당 섹션을 참조 하세요. 전체 코드를 보려면 CodePlex 웹 사이트의 [ F# 3.0 샘플 팩](https://archive.codeplex.com/?p=fsharp3sample) 에서 샘플을 다운로드 하세요.

```fsharp
namespace Samples.FSharp.RegexTypeProvider

open System.Reflection
open Microsoft.FSharp.Core.CompilerServices
open Samples.FSharp.ProvidedTypes
open System.Text.RegularExpressions

[<TypeProvider>]
type public CheckedRegexProvider() as this =
    inherit TypeProviderForNamespaces()

    // Get the assembly and namespace used to house the provided types
    let thisAssembly = Assembly.GetExecutingAssembly()
    let rootNamespace = "Samples.FSharp.RegexTypeProvider"
    let baseTy = typeof<obj>
    let staticParams = [ProvidedStaticParameter("pattern", typeof<string>)]

    let regexTy = ProvidedTypeDefinition(thisAssembly, rootNamespace, "RegexTyped", Some baseTy)

    do regexTy.DefineStaticParameters(
        parameters=staticParams,
        instantiationFunction=(fun typeName parameterValues ->

          match parameterValues with
          | [| :? string as pattern|] ->

            // Create an instance of the regular expression.
            //
            // This will fail with System.ArgumentException if the regular expression is not valid.
            // The exception will escape the type provider and be reported in client code.
            let r = System.Text.RegularExpressions.Regex(pattern)

            // Declare the typed regex provided type.
            // The type erasure of this type is 'obj', even though the representation will always be a Regex
            // This, combined with hiding the object methods, makes the IntelliSense experience simpler.
            let ty =
              ProvidedTypeDefinition(
                thisAssembly,
                rootNamespace,
                typeName,
                baseType = Some baseTy)

            ...

            ty
          | _ -> failwith "unexpected parameter values"))

    do this.AddNamespace(rootNamespace, [regexTy])

[<TypeProviderAssembly>]
do ()
```

다음 사항에 유의 하세요.

- 형식 공급자는 두 개의 정적 매개 변수 `pattern`를 사용 합니다 .이 매개 변수는 필수 `options`이며 기본값은 제공 되기 때문입니다 (선택 사항).

- 정적 인수를 제공한 후 정규식의 인스턴스를 만듭니다. Regex의 형식이 잘못 된 경우이 인스턴스는 예외를 throw 하 고이 오류는 사용자에 게 보고 됩니다.

- `DefineStaticParameters` 콜백 내에서 인수를 제공한 후에 반환 되는 형식을 정의 합니다.

- 이 코드를 `HideObjectMethods` true로 설정 하면 IntelliSense 환경이 간소화 됩니다. 이 `Equals`특성은 제공 된 개체에 대 `GetType` 한 IntelliSense 목록에서 `Finalize`, `GetHashCode`, 및 멤버를 표시 하지 않도록 합니다.

- 메서드의 기본 `obj` 형식으로를 사용 하지만 다음 예제와 같이 개체를 `Regex` 이 형식의 런타임 표현으로 사용 합니다.

- 정규식에 대 `Regex` 한 호출은 정규식이 <xref:System.ArgumentException> 유효 하지 않을 때을 throw 합니다. 컴파일러는이 예외를 catch 하 고 컴파일 타임 또는 Visual Studio 편집기에서 사용자에 게 오류 메시지를 보고 합니다. 이 예외를 사용 하면 응용 프로그램을 실행 하지 않고 정규식의 유효성을 검사할 수 있습니다.

위에서 정의한 형식은 의미 있는 메서드나 속성을 포함 하지 않기 때문에 아직 유용 하지 않습니다. 먼저 정적 `IsMatch` 메서드를 추가 합니다.

```fsharp
let isMatch =
    ProvidedMethod(
        methodName = "IsMatch",
        parameters = [ProvidedParameter("input", typeof<string>)],
        returnType = typeof<bool>,
        isStatic = true,
        invokeCode = fun args -> <@@ Regex.IsMatch(%%args.[0], pattern) @@>)

isMatch.AddXmlDoc "Indicates whether the regular expression finds a match in the specified input string."
ty.AddMember isMatch
```

이전 코드는 문자열을 입력 `IsMatch`으로 사용 하 고를 `bool`반환 하는 메서드를 정의 합니다. 유일한 까다로운 부분은 `args` `InvokeCode` 정의 내에서 인수를 사용 하는 것입니다. 이 예제 `args` 에서는이 메서드에 대 한 인수를 나타내는 인용구의 목록입니다. 메서드가 인스턴스 메서드인 경우 첫 번째 인수는 `this` 인수를 나타냅니다. 그러나 정적 메서드의 경우 인수는 모두 단순히 메서드에 대 한 명시적 인수입니다. 따옴표 붙은 값의 형식은 지정 된 반환 형식 (이 경우 `bool`)과 일치 해야 합니다. 또한이 코드에서는 `AddXmlDoc` 메서드를 사용 하 여 제공 된 메서드에 IntelliSense를 통해 제공할 수 있는 유용한 설명서가 있는지도 확인 합니다.

다음으로, 인스턴스 일치 메서드를 추가 합니다. 그러나이 메서드는 지정 `Match` 된 형식의 값을 반환 해야 그룹에 강력한 형식의 방식으로 액세스할 수 있습니다. 따라서 먼저 `Match` 형식을 선언 합니다. 이 형식은 정적 인수로 제공 된 패턴에 따라 달라 지므로이 형식은 매개 변수가 있는 형식 정의 내에 중첩 되어야 합니다.

```fsharp
let matchTy =
    ProvidedTypeDefinition(
        "MatchType",
        baseType = Some baseTy,
        hideObjectMethods = true)

ty.AddMember matchTy
```

그런 다음 각 그룹의 일치 형식에 하나의 속성을 추가 합니다. 런타임에 일치 항목은 <xref:System.Text.RegularExpressions.Match> 값으로 표시 되므로 속성을 정의 하는 따옴표는 <xref:System.Text.RegularExpressions.Match.Groups> 인덱싱된 속성을 사용 하 여 관련 그룹을 가져와야 합니다.

```fsharp
for group in r.GetGroupNames() do
    // Ignore the group named 0, which represents all input.
    if group <> "0" then
    let prop =
      ProvidedProperty(
        propertyName = group,
        propertyType = typeof<Group>,
        getterCode = fun args -> <@@ ((%%args.[0]:obj) :?> Match).Groups.[group] @@>)
        prop.AddXmlDoc(sprintf @"Gets the ""%s"" group from this match" group)
    matchTy.AddMember prop
```

다시, 제공 된 속성에 XML 문서를 추가 하 고 있음을 확인 합니다. 또한 `GetterCode` 함수를 제공 하는 경우 속성을 읽을 수 있으며 `SetterCode` 함수를 제공 하는 경우 속성을 쓸 수 있으므로 결과 속성은 읽기 전용입니다.

이제 다음 `Match` 형식의 값을 반환 하는 인스턴스 메서드를 만들 수 있습니다.

```fsharp
let matchMethod =
    ProvidedMethod(
        methodName = "Match",
        parameters = [ProvidedParameter("input", typeof<string>)],
        returnType = matchTy,
        invokeCode = fun args -> <@@ ((%%args.[0]:obj) :?> Regex).Match(%%args.[1]) :> obj @@>)

matchMeth.AddXmlDoc "Searches the specified input string for the first occurrence of this regular expression"

ty.AddMember matchMeth
```

인스턴스 메서드 `args.[0]` 를 만들기 때문에는 메서드가 호출 `args.[1]` 되 `RegexTyped` 는 인스턴스를 나타내고는 입력 인수입니다.

마지막으로 제공 된 형식의 인스턴스를 만들 수 있도록 생성자를 제공 합니다.

```fsharp
let ctor =
    ProvidedConstructor(
        parameters = [],
        invokeCode = fun args -> <@@ Regex(pattern, options) :> obj @@>)

ctor.AddXmlDoc("Initializes a regular expression instance.")

ty.AddMember ctor
```

생성자는 표준 .net Regex 인스턴스를 만들 때만 삭제 하 고,는 제공 된 형식을 삭제 하기 때문에 `obj` 개체에 다시 boxed 됩니다. 이와 같이 변경 하면 항목에서 이전에 지정한 샘플 API 사용이 예상 대로 작동 합니다. 다음 코드는 전체 및 최종입니다.

```fsharp
namespace Samples.FSharp.RegexTypeProvider

open System.Reflection
open Microsoft.FSharp.Core.CompilerServices
open Samples.FSharp.ProvidedTypes
open System.Text.RegularExpressions

[<TypeProvider>]
type public CheckedRegexProvider() as this =
    inherit TypeProviderForNamespaces()

    // Get the assembly and namespace used to house the provided types.
    let thisAssembly = Assembly.GetExecutingAssembly()
    let rootNamespace = "Samples.FSharp.RegexTypeProvider"
    let baseTy = typeof<obj>
    let staticParams = [ProvidedStaticParameter("pattern", typeof<string>)]

    let regexTy = ProvidedTypeDefinition(thisAssembly, rootNamespace, "RegexTyped", Some baseTy)

    do regexTy.DefineStaticParameters(
        parameters=staticParams,
        instantiationFunction=(fun typeName parameterValues ->

            match parameterValues with
            | [| :? string as pattern|] ->

                // Create an instance of the regular expression.

                let r = System.Text.RegularExpressions.Regex(pattern)

                // Declare the typed regex provided type.

                let ty =
                    ProvidedTypeDefinition(
                        thisAssembly,
                        rootNamespace,
                        typeName,
                        baseType = Some baseTy)

                ty.AddXmlDoc "A strongly typed interface to the regular expression '%s'"

                // Provide strongly typed version of Regex.IsMatch static method.
                let isMatch =
                    ProvidedMethod(
                        methodName = "IsMatch",
                        parameters = [ProvidedParameter("input", typeof<string>)],
                        returnType = typeof<bool>,
                        isStatic = true,
                        invokeCode = fun args -> <@@ Regex.IsMatch(%%args.[0], pattern) @@>)

                isMatch.AddXmlDoc "Indicates whether the regular expression finds a match in the specified input string"

                ty.AddMember isMatch

                // Provided type for matches
                // Again, erase to obj even though the representation will always be a Match
                let matchTy =
                    ProvidedTypeDefinition(
                        "MatchType",
                        baseType = Some baseTy,
                        hideObjectMethods = true)

                // Nest the match type within parameterized Regex type.
                ty.AddMember matchTy

                // Add group properties to match type
                for group in r.GetGroupNames() do
                    // Ignore the group named 0, which represents all input.
                    if group <> "0" then
                        let prop =
                          ProvidedProperty(
                            propertyName = group,
                            propertyType = typeof<Group>,
                            getterCode = fun args -> <@@ ((%%args.[0]:obj) :?> Match).Groups.[group] @@>)
                        prop.AddXmlDoc(sprintf @"Gets the ""%s"" group from this match" group)
                        matchTy.AddMember(prop)

                // Provide strongly typed version of Regex.Match instance method.
                let matchMeth =
                  ProvidedMethod(
                    methodName = "Match",
                    parameters = [ProvidedParameter("input", typeof<string>)],
                    returnType = matchTy,
                    invokeCode = fun args -> <@@ ((%%args.[0]:obj) :?> Regex).Match(%%args.[1]) :> obj @@>)
                matchMeth.AddXmlDoc "Searches the specified input string for the first occurrence of this regular expression"

                ty.AddMember matchMeth

                // Declare a constructor.
                let ctor =
                  ProvidedConstructor(
                    parameters = [],
                    invokeCode = fun args -> <@@ Regex(pattern) :> obj @@>)

                // Add documentation to the constructor.
                ctor.AddXmlDoc "Initializes a regular expression instance"

                ty.AddMember ctor

                ty
            | _ -> failwith "unexpected parameter values"))

    do this.AddNamespace(rootNamespace, [regexTy])

[<TypeProviderAssembly>]
do ()
```

### <a name="key-lessons"></a>주요 단원

이 섹션에서는 정적 매개 변수에서 작동 하는 형식 공급자를 만드는 방법에 대해 설명 했습니다. 공급자는 정적 매개 변수를 확인 하 고 해당 값을 기반으로 작업을 제공 합니다.

## <a name="a-type-provider-that-is-backed-by-local-data"></a>로컬 데이터로 지원 되는 형식 공급자입니다.

정적 매개 변수 뿐만 아니라 로컬 또는 원격 시스템의 정보를 기반으로 Api를 제공 하기 위해 형식 공급자를 사용 하는 경우가 많습니다. 이 섹션에서는 로컬 데이터 파일과 같은 로컬 데이터를 기반으로 하는 형식 공급자에 대해 설명 합니다.

### <a name="simple-csv-file-provider"></a>간단한 CSV 파일 공급자

간단한 예로 쉼표로 구분 된 값 (CSV) 형식으로 과학적 데이터에 액세스 하는 형식 공급자를 생각해 보세요. 이 섹션에서는 다음 표와 같이 CSV 파일에 헤더 행과 부동 소수점 데이터가 포함 되어 있다고 가정 합니다.

|거리 (미터)|시간 (초)|
|----------------|-------------|
|50.0|3.7|
|100.0|5.2|
|150.0|6.4|

이 섹션에서는 `Distance` 형식의 속성 `float<meter>` 및 `Time` 형식의 `float<second>`속성을 사용 하 여 행을 가져오는 데 사용할 수 있는 형식을 제공 하는 방법을 보여 줍니다. 편의상 다음과 같은 가정이 적용 됩니다.

- 헤더 이름은 단위 이거나 "이름 (단위)" 형식이 며 쉼표를 포함 하지 않습니다.

- 단위는 [fsharp.core module (F#)](https://msdn.microsoft.com/library/3cb43485-11f5-4aa7-a779-558f19d4013b) 모듈이 정의 하는 모든 SI (System 다국어) 단위입니다.

- 단위는 복합이 아닌 모든 단순 (예: 미터) (예: 미터/초)입니다.

- 모든 열은 부동 소수점 데이터를 포함 합니다.

더 완전 한 공급자는 이러한 제한을 완화 합니다.

첫 번째 단계는 API가 어떻게 보이는지를 고려 하는 것입니다. 이전 테이블의 콘텐츠(쉼표로 분리된 형식)를 사용하여 `info.csv` 파일을 지정한 경우 공급자의 사용자는 다음 예제와 비슷한 코드를 작성할 수 있어야 합니다.

```fsharp
let info = new MiniCsv<"info.csv">()
for row in info.Data do
let time = row.Time
printfn "%f" (float time)
```

이 경우 컴파일러는 이러한 호출을 다음 예제와 같은 항목으로 변환 해야 합니다.

```fsharp
let info = new CsvFile("info.csv")
for row in info.Data do
let (time:float) = row.[1]
printfn "%f" (float time)
```

최적의 변환에서는 형식 공급자가 형식 공급자의 어셈블리에서 실제 `CsvFile` 형식을 정의 해야 합니다. 형식 공급자는 종종 몇 가지 도우미 형식 및 메서드를 사용 하 여 중요 한 논리를 래핑합니다. 측정값은 런타임에 지워집니다 .를 `float[]` 행의 지워진 형식으로 사용할 수 있습니다. 컴파일러는 서로 다른 측정값 형식이 있는 것으로 다른 열을 처리 합니다. 예를 들어이 예제의 첫 번째 열에는 형식이 `float<meter>`있고, 두 번째 열 `float<second>`에는가 있습니다. 그러나 지워진 표현은 매우 간단 하 게 유지할 수 있습니다.

다음 코드는 구현의 핵심을 보여 줍니다.

```fsharp
// Simple type wrapping CSV data
type CsvFile(filename) =
    // Cache the sequence of all data lines (all lines but the first)
    let data =
        seq { for line in File.ReadAllLines(filename) |> Seq.skip 1 do
                 yield line.Split(',') |> Array.map float }
        |> Seq.cache
    member __.Data = data

[<TypeProvider>]
type public MiniCsvProvider(cfg:TypeProviderConfig) as this =
    inherit TypeProviderForNamespaces(cfg)

    // Get the assembly and namespace used to house the provided types.
    let asm = System.Reflection.Assembly.GetExecutingAssembly()
    let ns = "Samples.FSharp.MiniCsvProvider"

    // Create the main provided type.
    let csvTy = ProvidedTypeDefinition(asm, ns, "MiniCsv", Some(typeof<obj>))

    // Parameterize the type by the file to use as a template.
    let filename = ProvidedStaticParameter("filename", typeof<string>)
    do csvTy.DefineStaticParameters([filename], fun tyName [| :? string as filename |] ->

        // Resolve the filename relative to the resolution folder.
        let resolvedFilename = Path.Combine(cfg.ResolutionFolder, filename)

        // Get the first line from the file.
        let headerLine = File.ReadLines(resolvedFilename) |> Seq.head

        // Define a provided type for each row, erasing to a float[].
        let rowTy = ProvidedTypeDefinition("Row", Some(typeof<float[]>))

        // Extract header names from the file, splitting on commas.
        // use Regex matching to get the position in the row at which the field occurs
        let headers = Regex.Matches(headerLine, "[^,]+")

        // Add one property per CSV field.
        for i in 0 .. headers.Count - 1 do
            let headerText = headers.[i].Value

            // Try to decompose this header into a name and unit.
            let fieldName, fieldTy =
                let m = Regex.Match(headerText, @"(?<field>.+) \((?<unit>.+)\)")
                if m.Success then

                    let unitName = m.Groups.["unit"].Value
                    let units = ProvidedMeasureBuilder.Default.SI unitName
                    m.Groups.["field"].Value, ProvidedMeasureBuilder.Default.AnnotateType(typeof<float>,[units])

                else
                    // no units, just treat it as a normal float
                    headerText, typeof<float>

            let prop =
                ProvidedProperty(fieldName, fieldTy,
                    getterCode = fun [row] -> <@@ (%%row:float[]).[i] @@>)

            // Add metadata that defines the property's location in the referenced file.
            prop.AddDefinitionLocation(1, headers.[i].Index + 1, filename)
            rowTy.AddMember(prop)

        // Define the provided type, erasing to CsvFile.
        let ty = ProvidedTypeDefinition(asm, ns, tyName, Some(typeof<CsvFile>))

        // Add a parameterless constructor that loads the file that was used to define the schema.
        let ctor0 =
            ProvidedConstructor([],
                invokeCode = fun [] -> <@@ CsvFile(resolvedFilename) @@>)
        ty.AddMember ctor0

        // Add a constructor that takes the file name to load.
        let ctor1 = ProvidedConstructor([ProvidedParameter("filename", typeof<string>)],
            invokeCode = fun [filename] -> <@@ CsvFile(%%filename) @@>)
        ty.AddMember ctor1

        // Add a more strongly typed Data property, which uses the existing property at runtime.
        let prop =
            ProvidedProperty("Data", typedefof<seq<_>>.MakeGenericType(rowTy),
                getterCode = fun [csvFile] -> <@@ (%%csvFile:CsvFile).Data @@>)
        ty.AddMember prop

        // Add the row type as a nested type.
        ty.AddMember rowTy
        ty)

    // Add the type to the namespace.
    do this.AddNamespace(ns, [csvTy])
```

구현에 대 한 다음 사항에 유의 하세요.

- 오버 로드 된 생성자는 원본 파일 또는 동일한 스키마를 가진 파일을 읽을 수 있습니다. 이 패턴은 로컬 또는 원격 데이터 원본에 대 한 형식 공급자를 작성할 때 일반적으로 사용 되며,이 패턴을 사용 하면 로컬 파일을 원격 데이터의 템플릿으로 사용할 수 있습니다.

- 형식 공급자 생성자에 전달 된 [Typeproviderconfig](https://msdn.microsoft.com/library/1cda7b9a-3d07-475d-9315-d65e1c97eb44) 값을 사용 하 여 상대 파일 이름을 확인할 수 있습니다.

- `AddDefinitionLocation` 메서드를 사용 하 여 제공 된 속성의 위치를 정의할 수 있습니다. 따라서 제공 된 속성에서 `Go To Definition` 를 사용 하는 경우 CSV 파일은 Visual Studio에서 열립니다.

- `ProvidedMeasureBuilder` 형식을 사용 하 여 SI 단위를 조회 하 고 관련 `float<_>` 형식을 생성할 수 있습니다.

### <a name="key-lessons"></a>주요 단원

이 섹션에서는 데이터 원본 자체에 포함 된 간단한 스키마를 사용 하 여 로컬 데이터 원본에 대 한 형식 공급자를 만드는 방법에 대해 설명 했습니다.

## <a name="going-further"></a>자세히 살펴보기

다음 섹션에는 추가 연구에 대 한 제안이 포함 되어 있습니다.

### <a name="a-look-at-the-compiled-code-for-erased-types"></a>컴파일된 형식에 대 한 컴파일된 코드 살펴보기

형식 공급자를 사용 하는 방법에 대 한 자세한 내용은이 항목의 앞부분에서 사용 된를 사용 `HelloWorldTypeProvider` 하 여 다음 함수를 참조 하세요.

```fsharp
let function1 () =
    let obj1 = Samples.HelloWorldTypeProvider.Type1("some data")
    obj1.InstanceProperty
```

Ildasm.exe를 사용 하 여 결과 코드 디컴파일된 이미지는 다음과 같습니다.

```il
.class public abstract auto ansi sealed Module1
extends [mscorlib]System.Object
{
.custom instance void [FSharp.Core]Microsoft.FSharp.Core.CompilationMappingAtt
ribute::.ctor(valuetype [FSharp.Core]Microsoft.FSharp.Core.SourceConstructFlags)
= ( 01 00 07 00 00 00 00 00 )
.method public static int32  function1() cil managed
{
// Code size       24 (0x18)
.maxstack  3
.locals init ([0] object obj1)
IL_0000:  nop
IL_0001:  ldstr      "some data"
IL_0006:  unbox.any  [mscorlib]System.Object
IL_000b:  stloc.0
IL_000c:  ldloc.0
IL_000d:  call       !!0 [FSharp.Core_2]Microsoft.FSharp.Core.LanguagePrimit
ives/IntrinsicFunctions::UnboxGeneric<string>(object)
IL_0012:  callvirt   instance int32 [mscorlib_3]System.String::get_Length()
IL_0017:  ret
} // end of method Module1::function1

} // end of class Module1
```

예제에 나와 있는 것 처럼 형식 `Type1` `InstanceProperty` 및 속성의 모든 멘 션이 삭제 되어 관련 된 런타임 형식에 대 한 작업만 남게 됩니다.

### <a name="design-and-naming-conventions-for-type-providers"></a>형식 공급자의 디자인 및 명명 규칙

형식 공급자를 제작할 때 다음 규칙을 준수 합니다.

**연결 프로토콜에 대 한 공급자** 일반적으로 데이터 및 서비스 연결 프로토콜에 대 한 대부분의 공급자 dll 이름 (예: OData 또는 SQL 연결)은 `TypeProvider` 또는 `TypeProviders`로 끝나야 합니다. 예를 들어 다음 문자열과 유사한 DLL 이름을 사용 합니다.

`Fabrikam.Management.BasicTypeProviders.dll`

제공 된 형식이 해당 네임 스페이스의 멤버 인지 확인 하 고 구현 된 연결 프로토콜을 표시 합니다.

```fsharp
  Fabrikam.Management.BasicTypeProviders.WmiConnection<…>
  Fabrikam.Management.BasicTypeProviders.DataProtocolConnection<…>
```

**일반적인 코딩을 위한 유틸리티 공급자**입니다.  정규식의 경우와 같은 유틸리티 유형 공급자의 경우 다음 예제와 같이 형식 공급자가 기본 라이브러리의 일부일 수 있습니다.

```fsharp
#r "Fabrikam.Core.Text.Utilities.dll"
```

이 경우 제공 된 형식이 일반적인 .NET 디자인 규칙에 따라 적절 한 지점에 표시 됩니다.

```fsharp
  open Fabrikam.Core.Text.RegexTyped

  let regex = new RegexTyped<"a+b+a+b+">()
```

**Singleton 데이터 원본**입니다. 일부 형식 공급자는 단일 전용 데이터 원본에 연결 하 고 데이터만 제공 합니다. 이 경우 `TypeProvider` 접미사를 삭제 하 고 .net 명명에 대 한 일반 규칙을 사용 해야 합니다.

```fsharp
#r "Fabrikam.Data.Freebase.dll"

let data = Fabrikam.Data.Freebase.Astronomy.Asteroids
```

자세한 내용은이 항목의 뒷부분 `GetConnection` 에서 설명 하는 디자인 규칙을 참조 하세요.

### <a name="design-patterns-for-type-providers"></a>형식 공급자의 디자인 패턴

다음 섹션에서는 형식 공급자를 제작할 때 사용할 수 있는 디자인 패턴에 대해 설명 합니다.

#### <a name="the-getconnection-design-pattern"></a>GetConnection 디자인 패턴

다음 예제와 같이 fsharp.core의 형식 공급자가 `GetConnection` 사용 하는 패턴을 사용 하도록 대부분의 형식 공급자를 작성 해야 합니다.

```fsharp
#r "Fabrikam.Data.WebDataStore.dll"

type Service = Fabrikam.Data.WebDataStore<…static connection parameters…>

let connection = Service.GetConnection(…dynamic connection parameters…)

let data = connection.Astronomy.Asteroids
```

#### <a name="type-providers-backed-by-remote-data-and-services"></a>원격 데이터 및 서비스에서 지원 되는 형식 공급자

원격 데이터와 서비스에서 지원 되는 형식 공급자를 만들기 전에 연결 된 프로그래밍에 내재 된 다양 한 문제를 고려해 야 합니다. 이러한 문제에는 다음 사항이 포함 됩니다.

- 스키마 매핑

- 스키마가 변경 된 상태에서 선거의 및 무효화

- 스키마 캐싱

- 데이터 액세스 작업의 비동기 구현

- LINQ 쿼리를 비롯 한 지원 쿼리

- 자격 증명 및 인증

이 항목에서는 이러한 문제를 더 자세히 설명 하지 않습니다.

### <a name="additional-authoring-techniques"></a>추가 제작 기술

사용자 고유의 형식 공급자를 작성 하는 경우 다음과 같은 추가 기술을 사용할 수 있습니다.

### <a name="creating-types-and-members-on-demand"></a>요청 시 형식 및 멤버 만들기

프로 비전 된 유형 API는 지연 된 버전의 AddMember를 포함 합니다.

```fsharp
  type ProvidedType =
      member AddMemberDelayed  : (unit -> MemberInfo)      -> unit
      member AddMembersDelayed : (unit -> MemberInfo list) -> unit
```

이러한 버전은 형식의 주문형 공간을 만드는 데 사용 됩니다.

### <a name="providing-array-types-and-generic-type-instantiations"></a>배열 형식 및 제네릭 형식 인스턴스화 제공

`MakeArrayType`을 포함 `MakeGenericType` 하여`MakePointerType` 의<xref:System.Type>모든 인스턴스에서 일반, 및를 사용 하 여 제공 된 멤버 (시그니처에 배열 형식, byref 형식 및 제네릭 형식의 인스턴스화 포함)를 만듭니다. `ProvidedTypeDefinitions`

> [!NOTE]
> 에서 `ProvidedTypeBuilder.MakeGenericType`도우미를 사용 해야 하는 경우도 있습니다.  자세한 내용은 [형식 공급자 SDK 설명서](https://github.com/fsprojects/FSharp.TypeProviders.SDK/blob/master/README.md#explicit-construction-of-code-makegenerictype-makegenericmethod-and-uncheckedquotations) 를 참조 하세요.

### <a name="providing-unit-of-measure-annotations"></a>측정 단위 주석 제공

프로 비전 된 형식 API는 측정값 주석을 제공 하는 도우미를 제공 합니다. 예를 들어 형식을 `float<kg>`제공 하려면 다음 코드를 사용 합니다.

```fsharp
  let measures = ProvidedMeasureBuilder.Default
  let kg = measures.SI "kilogram"
  let m = measures.SI "meter"
  let float_kg = measures.AnnotateType(typeof<float>,[kg])
```

  형식을 `Nullable<decimal<kg/m^2>>`제공 하려면 다음 코드를 사용 합니다.

```fsharp
  let kgpm2 = measures.Ratio(kg, measures.Square m)
  let dkgpm2 = measures.AnnotateType(typeof<decimal>,[kgpm2])
  let nullableDecimal_kgpm2 = typedefof<System.Nullable<_>>.MakeGenericType [|dkgpm2 |]
```

### <a name="accessing-project-local-or-script-local-resources"></a>프로젝트 로컬 또는 스크립트 로컬 리소스 액세스

형식 공급자의 각 인스턴스에는 생성 중에 값 `TypeProviderConfig` 을 지정할 수 있습니다. 이 값에는 공급자에 대 한 "해결 폴더" (즉, 컴파일에 대 한 프로젝트 폴더 또는 스크립트가 포함 된 디렉터리), 참조 된 어셈블리 목록 및 기타 정보가 포함 됩니다.

### <a name="invalidation"></a>무효화

공급자는 스키마 가정이 변경 되었을 수 있음을 F# 언어 서비스에 알리기 위해 무효화 신호를 발생 시킬 수 있습니다. 무효화가 발생 하면 Visual Studio에서 공급자가 호스트 되는 경우 typecheck가 다시 실행 됩니다. 공급자가 대화형 또는 F# F# 컴파일러 (fsc.exe)에서 호스트 되는 경우이 신호는 무시 됩니다.

### <a name="caching-schema-information"></a>스키마 정보 캐싱

공급자는 종종 스키마 정보에 대 한 액세스를 캐시 해야 합니다. 정적 매개 변수 또는 사용자 데이터로 지정 된 파일 이름을 사용 하 여 캐시 된 데이터를 저장 해야 합니다. 스키마 캐싱의 예는 `LocalSchemaFile` `FSharp.Data.TypeProviders` 어셈블리의 형식 공급자에 있는 매개 변수입니다. 이러한 공급자의 구현에서이 정적 매개 변수는 네트워크를 통해 데이터 원본에 액세스 하는 대신 지정 된 로컬 파일의 스키마 정보를 사용 하도록 형식 공급자에 게 지시 합니다. 캐시 된 스키마 정보를 사용 하려면 정적 매개 변수도 `ForceUpdate` 로 `false`설정 해야 합니다. 유사한 기술을 사용 하 여 온라인 및 오프 라인 데이터 액세스를 사용할 수 있습니다.

### <a name="backing-assembly"></a>어셈블리 지원

`.dll` 또는`.exe` 파일을 컴파일할 때 생성 된 형식에 대 한 지원 .dll 파일은 결과 어셈블리에 정적으로 링크 됩니다. 이 링크는 IL (중간 언어) 형식 정의와 지원 어셈블리에서 관리 되는 모든 리소스를 최종 어셈블리에 복사 하 여 만듭니다. Interactive를 사용 F# 하는 경우 지원 .dll 파일은 복사 되지 않고 대신 F# 대화형 프로세스로 직접 로드 됩니다.

### <a name="exceptions-and-diagnostics-from-type-providers"></a>형식 공급자의 예외 및 진단

제공 된 형식의 모든 멤버를 사용 하면 예외가 throw 될 수 있습니다. 모든 경우에서 형식 공급자가 예외를 throw 하는 경우 호스트 컴파일러는 오류를 특정 형식 공급자에 게 특성 합니다.

- 형식 공급자 예외는 내부 컴파일러 오류가 발생 해서는 안 됩니다.

- 형식 공급자는 경고를 보고할 수 없습니다.

- 형식 공급자가 F# 컴파일러, F# 개발 환경 또는 F# 대화형에서 호스트 되는 경우 해당 공급자의 모든 예외가 catch 됩니다. 메시지 속성은 항상 오류 텍스트 이며 스택 추적이 표시 되지 않습니다. 예외를 throw 할 경우 `System.NotSupportedException`, `System.IO.IOException`, `System.Exception`와 같은 예를 throw 할 수 있습니다.

#### <a name="providing-generated-types"></a>생성 된 형식 제공

지금까지이 문서에서는 지워진 형식을 제공 하는 방법에 대해 설명 했습니다. 에서 F# 형식 공급자 메커니즘을 사용 하 여 생성 된 형식을 제공할 수도 있습니다 .이 형식은 사용자의 프로그램에 실제 .net 형식 정의로 추가 됩니다. 형식 정의를 사용 하 여 생성 된 제공 형식을 참조 해야 합니다.

```fsharp
open Microsoft.FSharp.TypeProviders

type Service = ODataService<"http://services.odata.org/Northwind/Northwind.svc/">
```

F# 3.0 릴리스에 포함 된 프로 비전 된 형식-0.2 도우미 코드는 생성 된 형식을 제공 하는 기능만 제한적으로 지원 됩니다. 다음 문은 생성 된 형식 정의에 대해 true 여야 합니다.

- `isErased`로 `false`설정 해야 합니다.

- 생성 된 형식은 생성 된 코드 조각에 대 한 `ProvidedAssembly()`컨테이너를 나타내는 새로 생성 된에 추가 되어야 합니다.

- 공급자에는 디스크에 일치 하는 .dll 파일과 함께 실제 지원 .NET .dll 파일이 있는 어셈블리가 있어야 합니다.

## <a name="rules-and-limitations"></a>규칙 및 제한 사항

형식 공급자를 작성 하는 경우에는 다음 규칙 및 제한 사항을 염두에 두어야 합니다.

### <a name="provided-types-must-be-reachable"></a>제공 된 형식에 연결할 수 있어야 합니다.

제공 된 모든 형식은 중첩 되지 않은 형식에서 연결할 수 있어야 합니다. 중첩 되지 않은 형식은 `TypeProviderForNamespaces` 생성자에 대 한 호출 또는에 대 `AddNamespace`한 호출에서 제공 됩니다. 예를 들어 공급자가 형식을 `StaticClass.P : T`제공 하는 경우 T가 중첩 되지 않은 형식 이거나 중첩 된 형식 인지 확인 해야 합니다.

예를 들어, 일부 공급자는 이러한 `DataTypes` `T1, T2, T3, ...` 형식을 포함 하는와 같은 정적 클래스를 포함 합니다. 그렇지 않으면 어셈블리 A의 T 형식에 대 한 참조를 찾았지만 해당 어셈블리에서 형식을 찾을 수 없다는 오류가 표시 됩니다. 이 오류가 표시 되 면 공급자 형식에서 모든 하위 형식에 연결할 수 있는지 확인 합니다. 참고: 이러한 `T1, T2, T3...` 형식을 *즉석* 형식 이라고 합니다. 이러한 항목은 액세스 가능한 네임 스페이스 또는 부모 형식에 저장 해야 합니다.

### <a name="limitations-of-the-type-provider-mechanism"></a>유형 공급자 메커니즘의 제한 사항

의 F# 형식 공급자 메커니즘에는 다음과 같은 제한 사항이 있습니다.

- 에서 F# 형식 공급자의 기본 인프라는 제공 된 제네릭 형식 또는 제공 된 제네릭 메서드를 지원 하지 않습니다.

- 메커니즘은 정적 매개 변수를 포함 하는 중첩 형식을 지원 하지 않습니다.

## <a name="development-tips"></a>개발 팁

개발 프로세스 중에 다음 팁을 유용 하 게 사용할 수 있습니다.

### <a name="run-two-instances-of-visual-studio"></a>Visual Studio의 두 인스턴스를 실행 합니다.

테스트 IDE는 형식 공급자가 다시 작성 되지 않도록 방지 하는 .dll 파일에 대 한 잠금을 사용 하기 때문에 한 인스턴스에서 형식 공급자를 개발 하 고 다른 공급자에서 공급자를 테스트할 수 있습니다. 따라서 공급자가 첫 번째 인스턴스에서 빌드되는 동안 Visual Studio의 두 번째 인스턴스를 닫은 다음 공급자가 작성 된 후에 두 번째 인스턴스를 다시 열어야 합니다.

### <a name="debug-type-providers-by-using-invocations-of-fscexe"></a>Fsc.exe 호출을 사용 하 여 형식 공급자를 디버그 합니다.

다음 도구를 사용 하 여 형식 공급자를 호출할 수 있습니다.

- fsc.exe ( F# 명령줄 컴파일러)

- fsi.exe ( F# 대화형 컴파일러)

- devenv.exe (Visual Studio)

테스트 스크립트 파일 (예: .fsx)에서 fsc.exe를 사용 하면 형식 공급자를 가장 쉽게 디버그할 수 있습니다. 명령 프롬프트에서 디버거를 시작할 수 있습니다.

```console
devenv /debugexe fsc.exe script.fsx
```

  인쇄 stdout 로깅을 사용할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [형식 공급자](index.md)
- [형식 공급자 SDK](https://github.com/fsprojects/FSharp.TypeProviders.SDK)
