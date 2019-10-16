---
title: 컬렉션 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 5f7749f3-aaf2-4319-b63c-bfa72e1e2b7a
ms.openlocfilehash: 7a4b891aa490d727a7f09bc19c11b8e505ef81f0
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64755001"
---
# <a name="collections-visual-basic"></a>컬렉션 (Visual Basic)

대부분의 애플리케이션의 경우 관련 개체의 그룹을 만들고 관리하려고 합니다. 개체를 그룹화하는 방법에는 개체 배열을 만들거나 개체 컬렉션을 만드는 두 가지가 있습니다.

배열은 고정된 개수의 강력한 형식 개체를 만들고 작업하는 데 가장 유용합니다. 배열에 대한 자세한 내용은 [배열](../../../visual-basic/programming-guide/language-features/arrays/index.md)을 참조하세요.

컬렉션은 개체 그룹에 대해 작업하는 보다 유연한 방법을 제공합니다. 배열과 달리, 애플리케이션의 요구가 변경됨에 따라 작업하는 개체 그룹이 동적으로 확장되거나 축소될 수 있습니다. 일부 컬렉션의 경우 키를 사용하여 개체를 신속하게 검색할 수 있도록 컬렉션에 추가하는 모든 개체에 키를 할당할 수 있습니다.

컬렉션은 클래스이므로 해당 컬렉션에 요소를 추가하려면 먼저 클래스 인스턴스를 선언해야 합니다.

컬렉션에 단일 데이터 형식의 요소만 포함된 경우 <xref:System.Collections.Generic?displayProperty=nameWithType> 네임스페이스의 클래스 중 하나를 사용할 수 있습니다. 제네릭 컬렉션은 다른 데이터 형식을 추가할 수 없도록 형식 안전성을 적용합니다. 제네릭 컬렉션에서 요소를 검색하는 경우 해당 데이터 형식을 결정하거나 변환할 필요가 없습니다.

> [!NOTE]
> 이 항목의 예제를 포함 [가져오기를](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) 에 대 한 문을 합니다 `System.Collections.Generic` 및 `System.Linq` 네임 스페이스입니다.

<a name="BKMK_SimpleCollection"></a>

## <a name="using-a-simple-collection"></a>간단한 컬렉션 사용

이 섹션의 예제에서는 강력한 형식의 개체 목록을 사용할 수 있게 해주는 제네릭 <xref:System.Collections.Generic.List%601> 클래스를 사용합니다.

다음 예제에서는 문자열 목록을 만들고 문자열을 사용 하 여 다음 반복을 [각각에 대 한 중... 다음](../../../visual-basic/language-reference/statements/for-each-next-statement.md) 문입니다.

```vb
' Create a list of strings.
Dim salmons As New List(Of String)
salmons.Add("chinook")
salmons.Add("coho")
salmons.Add("pink")
salmons.Add("sockeye")

' Iterate through the list.
For Each salmon As String In salmons
    Console.Write(salmon & " ")
Next
'Output: chinook coho pink sockeye
```

컬렉션의 내용을 사전에 알고 있는 경우 *컬렉션 이니셜라이저*를 사용하여 컬렉션을 초기화할 수 있습니다. 자세한 내용은 [컬렉션 이니셜라이저](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)를 참조하세요.

다음 예제는 컬렉션 이니셜라이저를 사용하여 컬렉션에 요소를 추가한다는 점을 제외하고 이전 예제와 같습니다.

```vb
' Create a list of strings by using a
' collection initializer.
Dim salmons As New List(Of String) From
    {"chinook", "coho", "pink", "sockeye"}

For Each salmon As String In salmons
    Console.Write(salmon & " ")
Next
'Output: chinook coho pink sockeye
```

사용할 수는 [에 대 한 중... 다음](../../../visual-basic/language-reference/statements/for-next-statement.md) 대신 문을 `For Each` 컬렉션을 반복 하는 문입니다. 인덱스 위치에 따라 컬렉션 요소에 액세스하여 이 작업을 수행합니다. 요소의 인덱스는 0부터 시작하고 요소 개수-1에서 끝납니다.

다음 예제에서는 `For Each` 대신 `For…Next`를 사용하여 컬렉션의 요소를 반복합니다.

```vb
Dim salmons As New List(Of String) From
    {"chinook", "coho", "pink", "sockeye"}

For index = 0 To salmons.Count - 1
    Console.Write(salmons(index) & " ")
Next
'Output: chinook coho pink sockeye
```

다음 예제에서는 제거할 개체를 지정하여 컬렉션에서 요소를 제거합니다.

```vb
' Create a list of strings by using a
' collection initializer.
Dim salmons As New List(Of String) From
    {"chinook", "coho", "pink", "sockeye"}

' Remove an element in the list by specifying
' the object.
salmons.Remove("coho")

For Each salmon As String In salmons
    Console.Write(salmon & " ")
Next
'Output: chinook pink sockeye
```

다음 예제에서는 제네릭 목록에서 요소를 제거합니다. 대신를 `For Each` 문에서 [에 대 한 중... 다음](../../../visual-basic/language-reference/statements/for-next-statement.md) 내림차순으로 반복 하는 문을 사용 합니다. 이는 <xref:System.Collections.Generic.List%601.RemoveAt%2A> 메서드로 인해 제거된 요소 뒤의 요소가 더 낮은 인덱스 값을 갖기 때문입니다.

```vb
Dim numbers As New List(Of Integer) From
    {0, 1, 2, 3, 4, 5, 6, 7, 8, 9}

' Remove odd numbers.
For index As Integer = numbers.Count - 1 To 0 Step -1
    If numbers(index) Mod 2 = 1 Then
        ' Remove the element by specifying
        ' the zero-based index in the list.
        numbers.RemoveAt(index)
    End If
Next

' Iterate through the list.
' A lambda expression is placed in the ForEach method
' of the List(T) object.
numbers.ForEach(
    Sub(number) Console.Write(number & " "))
' Output: 0 2 4 6 8
```

<xref:System.Collections.Generic.List%601>의 요소 형식에 대해 고유한 클래스를 정의할 수도 있습니다. 다음 예제에서, <xref:System.Collections.Generic.List%601>에서 사용되는 `Galaxy` 클래스는 코드에서 정의됩니다.

```vb
Private Sub IterateThroughList()
    Dim theGalaxies As New List(Of Galaxy) From
        {
            New Galaxy With {.Name = "Tadpole", .MegaLightYears = 400},
            New Galaxy With {.Name = "Pinwheel", .MegaLightYears = 25},
            New Galaxy With {.Name = "Milky Way", .MegaLightYears = 0},
            New Galaxy With {.Name = "Andromeda", .MegaLightYears = 3}
        }

    For Each theGalaxy In theGalaxies
        With theGalaxy
            Console.WriteLine(.Name & "  " & .MegaLightYears)
        End With
    Next

    ' Output:
    '  Tadpole  400
    '  Pinwheel  25
    '  Milky Way  0
    '  Andromeda  3
End Sub

Public Class Galaxy
    Public Property Name As String
    Public Property MegaLightYears As Integer
End Class
```

<a name="BKMK_KindsOfCollections"></a>

## <a name="kinds-of-collections"></a>컬렉션 종류

.NET Framework는 많은 일반적인 컬렉션을 제공합니다. 컬렉션의 각 형식은 특정 목적에 맞게 설계되었습니다.

이 섹션에서는 다음 몇 가지 일반적인 컬렉션 클래스에 대해 설명합니다.

- <xref:System.Collections.Generic> 클래스

- <xref:System.Collections.Concurrent> 클래스

- <xref:System.Collections> 클래스

- Visual Basic `Collection` 클래스

<a name="BKMK_Generic"></a>

### <a name="systemcollectionsgeneric-classes"></a>System.Collections.Generic 클래스

<xref:System.Collections.Generic> 네임스페이스의 클래스 중 하나를 사용하여 제네릭 컬렉션을 만들 수 있습니다. 제네릭 컬렉션은 컬렉션의 모든 항목에 동일한 데이터 형식이 있는 경우에 유용합니다. 제네릭 컬렉션은 원하는 데이터 형식만 추가할 수 있도록 하여 강력한 형식 지정을 적용합니다.

다음 표에서는 자주 사용되는 <xref:System.Collections.Generic?displayProperty=nameWithType> 네임스페이스 클래스 중 일부를 보여 줍니다.

|클래스|설명|
|---|---|
|<xref:System.Collections.Generic.Dictionary%602>|키에 따라 구성된 키/값 쌍의 컬렉션을 나타냅니다.|
|<xref:System.Collections.Generic.List%601>|인덱스로 액세스할 수 있는 개체 목록을 나타냅니다. 목록의 검색, 정렬 및 수정에 사용할 수 있는 메서드를 제공합니다.|
|<xref:System.Collections.Generic.Queue%601>|FIFO(선입선출) 방식의 개체 컬렉션을 나타냅니다.|
|<xref:System.Collections.Generic.SortedList%602>|연관된 <xref:System.Collections.Generic.IComparer%601> 구현을 기반으로 키에 따라 정렬된 키/값 쌍의 컬렉션을 나타냅니다.|
|<xref:System.Collections.Generic.Stack%601>|LIFO(후입선출) 방식의 개체 컬렉션을 나타냅니다.|

자세한 내용은 [일반적으로 사용되는 컬렉션 형식](../../../standard/collections/commonly-used-collection-types.md), [Collection 클래스 선택](../../../standard/collections/selecting-a-collection-class.md) 및 <xref:System.Collections.Generic?displayProperty=nameWithType>을 참조하세요.

<a name="BKMK_Concurrent"></a>

### <a name="systemcollectionsconcurrent-classes"></a>System.Collections.Concurrent 클래스

.NET Framework 4 이상에서 <xref:System.Collections.Concurrent> 네임스페이스의 컬렉션은 여러 스레드에서 컬렉션 항목에 액세스하기 위한 효율적이고 스레드로부터 안전한 작업을 제공합니다.

여러 스레드가 동시에 컬렉션에 액세스할 때마다 <xref:System.Collections.Generic?displayProperty=nameWithType> 및 <xref:System.Collections?displayProperty=nameWithType>의 해당 형식 대신 <xref:System.Collections.Concurrent> 네임스페이스의 클래스를 사용해야 합니다. 자세한 내용은 [스레드로부터 안전한 컬렉션](../../../standard/collections/thread-safe/index.md) 및 <xref:System.Collections.Concurrent>를 참조하세요.

<xref:System.Collections.Concurrent> 네임스페이스에 포함된 일부 클래스는 <xref:System.Collections.Concurrent.BlockingCollection%601>, <xref:System.Collections.Concurrent.ConcurrentDictionary%602>, <xref:System.Collections.Concurrent.ConcurrentQueue%601> 및 <xref:System.Collections.Concurrent.ConcurrentStack%601>입니다.

<a name="BKMK_Collections"></a>

### <a name="systemcollections-classes"></a>System.Collections 클래스

<xref:System.Collections?displayProperty=nameWithType> 네임스페이스의 클래스는 구체적 형식의 개체가 아니라 `Object` 형식의 개체로 요소를 저장합니다.

가능하면 항상 `System.Collections` 네임스페이스의 레거시 형식 대신 <xref:System.Collections.Generic?displayProperty=nameWithType> 네임스페이스 또는 <xref:System.Collections.Concurrent> 네임스페이스의 제네릭 컬렉션을 사용해야 합니다.

다음 표에서는 자주 사용되는 `System.Collections` 네임스페이스 클래스 중 일부를 보여 줍니다.

|클래스|설명|
|---|---|
|<xref:System.Collections.ArrayList>|필요에 따라 크기가 동적으로 증가하는 개체 배열을 나타냅니다.|
|<xref:System.Collections.Hashtable>|키의 해시 코드에 따라 구성된 키/값 쌍의 컬렉션을 나타냅니다.|
|<xref:System.Collections.Queue>|FIFO(선입선출) 방식의 개체 컬렉션을 나타냅니다.|
|<xref:System.Collections.Stack>|LIFO(후입선출) 방식의 개체 컬렉션을 나타냅니다.|

<xref:System.Collections.Specialized> 네임스페이스는 문자열 전용 컬렉션 및 연결된 목록과 하이브리드 사전 등의 특수한 강력한 형식의 컬렉션 클래스를 제공합니다.

<a name="BKMK_VisualBasic"></a>

### <a name="visual-basic-collection-class"></a>Visual Basic 컬렉션 클래스

Visual Basic <xref:Microsoft.VisualBasic.Collection> 클래스를 사용하여 숫자 인덱스 또는 `String` 키를 통해 컬렉션 항목에 액세스할 수 있습니다. 키를 지정하거나 지정하지 않고 컬렉션 개체에 항목을 추가할 수 있습니다. 키 없이 항목을 추가하는 경우 숫자 인덱스를 사용해서 액세스해야 합니다.

Visual Basic `Collection` 클래스는 해당 요소를 모두 `Object` 형식으로 저장하므로 모든 데이터 형식의 항목을 추가할 수 있습니다. 부적절한 데이터 형식이 추가되지 않도록 하는 보호 수단은 없습니다.

Visual Basic `Collection` 클래스를 사용하는 경우 컬렉션의 첫 번째 항목에 대한 인덱스는 1입니다. 이는 시작 인덱스가 0인 .NET Framework 컬렉션 클래스와 다릅니다.

가능하면 항상 Visual Basic `Collection` 클래스 대신 <xref:System.Collections.Generic?displayProperty=nameWithType> 네임스페이스 또는 <xref:System.Collections.Concurrent> 네임스페이스의 제네릭 컬렉션을 사용해야 합니다.

자세한 내용은 <xref:Microsoft.VisualBasic.Collection>을 참조하세요.

<a name="BKMK_KeyValuePairs"></a>

## <a name="implementing-a-collection-of-keyvalue-pairs"></a>키/값 쌍의 컬렉션 구현

<xref:System.Collections.Generic.Dictionary%602> 제네릭 컬렉션을 사용하면 각 요소의 키를 통해 컬렉션의 요소에 액세스할 수 있습니다. 사전에 추가하는 각 항목은 값과 관련 키로 이루어져 있습니다. `Dictionary` 클래스는 해시 테이블로 구현되므로 해당 키를 사용하여 값을 검색하는 것이 빠릅니다.

다음 예제에서는 `Dictionary` 컬렉션을 만들고 `For Each` 문을 사용하여 사전을 반복합니다.

```vb
Private Sub IterateThroughDictionary()
    Dim elements As Dictionary(Of String, Element) = BuildDictionary()

    For Each kvp As KeyValuePair(Of String, Element) In elements
        Dim theElement As Element = kvp.Value

        Console.WriteLine("key: " & kvp.Key)
        With theElement
            Console.WriteLine("values: " & .Symbol & " " &
                .Name & " " & .AtomicNumber)
        End With
    Next
End Sub

Private Function BuildDictionary() As Dictionary(Of String, Element)
    Dim elements As New Dictionary(Of String, Element)

    AddToDictionary(elements, "K", "Potassium", 19)
    AddToDictionary(elements, "Ca", "Calcium", 20)
    AddToDictionary(elements, "Sc", "Scandium", 21)
    AddToDictionary(elements, "Ti", "Titanium", 22)

    Return elements
End Function

Private Sub AddToDictionary(ByVal elements As Dictionary(Of String, Element),
ByVal symbol As String, ByVal name As String, ByVal atomicNumber As Integer)
    Dim theElement As New Element

    theElement.Symbol = symbol
    theElement.Name = name
    theElement.AtomicNumber = atomicNumber

    elements.Add(Key:=theElement.Symbol, value:=theElement)
End Sub

Public Class Element
    Public Property Symbol As String
    Public Property Name As String
    Public Property AtomicNumber As Integer
End Class
```

대신 컬렉션 이니셜라이저를 사용하여 `Dictionary` 컬렉션을 빌드하려면 `BuildDictionary` 및 `AddToDictionary` 메서드를 다음 메서드로 바꾸면 됩니다.

```vb
Private Function BuildDictionary2() As Dictionary(Of String, Element)
    Return New Dictionary(Of String, Element) From
        {
            {"K", New Element With
                {.Symbol = "K", .Name = "Potassium", .AtomicNumber = 19}},
            {"Ca", New Element With
                {.Symbol = "Ca", .Name = "Calcium", .AtomicNumber = 20}},
            {"Sc", New Element With
                {.Symbol = "Sc", .Name = "Scandium", .AtomicNumber = 21}},
            {"Ti", New Element With
                {.Symbol = "Ti", .Name = "Titanium", .AtomicNumber = 22}}
        }
End Function
```

다음 예제에서는 `Dictionary`의 <xref:System.Collections.Generic.Dictionary%602.ContainsKey%2A> 메서드 및 <xref:System.Collections.Generic.Dictionary%602.Item%2A> 속성을 사용하여 키를 통해 항목을 신속하게 찾습니다. `Item` 속성의 항목에 액세스할 수 있습니다를 `elements` 사용 하 여 컬렉션을 `elements(symbol)` Visual Basic의 코드입니다.

```vb
Private Sub FindInDictionary(ByVal symbol As String)
    Dim elements As Dictionary(Of String, Element) = BuildDictionary()

    If elements.ContainsKey(symbol) = False Then
        Console.WriteLine(symbol & " not found")
    Else
        Dim theElement = elements(symbol)
        Console.WriteLine("found: " & theElement.Name)
    End If
End Sub
```

다음 예제에서는 대신 <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> 메서드를 사용하여 키를 통해 항목을 신속하게 찾습니다.

```vb
Private Sub FindInDictionary2(ByVal symbol As String)
    Dim elements As Dictionary(Of String, Element) = BuildDictionary()

    Dim theElement As Element = Nothing
    If elements.TryGetValue(symbol, theElement) = False Then
        Console.WriteLine(symbol & " not found")
    Else
        Console.WriteLine("found: " & theElement.Name)
    End If
End Sub
```

<a name="BKMK_LINQ"></a>

## <a name="using-linq-to-access-a-collection"></a>LINQ를 사용하여 컬렉션에 액세스

LINQ(통합 언어 쿼리)를 사용하여 컬렉션에 액세스할 수 있습니다. LINQ 쿼리는 필터링, 정렬 및 그룹화 기능을 제공합니다. 자세한 내용은 [Getting Started with Visual Basic의 LINQ](../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)합니다.

다음 예제에서는 제네릭 `List`에 대해 LINQ 쿼리를 실행합니다. LINQ 쿼리는 결과를 포함하는 다른 컬렉션을 반환합니다.

```vb
Private Sub ShowLINQ()
    Dim elements As List(Of Element) = BuildList()

    ' LINQ Query.
    Dim subset = From theElement In elements
                  Where theElement.AtomicNumber < 22
                  Order By theElement.Name

    For Each theElement In subset
        Console.WriteLine(theElement.Name & " " & theElement.AtomicNumber)
    Next

    ' Output:
    '  Calcium 20
    '  Potassium 19
    '  Scandium 21
End Sub

Private Function BuildList() As List(Of Element)
    Return New List(Of Element) From
        {
            {New Element With
                {.Symbol = "K", .Name = "Potassium", .AtomicNumber = 19}},
            {New Element With
                {.Symbol = "Ca", .Name = "Calcium", .AtomicNumber = 20}},
            {New Element With
                {.Symbol = "Sc", .Name = "Scandium", .AtomicNumber = 21}},
            {New Element With
                {.Symbol = "Ti", .Name = "Titanium", .AtomicNumber = 22}}
        }
End Function

Public Class Element
    Public Property Symbol As String
    Public Property Name As String
    Public Property AtomicNumber As Integer
End Class
```

<a name="BKMK_Sorting"></a>

## <a name="sorting-a-collection"></a>컬렉션 정렬

다음 예제에서는 컬렉션 정렬 절차를 보여 줍니다. 예제에서는 <xref:System.Collections.Generic.List%601>에 저장된 `Car` 클래스 인스턴스를 정렬합니다. `Car` 클래스는 <xref:System.IComparable%601.CompareTo%2A> 메서드가 구현되어야 하는 <xref:System.IComparable%601> 인터페이스를 구현합니다.

<xref:System.IComparable%601.CompareTo%2A> 메서드를 호출할 때마다 정렬에 사용되는 단일 비교가 수행됩니다. `CompareTo` 메서드의 사용자 작성 코드는 다른 개체와 현재 개체의 각 비교에 대한 값을 반환합니다. 현재 개체가 다른 개체보다 작으면 반환되는 값이 0보다 작고, 현재 개체가 다른 개체보다 크면 0보다 크고, 같으면 0입니다. 이렇게 하면 보다 큼, 보다 작음 및 같음에 대한 조건을 코드에서 정의할 수 있습니다.

`ListCars` 메서드에서 `cars.Sort()` 문은 목록을 정렬합니다. <xref:System.Collections.Generic.List%601>의 <xref:System.Collections.Generic.List%601.Sort%2A> 메서드를 호출하면 `List`의 `Car` 개체에 대해 `CompareTo` 메서드가 자동으로 호출됩니다.

```vb
Public Sub ListCars()

    ' Create some new cars.
    Dim cars As New List(Of Car) From
    {
        New Car With {.Name = "car1", .Color = "blue", .Speed = 20},
        New Car With {.Name = "car2", .Color = "red", .Speed = 50},
        New Car With {.Name = "car3", .Color = "green", .Speed = 10},
        New Car With {.Name = "car4", .Color = "blue", .Speed = 50},
        New Car With {.Name = "car5", .Color = "blue", .Speed = 30},
        New Car With {.Name = "car6", .Color = "red", .Speed = 60},
        New Car With {.Name = "car7", .Color = "green", .Speed = 50}
    }

    ' Sort the cars by color alphabetically, and then by speed
    ' in descending order.
    cars.Sort()

    ' View all of the cars.
    For Each thisCar As Car In cars
        Console.Write(thisCar.Color.PadRight(5) & " ")
        Console.Write(thisCar.Speed.ToString & " ")
        Console.Write(thisCar.Name)
        Console.WriteLine()
    Next

    ' Output:
    '  blue  50 car4
    '  blue  30 car5
    '  blue  20 car1
    '  green 50 car7
    '  green 10 car3
    '  red   60 car6
    '  red   50 car2
End Sub

Public Class Car
    Implements IComparable(Of Car)

    Public Property Name As String
    Public Property Speed As Integer
    Public Property Color As String

    Public Function CompareTo(ByVal other As Car) As Integer _
        Implements System.IComparable(Of Car).CompareTo
        ' A call to this method makes a single comparison that is
        ' used for sorting.

        ' Determine the relative order of the objects being compared.
        ' Sort by color alphabetically, and then by speed in
        ' descending order.

        ' Compare the colors.
        Dim compare As Integer
        compare = String.Compare(Me.Color, other.Color, True)

        ' If the colors are the same, compare the speeds.
        If compare = 0 Then
            compare = Me.Speed.CompareTo(other.Speed)

            ' Use descending order for speed.
            compare = -compare
        End If

        Return compare
    End Function
End Class
```

<a name="BKMK_CustomCollection"></a>

## <a name="defining-a-custom-collection"></a>사용자 지정 컬렉션 정의

<xref:System.Collections.Generic.IEnumerable%601> 또는 <xref:System.Collections.IEnumerable> 인터페이스를 구현하여 컬렉션을 정의할 수 있습니다. 자세한 내용은 참조 하세요. [컬렉션을 열거](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/hwyysy67(v=vs.100))합니다.

사용자 지정 컬렉션을 정의할 수도 있지만, 일반적으로 이 항목의 앞부분에 있는 [컬렉션 종류](#kinds-of-collections)에서 설명한 .NET Framework에 포함된 컬렉션을 대신 사용하는 것이 좋습니다.

다음 예제에서는 `AllColors`라는 사용자 지정 컬렉션 클래스를 정의합니다. 이 클래스는 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 메서드가 구현되어야 하는 <xref:System.Collections.IEnumerable> 인터페이스를 구현합니다.

`GetEnumerator` 메서드는 `ColorEnumerator` 클래스의 인스턴스를 반환합니다. `ColorEnumerator`는 <xref:System.Collections.IEnumerator.Current%2A> 속성, <xref:System.Collections.IEnumerator.MoveNext%2A> 메서드 및 <xref:System.Collections.IEnumerator.Reset%2A> 메서드가 구현되어야 하는 <xref:System.Collections.IEnumerator> 인터페이스를 구현합니다.

```vb
Public Sub ListColors()
    Dim colors As New AllColors()

    For Each theColor As Color In colors
        Console.Write(theColor.Name & " ")
    Next
    Console.WriteLine()
    ' Output: red blue green
End Sub

' Collection class.
Public Class AllColors
    Implements System.Collections.IEnumerable

    Private _colors() As Color =
    {
        New Color With {.Name = "red"},
        New Color With {.Name = "blue"},
        New Color With {.Name = "green"}
    }

    Public Function GetEnumerator() As System.Collections.IEnumerator _
        Implements System.Collections.IEnumerable.GetEnumerator

        Return New ColorEnumerator(_colors)

        ' Instead of creating a custom enumerator, you could
        ' use the GetEnumerator of the array.
        'Return _colors.GetEnumerator
    End Function

    ' Custom enumerator.
    Private Class ColorEnumerator
        Implements System.Collections.IEnumerator

        Private _colors() As Color
        Private _position As Integer = -1

        Public Sub New(ByVal colors() As Color)
            _colors = colors
        End Sub

        Public ReadOnly Property Current() As Object _
            Implements System.Collections.IEnumerator.Current
            Get
                Return _colors(_position)
            End Get
        End Property

        Public Function MoveNext() As Boolean _
            Implements System.Collections.IEnumerator.MoveNext
            _position += 1
            Return (_position < _colors.Length)
        End Function

        Public Sub Reset() Implements System.Collections.IEnumerator.Reset
            _position = -1
        End Sub
    End Class
End Class

' Element class.
Public Class Color
    Public Property Name As String
End Class
```

<a name="BKMK_Iterators"></a>

## <a name="iterators"></a>반복기

*반복기*는 컬렉션에 대해 사용자 지정 반복을 수행하는 데 사용됩니다. 반복기는 메서드 또는 `get` 접근자일 수 있습니다. 반복기를 사용 하는 [Yield](../../../visual-basic/language-reference/statements/yield-statement.md) 문을 한 번에 하나씩 컬렉션의 각 요소를 반환 합니다.

사용 하 여 반복기를 호출 하는 [각각에 대 한 중... 다음](../../../visual-basic/language-reference/statements/for-each-next-statement.md) 문입니다. 각각의 `For Each` 루프의 반복이 반복기를 호출합니다. `Yield` 문이 반복기 메서드에 도달하면 식이 반환되고 코드에서 현재 위치는 유지됩니다. 다음에 반복기가 호출되면 해당 위치에서 실행이 다시 시작됩니다.

자세한 내용은 [반복기 (Visual Basic)](../../../visual-basic/programming-guide/concepts/iterators.md)합니다.

다음 예제에서는 반복기 메서드를 사용합니다. 반복기 메서드가 `Yield` 문 내에 있는 [에 대 한 중... 다음](../../../visual-basic/language-reference/statements/for-next-statement.md) 루프입니다. `ListEvenNumbers` 메서드에서 `For Each` 문 본문을 반복할 때마다 다음 `Yield` 문으로 진행하는 반복기 메서드에 대한 호출이 생성됩니다.

```vb
Public Sub ListEvenNumbers()
    For Each number As Integer In EvenSequence(5, 18)
        Console.Write(number & " ")
    Next
    Console.WriteLine()
    ' Output: 6 8 10 12 14 16 18
End Sub

Private Iterator Function EvenSequence(
ByVal firstNumber As Integer, ByVal lastNumber As Integer) _
As IEnumerable(Of Integer)

' Yield even numbers in the range.
    For number = firstNumber To lastNumber
        If number Mod 2 = 0 Then
            Yield number
        End If
    Next
End Function
```

## <a name="see-also"></a>참고자료

- [컬렉션 이니셜라이저](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)
- [프로그래밍 개념(Visual Basic)](../../../visual-basic/programming-guide/concepts/index.md)
- [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [LINQ to Objects(Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)
- [PLINQ(병렬 LINQ)](../../../standard/parallel-programming/parallel-linq-plinq.md)
- [컬렉션 및 데이터 구조](../../../standard/collections/index.md)
- [Collection 클래스 선택](../../../standard/collections/selecting-a-collection-class.md)
- [컬렉션 내에서 비교 및 정렬](../../../standard/collections/comparisons-and-sorts-within-collections.md)
- [제네릭 컬렉션 사용 기준](../../../standard/collections/when-to-use-generic-collections.md)
