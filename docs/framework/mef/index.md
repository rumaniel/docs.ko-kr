---
title: MEF(Managed Extensibility Framework)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Managed Extensibility Framework, overview
- MEF, overview
ms.assetid: 6c61b4ec-c6df-4651-80f1-4854f8b14dde
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6fc66837dc31dc1697bcb4ad6dddfb57bfb99bd4
ms.sourcegitcommit: 1e7ac70be1b4d89708c0d9552897515f2cbf52c4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68434090"
---
# <a name="managed-extensibility-framework-mef"></a>MEF(Managed Extensibility Framework)

이 항목에서는 .NET Framework 4에 도입된 Managed Extensibility Framework에 대해 간략하게 설명합니다.

<a name="what_is_mef"></a>
## <a name="what-is-mef"></a>MEF란?

MEF(Managed Extensibility Framework)는 확장 가능한 경량 애플리케이션을 만드는 데 사용할 수 있는 라이브러리입니다. 애플리케이션 개발자는 MEF를 통해 구성을 수행하지 않고도 확장을 검색하여 사용할 수 있습니다. 또한 확장명 개발자는 코드를 쉽게 캡슐화하고 취약한 강한 종속성을 방지할 수 있습니다. MEF를 통해 애플리케이션 내에서뿐 아니라 애플리케이션 간에도 확장을 다시 사용할 수 있습니다.

<a name="the_problem_of_extensibility"></a>
## <a name="the-problem-of-extensibility"></a>확장성 문제
 확장성을 지원해야 하는 대규모 애플리케이션을 설계한다고 가정해 보겠습니다. 애플리케이션은 작은 구성 요소를 여러 개 포함해야 할 수 있으며 이러한 구성 요소를 만들고 실행해야 합니다.

 이 경우 사용할 수 있는 가장 간단한 방식은 구성 요소를 애플리케이션에 코드로 포함하여 코드에서 직접 호출하는 것입니다. 그러나 이 방식에는 여러 가지 명백한 단점이 있습니다. 그중 가장 중요한 것은 소스 코드를 수정하지 않으면 새 구성 요소를 추가할 수가 없다는 것입니다. 웹 애플리케이션의 경우에는 이러한 제한이 있어도 큰 문제가 없을 수 있지만 클라이언트 애플리케이션에서는 이러한 제한이 있어서는 안 됩니다. 또한 타사에서 개발한 구성 요소의 소스 코드에는 액세스할 수 없으며 자신이 개발한 구성 요소를 타사에서 액세스하도록 허용할 수 없다는 점도 문제입니다.

 이 방식보다 약간 더 고급 방식은 애플리케이션과 구성 요소를 분리할 수 있도록 확장점(인터페이스)을 제공하는 것입니다. 이 모델에서는 구성 요소가 구현할 수 있는 인터페이스와 구성 요소가 애플리케이션과 상호 작용하는 데 사용할 수 있는 API를 제공할 수 있습니다. 그러면 소스 코드 액세스가 필요하다는 문제는 해결되지만 이 방식에도 고유한 문제점이 있습니다.

 애플리케이션에는 자체적으로 구성 요소를 검색하는 기능이 없으므로 사용 가능하며 로드해야 하는 구성 요소를 명시적으로 지정해야 합니다. 일반적으로는 이를 위해 사용 가능한 구성 요소를 구성 파일에 명시적으로 등록합니다. 따라서 구성 요소가 올바른지를 확인하는 과정에서 유지 관리 문제가 발생할 수 있습니다(특히 업데이트를 수행하는 개발자가 아닌 최종 사용자의 경우).

 또한 구성 요소는 엄격하게 정의된 애플리케이션 자체 채널을 통해서가 아니면 서로 통신할 수 없습니다. 일반적으로 애플리케이션 설계자가 특정 통신이 필요함을 예측하지 못했다면 이러한 통신은 불가능합니다.

 마지막으로, 구성 요소 개발자는 구현하는 인터페이스를 포함하는 어셈블리에 대한 강한 종속성을 허용해야 합니다. 이로 인해 구성 요소를 둘 이상의 애플리케이션에서 사용하기가 어려워지며, 구성 요소용 테스트 프레임워크를 만들 때도 문제가 발생할 수 있습니다.

<a name="what_mef_provides"></a>
## <a name="what-mef-provides"></a>MEF에서 제공하는 기능
 이처럼 사용 가능한 구성 요소를 명시적으로 등록하는 대신 MEF는 *컴퍼지션*을 통해 구성 요소를 암시적으로 검색하는 방법을 제공합니다. MEF 구성 요소(‘파트’)는 해당 종속성(*Import*)과 제공하는 기능(*Export*)을 모두 선언적으로 지정합니다.  파트를 작성할 때 MEF 컴퍼지션 엔진은 다른 파트에서 제공되는 항목을 사용하여 Import를 충족합니다.

 이러한 방식이 사용되므로 이전 섹션에서 설명한 문제가 해결됩니다. MEF 파트는 해당 기능을 선언적으로 지정하기 때문에 런타임에 검색이 가능합니다. 따라서 애플리케이션이 하드 코드된 참조나 취약한 구성 파일 없이도 파트를 사용할 수 있습니다. MEF를 사용하는 경우 애플리케이션이 파트를 인스턴스화하거나 어셈블리를 로드하지 않고도 메타데이터를 기준으로 파트를 검색 및 검사할 수 있습니다. 그러므로 확장을 로드해야 하는 시기와 방법을 면밀하게 지정하지 않아도 됩니다.

 파트너는 제공된 Export뿐 아니라 Import(다른 파트에 의해 채워짐)도 지정할 수 있습니다. 따라서 파트가 서로 쉽게 통신할 수 있으며 효율적인 코드 팩터링이 허용됩니다. 예를 들어 여러 구성 요소에 공통적으로 사용되는 서비스를 별도의 파트에 팩터링하여 쉽게 수정하거나 대체할 수 있습니다.

 MEF 모델에서는 특정 애플리케이션 어셈블리에 대한 강한 종속성이 필요하지 않으므로 애플리케이션 간에 확장을 다시 사용할 수 있습니다. 이로 인해 애플리케이션에 관계없이 확장명 구성 요소를 테스트하기 위한 테스트 경도를 쉽게 개발할 수 있습니다.

 MEF를 사용하여 작성된 확장 가능한 애플리케이션은 확장 구성 요소를 통해 채울 수 있는 Import를 선언하며, 애플리케이션 서비스를 확장에 노출하기 위해 Export도 선언할 수 있습니다. 각 확장명 구성 요소는 Export를 선언하며 Import도 선언할 수 있습니다. 이러한 방식으로 인해 확장명 구성 요소 자체를 자동으로 확장할 수 있습니다.

<a name="where_is_mef_available"></a>
## <a name="where-is-mef-available"></a>MEF 제공 위치
 MEF는 .NET Framework 4의 필수 요소로, .NET Framework를 사용하는 모든 위치에서 사용 가능합니다. Windows Forms, WPF 또는 기타 기술을 사용하는 클라이언트 애플리케이션이나 ASP.NET을 사용하는 서버 애플리케이션에서 MEF를 사용할 수 있습니다.

<a name="mef_and_maf"></a>
## <a name="mef-and-maf"></a>MEF 및 MAF
 이전 버전의 .NET Framework에는 애플리케이션이 확장을 격리 및 관리하도록 허용하는 MAF(Managed Add-in Framework)가 도입되었습니다. MAF는 MEF에 비해 다소 수준이 높으며 확장 격리와 어셈블리 로드/언로드에 주력하는 반면 MEF에서는 검색 기능, 확장성 및 이동성에 주력합니다. 이 두 프레임워크는 원활하게 상호 작용하며, 애플리케이션 하나에서 두 프레임워크를 모두 사용할 수 있습니다.

<a name="simplecalculator_an_example_application"></a>

## <a name="simplecalculator-an-example-application"></a>SimpleCalculator: 예제 애플리케이션

MEF에서 수행할 수 있는 작업을 확인하는 가장 간단한 방법은 간단한 MEF 애플리케이션을 빌드하는 것입니다. 이 예제에서는 SimpleCalculator라는 매우 간단한 계산기를 빌드합니다. SimpleCalculator에서는 "5+3" 또는 "6-2"와 같은 형식의 기본적인 산술 명령을 수락하고 정답을 반환하는 콘솔 응용 프로그램을 만들려고 합니다. MEF를 사용하면 애플리케이션 코드를 변경하지 않고도 새 연산자를 추가할 수 있습니다.

이 예제의 전체 코드를 다운로드하려면 [SimpleCalculator sample](https://code.msdn.microsoft.com/windowsdesktop/Simple-Calculator-MEF-1152654e)(SimpleCalculator 샘플)을 참조하세요.

> [!NOTE]
> SimpleCalculator는 사용 방식을 보여 주는 실제 시나리오를 제공하기보다는 MEF의 개념과 구문을 제시하는 데 사용됩니다. MEF의 이점을 가장 효율적으로 활용할 수 있는 대부분의 애플리케이션은 SimpleCalculator보다 복잡합니다. 보다 포괄적인 예제는 GitHub에서 [Managed Extensibility Framework](https://github.com/MicrosoftArchive/mef)를 참조하세요.

- 우선 Visual Studio에서 새 콘솔 애플리케이션 프로젝트를 만들고 이름을 `SimpleCalculator`로 지정합니다.

- 그런 다음 MEF가 상주하는 System.ComponentModel.Composition 어셈블리에 대한 참조를 추가합니다.

- Module1.vb나 Program.cs를 열고 System.ComponentModel.Composition 및 System.ComponentModel.Composition.Hosting에 대해 `Imports` 또는 `using` 문을 추가합니다. 이 두 네임스페이스는 확장 가능한 애플리케이션을 개발하는 데 필요한 MEF 형식을 포함합니다.

- Visual Basic을 사용하는 경우 `Module1` 모듈을 선언하는 줄에 `Public` 키워드를 추가합니다.

<a name="composition_container_and_catalogs"></a>

## <a name="composition-container-and-catalogs"></a>컴퍼지션 컨테이너 및 카탈로그

MEF 컴퍼지션 모델에서 핵심적인 요소는 사용 가능한 모든 파트를 포함하며 컴퍼지션을 수행하는 ‘컴퍼지션 컨테이너’입니다.  컴퍼지션이란 Import를 Export에 일치시키는 작업입니다. SimpleCalculator에서는 가장 일반적인 유형의 컴퍼지션 컨테이너인 <xref:System.ComponentModel.Composition.Hosting.CompositionContainer>를 사용합니다.

Visual Basic을 사용하는 경우 Module1.vb에서 `Program`이라는 public 클래스를 추가합니다.

Module1.vb 또는 Program.cs의 `Program` 클래스에 다음 줄을 추가합니다.

```vb
Dim _container As CompositionContainer
```

```csharp
private CompositionContainer _container;
```

컴퍼지션 컨테이너는 사용 가능한 파트를 검색하기 위해 ‘카탈로그’를 사용합니다.  카탈로그는 일부 소스에서 사용 가능한 파트를 검색하는 개체입니다. MEF는 제공된 형식, 어셈블리 또는 디렉터리에서 파트를 검색하기 위한 카탈로그를 제공합니다. 애플리케이션 개발자는 쉽게 새 카탈로그를 만들어 웹 서비스 등의 다른 소스에서 파트를 검색할 수 있습니다.

`Program` 클래스에 다음 생성자를 추가합니다.

```vb
Public Sub New()
    ' An aggregate catalog that combines multiple catalogs.
     Dim catalog = New AggregateCatalog()

    ' Adds all the parts found in the same assembly as the Program class.
    catalog.Catalogs.Add(New AssemblyCatalog(GetType(Program).Assembly))

    ' Create the CompositionContainer with the parts in the catalog.
    _container = New CompositionContainer(catalog)

    ' Fill the imports of this object.
    Try
        _container.ComposeParts(Me)
    Catch ex As CompositionException
        Console.WriteLine(ex.ToString)
    End Try
End Sub
```

```csharp
private Program()
{
    // An aggregate catalog that combines multiple catalogs.
    var catalog = new AggregateCatalog();
    // Adds all the parts found in the same assembly as the Program class.
    catalog.Catalogs.Add(new AssemblyCatalog(typeof(Program).Assembly));

    // Create the CompositionContainer with the parts in the catalog.
    _container = new CompositionContainer(catalog);

    // Fill the imports of this object.
    try
    {
        this._container.ComposeParts(this);
    }
    catch (CompositionException compositionException)
    {
        Console.WriteLine(compositionException.ToString());
   }
}
```

<xref:System.ComponentModel.Composition.AttributedModelServices.ComposeParts%2A>를 호출하면 컴퍼지션 컨테이너에 특정 파트 집합(여기서는 현재 `Program` 인스턴스)을 작성하도록 명령합니다. 그러나 이 시점에서는 `Program`에 채울 Import가 없으므로 아무 작업도 수행되지 않습니다.

<a name="imports_and_exports_with_attributes"></a>
## <a name="imports-and-exports-with-attributes"></a>특성이 포함된 Import 및 Export
 먼저 `Program`에서 계산기 Import를 수행합니다. 그러면 `Program`으로 전송되는 콘솔 입력 및 출력과 같은 사용자 인터페이스 관련 사항을 계산기 논리에서 분리할 수 있습니다.

 `Program` 클래스에 다음 코드를 추가합니다.

```vb
<Import(GetType(ICalculator))>
Public Property calculator As ICalculator
```

```csharp
[Import(typeof(ICalculator))]
public ICalculator calculator;
```

 `calculator` 개체는 일반적인 방식으로 선언되지만 여기서는 해당 개체가 <xref:System.ComponentModel.Composition.ImportAttribute> 특성으로 데코레이팅되어 있습니다. 이 특성은 Import로 지정할 항목을 선언합니다 즉, 개체를 구성할 때 컴퍼지션 엔진에서 특성이 채워집니다.

 모든 Import에는 일치시킬 Export를 결정하는 ‘계약’이 있습니다.  계약은 명시적으로 지정된 문자열일 수도 있고 MEF가 특정 형식(여기서는 `ICalculator` 인터페이스)에서 자동으로 생성할 수도 있습니다. 일치하는 계약을 사용하여 선언된 Export는 이 Import를 충족합니다. 여기서는 `calculator` 개체의 실제 형식이 `ICalculator`이지만 반드시 형식이 일치해야 하는 것은 아닙니다. 계약은 가져오는 개체의 형식과는 별개입니다. 그러므로 여기서 `typeof(ICalculator)`를 빼도 됩니다. 명시적으로 지정하지 않는 경우 MEF는 계약이 Import 형식을 기준으로 한다고 자동으로 가정합니다.

 아래의 매우 간단한 인터페이스를 모듈 또는 `SimpleCalculator` 네임스페이스에 추가합니다.

```vb
Public Interface ICalculator
    Function Calculate(ByVal input As String) As String
End Interface
```

```csharp
public interface ICalculator
{
    String Calculate(String input);
}
```

 `ICalculator`를 정의한 후에는 이 형식을 구현하는 클래스를 지정해야 합니다. 모듈 또는 `SimpleCalculator` 네임스페이스에 다음 클래스를 추가합니다.

```vb
<Export(GetType(ICalculator))>
Public Class MySimpleCalculator
   Implements ICalculator

End Class
```

```csharp
[Export(typeof(ICalculator))]
class MySimpleCalculator : ICalculator
{

}
```

 위의 코드에는 `Program`의 Import와 일치하는 Export가 포함되어 있습니다. Export와 Import가 일치하려면 Export에 동일한 계약이 있어야 합니다. `typeof(MySimpleCalculator)` 기반 계약 하의 Export를 지정하는 경우 불일치가 발생하며 Import는 채워지지 않습니다. 계약은 정확히 일치해야 합니다.

 컴퍼지션 컨테이너는 이 어셈블리에서 사용 가능한 모든 파트로 채워지므로 `MySimpleCalculator` 파트를 사용할 수 있습니다. `Program`의 생성자가 `Program` 개체에 대해 컴퍼지션을 수행할 때 해당 Import는 해당 용도로 작성되는 `MySimpleCalculator` 개체로 채워집니다.

 사용자 인터페이스 계층(`Program`)은 다른 항목을 확인할 필요가 없습니다. 따라서 `Main` 메서드에서 나머지 사용자 인터페이스 논리를 채울 수 있습니다.

 `Main` 메서드에 다음 코드를 추가합니다.

```vb
Sub Main()
    ' Composition is performed in the constructor.
    Dim p As New Program()
    Dim s As String
    Console.WriteLine("Enter Command:")
    While (True)
        s = Console.ReadLine()
        Console.WriteLine(p.calculator.Calculate(s))
    End While
End Sub
```

```csharp
static void Main(string[] args)
{
    // Composition is performed in the constructor.
    var p = new Program();
    String s;
    Console.WriteLine("Enter Command:");
    while (true)
    {
        s = Console.ReadLine();
        Console.WriteLine(p.calculator.Calculate(s));
    }
}
```

 이 코드는 단순히 입력 줄을 읽고 결과에서 `Calculate`의 `ICalculator` 함수를 호출하여 콘솔에 쓰기 저장합니다. `Program`에서 필요한 코드는 이것뿐입니다. 나머지 모든 작업은 파트에서 수행됩니다.

<a name="further_imports_and_importmany"></a>
## <a name="further-imports-and-importmany"></a>추가 Import 및 ImportMany
 SimpleCalculator를 확장하려면 operations 목록을 가져와야 합니다. 일반적인 <xref:System.ComponentModel.Composition.ImportAttribute> 특성은 <xref:System.ComponentModel.Composition.ExportAttribute> 하나만으로 채워집니다. 이 클래스를 둘 이상 사용할 수 있는 경우에는 컴퍼지션 엔진에서 오류가 발생합니다. Export를 수에 관계없이 채울 수 있는 Import를 만들려는 경우에는 <xref:System.ComponentModel.Composition.ImportManyAttribute> 특성을 사용하면 됩니다.

 `MySimpleCalculator` 클래스에 다음 operations 속성을 추가합니다.

```vb
<ImportMany()>
Public Property operations As IEnumerable(Of Lazy(Of IOperation, IOperationData))
```

```csharp
[ImportMany]
IEnumerable<Lazy<IOperation, IOperationData>> operations;
```

 <xref:System.Lazy%602>는 Export에 대한 간접 참조를 저장할 수 있도록 MEF에서 제공하는 형식입니다. 여기서는 내보낸 개체 자체뿐 아니라 내보낸 개체를 설명하는 정보인 ‘내보내기 메타데이터’도 제공됩니다.  각 <xref:System.Lazy%602>는 실제 연산을 나타내는 `IOperation` 개체와 해당 메타데이터를 나타내는 `IOperationData` 개체를 포함합니다.

 모듈 또는 `SimpleCalculator` 네임스페이스에 다음과 같은 간단한 인터페이스를 추가합니다.

```vb
Public Interface IOperation
    Function Operate(ByVal left As Integer, ByVal right As Integer) As Integer
End Interface

Public Interface IOperationData
    ReadOnly Property Symbol As Char
End Interface
```

```csharp
public interface IOperation
{
     int Operate(int left, int right);
}

public interface IOperationData
{
    Char Symbol { get; }
}
```

 여기서 각 연산의 메타데이터는 +, -, * 등 해당 연산을 나타내는 기호입니다. 추가 연산을 사용하려면 모듈 또는 `SimpleCalculator` 네임스페이스에 다음 클래스를 추가합니다.

```vb
<Export(GetType(IOperation))>
<ExportMetadata("Symbol", "+"c)>
Public Class Add
    Implements IOperation

    Public Function Operate(ByVal left As Integer, ByVal right As Integer) As Integer Implements IOperation.Operate
        Return left + right
    End Function
End Class
```

```csharp
[Export(typeof(IOperation))]
[ExportMetadata("Symbol", '+')]
class Add: IOperation
{
    public int Operate(int left, int right)
    {
        return left + right;
    }
}
```

 <xref:System.ComponentModel.Composition.ExportAttribute> 특성은 이전과 같이 작동합니다. <xref:System.ComponentModel.Composition.ExportMetadataAttribute> 특성은 메타데이터를 해당 Export에 이름-값 쌍 형식으로 연결합니다. `Add` 클래스가 `IOperation`을 구현하는 동안에는 `IOperationData`를 구현하는 클래스가 명시적으로 정의되지 않습니다. 대신 제공된 메타데이터 이름을 기준으로 하는 속성을 사용하여 MEF에서 클래스를 암시적으로 만듭니다. 이는 MEF에서 메타데이터에 액세스하는 여러 방법 중 하나입니다.

 MEF에서 컴퍼지션은 ‘재귀’ 방식으로 수행됩니다.  즉, 명시적으로 구성한 `Program` 개체가 `ICalculator` 형식으로 확인된 `MySimpleCalculator`를 가져왔습니다. `MySimpleCalculator`는 `IOperation` 개체 컬렉션을 가져오며 해당 Import는 `MySimpleCalculator`를 만들 때 `Program`의 Import와 동시에 채워집니다. `Add` 클래스가 추가 Import를 선언한 경우에는 해당 Import도 채워지는 식으로 작업이 진행됩니다. 채워지지 않은 Import가 있으면 컴퍼지션 오류가 발생합니다. 그러나 Import를 선택 사항으로 선언하거나 Import에 기본값을 할당할 수는 있습니다.

<a name="calculator_logic"></a>
## <a name="calculator-logic"></a>계산기 논리
 이러한 파트를 배치한 후에는 계산기 논리 자체만 추가하면 됩니다. `MySimpleCalculator` 클래스에 다음 코드를 추가하여 `Calculate` 메서드를 구현합니다.

```vb
Public Function Calculate(ByVal input As String) As String Implements ICalculator.Calculate
    Dim left, right As Integer
    Dim operation As Char
    ' Finds the operator.
    Dim fn = FindFirstNonDigit(input)
    If fn < 0 Then
        Return "Could not parse command."
    End If
    operation = input(fn)
    Try
        ' Separate out the operands.
        left = Integer.Parse(input.Substring(0, fn))
        right = Integer.Parse(input.Substring(fn + 1))
    Catch ex As Exception
        Return "Could not parse command."
    End Try
    For Each i As Lazy(Of IOperation, IOperationData) In operations
        If i.Metadata.symbol = operation Then
            Return i.Value.Operate(left, right).ToString()
        End If
    Next
    Return "Operation not found!"
End Function
```

```csharp
public String Calculate(String input)
{
    int left;
    int right;
    char operation;
    // Finds the operator.
    int fn = FindFirstNonDigit(input); 
    if (fn < 0) return "Could not parse command.";

    try
    {
        // Separate out the operands.
        left = int.Parse(input.Substring(0, fn));
        right = int.Parse(input.Substring(fn + 1));
    }
    catch
    {
        return "Could not parse command.";
    }

    operation = input[fn];

    foreach (Lazy<IOperation, IOperationData> i in operations)
    {
        if (i.Metadata.Symbol.Equals(operation)) return i.Value.Operate(left, right).ToString();
    }
    return "Operation Not Found!";
}
```

 초기 단계에서는 입력 문자열을 왼쪽 및 오른쪽 피연산자와 연산자 문자로 구문 분석합니다. `foreach` 루프에서는 `operations` 컬렉션의 모든 멤버를 검사합니다. 이러한 개체는 <xref:System.Lazy%602> 형식이며 <xref:System.Lazy%602.Metadata%2A> 속성과 <xref:System.Lazy%601.Value%2A> 속성을 각각 사용하여 해당 메타데이터 값과 내보낸 개체에 액세스할 수 있습니다. 여기서 `Symbol` 개체의 `IOperationData` 속성이 일치하는 것으로 확인되면 계산기는 `Operate` 개체의 `IOperation` 메서드를 호출하고 결과를 반환합니다.

 계산기를 완성하려면 문자열에서 숫자가 아닌 첫 번째 문자의 위치를 반환하는 도우미 메서드도 필요합니다. `MySimpleCalculator` 클래스에 다음 도우미 메서드를 추가합니다.

```vb
Private Function FindFirstNonDigit(ByVal s As String) As Integer
    For i = 0 To s.Length - 1
        If (Not (Char.IsDigit(s(i)))) Then Return i
    Next
    Return -1
End Function
```

```csharp
private int FindFirstNonDigit(string s)
{
    for (int i = 0; i < s.Length; i++)
    {
        if (!(Char.IsDigit(s[i]))) return i;
    }
    return -1;
}
```

 이제 프로젝트를 컴파일하고 실행할 수 있습니다. Visual Basic에서 `Public` 키워드를 `Module1`에 추가했는지 확인합니다. 콘솔 창에서 “5+3” 등의 더하기 연산을 입력하면 계산기가 결과를 반환합니다. 다른 연산자를 추가하면 “Operation Not Found!” 메시지가 반환됩니다.

<a name="extending_simplecalculator_using_a_new_class"></a>
## <a name="extending-simplecalculator-using-a-new-class"></a>새 클래스를 사용하여 SimpleCalculator 확장
 계산기가 작동하면 새 연산을 쉽게 추가할 수 있습니다. 모듈 또는 `SimpleCalculator` 네임스페이스에 다음 클래스를 추가합니다.

```vb
<Export(GetType(IOperation))>
<ExportMetadata("Symbol", "-"c)>
Public Class Subtract
    Implements IOperation

    Public Function Operate(ByVal left As Integer, ByVal right As Integer) As Integer Implements IOperation.Operate
        Return left - right
    End Function
End Class
```

```csharp
[Export(typeof(IOperation))]
[ExportMetadata("Symbol", '-')]
class Subtract : IOperation
{
    public int Operate(int left, int right)
    {
        return left - right;
    }
}
```

 프로젝트를 컴파일하고 실행합니다. "5-3"과 같은 빼기 연산을 입력합니다. 이제 계산기에서 더하기는 물론 빼기도 지원합니다.

<a name="extending_simplecalculator_using_a_new_assembly"></a>
## <a name="extending-simplecalculator-using-a-new-assembly"></a>새 어셈블리를 사용하여 SimpleCalculator 확장
 소스 코드에 클래스를 추가하는 것은 간단하지만 MEF는 애플리케이션 자체의 소스 외부에서 파트를 확인할 수 있는 기능을 제공합니다. 이 기능을 확인하려면 <xref:System.ComponentModel.Composition.Hosting.DirectoryCatalog>를 추가하여 자체 어셈블리는 물론 디렉터리에서도 파트를 검색하도록 SimpleCalculator를 수정해야 합니다.

 `Extensions`라는 새 디렉터리를 SimpleCalculator 프로젝트에 추가합니다. 솔루션 수준이 아닌 프로젝트 수준에 디렉터리를 추가해야 합니다. `ExtendedOperations`라는 새 클래스 라이브러리 프로젝트를 솔루션에 추가합니다. 새 프로젝트가 별도의 어셈블리로 컴파일됩니다.

 ExtendedOperations 프로젝트에 대해 프로젝트 속성 디자이너를 열고 **컴파일** 또는 **빌드** 탭을 클릭합니다. **빌드 출력 경로** 또는 **출력 경로**가 SimpleCalculator 프로젝트 디렉터리의 Extensions 디렉터리(..\SimpleCalculator\Extensions\\)를 가리키도록 변경합니다.

 Module1.vb 또는 Program.cs 에서 `Program` 생성자에 다음 줄을 추가합니다.

```vb
catalog.Catalogs.Add(New DirectoryCatalog("C:\SimpleCalculator\SimpleCalculator\Extensions"))
```

```csharp
catalog.Catalogs.Add(new DirectoryCatalog("C:\\SimpleCalculator\\SimpleCalculator\\Extensions"));
```

 예제 경로를 Extensions 디렉터리의 경로로 바꿉니다. 이 경로는 디버깅용으로만 사용할 수 있습니다. 프로덕션 애플리케이션에서는 상대 경로를 사용합니다. 이제 <xref:System.ComponentModel.Composition.Hosting.DirectoryCatalog>는 Extensions 디렉터리의 어셈블리에서 발견되는 파트를 컴퍼지션 컨테이너에 추가합니다.

 ExtendedOperations 프로젝트에서 SimpleCalculator 및 System.ComponentModel.Composition에 대한 참조를 추가합니다. ExtendedOperations 클래스 파일에서 System.ComponentModel.Composition에 대해 `Imports` 또는 `using` 문을 추가합니다. Visual Basic에서 SimpleCalculator에 대해 `Imports` 문도 추가합니다. 그런 다음 ExtendedOperations 클래스 파일에 다음 클래스를 추가합니다.

```vb
<Export(GetType(SimpleCalculator.IOperation))>
<ExportMetadata("Symbol", "%"c)>
Public Class Modulo
    Implements IOperation

    Public Function Operate(ByVal left As Integer, ByVal right As Integer) As Integer Implements IOperation.Operate
        Return left Mod right
    End Function
End Class
```

```csharp
[Export(typeof(SimpleCalculator.IOperation))]
[ExportMetadata("Symbol", '%')]
public class Mod : SimpleCalculator.IOperation
{
    public int Operate(int left, int right)
    {
        return left % right;
    }
}
```

 계약이 일치하려면 <xref:System.ComponentModel.Composition.ExportAttribute> 특성의 형식이 <xref:System.ComponentModel.Composition.ImportAttribute>와 같아야 합니다.

 프로젝트를 컴파일하고 실행합니다. 새 Mod(%) 연산자를 테스트합니다.

<a name="conclusion"></a>
## <a name="conclusion"></a>결론
 이 항목에서는 MEF의 기본 개념에 대해 설명했습니다.

- 파트, 카탈로그 및 컴퍼지션 컨테이너

     파트와 컴퍼지션은 MEF 애플리케이션의 기본 구성 요소입니다. 파트는 값을 가져오거나 내보내는 모든 개체(자기 자신 포함)입니다. 카탈로그는 특정 소스의 파트 컬렉션을 제공합니다. 컴퍼지션 컨테이너는 카탈로그에서 제공하는 파트를 사용하여 컴퍼지션(Import와 Export의 바인딩)을 수행합니다.

- Import 및 Export

     구성 요소는 Import와 Export를 사용하여 통신합니다. 구성 요소는 Import를 통해 특정 값이나 개체의 요구 사항을 지정하고 Export를 통해 값 사용 가능 여부를 지정합니다. 계약을 통해 Export 목록에서 각 Import와 일치하는 항목을 찾습니다.

<a name="where_do_i_go_now"></a>
## <a name="where-do-i-go-now"></a>다음 단계
 이 예제의 전체 코드를 다운로드하려면 [SimpleCalculator sample](https://code.msdn.microsoft.com/windowsdesktop/Simple-Calculator-MEF-1152654e)(SimpleCalculator 샘플)을 참조하세요.

 코드 예제에 대한 자세한 내용은 [Managed Extensibility Framework](https://github.com/MicrosoftArchive/mef)를 참조하세요. MEF 형식 목록은 <xref:System.ComponentModel.Composition?displayProperty=nameWithType> 네임스페이스를 참조하세요.
