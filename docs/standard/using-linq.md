---
title: LINQ(Language-Integrated Query)
description: LINQ가 표현력 있는 선언형 코드를 작성하는 한 가지 방법으로 API와 언어 수준 쿼리 기능을 C# 및 VB에 제공하는 방법을 알아봅니다.
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
dev_langs:
- csharp
- vb
ms.technology: dotnet-standard
ms.assetid: c00939e1-59e3-4e61-8fe9-08ad6b3f1295
ms.openlocfilehash: 2e4b23b7bf197c9984c53b2f4cc2acaa61731d38
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68238626"
---
# <a name="linq-language-integrated-query"></a>LINQ(Language-Integrated Query)

## <a name="what-is-it"></a>LINQ란?

LINQ는 표현력 있는 선언형 코드를 작성하는 한 가지 방법으로 [고차 함수](https://en.wikipedia.org/wiki/Higher-order_function) API와 언어 수준 쿼리 기능을 C# 및 VB에 제공합니다.

언어 수준 쿼리 구문:

```csharp
var linqExperts = from p in programmers
                  where p.IsNewToLINQ
                  select new LINQExpert(p);
```

```vb
Dim linqExperts = From p in programmers
                  Where p.IsNewToLINQ
                  Select New LINQExpert(p)
```

`IEnumerable<T>` API를 사용한 동일한 예제:

```csharp
var linqExperts = programmers.Where(p => p.IsNewToLINQ)
                             .Select(p => new LINQExpert(p));
```

```vb
Dim linqExperts = programmers.Where(Function(p) p.IsNewToLINQ).
                             Select(Function(p) New LINQExpert(p))
```

## <a name="linq-is-expressive"></a>LINQ의 뛰어난 표현력

애완 동물 목록이 있고, 해당 `RFID` 값으로 애완 동물에 직접 액세스할 수 있는 사전으로 이 목록을 변환하려 한다고 가정해봅시다.

기존의 명령형 코드:

```csharp
var petLookup = new Dictionary<int, Pet>();

foreach (var pet in pets)
{
    petLookup.Add(pet.RFID, pet);
}
```

```vb
Dim petLookup = New Dictionary(Of Integer, Pet)()

For Each pet in pets
    petLookup.Add(pet.RFID, pet)
Next
```

코드의 숨은 의도는 새 `Dictionary<int, Pet>`을 만들고 루프를 통해 사전에 추가하는 것이 아니라 기존 목록을 사전으로 변환하는 것입니다. LINQ는 이 의도를 유지하지만 명령형 코드는 유지하지 않습니다.

해당되는 LINQ 식:

```csharp
var petLookup = pets.ToDictionary(pet => pet.RFID);
```

```vb
Dim petLookup = pets.ToDictionary(Function(pet) pet.RFID)
```

LINQ를 사용하는 코드는 프로그래머로 추론할 때 의도와 코드를 일치시키기 때문에 유용합니다. 그 외에도 코드가 간소화되는 이점이 있습니다. 위와 같이 코드베이스의 상당 부분이 1/3만큼 줄어든다고 상상해 보세요. 멋지지 않나요?

## <a name="linq-providers-simplify-data-access"></a>데이터 액세스를 간소화하는 LINQ 공급자

소프트웨어의 상당 부분은 실생활에서 일부 소스(데이터베이스, JSON, XML 등)의 데이터를 처리하면서 발전합니다. 이 과정에서 각 데이터 소스에 대한 새로운 API를 학습해야 하며, 이는 꽤 번거로울 수 있습니다. LINQ는 데이터 액세스의 공통 요소를 선택한 데이터 소스에 관계없이 동일하게 표시되는 쿼리 구문으로 추상화하여 이 과정을 간소화합니다.

특정 특성 값을 가진 모든 XML 요소를 찾는다고 가정해봅시다.

```csharp
public static IEnumerable<XElement> FindAllElementsWithAttribute(XElement documentRoot, string elementName,
                                           string attributeName, string value)
{
    return from el in documentRoot.Elements(elementName)
           where (string)el.Element(attributeName) == value
           select el;
}
```

```vb
Public Shared Function FindAllElementsWithAttribute(documentRoot As XElement, elementName As String,
                                           attributeName As String, value As String) As IEnumerable(Of XElement)
    Return From el In documentRoot.Elements(elementName)
           Where el.Element(attributeName).ToString() = value
           Select el
End Function

```

이 작업을 수행하기 위해 수동으로 XML 문서를 트래버스하는 코드를 작성하는 것이 훨씬 더 어려울 것입니다.

XML 조작이 LINQ 공급자로 수행할 수 있는 유일한 작업은 아닙니다. [LINQ to SQL](../../docs/framework/data/adonet/sql/linq/index.md)은 MSSQL Server Database에 대한 기본적인 ORM(개체 관계형 매퍼)입니다. [JSON.NET](https://www.newtonsoft.com/json/help/html/LINQtoJSON.htm) 라이브러리는 LINQ를 통한 효율적인 JSON 문서 통과 기능을 제공합니다. 또한 필요한 작업을 수행하는 라이브러리가 없을 경우 [고유한 LINQ 공급자를 작성](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2012/bb546158(v=vs.110))할 수도 있습니다.

## <a name="why-use-the-query-syntax"></a>왜 쿼리 구문을 사용하나요?

자주 제기되는 질문입니다. 결국,

```csharp
var filteredItems = myItems.Where(item => item.Foo);
```

```vb
Dim filteredItems = myItems.Where(Function(item) item.Foo)
```

위 코드가 아래 코드보다 훨씬 더 간결합니다.

```csharp
var filteredItems = from item in myItems
                    where item.Foo
                    select item;
```

```vb
Dim filteredItems = From item In myItems
                    Where item.Foo
                    Select item
```

API 구문이 쿼리 구문보다 더 간결한 방법이 아닌가요?

아니요. 쿼리 구문에서는 **let** 절을 사용할 수 있습니다. 이 절을 통해 식 범위 내에서 변수를 도입 및 바인딩하고 식의 후속 부분에서 사용할 수 있습니다. API 구문만 사용하여 동일한 코드를 재현할 수도 있지만 읽기 어려운 코드가 될 가능성이 큽니다.

따라서 **쿼리 구문을 사용해야 하나요?** 란 질문을 하게 됩니다.

다음과 같은 경우 이 질문에 대한 대답은 **예**입니다.

* 기존 코드베이스에서 이미 쿼리 구문을 사용하는 경우
* 복잡성으로 인해 쿼리 내에서 변수 범위를 지정해야 하는 경우
* 쿼리 구문을 선호하며 코드베이스에 방해가 되지 않는 경우

다음과 같은 경우 이 질문에 대한 대답은 **아니요**입니다.

* 기존 코드베이스에서 이미 API 구문을 사용하는 경우
* 쿼리 내에서 변수 범위를 지정할 필요가 없는 경우
* API 구문을 선호하며 코드베이스에 방해가 되지 않는 경우

## <a name="essential-samples"></a>필수 샘플

LINQ 샘플의 포괄적인 목록은 [101 LINQ 샘플](https://code.msdn.microsoft.com/101-LINQ-Samples-3fb9811b)을 참조하세요.

다음은 일부 LINQ 핵심 부분의 간단한 데모입니다. LINQ는 여기에 설명된 것보다 훨씬 더 많은 기능을 제공하기 때문에 포괄적인 목록은 아닙니다.

* 가장 중요한 요소 - `Where`, `Select` 및 `Aggregate`:

```csharp
// Filtering a list.
var germanShepards = dogs.Where(dog => dog.Breed == DogBreed.GermanShepard);

// Using the query syntax.
var queryGermanShepards = from dog in dogs
                          where dog.Breed == DogBreed.GermanShepard
                          select dog;

// Mapping a list from type A to type B.
var cats = dogs.Select(dog => dog.TurnIntoACat());

// Using the query syntax.
var queryCats = from dog in dogs
                select dog.TurnIntoACat();

// Summing the lengths of a set of strings.
int seed = 0;
int sumOfStrings = strings.Aggregate(seed, (s1, s2) => s1.Length + s2.Length);
```

```vb
' Filtering a list.
Dim germanShepards = dogs.Where(Function(dog) dog.Breed = DogBreed.GermanShepard)

' Using the query syntax.
Dim queryGermanShepards = From dog In dogs
                          Where dog.Breed = DogBreed.GermanShepard
                          Select dog

' Mapping a list from type A to type B.
Dim cats = dogs.Select(Function(dog) dog.TurnIntoACat())

' Using the query syntax.
Dim queryCats = From dog In dogs
                Select dog.TurnIntoACat()

' Summing the lengths of a set of strings.
Dim seed As Integer = 0
Dim sumOfStrings As Integer = strings.Aggregate(seed, Function(s1, s2) s1.Length + s2.Length)
```

* 목록의 목록 평면화:

```csharp
// Transforms the list of kennels into a list of all their dogs.
var allDogsFromKennels = kennels.SelectMany(kennel => kennel.Dogs);
```

```vb
' Transforms the list of kennels into a list of all their dogs.
Dim allDogsFromKennels = kennels.SelectMany(Function(kennel) kennel.Dogs)
```

* 두 집합 간의 합집합(사용자 지정 비교 연산자 사용):

```csharp
public class DogHairLengthComparer : IEqualityComparer<Dog>
{
    public bool Equals(Dog a, Dog b)
    {
        if (a == null && b == null)
        {
            return true;
        }
        else if ((a == null && b != null) ||
                 (a != null && b == null))
        {
            return false;
        }
        else
        {
            return a.HairLengthType == b.HairLengthType;
        }
    }

    public int GetHashCode(Dog d)
    {
        // Default hashcode is enough here, as these are simple objects.
        return d.GetHashCode();
    }
}

...

// Gets all the short-haired dogs between two different kennels.
var allShortHairedDogs = kennel1.Dogs.Union(kennel2.Dogs, new DogHairLengthComparer());
```

```vb
Public Class DogHairLengthComparer 
  Inherits IEqualityComparer(Of Dog)

  Public Function Equals(a As Dog,b As Dog) As Boolean
      If a Is Nothing AndAlso b Is Nothing Then
          Return True
      ElseIf (a Is Nothing AndAlso b IsNot Nothing) OrElse (a IsNot Nothing AndAlso b Is Nothing) Then
          Return False
      Else
          Return a.HairLengthType = b.HairLengthType
      End If
  End Function

  Public Function GetHashCode(d As Dog) As Integer
      ' Default hashcode is enough here, as these are simple objects.
      Return d.GetHashCode()
  End Function
End Class

...

' Gets all the short-haired dogs between two different kennels.
Dim allShortHairedDogs = kennel1.Dogs.Union(kennel2.Dogs, New DogHairLengthComparer())
```

* 두 집합 간의 교집합:

```csharp
// Gets the volunteers who spend share time with two humane societies.
var volunteers = humaneSociety1.Volunteers.Intersect(humaneSociety2.Volunteers,
                                                     new VolunteerTimeComparer());
```

```vb
' Gets the volunteers who spend share time with two humane societies.
Dim volunteers = humaneSociety1.Volunteers.Intersect(humaneSociety2.Volunteers,
                                                     New VolunteerTimeComparer())
```

* 순서:

```csharp
// Get driving directions, ordering by if it's toll-free before estimated driving time.
var results = DirectionsProcessor.GetDirections(start, end)
              .OrderBy(direction => direction.HasNoTolls)
              .ThenBy(direction => direction.EstimatedTime);
```

```vb
' Get driving directions, ordering by if it's toll-free before estimated driving time.
Dim results = DirectionsProcessor.GetDirections(start, end).
                OrderBy(Function(direction) direction.HasNoTolls).
                ThenBy(Function(direction) direction.EstimatedTime)
```

* 마지막으로, 고급 샘플: 동일한 형식을 가진 두 인스턴스의 속성 값이 같은지 확인([이 StackOverflow 게시물](https://stackoverflow.com/a/844855)에서 가져와 수정함):

```csharp
public static bool PublicInstancePropertiesEqual<T>(this T self, T to, params string[] ignore) where T : class
{
    if (self == null || to == null)
    {
        return self == to;
    }
    
    // Selects the properties which have unequal values into a sequence of those properties.
    var unequalProperties = from property in typeof(T).GetProperties(BindingFlags.Public | BindingFlags.Instance)
                            where !ignore.Contains(property.Name)
                            let selfValue = property.GetValue(self, null)
                            let toValue = property.GetValue(to, null)
                            where !Equals(selfValue, toValue)
                            select property;
    return !unequalProperties.Any();
}
```

```vb
<System.Runtime.CompilerServices.Extension()> 
Public Function PublicInstancePropertiesEqual(Of T As Class)(self As T, [to] As T, ParamArray ignore As String()) As Boolean
    If self Is Nothing OrElse [to] Is Nothing Then
        Return self Is [to]
    End If

    ' Selects the properties which have unequal values into a sequence of those properties.
    Dim unequalProperties = From [property] In GetType(T).GetProperties(BindingFlags.Public Or BindingFlags.Instance) 
                            Where Not ignore.Contains([property].Name)
                            Let selfValue = [property].GetValue(self, Nothing)
                            Let toValue = [property].GetValue([to], Nothing)
                            Where Not Equals(selfValue, toValue) Select [property]
    Return Not unequalProperties.Any()
End Function
```

## <a name="plinq"></a>PLINQ

PLINQ 또는 병렬 LINQ는 LINQ 식에 대한 병렬 실행 엔진입니다. 즉, 여러 스레드 간에 LINQ 정규식을 일반적으로 병렬 처리할 수 있습니다. 이 작업은 식 앞의 `AsParallel()` 호출을 통해 수행됩니다.

다음을 살펴보세요.

```csharp
public static string GetAllFacebookUserLikesMessage(IEnumerable<FacebookUser> facebookUsers)
{
    var seed = default(UInt64);

    Func<UInt64, UInt64, UInt64> threadAccumulator = (t1, t2) => t1 + t2;
    Func<UInt64, UInt64, UInt64> threadResultAccumulator = (t1, t2) => t1 + t2;
    Func<Uint64, string> resultSelector = total => $"Facebook has {total} likes!";

    return facebookUsers.AsParallel()
                        .Aggregate(seed, threadAccumulator, threadResultAccumulator, resultSelector);
}
```

```vb
Public Shared GetAllFacebookUserLikesMessage(facebookUsers As IEnumerable(Of FacebookUser)) As String
{
    Dim seed As UInt64 = 0

    Dim threadAccumulator As Func(Of UInt64, UInt64, UInt64) = Function(t1, t2) t1 + t2
    Dim threadResultAccumulator As Func(Of UInt64, UInt64, UInt64) = Function(t1, t2) t1 + t2
    Dim resultSelector As Func(Of Uint64, string) = Function(total) $"Facebook has {total} likes!"

    Return facebookUsers.AsParallel().
                        Aggregate(seed, threadAccumulator, threadResultAccumulator, resultSelector)
}
```

이 코드는 필요에 따라 시스템 스레드 간에 `facebookUsers`를 분할하고, 각 스레드의 총계를 병렬로 합산한 다음, 각 스레드에서 계산된 결과를 합산하고 그 결과를 멋진 문자열로 프로젝션합니다.

다이어그램 형식:

![PLINQ 다이어그램](./media/using-linq/plinq-diagram.png)

LINQ를 통해 쉽게 표현될 수 있는 병렬화 가능한 CPU 바인딩된 작업(즉, 순수 함수이며 부작용 없음)에 PLINQ를 사용하는 것이 좋습니다. 부작용이 _있는_ 작업의 경우 [작업 병렬 라이브러리](./parallel-programming/task-parallel-library-tpl.md)를 사용하는 것이 좋습니다.

## <a name="further-resources"></a>추가 리소스:

* [101 LINQ 샘플](https://code.msdn.microsoft.com/101-LINQ-Samples-3fb9811b)
* [Linqpad](https://www.linqpad.net/), 실습 환경 및 C#/F#/VB에 대한 데이터베이스 쿼리 엔진
* [EduLinq](https://codeblog.jonskeet.uk/2011/02/23/reimplementing-linq-to-objects-part-45-conclusion-and-list-of-posts/), LINQ-to-objects 구현 방법 학습을 위한 eBook
