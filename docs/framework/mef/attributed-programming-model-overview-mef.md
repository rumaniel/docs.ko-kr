---
title: 특성을 사용하는 프로그래밍 모델 개요(MEF)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- MEF, attributed programming model
- attributed programming model [MEF]
ms.assetid: 49b787ff-2741-4836-ad51-c3017dc592d4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7dab1474454f8169d8d0d80413c6fb95677fb4bf
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49453397"
---
# <a name="attributed-programming-model-overview-mef"></a>특성을 사용하는 프로그래밍 모델 개요(MEF)
MEF(Managed Extensibility Framework)에서 *프로그래밍 모델* 은 MEF가 작동하는 개념 개체 집합을 정의하는 특정 방법입니다. 이러한 개념 개체에는 파트, 가져오기 및 내보내기가 포함됩니다. MEF에서는 이러한 개체를 사용하지만 이러한 개체를 표현해야 하는 방법을 지정하지는 않습니다. 따라서 사용자 지정 프로그래밍 모델을 비롯한 매우 다양한 프로그래밍 모델이 가능합니다.  
  
 MEF에 사용되는 기본 프로그래밍 모델은 *특성 사용 프로그래밍 모델*입니다. 특성 사용 프로그래밍 모델에서 파트, 가져오기, 내보내기 및 기타 개체는 일반 .NET Framework 클래스를 데코레이팅하는 특성으로 정의됩니다. 이 항목에서는 특성 사용 프로그래밍 모델에서 제공하는 특성을 사용하여 MEF 응용 프로그램을 만드는 방법을 설명합니다.  
  
<a name="import_and_export_basics"></a>   
## <a name="import-and-export-basics"></a>가져오기 및 내보내기 기본 사항  
 *내보내기* 는 파트가 컨테이너의 다른 파트에 제공하는 값이고, *가져오기* 는 사용 가능한 내보내기에서 채울 파트가 컨테이너에 표현하는 요구 사항입니다. 특성 사용 프로그래밍 모델에서 가져오기 및 내보내기는 `Import` 및 `Export` 특성으로 클래스 또는 멤버를 데코레이팅하여 선언됩니다. `Export` 특성은 클래스, 필드, 속성 또는 메서드를 데코레이팅할 수 있는 반면, `Import` 특성은 필드, 속성 또는 생성자 매개 변수를 데코레이팅할 수 있습니다.  
  
 가져오기를 내보내기와 일치시키려면 가져오기와 내보내기가 동일한 *계약*을 포함해야 합니다. 계약은 *계약 이름*이라는 문자열과 *계약 형식*이라는 내보내거나 가져온 개체의 형식으로 구성됩니다. 계약 이름과 계약 형식이 둘 다 일치해야만 내보내기가 특정 가져오기를 수행하는 것으로 간주됩니다.  
  
 계약 매개 변수의 어느 하나 또는 둘 다는 암시적이거나 명시적일 수 있습니다. 다음 코드는 기본 가져오기를 선언하는 클래스를 보여 줍니다.  
  
```vb  
Public Class MyClass1  
    <Import()>  
    Public Property MyAddin As IMyAddin  
End Class  
```  
  
```csharp  
public class MyClass  
{  
    [Import]  
    public IMyAddin MyAddin { get; set; }  
}  
```  
  
 이 가져오기에서 `Import` 특성에는 연결된 계약 형식과 계약 이름 매개 변수가 둘 다 없습니다. 따라서 계약 형식과 계약 이름 매개 변수는 둘 다 데코레이팅된 속성에서 유추됩니다. 이 경우 계약 형식은 `IMyAddin`이 되고, 계약 이름은 계약 형식에서 만들어진 고유한 문자열이 됩니다. (즉, 계약 이름은 이름도 `IMyAddin`형식에서 유추된 내보내기와만 일치합니다.)  
  
 다음은 이전 가져오기와 일치하는 내보내기를 보여 줍니다.  
  
```vb  
<Export(GetType(IMyAddin))>  
Public Class MyLogger  
    Implements IMyAddin  
  
End Class  
```  
  
```csharp  
[Export(typeof(IMyAddin))]  
public class MyLogger : IMyAddin { }  
```  
  
 이 내보내기에서 계약 형식은 `IMyAddin` 특성의 매개 변수로 지정되었기 때문에 `Export` 입니다. 내보낸 형식은 계약 형식과 동일하고 계약 형식에서 파생되거나, 인터페이스인 경우 계약 형식을 구현해야 합니다. 이 내보내기에서 실제 형식 `MyLogger` 는 인터페이스 `IMyAddin`을 구현합니다. 계약 이름은 계약 형식에서 유추됩니다. 즉, 이 내보내기는 이전 가져오기와 일치합니다.  
  
> [!NOTE]
>  내보내기 및 가져오기는 일반적으로 public 클래스 또는 멤버에 대해 선언되어야 합니다. 다른 선언도 지원되지만 private, protected 또는 내부 멤버를 내보내거나 가져오면 파트에 대한 격리 모델이 손상되므로 권장되지 않습니다.  
  
 일치로 간주되기 위해서는 계약 형식이 내보내기 및 가져오기에 대해 정확히 일치해야 합니다. 다음 내보내기를 살펴보세요.  
  
```vb  
<Export()> 'WILL NOT match the previous import!  
Public Class MyLogger  
    Implements IMyAddin  
  
End Class  
```  
  
```csharp  
[Export] //WILL NOT match the previous import!  
public class MyLogger : IMyAddin { }  
```  
  
 이 내보내기에서 계약 형식은 `MyLogger` 이 아니라 `IMyAddin`입니다. `MyLogger` 가 `IMyAddin`을 구현하므로 `IMyAddin` 개체로 캐스팅될 수 있다고 하더라도 이 내보내기는 계약 형식이 동일하지 않기 때문에 이전 가져오기와 일치하지 않습니다.  
  
 일반적으로 계약 이름을 지정할 필요가 없으며, 대부분의 계약은 계약 형식 및 메타데이터 측면에서 정의되어야 합니다. 그러나 특정 상황에서는 계약 이름을 직접 지정해야 합니다. 가장 일반적인 경우는 클래스가 공용 형식(예: 기본 형식)을 공유하는 여러 값을 내보내는 경우입니다. 계약 이름은 `Import` 또는 `Export` 특성의 첫 번째 매개 변수로 지정할 수 있습니다. 다음 코드는 계약 이름이 `MajorRevision`으로 지정된 가져오기 및 내보내기를 보여 줍니다.  
  
```vb  
Public Class MyExportClass  
  
    'This one will match  
    <Export("MajorRevision")>  
    Public ReadOnly Property MajorRevision As Integer  
        Get  
            Return 4  
        End Get  
    End Property  
  
    <Export("MinorRevision")>  
    Public ReadOnly Property MinorRevision As Integer  
        Get  
            Return 16  
        End Get  
    End Property  
End Class  
```  
  
```csharp  
public class MyClass  
{  
    [Import("MajorRevision")]  
    public int MajorRevision { get; set; }  
}  
  
public class MyExportClass  
{   
    [Export("MajorRevision")] //This one will match.  
    public int MajorRevision = 4;  
  
    [Export("MinorRevision")]  
    public int MinorRevision = 16;  
}  
```  
  
 계약 형식이 지정되지 않은 경우 가져오기 또는 내보내기 형식에서 계속 유추됩니다. 그러나 계약 이름이 명시적으로 지정된 경우에도 일치로 간주되기 위해서는 계약 형식도 가져오기 및 내보내기에 대해 정확히 일치해야 합니다. 예를 들어, `MajorRevision` 필드가 문자열인 경우 유추된 계약 형식이 일치하지 않으며 계약 이름이 동일하더라도 내보내기가 가져오기와 일치하지 않습니다.  
  
### <a name="importing-and-exporting-a-method"></a>메서드 가져오기 및 내보내기  
 `Export` 특성도 클래스, 속성 또는 함수와 동일한 방법으로 메서드를 데코레이팅할 수 있습니다. 메서드 내보내기는 형식이 유추될 수 없으르모 계약 형식 또는 계약 이름을 지정해야 합니다. 지정된 형식은 사용자 지정 대리자 또는 제네릭 형식(예: `Func`)일 수 있습니다. 다음 클래스는 `DoSomething`이라는 메서드를 내보냅니다.  
  
```vb  
Public Class MyAddin  
  
    'Explicitly specifying a generic type  
    <Export(GetType(Func(Of Integer, String)))>  
    Public Function DoSomething(ByVal TheParam As Integer) As String  
        Return Nothing 'Function body goes here  
    End Function  
  
End Class  
```  
  
```csharp  
public class MyAddin  
{  
    //Explicitly specifying a generic type.  
    [Export(typeof(Func<int, string>))]  
    public string DoSomething(int TheParam);  
}  
```  
  
 이 클래스에서 `DoSomething` 메서드는 `int` 매개 변수를 하나 사용하고 `string`을 반환합니다. 이 내보내기를 일치시키려면 파트 가져오기에서 적절한 멤버를 선언해야 합니다. 다음 클래스는 `DoSomething` 메서드를 가져옵니다.  
  
```vb  
Public Class MyClass1  
  
    'Contract name must match!  
    <Import()>  
    Public Property MajorRevision As Func(Of Integer, String)  
End Class  
```  
  
```csharp  
public class MyClass  
{  
    [Import] //Contract name must match!  
    public Func<int, string> DoSomething { get; set; }  
}  
```  
  
 `Func<T, T>` 개체를 사용하는 방법에 대한 자세한 내용은 <xref:System.Func%602>를 참조하세요.  
  
<a name="types_of_imports"></a>   
## <a name="types-of-imports"></a>가져오기 형식  
 MEF는 동적 가져오기, 지연 가져오기, 필수 가져오기 및 선택적 가져오기를 비롯한 여러 가져오기 형식을 지원합니다.  
  
### <a name="dynamic-imports"></a>동적 가져오기  
 일부 경우 가져오기 클래스는 특정 계약 이름을 가진 모든 형식의 내보내기와 일치할 수 있습니다. 이 시나리오에서 클래스는 *동적 가져오기*를 선언할 수 있습니다. 다음 가져오기는 계약 이름이 "TheString"인 모든 내보내기와 일치합니다.  
  
```vb  
Public Class MyClass1  
  
    <Import("TheString")>  
    Public Property MyAddin  
  
End Class  
```  
  
```csharp  
public class MyClass  
{  
    [Import("TheString")]  
    public dynamic MyAddin { get; set; }  
}  
```  
  
 계약 형식이 `dynamic` 키워드에서 유추되는 경우 모든 계약 형식과 일치합니다. 이 경우 가져오기는 **항상** 일치시킬 계약 이름을 지정해야 합니다. (계약 이름이 지정되지 않은 경우 가져오기는 아무 내보내기와도 일치하지 않는 것으로 간주됩니다.) 다음 두 내보내기는 모두 이전 가져오기와 일치합니다.  
  
```vb  
<Export("TheString", GetType(IMyAddin))>  
Public Class MyLogger  
    Implements IMyAddin  
  
End Class  
  
<Export("TheString")>  
Public Class MyToolbar  
  
End Class  
```  
  
```csharp  
[Export("TheString", typeof(IMyAddin))]  
public class MyLogger : IMyAddin { }  
  
[Export("TheString")]  
public class MyToolbar { }  
```  
  
 물론, 가져오기 클래스는 임의 형식의 개체를 처리하도록 준비되어야 합니다.  
  
### <a name="lazy-imports"></a>지연 가져오기  
 일부 경우 가져오기 클래스는 개체가 즉시 인스턴스화되지 않도록 가져온 개체에 대한 간접 참조를 필요로 할 수 있습니다. 이 시나리오에서 클래스는 *계약 형식을 사용하여* 지연 가져오기 `Lazy<T>`를 선언할 수 있습니다. 다음 가져오기 속성은 지연 가져오기를 선언합니다.  
  
```vb  
Public Class MyClass1  
  
    <Import()>  
    Public Property MyAddin As Lazy(Of IMyAddin)  
  
End Class  
```  
  
```csharp  
public class MyClass  
{  
    [Import]  
    public Lazy<IMyAddin> MyAddin { get; set; }  
}  
```  
  
 컴퍼지션 엔진의 관점에서 `Lazy<T>` 계약 형식은 `T`계약 형식과 같다고 간주됩니다. 따라서 이전 가져오기는 다음 내보내기와 일치합니다.  
  
```vb  
<Export(GetType(IMyAddin))>  
Public Class MyLogger  
    Implements IMyAddin  
  
End Class  
```  
  
```csharp  
[Export(typeof(IMyAddin))]  
public class MyLogger : IMyAddin { }  
```  
  
 앞의 "기본 가져오기 및 내보내기" 섹션에서 설명한 것처럼, 지연 가져오기를 위해 계약 이름과 계약 형식을 `Import` 특성에 지정할 수 있습니다.  
  
### <a name="prerequisite-imports"></a>필수 가져오기  
 내보낸 MEF 파트는 일반적으로 일치하는 가져오기를 채우기 위한 필요성이나 직접 요청에 대한 응답으로 컴퍼지션 엔진에 의해 만들어집니다. 기본적으로 파트를 만들 때 컴퍼지션 엔진은 매개 변수가 없는 생성자를 사용합니다. 엔진이 다른 생성자를 사용하도록 하려면 해당 생성자에 `ImportingConstructor` 특성을 표시하면 됩니다.  
  
 각 파트에는 컴퍼지션 엔진에서 사용될 생성자가 하나만 포함될 수 있습니다. 기본 생성자를 제공하지 않고 `ImportingConstructor` 특성을 제공하지 않거나, 둘 이상의 `ImportingConstructor` 특성을 제공하면 오류가 발생합니다.  
  
 `ImportingConstructor` 특성이 표시된 생성자의 매개 변수를 채우기 위해 모든 해당 매개 변수가 자동으로 가져오기로 선언됩니다. 이 방법은 파트 초기화 중에 사용되는 가져오기를 선언하는 편리한 방법입니다. 다음 클래스에서는 `ImportingConstructor` 를 사용하여 가져오기를 선언합니다.  
  
```vb  
Public Class MyClass1  
  
    Private _theAddin As IMyAddin  
  
    'Default constructor will NOT be used  
    'because the ImportingConstructor  
    'attribute is present.  
    Public Sub New()  
  
    End Sub  
  
    'This constructor will be used.  
    'An import with contract type IMyAddin  
    'is declared automatically.  
    <ImportingConstructor()>  
    Public Sub New(ByVal MyAddin As IMyAddin)  
        _theAddin = MyAddin  
    End Sub  
  
End Class  
```  
  
```csharp  
public class MyClass   
{  
    private IMyAddin _theAddin;  
  
    //Default constructor will NOT be  
    //used because the ImportingConstructor  
    //attribute is present.  
    public MyClass() { }  
  
    //This constructor will be used.  
    //An import with contract type IMyAddin is   
    //declared automatically.  
    [ImportingConstructor]   
    public MyClass(IMyAddin MyAddin)   
    {  
        _theAddin = MyAddin;  
    }  
}  
```  
  
 기본적으로 `ImportingConstructor` 특성은 모든 매개 변수 가져오기에 유추된 계약 형식 및 계약 이름을 사용합니다. `Import` 특성으로 매개 변수를 데코레이팅하여 이를 재정의할 수 있습니다. 그러면 계약 형식 및 계약 이름을 명시적으로 정의할 수 있습니다. 다음 코드는 이 구문을 사용하여 부모 클래스 대신 파생 클래스를 가져오는 생성자를 보여 줍니다.  
  
```vb  
<ImportingConstructor()>  
Public Sub New(<Import(GetType(IMySubAddin))> ByVal MyAddin As IMyAddin)  
  
End Sub  
```  
  
```csharp  
[ImportingConstructor]   
public MyClass([Import(typeof(IMySubAddin))]IMyAddin MyAddin)   
{  
    _theAddin = MyAddin;  
}  
```  
  
 특히, 컬렉션 매개 변수에 주의해야 합니다. 예를 들어, `ImportingConstructor` 형식의 매개 변수로 생성자에 `IEnumerable<int>`를 지정하는 경우 가져오기는 `IEnumerable<int>`형식의 내보내기 집합 대신 `int`형식의 단일 내보내기와 일치합니다. `int`형식의 내보내기 집합을 일치시키려면 `ImportMany` 특성으로 매개 변수를 데코레이팅해야 합니다.  
  
 `ImportingConstructor` 특성에 의해 가져오기로 선언된 매개 변수는 *필수 가져오기*로도 표시됩니다. MEF는 일반적으로 내보내기 및 가져오기가 *사이클*을 형성하는 것을 허용합니다. 예를 들어, 사이클에서는 개체 A가 개체 B를 가져온 다음 개체 A를 가져옵니다. 일반적인 상황에서는 사이클이 문제가 되지 않으며 컴퍼지션 컨테이너가 두 개체를 모두 정상적으로 생성합니다.  
  
 가져온 값이 파트의 생성자에 필요한 경우 해당 개체는 사이클에 참여할 수 없습니다. 개체 A가 개체 B가 스스로 생성될 수 있기 전에 생성되기를 요구하고 개체 B가 개체 A를 가져오면 사이클이 해결될 수 없어 컴퍼지션 오류가 발생합니다. 따라서 생성자 매개 변수에 대해 선언된 가져오기는 필수 가져오기이며, 해당 매개 변수를 필요로 하는 개체의 모든 내보내기를 사용할 수 있기 전에 모두 채워져야 합니다.  
  
### <a name="optional-imports"></a>선택적 가져오기  
 `Import` 특성은 파트가 작동하기 위한 요구 사항을 지정합니다. 가져오기를 수행할 수 없는 경우 해당 파트의 컴퍼지션이 실패하고 파트를 사용할 수 없습니다.  
  
 *속성을 사용하여 가져오기가* 선택적 `AllowDefault` 이 되도록 지정할 수 있습니다. 이 경우 가져오기가 사용 가능한 모든 내보내기와 일치하지 않더라도 컴퍼지션이 성공하며, 가져오기 속성이 해당 속성 형식의 기본값(개체 속성의 경우 `null`, 부울의 경우 `false` 또는 숫자 속성의 경우 0)으로 설정됩니다. 다음 클래스에서는 선택적 가져오기를 사용합니다.  
  
```vb  
Public Class MyClass1  
  
    <Import(AllowDefault:=True)>  
    Public Property thePlugin As Plugin  
  
    'If no matching export is available,  
    'thePlugin will be set to null.  
End Class  
```  
  
```csharp  
public class MyClass  
{  
    [Import(AllowDefault = true)]  
    public Plugin thePlugin { get; set; }  
  
    //If no matching export is avaliable,  
    //thePlugin will be set to null.  
}  
```  
  
### <a name="importing-multiple-objects"></a>여러 개체 가져오기  
 `Import` 특성은 하나의 내보내기와 일치하는 경우에만 성공적으로 구성됩니다. 다른 경우에는 컴퍼지션 오류가 발생합니다. 동일한 계약과 일치하는 둘 이상의 내보내기를 가져오려면 `ImportMany` 특성을 사용합니다. 이 특성이 표시된 가져오기는 항상 선택적입니다. 예를 들어, 일치하는 내보내기가 없는 경우 컴퍼지션이 실패하지 않습니다. 다음 클래스는 `IMyAddin`형식의 임의 개수의 내보내기를 가져옵니다.  
  
```vb  
Public Class MyClass1  
  
    <ImportMany()>  
    Public Property MyAddin As IEnumerable(Of IMyAddin)  
  
End Class  
```  
  
```csharp  
public class MyClass  
{  
    [ImportMany]  
    public IEnumerable<IMyAddin> MyAddin { get; set; }  
}  
```  
  
 일반 `IEnumerable<T>` 구문 및 메서드를 사용하여, 가져온 배열에 액세스할 수 있습니다. 대신 일반 배열(`IMyAddin[]`)을 사용할 수도 있습니다.  
  
 이 패턴은 `Lazy<T>` 구문과 함께 사용할 때 매우 중요할 수 있습니다. 예를 들어, `ImportMany`, `IEnumerable<T>`및 `Lazy<T>`를 사용하여 임의 개수의 개체에 대한 간접 참조를 가져오고 필요해진 개체만 인스턴스화할 수 있습니다. 다음 클래스는 이 패턴을 보여 줍니다.  
  
```vb  
Public Class MyClass1  
  
    <ImportMany()>  
    Public Property MyAddin As IEnumerable(Of Lazy(Of IMyAddin))  
  
End Class  
```  
  
```csharp  
public class MyClass  
{  
    [ImportMany]  
    public IEnumerable<Lazy<IMyAddin>> MyAddin { get; set; }  
}  
```  
  
<a name="avoiding_discovery"></a>   
## <a name="avoiding-discovery"></a>검색 방지  
 일부 경우 파트가 카탈로그의 일부로 검색되지 않도록 하려 할 수 있습니다. 예를 들어, 파트가 사용하기 위한 용도가 아니라 상속되도록 할 기본 클래스일 수 있습니다. 여기에는 두 가지 방법이 있습니다. 첫째, 파트 클래스에 `abstract` 키워드를 사용할 수 있습니다. 추상 클래스는 추상 클래스에서 파생된 클래스에 상속된 내보내기를 제공할 수 있더라도 절대로 내보내기를 제공하지 않습니다.  
  
 클래스를 추상화할 수 없는 경우 클래스를 `PartNotDiscoverable` 특성으로 데코레이팅할 수 있습니다. 이 특성으로 데코레이팅된 파트는 모든 카탈로그에 포함되지 않습니다. 다음 예제에서는 이러한 패턴을 보여 줍니다. `DataOne` 은 카탈로그에 의해 검색됩니다. `DataTwo` 는 추상이므로 검색되지 않습니다. `DataThree` 는 `PartNotDiscoverable` 특성을 사용했으므로 검색되지 않습니다.  
  
```vb  
<Export()>  
Public Class DataOne  
    'This part will be discovered   
    'as normal by the catalog.  
End Class  
  
<Export()>  
Public MustInherit Class DataTwo  
    'This part will not be discovered  
    'by the catalog.  
End Class  
  
<PartNotDiscoverable()>  
<Export()>  
Public Class DataThree  
    'This part will also not be discovered  
    'by the catalog.  
End Class  
```  
  
```csharp  
[Export]  
public class DataOne  
{  
    //This part will be discovered  
    //as normal by the catalog.  
}  
  
[Export]  
public abstract class DataTwo  
{  
    //This part will not be discovered  
    //by the catalog.  
}  
  
[PartNotDiscoverable]  
[Export]  
public class DataThree  
{  
    //This part will also not be discovered  
    //by the catalog.  
}  
```  
  
<a name="metadata_and_metadata_views"></a>   
## <a name="metadata-and-metadata-views"></a>메타데이터 및 메타데이터 보기  
 내보내기는 자신에 대한 *메타데이터*라는 추가 정보를 제공할 수 있습니다. 메타데이터는 가져오기 파트에 내보낸 개체의 속성을 전달하는 데 사용될 수 있습니다. 가져오기 파트에서는 이 데이터를 사용하여 사용할 내보내기를 확인하거나, 내보내기를 구성할 필요 없이 내보내기에 대한 정보를 수집할 수 있습니다. 따라서 메타데이터를 사용하려면 가져오기가 지연이어야 합니다.  
  
 일반적으로 메타데이터를 사용하기 위해서는 사용할 수 있는 메타데이터를 선언하는 *메타데이터 보기*라는 인터페이스를 선언합니다. 메타데이터 보기 인터페이스는 속성만 포함해야 하고, 해당 속성은 `get` 접근자를 포함해야 합니다. 다음 인터페이스는 메타데이터 보기의 예입니다.  
  
```vb  
Public Interface IPluginMetadata  
  
    ReadOnly Property Name As String  
  
    <DefaultValue(1)>  
    ReadOnly Property Version As Integer  
  
End Interface  
```  
  
```csharp  
public interface IPluginMetadata  
{  
    string Name { get; }  
  
    [DefaultValue(1)]    
    int Version { get; }  
}  
```  
  
 또한 제네릭 컬렉션 `IDictionary<string, object>`를 메타데이터 보기로 사용할 수 있지만, 이는 형식 검사의 이점을 없애므로 피해야 합니다.  
  
 일반적으로 메타데이터 보기에 명명된 모든 속성은 필수이고 이러한 속성을 제공하지 않는 모든 내보내기는 일치로 간주되지 않습니다. `DefaultValue` 특성은 속성이 선택 사항임을 지정합니다. 속성이 포함되어 있지 않으면 속성에 `DefaultValue`의 매개 변수로 지정된 기본값이 할당됩니다. 다음은 메타데이터로 데코레이팅된 서로 다른 두 클래스입니다. 이러한 클래스는 둘 다 이전 메타데이터 보기와 일치합니다.  
  
```vb  
<Export(GetType(IPlugin))>  
<ExportMetadata("Name", "Logger")>  
<ExportMetadata("Version", 4)>  
Public Class MyLogger  
    Implements IPlugin  
  
End Class  
  
'Version is not required because of the DefaultValue  
<Export(GetType(IPlugin))>  
<ExportMetadata("Name", "Disk Writer")>  
Public Class DWriter  
    Implements IPlugin  
  
End Class  
```  
  
```csharp  
[Export(typeof(IPlugin)),  
    ExportMetadata("Name", "Logger"),  
    ExportMetadata("Version", 4)]  
public class Logger : IPlugin  
{  
}  
  
[Export(typeof(IPlugin)),  
    ExportMetadata("Name", "Disk Writer")]   
    //Version is not required because of the DefaultValue  
public class DWriter : IPlugin  
{  
}  
```  
  
 메타데이터는 `Export` 특성 뒤에 `ExportMetadata` 특성을 사용하여 표현되어 있습니다. 메타데이터의 각 조각은 이름/값 쌍으로 구성되어 있습니다. 메타데이터의 이름 부분은 메타데이터 보기에서 해당 속성의 이름과 일치해야 하며, 값은 해당 속성에 할당됩니다.  
  
 사용할 메타데이터 보기(있는 경우)를 지정하는 것은 가져오기입니다. 메타데이터가 포함된 가져오기는 지연 가져오기로 선언되고, 메타데이터 인터페이스는 `Lazy<T,T>`에 대한 두 번째 형식 매개 변수로 포함됩니다. 다음 클래스는 메타데이터가 포함된 이전 파트를 가져옵니다.  
  
```vb  
Public Class Addin  
  
    <Import()>  
    Public Property plugin As Lazy(Of IPlugin, IPluginMetadata)  
End Class  
```  
  
```csharp  
public class Addin  
{  
    [Import]  
    public Lazy<IPlugin, IPluginMetadata> plugin;  
}  
```  
  
 많은 경우에 사용 가능한 가져오기를 통해 구문 분석하고 하나의 가져오기만 선택 및 인스턴스화하거나 특정 조건에 맞도록 컬렉션을 필터링하기 위해 메타데이터를 `ImportMany` 특성과 결합하려고 할 것입니다. 다음 클래스는 `IPlugin` 값 "Logger"가 포함된 `Name` 개체만 인스턴스화합니다.  
  
```vb  
Public Class User  
  
    <ImportMany()>  
    Public Property plugins As IEnumerable(Of Lazy(Of IPlugin, IPluginMetadata))  
  
    Public Function InstantiateLogger() As IPlugin  
  
        Dim logger As IPlugin  
        logger = Nothing  
  
        For Each Plugin As Lazy(Of IPlugin, IPluginMetadata) In plugins  
            If (Plugin.Metadata.Name = "Logger") Then  
                logger = Plugin.Value  
            End If  
        Next  
        Return logger  
    End Function  
  
End Class  
```  
  
```csharp  
public class User  
{  
    [ImportMany]  
    public IEnumerable<Lazy<IPlugin, IPluginMetadata>> plugins;  
  
    public IPlugin InstantiateLogger ()  
    {  
        IPlugin logger = null;  
  
        foreach (Lazy<IPlugin, IPluginMetadata> plugin in plugins)  
        {  
            if (plugin.Metadata.Name = "Logger") logger = plugin.Value;  
        }  
        return logger;  
    }  
}  
```  
  
<a name="import_and_export_inheritance"></a>   
## <a name="import-and-export-inheritance"></a>가져오기 및 내보내기 상속  
 클래스가 파트에서 상속되면 해당 클래스도 파트가 될 수 있습니다. 가져오기는 항상 서브클래스에서 상속됩니다. 따라서 파트의 서브클래스는 항상 부모 클래스와 동일한 가져오기가 포함된 파트가 됩니다.  
  
 `Export` 특성을 사용하여 선언된 내보내기는 서브클래스에서 상속되지 않습니다. 그러나 파트는 `InheritedExport` 특성을 사용하여 자신을 내보낼 수 있습니다. 파트의 서브클래스는 계약 이름 및 계약 형식을 포함하여 동일한 내보내기를 상속하고 제공합니다. `Export` 특성과 달리, `InheritedExport` 는 클래스 수준에만 적용될 수 있으며 멤버 수준에는 적용될 수 없습니다. 따라서 멤버 수준 내보내기는 상속될 수 없습니다.  
  
 다음 4개의 클래스는 가져오기 및 내보내기 상속의 원칙을 보여 줍니다. `NumTwo` 는 `NumOne`에서 상속되므로 `NumTwo` 는 `IMyData`를 가져옵니다. 일반 내보내기는 상속되지 않으므로 `NumTwo` 는 아무것도 내보내지 않습니다. `NumFour` 는 `NumThree`에서 상속됩니다. `NumThree` 는 `InheritedExport`를 사용했으므로 `NumFour` 에는 계약 형식이 `NumThree`인 내보내기가 하나 포함됩니다. 멤버 수준 내보내기는 절대 상속되지 않으므로 `IMyData` 는 내보내지지 않습니다.  
  
```vb  
<Export()>  
Public Class NumOne  
    <Import()>  
    Public Property MyData As IMyData  
End Class  
  
Public Class NumTwo  
    Inherits NumOne  
  
    'Imports are always inherited, so NumTwo will  
    'Import IMyData  
  
    'Ordinary exports are not inherited, so  
    'NumTwo will NOT export anything.  As a result it  
    'will not be discovered by the catalog!  
  
End Class  
  
<InheritedExport()>  
Public Class NumThree  
  
    <Export()>  
    Public Property MyData As IMyData  
  
    'This part provides two exports, one of  
    'contract type NumThree, and one of   
    'contract type IMyData.  
  
End Class  
  
Public Class NumFour  
    Inherits NumThree  
  
    'Because NumThree used InheritedExport,  
    'this part has one export with contract   
    'type NumThree.  
  
    'Member-level exports are never inherited,  
    'so IMyData is not exported.  
  
End Class  
```  
  
```csharp  
[Export]  
public class NumOne  
{  
    [Import]  
    public IMyData MyData { get; set; }  
}  
  
public class NumTwo : NumOne  
{  
    //Imports are always inherited, so NumTwo will   
    //import IMyData.  
  
    //Ordinary exports are not inherited, so   
    //NumTwo will NOT export anything. As a result it   
    //will not be discovered by the catalog!  
}  
  
[InheritedExport]  
public class NumThree  
{  
    [Export]  
    Public IMyData MyData { get; set; }  
  
    //This part provides two exports, one of  
    //contract type NumThree, and one of  
    //contract type IMyData.  
}  
  
public class NumFour : NumThree  
{  
    //Because NumThree used InheritedExport,  
    //this part has one export with contract  
    //type NumThree.  
  
    //Member-level exports are never inherited,  
    //so IMyData is not exported.  
}  
```  
  
 `InheritedExport` 특성이 연결된 메타데이터가 있는 경우 해당 메타데이터도 상속됩니다. (자세한 내용은 앞의 "메타데이터 및 메타데이터 보기" 섹션을 참조하세요.) 상속된 메타데이터는 서브클래스에 의해 수정될 수 없습니다. 그러나 동일한 계약 이름 및 계약 형식을 사용하되 새 메타데이터를 포함하여 `InheritedExport` 특성을 다시 선언함으로써 서브클래스는 상속된 메타데이터를 새 메타데이터로 바꿀 수 있습니다. 다음 클래스에서는 이 원칙을 보여 줍니다. `MegaLogger` 파트는 `Logger` 에서 상속되고 `InheritedExport` 특성을 포함합니다. `MegaLogger` 는 Status라는 새 메타데이터를 다시 선언하므로 `Logger`에서 Name 및 Version을 상속하지 않습니다.  
  
```vb  
<InheritedExport(GetType(IPlugin))>  
<ExportMetadata("Name", "Logger")>  
<ExportMetadata("Version", 4)>  
Public Class Logger  
    Implements IPlugin  
  
    'Exports with contract type IPlugin  
    'and metadata "Name" and "Version".  
End Class  
  
Public Class SuperLogger  
    Inherits Logger  
  
    'Exports with contract type IPlugin and   
    'metadata "Name" and "Version", exactly the same  
    'as the Logger class.  
  
End Class  
  
<InheritedExport(GetType(IPlugin))>  
<ExportMetadata("Status", "Green")>  
Public Class MegaLogger  
    Inherits Logger  
  
    'Exports with contract type IPlugin and   
    'metadata "Status" only. Re-declaring   
    'the attribute replaces all metadata.  
  
End Class  
```  
  
```csharp  
[InheritedExport(typeof(IPlugin)),  
    ExportMetadata("Name", "Logger"),  
    ExportMetadata("Version", 4)]  
public class Logger : IPlugin  
{  
    //Exports with contract type IPlugin and   
    //metadata "Name" and "Version".  
}  
  
public class SuperLogger : Logger  
{  
    //Exports with contract type IPlugin and   
    //metadata "Name" and "Version", exactly the same  
    //as the Logger class.  
}  
  
[InheritedExport(typeof(IPlugin)),  
    ExportMetadata("Status", "Green")]  
public class MegaLogger : Logger        {  
    //Exports with contract type IPlugin and   
    //metadata "Status" only. Re-declaring   
    //the attribute replaces all metadata.  
}  
```  
  
 메타데이터를 재정의하기 위해 `InheritedExport` 특성을 다시 선언할 때 계약 형식이 동일한지 확인합니다. (앞의 예제에서 `IPlugin`이 계약 형식입니다.) 계약 형식이 다를 경우 재정의하는 대신 두 번째 특성이 파트에서 두 번째 독립 내보내기를 만듭니다. 일반적으로 이는 앞의 예제에 표시된 것처럼 `InheritedExport` 특성을 재정의할 때 계약 형식을 명시적으로 지정해야 함을 의미합니다.  
  
 인터페이스는 직접 인스턴스화될 수 없으므로 일반적으로 `Export` 또는 `Import` 특성으로 데코레이팅될 수 없습니다. 그러나 인터페이스는 인터페이스 수준에서 `InheritedExport` 특성으로 데코레이팅될 수 있고, 연결된 모든 메타데이터와 함께 해당 내보내기는 모든 구현 클래스에서 상속됩니다. 그러나 인터페이스 자체는 파트로 사용할 수 없습니다.  
  
<a name="custom_export_attributes"></a>   
## <a name="custom-export-attributes"></a>사용자 지정 내보내기 특성  
 기본 내보내기 특성 `Export` 및 `InheritedExport`는 메타데이터를 특성 속성으로 포함하도록 확장될 수 있습니다. 이 기법은 유사한 메타데이터를 많은 파트에 적용하거나 메타데이터 특성의 상속 트리를 만들 때 유용합니다.  
  
 사용자 지정 특성은 계약 형식, 계약 이름 또는 다른 모든 메타데이터를 지정할 수 있습니다. 사용자 지정 특성을 정의하려면 `ExportAttribute` (또는 `InheritedExportAttribute`)에서 상속되는 클래스를 `MetadataAttribute` 특성으로 데코레이팅해야 합니다. 다음 클래스에서는 사용자 지정 특성을 정의합니다.  
  
```vb  
<MetadataAttribute()>  
<AttributeUsage(AttributeTargets.Class, AllowMultiple:=false)>  
Public Class MyAttribute  
    Inherits ExportAttribute  
  
    Public Property MyMetadata As String  
  
    Public Sub New(ByVal myMetadata As String)  
        MyBase.New(GetType(IMyAddin))  
  
        myMetadata = myMetadata  
    End Sub  
  
End Class  
```  
  
```csharp  
[MetadataAttribute]  
[AttributeUsage(AttributeTargets.Class, AllowMultiple=false)]  
public class MyAttribute : ExportAttribute  
{  
    public MyAttribute(string myMetadata)   
        : base(typeof(IMyAddin))  
    {  
        MyMetadata = myMetadata;  
    }  
  
    public string MyMetadata { get; private set; }  
}  
```  
  
 이 클래스는 계약 형식이 `MyAttribute` 이고 `IMyData` 라는 메타데이터가 포함된 `MyMetadata`라는 사용자 지정 특성을 정의합니다. 클래스의 `MetadataAttribute` 특성이 표시된 모든 속성은 사용자 지정 특성에 정의된 메타데이터로 간주됩니다. 다음 두 선언은 동일합니다.  
  
```vb  
<Export(GetType(IMyAddin))>  
<ExportMetadata("MyMetadata", "theData")>  
Public Property myAddin As MyAddin  
  
<MyAttribute("theData")>  
Public Property myAddin As MyAddin  
```  
  
```csharp  
[Export(typeof(IMyAddin)),   
    ExportMetadata("MyMetadata", "theData")]  
public MyAddin myAddin { get; set; }  
```  
  
```  
[MyAttribute("theData")]  
public MyAddin myAddin { get; set; }  
```  
  
 첫 번째 선언에서 계약 형식 및 메타데이터는 명시적으로 정의되어 있습니다. 두 번째 선언에서 계약 형식 및 메타데이터는 사용자 지정 특성에서 암시적입니다. 특히 많은 양의 동일한 메타데이터를 많은 파트에 적용해야 하는 경우(예: 만든 이 또는 저작권 정보) 사용자 지정 특성을 사용하면 많은 시간을 절약하고 중복을 많이 줄일 수 있습니다. 또한 사용자 지정 특성의 상속 트리를 만들어 변형을 허용할 수 있습니다.  
  
 사용자 지정 특성에 선택적 메타데이터를 만들려면 `DefaultValue` 특성을 사용하면 됩니다. 이 특성이 사용자 지정 특성 클래스의 속성에 적용되면 데코레이팅된 속성이 선택적이며 내보내기에서 제공할 필요가 없도록 지정됩니다. 속성의 값이 제공되지 않으면 속성에 해당 속성 형식의 기본값이 할당됩니다(일반적으로 `null`, `false`또는 0).  
  
<a name="creation_policies"></a>   
## <a name="creation-policies"></a>만들기 정책  
 파트가 가져오기를 지정하고 컴퍼지션이 수행되면 컴퍼지션 컨테이너가 일치하는 내보내기를 찾으려고 합니다. 컴퍼지션 컨테이너가 가져오기를 내보내기와 성공적으로 일치시키면 가져오기 멤버가 내보낸 개체의 인스턴스로 설정됩니다. 이 인스턴스를 가져오는 위치는 내보내기 파트의 *만들기 정책*에 의해 제어됩니다.  
  
 가능한 두 가지 만들기 정책은 *공유* 및 *비공유*입니다. 만들기 정책이 공유인 파트는 컨테이너에서 해당 계약이 포함된 파트에 대해 모든 가져오기 간에 공유됩니다. 컴퍼지션 엔진이 일치 항목을 찾았고 가져오기 속성을 설정해야 하는 경우 컴퍼지션 엔진은 아직 파트가 없는 경우에만 파트의 새 복사본을 인스턴스화하고 그렇지 않으면 기존 복사본을 제공합니다. 즉, 많은 개체가 동일한 파트에 대한 참조를 포함할 수 있습니다. 이러한 파트는 많은 위치에서 변경될 수 있는 내부 상태를 사용해서는 안 됩니다. 이 정책은 정적 파트, 서비스를 제공하는 파트, 많은 메모리 또는 다른 리소스를 사용하는 파트에 적합합니다.  
  
 만들기 정책이 비공유인 파트는 해당 내보내기 중 하나와 일치하는 가져오기 발견될 때마다 만들어집니다. 따라서 새 복사본은 파트의 내보낸 계약 중 하나와 일치하는 컨테이너의 모든 가져오기에 대해 인스턴스화됩니다. 이러한 복사본의 내부 상태는 공유되지 않습니다. 이 정책은 각 가져오기에 고유한 내부 상태가 필요한 경우에 적합합니다.  
  
 가져오기와 내보내기는 둘 다 파트의 만들기 정책을 `Shared`, `NonShared`또는 `Any`값 중에서 지정할 수 있습니다. 가져오기와 내보내기 둘 다 기본값은 `Any` 입니다. `Shared` 또는 `NonShared` 를 지정하는 내보내기는 동일한 값을 지정하거나 `Any`를 지정하는 가져오기와만 일치합니다. 마찬가지로, `Shared` 또는 `NonShared` 를 지정하는 가져오기는 동일한 값을 지정하거나 `Any`를 지정하는 내보내기와만 일치합니다. 계약 이름 또는 계약 형식이 일치하지 않는 가져오기 및 내보내기와 동일한 방식으로, 만들기 정책이 호환되지 않는 가져오기와 내보내기는 일치로 간주되지 않습니다. 가져오기와 내보내기가 둘 다 `Any`를 지정하거나, 만들기 정책을 지정하지 않고 기본값인 `Any`로 설정되면 만들기 정책이 기본값인 공유로 설정됩니다.  
  
 다음 예제에서는 만들기 정책을 지정하는 가져오기와 내보내기를 둘 다 보여 줍니다. `PartOne` 은 만들기 정책을 지정하지 않으므로 기본값은 `Any`입니다. `PartTwo` 은 만들기 정책을 지정하지 않으므로 기본값은 `Any`입니다. 가져오기와 내보내기 둘 다 기본값인 `Any`로 설정되므로 `PartOne` 은 공유됩니다. `PartThree` 는 `Shared` 만들기 정책을 지정하므로 `PartTwo` 와 `PartThree` 는 `PartOne`의 동일한 복사본을 공유합니다. `PartFour` 는 `NonShared` 만들기 정책을 지정하므로 `PartFour` 는 `PartFive`에서 공유되지 않습니다. `PartSix` 는 `NonShared` 만들기 정책을 지정합니다. `PartFive` 와 `PartSix` 는 각각 별도의 `PartFour`복사본을 받습니다. `PartSeven` 는 `Shared` 만들기 정책을 지정합니다. 만들기 정책이 `PartFour` 인 내보낸 `Shared`가 없으므로 `PartSeven` 가져오기는 아무것과도 일치하지 않으며 채워지지 않습니다.  
  
```vb  
<Export()>  
Public Class PartOne  
    'The default creation policy for an export is Any.  
End Class  
  
Public Class PartTwo  
  
    <Import()>  
    Public Property partOne As PartOne  
  
    'The default creation policy for an import is Any.  
    'If both policies are Any, the part will be shared.  
  
End Class  
  
Public Class PartThree  
  
    <Import(RequiredCreationPolicy:=CreationPolicy.Shared)>  
    Public Property partOne As PartOne  
  
    'The Shared creation policy is explicitly specified.  
    'PartTwo and PartThree will receive references to the  
    'SAME copy of PartOne.  
  
End Class  
  
<Export()>  
<PartCreationPolicy(CreationPolicy.NonShared)>  
Public Class PartFour  
    'The NonShared creation policy is explicitly specified.  
End Class  
  
Public Class PartFive  
  
    <Import()>  
    Public Property partFour As PartFour  
  
    'The default creation policy for an import is Any.  
    'Since the export's creation policy was explictly  
    'defined, the creation policy for this property will  
    'be non-shared.  
  
End Class  
  
Public Class PartSix  
  
    <Import(RequiredCreationPolicy:=CreationPolicy.NonShared)>  
    Public Property partFour As PartFour  
  
    'Both import and export specify matching creation   
    'policies.  PartFive and PartSix will each receive   
    'SEPARATE copies of PartFour, each with its own  
    'internal state.  
  
End Class  
  
Public Class PartSeven  
  
    <Import(RequiredCreationPolicy:=CreationPolicy.Shared)>  
    Public Property partFour As PartFour  
  
    'A creation policy mismatch.  Because there is no   
    'exported PartFour with a creation policy of Shared,  
    'this import does not match anything and will not be  
    'filled.  
  
End Class  
```  
  
```csharp  
[Export]  
public class PartOne  
{  
    //The default creation policy for an export is Any.  
}  
  
public class PartTwo  
{  
    [Import]  
    public PartOne partOne { get; set; }  
  
    //The default creation policy for an import is Any.  
    //If both policies are Any, the part will be shared.  
}  
  
public class PartThree  
{  
    [Import(RequiredCreationPolicy = CreationPolicy.Shared)]  
    public PartOne partOne { get; set; }  
  
    //The Shared creation policy is explicitly specified.  
    //PartTwo and PartThree will receive references to the  
    //SAME copy of PartOne.  
}  
  
[Export]  
[PartCreationPolicy(CreationPolicy.NonShared)]  
public class PartFour  
{  
    //The NonShared creation policy is explicitly specified.  
}  
  
public class PartFive  
{  
    [Import]  
    public PartFour partFour { get; set; }  
  
    //The default creation policy for an import is Any.  
    //Since the export's creation policy was explictly  
    //defined, the creation policy for this property will  
    //be non-shared.  
}  
  
public class PartSix  
{  
    [Import(RequiredCreationPolicy = CreationPolicy.NonShared)]  
    public PartFour partFour { get; set; }  
  
    //Both import and export specify matching creation   
    //policies.  PartFive and PartSix will each receive   
    //SEPARATE copies of PartFour, each with its own  
    //internal state.  
}  
  
public class PartSeven  
{  
    [Import(RequiredCreationPolicy = CreationPolicy.Shared)]  
    public PartFour partFour { get; set; }  
  
    //A creation policy mismatch.  Because there is no   
    //exported PartFour with a creation policy of Shared,  
    //this import does not match anything and will not be  
    //filled.  
}  
```  
  
<a name="life_cycle_and_disposing"></a>   
## <a name="life-cycle-and-disposing"></a>수명 주기 및 삭제  
 파트는 컴퍼지션 컨테이너에 호스트되므로 해당 수명 주기는 일반 개체보다 복잡할 수 있습니다. 파트는 중요한 두 수명 주기 관련 인터페이스 `IDisposable` 및 `IPartImportsSatisfiedNotification`을 구현할 수 있습니다.  
  
 종료 시 작업이 수행되도록 요구하는 파트나 리소스를 해제해야 하는 파트는 일반적인 .NET Framework 개체의 경우처럼 `IDisposable`을 구현해야 합니다. 그러나 컨테이너는 파트에 대한 참조를 만들고 유지 관리하므로 파트를 소유한 컨테이너만 파트에 대해 `Dispose` 메서드를 호출해야 합니다. 컨테이너 자체는 `IDisposable`을 구현하고, `Dispose` 에서 해당 정리 부분으로 소유한 모든 파트에 대해 `Dispose` 를 호출합니다. 따라서 항상 컴퍼지션 컨테이너와 컴퍼지션 컨테이너가 소유한 모든 파트가 더 이상 필요하지 않으면 해당 컴퍼지션 컨테이너를 삭제해야 합니다.  
  
 수명이 긴 컴퍼지션 컨테이너의 경우, 만들기 정책이 비공유인 파트의 메모리 소비량이 문제가 될 수 있습니다. 이러한 비공유 파트는 여러 번 만들어질 수 있으며 컨테이너 자체가 삭제될 때까지 삭제되지 않습니다. 이 문제를 해결하기 위해 컨테이너는 `ReleaseExport` 메서드를 제공합니다. 비공유 내보내기에 대해 이 메서드를 호출하면 컴퍼지션 컨테이너에서 해당 내보내기가 제거되고 삭제됩니다. 제거된 내보내기에서만 사용된 파트와 트리에서 해당 파트 아래의 모든 항목도 제거되고 삭제됩니다. 컴퍼지션 컨테이너 자체를 삭제하지 않고도 이러한 방식으로 리소스를 회수할 수 있습니다.  
  
 `IPartImportsSatisfiedNotification` 은 `OnImportsSatisfied`라는 메서드 하나를 포함합니다. 이 메서드는 컴퍼지션이 완료되고 파트의 가져오기가 사용할 준비가 되면 인터페이스를 구현하는 모든 파트에서 컴퍼지션 컨테이너에 의해 호출됩니다. 다른 파트의 가져오기를 채우기 위해 컴퍼지션 엔진에 의해 파트가 만들어집니다. 파트의 가져오기가 설정되기 전에는 파트 생성자의 가져온 값이 `ImportingConstructor` 특성을 사용하여 필수 구성 요소로 지정되지 않은 한 해당 값을 사용하거나 조작하는 모든 초기화를 수행할 수 없습니다. 이 방법은 일반적으로 선호되는 방법이지만 일부 경우 생성자 삽입을 사용하지 못할 수도 있습니다. 이러한 경우 `OnImportsSatisfied`에서 초기화를 수행할 수 있으며 파트가 `IPartImportsSatisfiedNotification`을 구현해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Channel 9 동영상: Managed Extensibility Framework로 응용 프로그램 열기](https://channel9.msdn.com/events/TechEd/NorthAmerica/2009/DTL328)  
 [Channel 9 동영상: MEF(Managed Extensibility Framework) 2.0](https://channel9.msdn.com/posts/NET-45-Oleg-Lvovitch-and-Kevin-Ransom-Managed-Extensibility-Framework-MEF-20)
