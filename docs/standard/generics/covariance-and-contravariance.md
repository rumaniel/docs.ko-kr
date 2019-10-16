---
title: 제네릭의 공 분산과 반공 분산
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- generics, covariance and contravariance
- generics, variance
- covariance and contravariance in generics
- generic type parameters
ms.assetid: 2678dc63-c7f9-4590-9ddc-0a4df684d42e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 08e6458f0a14b78c6d05f706afa710931d60094a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69948794"
---
# <a name="covariance-and-contravariance-in-generics"></a>제네릭의 공 분산과 반공 분산
<a name="top"></a> 공변성(Covariance)과 반공변성(Contravariance)은 원래 지정된 것보다 더 많이 파생되거나(더 구체적인) 더 적게 파생된 형식(덜 구체적인)을 사용할 수 있는 능력을 지칭하는 용어입니다. 제네릭 형식 매개 변수는 더욱 유연하게 제네릭 형식을 할당하고 사용할 수 있도록 공변성과 반공변성을 지원합니다. 형식 시스템을 참조할 때 공변성, 반공변성 및 불변성의 정의는 다음과 같습니다. 이 예제에서는 `Base` 라는 기본 클래스와 `Derived`라는 파생 클래스가 있는 것으로 가정합니다.  
  
- `Covariance`  
  
     원래 지정된 것보다 더 많이 파생된 형식을 사용할 수 있습니다.  
  
     `IEnumerable<Derived>`의 인스턴스(Visual Basic의 `IEnumerable(Of Derived)`)를 `IEnumerable<Base>` 형식의 변수에 할당할 수 있습니다.  
  
- `Contravariance`  
  
     원래 지정된 것보다 더 제네릭한(덜 파생적인) 형식을 사용할 수 있습니다.  
  
     `Action<Base>` 의 인스턴스(Visual Basic의`Action(Of Base)` )를 `Action<Derived>`형식의 변수에 할당할 수 있습니다.  
  
- `Invariance`  
  
     원래 지정된 형식만 사용할 수 있다는 의미이므로, 불변하는 제네릭 형식 매개 변수는 공변성도, 반공변성도 아닙니다.  
  
     `List<Base>`의 인스턴스(Visual Basic의 `List(Of Base)`)를 `List<Derived>` 형식의 변수에 할당할 수 없고, 그 반대로도 할당할 수 없습니다.  
  
 다음 코드에 표시된 것처럼, 공변 형식 매개 변수를 사용하여 일반적인 [다형성](../../csharp/programming-guide/classes-and-structs/polymorphism.md)과 매우 비슷한 할당을 수행할 수 있습니다.  
  
 [!code-csharp[CoContraSimpleIEnum#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontrasimpleienum/cs/example.cs#1)]
 [!code-vb[CoContraSimpleIEnum#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontrasimpleienum/vb/example.vb#1)]  
  
 <xref:System.Collections.Generic.List%601> 클래스는 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스를 구현하므로 `List<Derived>` (Visual Basic의 경우`List(Of Derived)` )는 `IEnumerable<Derived>`를 구현합니다. 나머지 작업은 공변 형식 매개 변수가 처리합니다.  
  
 그러나 반공변성은 직관적으로 이해하기가 어려울 수 있습니다. 다음 예제에서는 `Action<Base>` (Visual Basic의 경우`Action(Of Base)` ) 형식의 대리자를 만든 다음 이 대리자를 `Action<Derived>`형식의 변수에 할당합니다.  
  
 [!code-csharp[CoContraSimpleAction#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontrasimpleaction/cs/example.cs#1)]
 [!code-vb[CoContraSimpleAction#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontrasimpleaction/vb/example.vb#1)]  
  
 이는 순서가 뒤바뀐 것처럼 보이지만 실제로는 형식이 안전한 코드로서 문제 없이 컴파일 및 실행됩니다. 람다 식이 할당된 대리자와 일치하므로 `Base` 형식의 매개 변수 하나를 취하고 반환 값이 없는 메서드를 정의할 수 있습니다. 결과로 얻은 대리자를 `Action<Derived>` 형식의 변수에 할당할 수 있습니다. `T` 대리자의 형식 매개 변수 <xref:System.Action%601> 가 반공변성을 지니기 때문입니다. `T` 에서 매개 변수 형식을 지정하므로 이는 형식이 안전한 코드입니다. `Action<Base>` 형식의 대리자를 `Action<Derived>`형식의 대리자인 것처럼 호출하는 경우 해당 인수가 `Derived`형식이어야 합니다. 메서드의 매개 변수가 `Base`형식이므로 이 인수를 내부 메서드에 항상 안전하게 전달할 수 있습니다.  
  
 일반적으로 공변 형식 매개 변수는 대리자의 반환 형식으로 사용할 수 있으며, 반공변 형식 매개 변수는 매개 변수 형식으로 사용할 수 있습니다. 인터페이스의 경우 공변 형식 매개 변수는 인터페이스 메서드의 반환 형식으로 사용할 수 있으며, 반공변 형식 매개 변수는 인터페이스 메서드의 매개 변수 형식으로 사용할 수 있습니다.  
  
 공변성(Covariance) 및 반공변성(Contravariance)을 전체적으로 *차이*라고 합니다. 공변 또는 반공변 여부가 표시되지 않은 제네릭 형식 매개 변수를 *고정(invariant)* 매개 변수라고 합니다. 다음은 공용 언어 런타임의 가변성에 대한 간략한 설명입니다.  
  
- .NET Framework 4에서는 variant 형식 매개 변수가 제네릭 인터페이스와 제네릭 대리자 형식에만 사용됩니다.  
  
- 제네릭 인터페이스 또는 제네릭 대리자 형식은 공변 및 반공변 형식 매개 변수를 둘 다 가질 수 있습니다.  
  
- 가변성은 참조 형식에만 적용되므로 variant 형식 매개 변수에 대한 값 형식을 지정하면 이 형식 매개 변수는 결과로 생성되는 형식에 대해 invariant가 됩니다.  
  
- 대리자 결합에는 가변성이 적용되지 않습니다. 즉, 두 대리자의 형식이 `Action<Derived>` 및 `Action<Base>` (Visual Basic의 경우`Action(Of Derived)` 및 `Action(Of Base)` )라고 할 때 결과의 형식이 안전하더라도 둘째 대리자를 첫째 대리자와 결합할 수 없습니다. 가변성을 통해 둘째 대리자를 `Action<Derived>`형식의 변수에 할당할 수 있지만, 대리자를 결합하기 위해서는 해당 형식이 정확하게 일치해야 합니다.  
  
 다음 하위 단원에서는 공변 및 반공변 형식 매개 변수에 대해 자세히 설명합니다.  
  
- [공변 형식 매개 변수가 있는 제네릭 인터페이스](#InterfaceCovariantTypeParameters)  
  
- [반공변 제네릭 형식 매개 변수가 있는 제네릭 인터페이스](#InterfaceCovariantTypeParameters)  
  
- [variant 형식 매개 변수가 있는 제네릭 대리자](#DelegateVariantTypeParameters)  
  
- [variant 제네릭 인터페이스 및 대리자 정의](#DefiningVariantTypeParameters)  
  
- [variant 제네릭 인터페이스 및 대리자 형식의 목록](#VariantList)  
  
<a name="InterfaceCovariantTypeParameters"></a>   
## <a name="generic-interfaces-with-covariant-type-parameters"></a>공변 형식 매개 변수가 있는 제네릭 인터페이스  
 .NET Framework 4부터는 여러 제네릭 인터페이스에 공변 형식 매개 변수가 있습니다(예: <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.Generic.IEnumerator%601>, <xref:System.Linq.IQueryable%601>및 <xref:System.Linq.IGrouping%602>). 이러한 인터페이스의 모든 형식 매개 변수는 공변성이므로, 형식 매개 변수는 멤버의 반환 형식에만 사용됩니다.  
  
 다음 예제에서는 공변 형식 매개 변수를 사용하는 방법을 보여 줍니다. 이 예제에서는 두 가지 형식을 정의합니다. 그중 하나인 `Base` 에는 `PrintBases` (Visual Basic의 경우 `IEnumerable<Base>` )를 취하고 요소를 출력하는`IEnumerable(Of Base)` 라는 정적 메서드가 있습니다. `Derived` 는 `Base`에서 상속됩니다. 이 예제에서는 빈 `List<Derived>` (Visual Basic의 경우`List(Of Derived)` )를 만든 다음 이 형식을 캐스팅하지 않은 채 `PrintBases` 에 전달하고 `IEnumerable<Base>` 형식의 변수에 할당하는 방법을 보여 줍니다. <xref:System.Collections.Generic.List%601> 은 단일 공변 형식 매개 변수가 있는 <xref:System.Collections.Generic.IEnumerable%601>을 구현합니다. `IEnumerable<Derived>` 의 인스턴스를 `IEnumerable<Base>`대신 사용할 수 있는 것은 공변 형식 매개 변수 때문입니다.  
  
 [!code-csharp[CoContravarianceInClrGenericI#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravarianceinclrgenerici/cs/example.cs#1)]
 [!code-vb[CoContravarianceInClrGenericI#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravarianceinclrgenerici/vb/example.vb#1)]  
  
 [맨 위로 이동](#top)  
  
<a name="InterfaceContravariantTypeParameters"></a>   
## <a name="generic-interfaces-with-contravariant-generic-type-parameters"></a>반공변 제네릭 형식 매개 변수가 있는 제네릭 인터페이스  
 .NET Framework 4부터는 여러 제네릭 인터페이스에 반공변 형식 매개 변수가 있습니다(예: <xref:System.Collections.Generic.IComparer%601>, <xref:System.IComparable%601> 및 <xref:System.Collections.Generic.IEqualityComparer%601>). 이러한 인터페이스에는 반공변 형식 매개 변수만 있으므로 형식 매개 변수가 인터페이스 멤버의 매개 변수 형식으로만 사용됩니다.  
  
 다음 예제에서는 반공변 형식 매개 변수를 사용하는 방법을 보여 줍니다. 이 예제에서는`MustInherit` 속성을 사용하여 추상(Visual Basic의 경우 `Shape` ) `Area` 클래스를 정의합니다. 이 예제에서는 또한 `ShapeAreaComparer` (Visual Basic의 경우 `IComparer<Shape>` )를 구현하는`IComparer(Of Shape)` 클래스를 정의합니다. <xref:System.Collections.Generic.IComparer%601.Compare%2A?displayProperty=nameWithType> 메서드 구현은 `Area` 속성의 값을 기반으로 하므로 `ShapeAreaComparer` 를 사용하여 `Shape` 개체를 영역별로 정렬할 수 있습니다.  
  
 `Circle` 클래스는 `Shape` 를 상속하고 `Area`를 재정의합니다. 이 예제에서는 <xref:System.Collections.Generic.SortedSet%601> (Visual Basic의 경우 `Circle` )을 받아 들이는 생성자를 사용하여 `IComparer<Circle>` 개체의`IComparer(Of Circle)` 을 만듭니다. 하지만 이 예제에서는 `IComparer<Circle>`을 전달하는 대신 `ShapeAreaComparer` 를 구현하는 `IComparer<Shape>`개체를 전달합니다. 이 예제에서는`Shape`제네릭 인터페이스의 형식 매개 변수가 반공변 형식이기 때문에 코드에서 더 많이 파생된 형식(`Circle`)의 비교자를 호출하더라도 더 적게 파생된 형식( <xref:System.Collections.Generic.IComparer%601> )의 비교자를 전달할 수 있습니다.  
  
 새 `Circle` 개체를 `SortedSet<Circle>`에 추가하면 기존 요소에 대해 새 요소를 비교할 때마다 `IComparer<Shape>.Compare` 개체의`IComparer(Of Shape).Compare` 메서드(Visual Basic의 경우 `ShapeAreaComparer` 메서드)가 호출됩니다. 메서드의 매개 변수 형식(`Shape`)은 전달되는 형식(`Circle`)보다 더 적게 파생되었으므로 호출에서 형식 안전성을 유지합니다. 반공변성은 `ShapeAreaComparer` 가 `Shape`에서 파생되는 혼합된 형식 컬렉션뿐만 아니라 모든 단일 형식의 컬렉션을 정렬할 수 있게 해줍니다.  
  
 [!code-csharp[CoContravarianceInClrGenericI2#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravarianceinclrgenerici2/cs/example.cs#1)]
 [!code-vb[CoContravarianceInClrGenericI2#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravarianceinclrgenerici2/vb/example.vb#1)]  
  
 [맨 위로 이동](#top)  
  
<a name="DelegateVariantTypeParameters"></a>   
## <a name="generic-delegates-with-variant-type-parameters"></a>variant 형식 매개 변수가 있는 제네릭 대리자  
 .NET Framework 4에서는 <xref:System.Func%602> 같은 `Func` 제네릭 대리자가 공변 반환 형식과 반공변 매개 변수 형식을 사용합니다. `Action` 같은 <xref:System.Action%602>제네릭 대리자는 반공변 매개 변수 형식을 사용합니다. 즉, 더 많이 파생된 매개 변수 형식과 더 적게 파생된 반환 형식( `Func` 제네릭 대리자의 경우)이 있는 변수에 대리자를 할당할 수 있습니다.  
  
> [!NOTE]
> `Func` 제네릭 대리자의 마지막 제네릭 형식 매개 변수는 대리자 시그니처에 반환 값의 형식을 지정합니다. 이 제네릭 형식 매개 변수는 공변(`out` 키워드)인 반면 다른 한 제네릭 형식 매개 변수는 반공변(`in` 키워드)입니다.  
  
 다음 코드에서는 이를 보여 줍니다. 코드의 첫 부분에서는 `Base`라는 클래스, `Derived` 를 상속하는 `Base`라는 클래스 및 `static` 라는`Shared` 메서드(Visual Basic의 경우 `MyMethod`)가 있는 또 다른 클래스를 정의합니다. 이 메서드는 `Base`의 인스턴스를 사용하고 `Derived`의 인스턴스를 반환합니다. 인수가 `Derived`의 인스턴스이면 `MyMethod`에서 이 인스턴스를 반환하고, 인수가 `Base`의 인스턴스이면 `MyMethod`에서 `Derived`의 새 인스턴스를 반환합니다. 이 예제에서는 `Main()` 내에서 `Func<Base, Derived>`를 나타내고 이를 `Func(Of Base, Derived)` 변수에 저장하는 `MyMethod`(Visual Basic의 경우 `f1`)의 인스턴스를 만듭니다.  
  
 [!code-csharp[CoContravarianceDelegates#2](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#2)]
 [!code-vb[CoContravarianceDelegates#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#2)]  
  
 코드의 둘째 부분에서는 반환 형식이 공변적이기 때문에 `Func<Base, Base>` (Visual Basic의 경우`Func(Of Base, Base)` ) 형식의 변수에 대리자를 할당할 수 있음을 보여 줍니다.  
  
 [!code-csharp[CoContravarianceDelegates#3](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#3)]
 [!code-vb[CoContravarianceDelegates#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#3)]  
  
 코드의 셋째 부분에서는 매개 변수 형식이 반공변적이기 때문에 `Func<Derived, Derived>` (Visual Basic의 경우`Func(Of Derived, Derived)` ) 형식의 변수에 대리자를 할당할 수 있음을 보여 줍니다.  
  
 [!code-csharp[CoContravarianceDelegates#4](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#4)]
 [!code-vb[CoContravarianceDelegates#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#4)]  
  
 코드의 마지막 부분에서는 반공변 매개 변수 형식과 공변 반환 형식의 효과를 결합하여 `Func<Derived, Base>` (Visual Basic의 경우`Func(Of Derived, Base)` ) 형식의 변수에 대리자를 할당할 수 있음을 보여 줍니다.  
  
 [!code-csharp[CoContravarianceDelegates#5](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#5)]
 [!code-vb[CoContravarianceDelegates#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#5)]  
  
### <a name="variance-in-generic-and-non-generic-delegates"></a>제네릭 및 제네릭이 아닌 대리자의 가변성  
 위의 코드에서 `MyMethod` 의 시그니처는 생성된 제네릭 대리자 `Func<Base, Derived>` (Visual Basic의 경우`Func(Of Base, Derived)` )의 시그니처와 정확하게 일치합니다. 이 예제에서는 모든 대리자 형식이 제네릭 대리자 형식 <xref:System.Func%602>에서 생성되는 한 더 많이 파생된 매개 변수 형식과 더 적게 파생된 반환 형식이 있는 메서드 매개 변수 또는 변수에 이 제네릭 대리자를 저장할 수 있음을 보여 줍니다.  
  
 다음은 중요한 내용입니다. 제네릭 대리자의 형식 매개 변수가 지니는 공변성 및 반공변성의 효과는 일반적인 대리자 바인딩이 지니는 공변성 및 반의 효과와 비슷합니다. 자세한 내용은 [대리자의 가변성(C#)](../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md) 및 [대리자의 가변성(Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)을 참조하세요. 그러나 대리자 바인딩의 가변성은 variant 형식 매개 변수가 있는 제네릭 대리자 형식뿐 아니라 모든 대리자 형식에서 작동합니다. 또한 대리자 바인딩이 가변성을 지니면 더 제한적인 매개 변수 형식과 덜 제한적인 반환 형식이 있는 임의의 대리자에 메서드를 바인딩할 수 있는 반면, 제네릭 대리자의 할당은 두 대리자 형식이 모두 동일한 제네릭 형식 정의에서 생성되는 경우에만 작동합니다.  
  
 다음 예제에서는 대리자 바인딩의 가변성과 제네릭 형식 매개 변수의 가변성이 결합된 효과를 보여 줍니다. 이 예제에서는 가장 적게 파생된 형식(`Type1`)부터 가장 많이 파생된 형식(`Type3`)까지 세 개의 형식을 포함하는 형식 계층을 정의합니다. 일반적인 대리자 바인딩의 가변성은 `Type1` 의 매개 변수 형식과 `Type3` 의 반환 형식이 있는 제네릭 대리자에 `Type2` 의 매개 변수 형식과 `Type2`의 반환 형식이 있는 메서드를 바인딩하는 데 사용됩니다. 결과로 생성된 제네릭 대리자는 제네릭 형식 매개 변수의 공 분산과 반공 분산을 사용하여 제네릭 대리자의 매개 변수 형식과 반환 형식이 각각 `Type3` 과 `Type1`인 다른 변수에 할당됩니다. 이 두 번째 할당을 수행하려면 변수 형식과 대리자 형식이 둘 다 같은 제네릭 형식 정의(이 예제의 경우 <xref:System.Func%602>)에서 생성된 것이어야 합니다.  
  
 [!code-csharp[CoContravarianceDelegatesGenRelaxed#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegatesgenrelaxed/cs/example.cs#1)]
 [!code-vb[CoContravarianceDelegatesGenRelaxed#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegatesgenrelaxed/vb/example.vb#1)]  
  
 [맨 위로 이동](#top)  
  
<a name="DefiningVariantTypeParameters"></a>   
## <a name="defining-variant-generic-interfaces-and-delegates"></a>variant 제네릭 인터페이스 및 대리자 정의  
 .NET Framework 4부터는 Visual Basic과 C#에서 인터페이스와 대리자의 제네릭 형식 매개 변수를 공변 또는 반공변으로 표시하는 데 사용할 수 있는 키워드를 제공합니다.  
  
> [!NOTE]
> .NET Framework 버전 2.0부터는 공용 언어 런타임에서 제네릭 형식 매개 변수에 대한 가변성 주석을 지원합니다. .NET Framework 4 이전에서는 이러한 주석이 있는 제네릭 클래스를 정의하는 유일한 방법이 MSIL(Microsoft Intermediate Language)을 사용하여 [Ilasm.exe (IL 어셈블러)](../../../docs/framework/tools/ilasm-exe-il-assembler.md)로 클래스를 컴파일하거나 동적 어셈블리에 클래스를 내보내는 것입니다.  
  
 공변 형식 매개 변수는 `out` 키워드(Visual Basic의 경우`Out` 키워드, `+` MSIL 어셈블러 [의 경우](../../../docs/framework/tools/ilasm-exe-il-assembler.md))로 표시됩니다. 공변 형식 매개 변수는 인터페이스에 속하는 메서드의 반환 값이나 대리자의 반환 형식으로 사용할 수 있지만 인터페이스 메서드에 대한 제네릭 형식 제약 조건으로는 사용할 수 없습니다.  
  
> [!NOTE]
> 인터페이스의 메서드에 제네릭 대리자 형식인 매개 변수가 있으면 인터페이스 형식의 공변 형식 매개 변수를 사용하여 대리자 형식의 반공변 형식 매개 변수를 지정할 수 있습니다.  
  
 반공변 형식 매개 변수는 `in` 키워드(Visual Basic의 경우`In` 키워드, `-` MSIL 어셈블러 [의 경우](../../../docs/framework/tools/ilasm-exe-il-assembler.md))로 표시됩니다. 반공변 형식 매개 변수는 인터페이스에 속하는 메서드의 매개 변수 형식이나 대리자의 매개 변수 형식으로 사용할 수 있으며 인터페이스 메서드의 제네릭 형식 제약 조건으로도 사용할 수 있습니다.  
  
 variant 형식 매개 변수를 사용할 수 있는 것은 인터페이스 형식과 대리자 형식뿐입니다. 인터페이스 형식이나 대리자 형식은 공변 및 반공변 형식 매개 변수를 둘 다 가질 수 있습니다.  
  
 Visual Basic과 C#에서는 공변 및 반공변 형식 매개 변수의 사용 규칙을 위반하거나 인터페이스와 대리자가 아닌 다른 형식의 형식 매개 변수에 공 분산 및 반공 분산 주석을 추가할 수 없습니다. [MSIL 어셈블러](../../../docs/framework/tools/ilasm-exe-il-assembler.md) 에서는 이러한 검사를 수행하지 않지만 규칙을 위반하는 형식을 로드하려고 하면 <xref:System.TypeLoadException> 이 throw됩니다.  
  
 자세한 내용과 예제 코드는 [제네릭 인터페이스의 가변성(C#)](../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md) 및 [제네릭 인터페이스의 가변성(Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)을 참조하세요.  
  
 [맨 위로 이동](#top)  
  
<a name="VariantList"></a>   
## <a name="list-of-variant-generic-interface-and-delegate-types"></a>variant 제네릭 인터페이스 및 대리자 형식의 목록  
 .NET Framework 4에서는 다음 인터페이스 및 대리자 형식에서 공변 및/또는 반공변 형식 매개 변수를 사용합니다.  
  
|형식|공변 형식 매개 변수|반공변 형식 매개 변수|  
|----------|-------------------------------|-----------------------------------|  
|<xref:System.Action%601> - <xref:System.Action%6016>||예|  
|<xref:System.Comparison%601>||예|  
|<xref:System.Converter%602>|예|예|  
|<xref:System.Func%601>|예||  
|<xref:System.Func%602> - <xref:System.Func%6017>|예|예|  
|<xref:System.IComparable%601>||예|  
|<xref:System.Predicate%601>||예|  
|<xref:System.Collections.Generic.IComparer%601>||예|  
|<xref:System.Collections.Generic.IEnumerable%601>|예||  
|<xref:System.Collections.Generic.IEnumerator%601>|예||  
|<xref:System.Collections.Generic.IEqualityComparer%601>||예|  
|<xref:System.Linq.IGrouping%602>|예||  
|<xref:System.Linq.IOrderedEnumerable%601>|예||  
|<xref:System.Linq.IOrderedQueryable%601>|예||  
|<xref:System.Linq.IQueryable%601>|예||  
  
## <a name="see-also"></a>참고 항목

- [공변성(Covariance) 및 반공변성(Contravariance)(C#)](../../csharp/programming-guide/concepts/covariance-contravariance/index.md)
- [공변성(covariance) 및 반공변성(contravariance)(Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/index.md)
- [대리자의 가변성(C#)](../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
- [대리자의 가변성(Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
