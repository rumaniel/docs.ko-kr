---
title: 반복기 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: f26b5c1e-fe9d-4004-b287-da7919d717ae
ms.openlocfilehash: db84e5d7956f0b160520fa831607e3f7548fc976
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69913147"
---
# <a name="iterators-visual-basic"></a>반복기 (Visual Basic)
*반복기*는 목록 및 배열과 같은 컬렉션을 단계별로 실행하는 데 사용할 수 있습니다.  
  
 반복기 메서드 또는 `get` 접근자는 컬렉션에 대해 사용자 지정 반복을 수행합니다. 반복기 메서드는 [Yield](../../../visual-basic/language-reference/statements/yield-statement.md) 문을 사용 하 여 각 요소를 한 번에 하나씩 반환 합니다. `Yield` 문에 도달하면 코드의 현재 위치가 기억됩니다. 다음에 반복기 함수가 호출되면 해당 위치에서 실행이 다시 시작됩니다.  
  
 For Each ...를 사용 하 여 클라이언트 코드에서 반복기를 사용 합니다. [ 다음](../../../visual-basic/language-reference/statements/for-each-next-statement.md) 문 또는 LINQ 쿼리 사용.  
  
 다음 예제에서 `For Each` 루프의 첫 번째 반복은 첫 번째 `Yield` 문에 도달할 때까지 `SomeNumbers` 반복기 메서드에서 실행이 계속되도록 합니다. 이 반복은 3 값을 반환하며 반복기 메서드에서 현재 위치는 유지됩니다. 루프의 다음 반복에서는 반복기 메서드의 실행이 중지되었던 위치에서 계속되고 `Yield` 문에 도달하면 다시 중지됩니다. 이 반복은 값 5를 반환하며 반복기 메서드에서 현재 위치는 다시 유지됩니다. 루프는 반복기 메서드의 끝에 도달하면 완료됩니다.  
  
```vb  
Sub Main()  
    For Each number As Integer In SomeNumbers()  
        Console.Write(number & " ")  
    Next  
    ' Output: 3 5 8  
    Console.ReadKey()  
End Sub  
  
Private Iterator Function SomeNumbers() As System.Collections.IEnumerable  
    Yield 3  
    Yield 5  
    Yield 8  
End Function  
```  
  
 반복기 메서드 또는 `get` 접근자의 반환 형식은 <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator> 또는 <xref:System.Collections.Generic.IEnumerator%601>일 수 있습니다.  
  
 `Exit Function` 또는`Return` 문을 사용 하 여 반복을 종료할 수 있습니다.  
  
 Visual Basic 반복기 함수 또는 `get` 접근자 선언에는 [반복기](../../../visual-basic/language-reference/modifiers/iterator.md) 한정자가 포함 되어 있습니다.  
  
 반복기는 Visual Studio 2012의 Visual Basic에서 도입 되었습니다.  
  
 **항목 내용**  
  
- [단순 반복기](#BKMK_SimpleIterator)  
  
- [컬렉션 클래스 만들기](#BKMK_CollectionClass)  
  
- [Try 블록](#BKMK_TryBlocks)  
  
- [무명 메서드](#BKMK_AnonymousMethods)  
  
- [제네릭 목록과 함께 반복기 사용](#BKMK_GenericList)  
  
- [구문 정보](#BKMK_SyntaxInformation)  
  
- [기술 구현](#BKMK_Technical)  
  
- [반복기 사용](#BKMK_UseOfIterators)  
  
> [!NOTE]
> 간단한 반복기 예제를 제외한 항목의 모든 예제에 대해서는 `System.Collections` 및 `System.Collections.Generic` 네임 스페이스에 대 한 [Imports](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) 문을 포함 합니다.  
  
## <a name="BKMK_SimpleIterator"></a> 단순 반복기  
 다음 예제에는 `Yield` [에 대 한 단일 문이 있습니다 ... Next](../../../visual-basic/language-reference/statements/for-next-statement.md) 루프. `Main`에서 `For Each` 문 본문을 반복할 때마다 다음 `Yield` 문으로 진행하는 반복기 함수에 대한 호출이 생성됩니다.  
  
```vb  
Sub Main()  
    For Each number As Integer In EvenSequence(5, 18)  
        Console.Write(number & " ")  
    Next  
    ' Output: 6 8 10 12 14 16 18  
    Console.ReadKey()  
End Sub  
  
Private Iterator Function EvenSequence(  
ByVal firstNumber As Integer, ByVal lastNumber As Integer) _  
As System.Collections.Generic.IEnumerable(Of Integer)  
  
    ' Yield even numbers in the range.  
    For number As Integer = firstNumber To lastNumber  
        If number Mod 2 = 0 Then  
            Yield number  
        End If  
    Next  
End Function  
```  
  
## <a name="BKMK_CollectionClass"></a> 컬렉션 클래스 만들기  
 다음 예제에서 `DaysOfTheWeek` 클래스는 <xref:System.Collections.IEnumerable> 인터페이스를 구현하며, <xref:System.Collections.IEnumerable.GetEnumerator%2A> 메서드가 필요합니다. 컴파일러는 `GetEnumerator` 메서드를 암시적으로 호출하며, <xref:System.Collections.IEnumerator>가 반환됩니다.  
  
 메서드 `GetEnumerator` 는 `Yield` 문을 사용 하 여 각 문자열을 한 번에 하나씩 반환 하 고 `Iterator` , 한정자는 함수 선언에 있습니다.  
  
```vb  
Sub Main()  
    Dim days As New DaysOfTheWeek()  
    For Each day As String In days  
        Console.Write(day & " ")  
    Next  
    ' Output: Sun Mon Tue Wed Thu Fri Sat  
    Console.ReadKey()  
End Sub  
  
Private Class DaysOfTheWeek  
    Implements IEnumerable  
  
    Public days =  
        New String() {"Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"}  
  
    Public Iterator Function GetEnumerator() As IEnumerator _  
        Implements IEnumerable.GetEnumerator  
  
        ' Yield each day of the week.  
        For i As Integer = 0 To days.Length - 1  
            Yield days(i)  
        Next  
    End Function  
End Class  
```  
  
 다음 예제에서는 동물 컬렉션을 포함하는 `Zoo` 클래스를 만듭니다.  
  
 클래스 인스턴스(`theZoo`)를 참조하는 `For Each` 문은 `GetEnumerator` 메서드를 암시적으로 호출합니다. `Birds` 및 `Mammals` 속성을 참조하는 `For Each` 문은 `AnimalsForType` 명명된 반복기 메서드를 사용합니다.  
  
```vb  
Sub Main()  
    Dim theZoo As New Zoo()  
  
    theZoo.AddMammal("Whale")  
    theZoo.AddMammal("Rhinoceros")  
    theZoo.AddBird("Penguin")  
    theZoo.AddBird("Warbler")  
  
    For Each name As String In theZoo  
        Console.Write(name & " ")  
    Next  
    Console.WriteLine()  
    ' Output: Whale Rhinoceros Penguin Warbler  
  
    For Each name As String In theZoo.Birds  
        Console.Write(name & " ")  
    Next  
    Console.WriteLine()  
    ' Output: Penguin Warbler  
  
    For Each name As String In theZoo.Mammals  
        Console.Write(name & " ")  
    Next  
    Console.WriteLine()  
    ' Output: Whale Rhinoceros  
  
    Console.ReadKey()  
End Sub  
  
Public Class Zoo  
    Implements IEnumerable  
  
    ' Private members.  
    Private animals As New List(Of Animal)  
  
    ' Public methods.  
    Public Sub AddMammal(ByVal name As String)  
        animals.Add(New Animal With {.Name = name, .Type = Animal.TypeEnum.Mammal})  
    End Sub  
  
    Public Sub AddBird(ByVal name As String)  
        animals.Add(New Animal With {.Name = name, .Type = Animal.TypeEnum.Bird})  
    End Sub  
  
    Public Iterator Function GetEnumerator() As IEnumerator _  
        Implements IEnumerable.GetEnumerator  
  
        For Each theAnimal As Animal In animals  
            Yield theAnimal.Name  
        Next  
    End Function  
  
    ' Public members.  
    Public ReadOnly Property Mammals As IEnumerable  
        Get  
            Return AnimalsForType(Animal.TypeEnum.Mammal)  
        End Get  
    End Property  
  
    Public ReadOnly Property Birds As IEnumerable  
        Get  
            Return AnimalsForType(Animal.TypeEnum.Bird)  
        End Get  
    End Property  
  
    ' Private methods.  
    Private Iterator Function AnimalsForType( _  
    ByVal type As Animal.TypeEnum) As IEnumerable  
        For Each theAnimal As Animal In animals  
            If (theAnimal.Type = type) Then  
                Yield theAnimal.Name  
            End If  
        Next  
    End Function  
  
    ' Private class.  
    Private Class Animal  
        Public Enum TypeEnum  
            Bird  
            Mammal  
        End Enum  
  
        Public Property Name As String  
        Public Property Type As TypeEnum  
    End Class  
End Class  
```  
  
## <a name="BKMK_TryBlocks"></a>Try 블록  
 `Yield` Try 블록`Try` 에 문을 사용할 수 있는 Visual Basic. [ Catch ... Finally 문](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md). `Yield` `Catch` 문이 있는 `Finally` 블록은 블록을 포함할 수 있으며 블록을 포함할 수 있습니다. `Try`  
  
 다음 예제에서는 반복기 `Try`함수 `Catch`에, `Finally` 및 블록을 포함 합니다. 반복기 `Finally` 함수의 블록은 `For Each` 반복이 완료 되기 전에 실행 됩니다.  
  
```vb  
Sub Main()  
    For Each number As Integer In Test()  
        Console.WriteLine(number)  
    Next  
    Console.WriteLine("For Each is done.")  
  
    ' Output:  
    '  3  
    '  4  
    '  Something happened. Yields are done.  
    '  Finally is called.  
    '  For Each is done.  
    Console.ReadKey()  
End Sub  
  
Private Iterator Function Test() As IEnumerable(Of Integer)  
    Try  
        Yield 3  
        Yield 4  
        Throw New Exception("Something happened. Yields are done.")  
        Yield 5  
        Yield 6  
    Catch ex As Exception  
        Console.WriteLine(ex.Message)  
    Finally  
        Console.WriteLine("Finally is called.")  
    End Try  
End Function  
```  
  
 `Yield` 문은 `Catch` 블록이 나 블록`Finally` 안에 있을 수 없습니다.  
  
 반복기 메서드 대신 `Catch` `Finally` 본문이 예외를 throw 하는 경우에는 반복기 함수의 블록이 실행 되지 않지만 반복기 함수의 블록이 실행 됩니다. `For Each` 반복기 `Catch` 함수 내의 블록은 반복기 함수 내에서 발생 하는 예외만 catch 합니다.  
  
## <a name="BKMK_AnonymousMethods"></a>무명 메서드  
 Visual Basic에서 익명 함수는 반복기 함수 일 수 있습니다. 다음은 이에 대한 예입니다.  
  
```vb  
Dim iterateSequence = Iterator Function() _  
                      As IEnumerable(Of Integer)  
                          Yield 1  
                          Yield 2  
                      End Function  
  
For Each number As Integer In iterateSequence()  
    Console.Write(number & " ")  
Next  
' Output: 1 2  
Console.ReadKey()  
```  
  
 다음 예제에는 인수의 유효성을 검사 하는 비 반복기 메서드가 있습니다. 메서드는 컬렉션 요소를 설명 하는 익명 반복기의 결과를 반환 합니다.  
  
```vb  
Sub Main()  
    For Each number As Integer In GetSequence(5, 10)  
        Console.Write(number & " ")  
    Next  
    ' Output: 5 6 7 8 9 10  
    Console.ReadKey()  
End Sub  
  
Public Function GetSequence(ByVal low As Integer, ByVal high As Integer) _  
As IEnumerable  
    ' Validate the arguments.  
    If low < 1 Then  
        Throw New ArgumentException("low is too low")  
    End If  
    If high > 140 Then  
        Throw New ArgumentException("high is too high")  
    End If  
  
    ' Return an anonymous iterator function.  
    Dim iterateSequence = Iterator Function() As IEnumerable  
                              For index = low To high  
                                  Yield index  
                              Next  
                          End Function  
    Return iterateSequence()  
End Function  
```  
  
 유효성 검사가 반복기 함수 내에 있는 경우 `For Each` 본문의 첫 번째 반복이 시작 될 때까지 유효성 검사를 수행할 수 없습니다.  
  
## <a name="BKMK_GenericList"></a> 제네릭 목록과 함께 반복기 사용  
 다음 예제에서 `Stack(Of T)` 제네릭 클래스는 <xref:System.Collections.Generic.IEnumerable%601> 제네릭 인터페이스를 구현합니다. `Push` 메서드는 `T` 형식의 배열에 값을 할당합니다. <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 메서드는 `Yield` 문을 사용하여 배열 값을 반환합니다.  
  
 제네릭 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 메서드뿐 아니라 제네릭이 아닌 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 메서드도 구현해야 합니다. <xref:System.Collections.Generic.IEnumerable%601>이 <xref:System.Collections.IEnumerable>에서 상속하기 때문입니다. 제네릭이 아닌 구현은 제네릭 구현을 따릅니다.  
  
 예제에서는 명명된 반복기를 사용하여 동일한 데이터 컬렉션을 반복하는 다양한 방법을 지원합니다. 이러한 명명된 반복기는 `TopToBottom` 및 `BottomToTop` 속성과 `TopN` 메서드입니다.  
  
 속성 `BottomToTop` 선언에는 `Iterator` 키워드가 포함 됩니다.  
  
```vb  
Sub Main()  
    Dim theStack As New Stack(Of Integer)  
  
    ' Add items to the stack.  
    For number As Integer = 0 To 9  
        theStack.Push(number)  
    Next  
  
    ' Retrieve items from the stack.  
    ' For Each is allowed because theStack implements  
    ' IEnumerable(Of Integer).  
    For Each number As Integer In theStack  
        Console.Write("{0} ", number)  
    Next  
    Console.WriteLine()  
    ' Output: 9 8 7 6 5 4 3 2 1 0  
  
    ' For Each is allowed, because theStack.TopToBottom  
    ' returns IEnumerable(Of Integer).  
    For Each number As Integer In theStack.TopToBottom  
        Console.Write("{0} ", number)  
    Next  
    Console.WriteLine()  
    ' Output: 9 8 7 6 5 4 3 2 1 0  
  
    For Each number As Integer In theStack.BottomToTop  
        Console.Write("{0} ", number)  
    Next  
    Console.WriteLine()  
    ' Output: 0 1 2 3 4 5 6 7 8 9   
  
    For Each number As Integer In theStack.TopN(7)  
        Console.Write("{0} ", number)  
    Next  
    Console.WriteLine()  
    ' Output: 9 8 7 6 5 4 3  
  
    Console.ReadKey()  
End Sub  
  
Public Class Stack(Of T)  
    Implements IEnumerable(Of T)  
  
    Private values As T() = New T(99) {}  
    Private top As Integer = 0  
  
    Public Sub Push(ByVal t As T)  
        values(top) = t  
        top = top + 1  
    End Sub  
  
    Public Function Pop() As T  
        top = top - 1  
        Return values(top)  
    End Function  
  
    ' This function implements the GetEnumerator method. It allows  
    ' an instance of the class to be used in a For Each statement.  
    Public Iterator Function GetEnumerator() As IEnumerator(Of T) _  
        Implements IEnumerable(Of T).GetEnumerator  
  
        For index As Integer = top - 1 To 0 Step -1  
            Yield values(index)  
        Next  
    End Function  
  
    Public Iterator Function GetEnumerator1() As IEnumerator _  
        Implements IEnumerable.GetEnumerator  
  
        Yield GetEnumerator()  
    End Function  
  
    Public ReadOnly Property TopToBottom() As IEnumerable(Of T)  
        Get  
            Return Me  
        End Get  
    End Property  
  
    Public ReadOnly Iterator Property BottomToTop As IEnumerable(Of T)  
        Get  
            For index As Integer = 0 To top - 1  
                Yield values(index)  
            Next  
        End Get  
    End Property  
  
    Public Iterator Function TopN(ByVal itemsFromTop As Integer) _  
        As IEnumerable(Of T)  
  
        ' Return less than itemsFromTop if necessary.  
        Dim startIndex As Integer =  
            If(itemsFromTop >= top, 0, top - itemsFromTop)  
  
        For index As Integer = top - 1 To startIndex Step -1  
            Yield values(index)  
        Next  
    End Function  
End Class  
```  
  
## <a name="BKMK_SyntaxInformation"></a> 구문 정보  
 반복기는 메서드 또는 `get` 접근자로 발생할 수 있습니다. 반복기는 이벤트, 인스턴스 생성자, 정적 생성자 또는 정적 소멸자에서 발생할 수 없습니다.  
  
 `Yield` 문의 식 형식에서 반복기의 반환 형식으로 암시적 변환이 있어야 합니다.  
  
 Visual Basic 반복기 메서드에는 `ByRef` 매개 변수를 사용할 수 없습니다.  
  
 Visual Basic에서 "Yield"는 예약 된 단어가 아니므로 `Iterator` `get` 메서드나 접근자에서 사용 되는 경우에만 특별 한 의미가 있습니다.  
  
## <a name="BKMK_Technical"></a> 기술 구현  
 반복기를 메서드로 작성하는 경우에도 컴파일러는 실제로 상태 시스템인 중첩 클래스로 변환합니다. 이 클래스는 클라이언트 코드의 `For Each...Next` 루프가 계속되는 한 반복기의 위치를 추적합니다.  
  
 컴파일러의 용도를 확인하려면 Ildasm.exe 도구를 사용하여 반복기 메서드에 대해 생성되는 Microsoft Intermediate Language 코드를 확인할 수 있습니다.  
  
 [클래스](../../../csharp/language-reference/keywords/class.md) 또는 [구조체](../../../csharp/language-reference/keywords/struct.md)에 대 한 반복기를 만들 때 전체 <xref:System.Collections.IEnumerator> 인터페이스를 구현할 필요가 없습니다. 컴파일러는 반복기를 검색할 경우 <xref:System.Collections.IEnumerator> 또는 <xref:System.Collections.Generic.IEnumerator%601> 인터페이스의 `Current`, `MoveNext` 및 `Dispose` 메서드를 자동으로 생성합니다.  
  
 `For Each…Next` 루프를 연속 반복하거나 `IEnumerator.MoveNext`를 직접 호출하면 다음 반복기 코드 본문이 이전 `Yield` 문 다음에 다시 시작됩니다. 그런 다음 반복기 본문의 끝 `Yield` 에 도달 하거나 `Exit Function` 또는 `Return` 문이 발생할 때까지 다음 문으로 계속 합니다.  
  
 반복기는 메서드를 <xref:System.Collections.IEnumerator.Reset%2A?displayProperty=nameWithType> 지원 하지 않습니다. 처음부터 다시 반복하려면 새 반복기를 가져와야 합니다.  
  
 자세한 내용은 [Visual Basic 언어 사양](../../../visual-basic/reference/language-specification/index.md)을 참조 하세요.  
  
## <a name="BKMK_UseOfIterators"></a> 반복기 사용  
 반복기를 사용하면 복잡한 코드를 사용하여 목록 시퀀스를 채워야 하는 경우 `For Each` 루프의 단순성을 유지할 수 있습니다. 이 기능은 다음을 수행하려는 경우에 유용할 수 있습니다.  
  
- 첫 번째 `For Each` 루프 반복 후 목록 시퀀스를 수정합니다.  
  
- 첫 번째 `For Each` 루프 반복 전에 큰 목록이 완전히 로드되지 않도록 합니다. 한 가지 예로 테이블 행을 일괄 로드하는 페이징 페치가 있으며, 또 다른 예로 .NET Framework 내에서 반복기를 구현하는 <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> 메서드가 있습니다.  
  
- 반복기에서 목록 작성을 캡슐화합니다. 반복기 메서드에서 목록을 빌드한 후 루프에서 각 결과를 생성할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Collections.Generic>
- <xref:System.Collections.Generic.IEnumerable%601>
- [For Each...Next 문](../../../visual-basic/language-reference/statements/for-each-next-statement.md)
- [Yield 문](../../../visual-basic/language-reference/statements/yield-statement.md)
- [반복기](../../../visual-basic/language-reference/modifiers/iterator.md)
