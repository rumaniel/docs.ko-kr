---
title: AttributeUsage (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 48757216-c21d-4051-86d5-8a3e03c39d2c
ms.openlocfilehash: 84c3d175aede5d8066198592ffac601c0bd97620
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71351819"
---
# <a name="attributeusage-visual-basic"></a>AttributeUsage (Visual Basic)
사용자 지정 특성 클래스를 사용하는 방법을 결정합니다. `AttributeUsage`는 새 특성 적용 방법을 제어하기 위해 사용자 지정 특성 정의에 적용할 수 있는 특성입니다. 기본 설정은 명시적으로 적용될 경우 다음과 같이 표시됩니다.  
  
```vb  
<System.AttributeUsage(System.AttributeTargets.All,   
                   AllowMultiple:=False,   
                   Inherited:=True)>   
Class NewAttribute  
    Inherits System.Attribute  
End Class  
```  
  
 이 예제에서 `NewAttribute` 클래스는 모든 특성 가능 코드 엔터티에 적용될 수 있지만 각 엔터티에 한 번만 적용될 수 있습니다. 이 특성은 기본 클래스에 적용될 때 파생 클래스가 상속합니다.  
  
 `AllowMultiple` 및 `Inherited` 인수는 선택 사항이므로 이 코드에 미치는 영향은 같습니다.  
  
```vb  
<System.AttributeUsage(System.AttributeTargets.All)>   
Class NewAttribute  
    Inherits System.Attribute  
End Class  
```  
  
 첫 번째 `AttributeUsage` 인수는 <xref:System.AttributeTargets> 열거형의 요소가 하나 이상이어야 합니다. 다음과 같이 OR 연산자를 사용하여 여러 대상 형식을 함께 연결할 수 있습니다.  
  
```vb  
Imports System  
```  
  
```vb  
<AttributeUsage(AttributeTargets.Property Or AttributeTargets.Field)>   
Class NewPropertyOrFieldAttribute  
    Inherits Attribute  
End Class  
```  
  
 `AllowMultiple` 인수를 `true`로 설정하면 다음과 같이 결과 특성을 단일 엔터티에 두 번 이상 적용할 수 있습니다.  
  
```vb  
Imports System  
```  
  
```vb  
<AttributeUsage(AttributeTargets.Class, AllowMultiple:=True)>   
Class MultiUseAttr  
    Inherits Attribute  
End Class  
  
<MultiUseAttr(), MultiUseAttr()>   
Class Class1  
End Class  
```  
  
 이 경우 `AllowMultiple`이 `true`로 설정되므로 `MultiUseAttr`를 반복적으로 적용할 수 있습니다. 여러 특성을 적용하기 위해 표시된 두 형식이 모두 유효합니다.  
  
 `Inherited`를 `false`로 설정하면 특성이 지정된 클래스에서 파생된 클래스가 특성을 상속하지 않습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
```vb  
Imports System  
```  
  
```vb  
<AttributeUsage(AttributeTargets.Class, Inherited:=False)>   
Class Attr1  
    Inherits Attribute  
End Class  
  
<Attr1()>   
Class BClass  
  
End Class    
  
Class DClass  
    Inherits BClass  
End Class  
```  
  
 이 경우 `Attr1`은 상속을 통해 `DClass`에 적용되지 않습니다.  
  
## <a name="remarks"></a>설명  
 `AttributeUsage` 특성은 단일 사용 특성입니다. 같은 클래스에 두 번 이상 적용될 수 없습니다. `AttributeUsage`는 <xref:System.AttributeUsageAttribute>의 별칭입니다.  
  
 자세한 내용은 [리플렉션을 사용하여 특성 액세스(Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `AttributeUsage` 특성에 대한 `Inherited` 및 `AllowMultiple`의 영향과 클래스에 적용되는 사용자 지정 특성을 열거하는 방법을 보여 줍니다.  
  
```vb  
Imports System  
```  
  
```vb  
' Create some custom attributes:  
<AttributeUsage(System.AttributeTargets.Class, Inherited:=False)>   
Class A1  
    Inherits System.Attribute  
End Class  
  
<AttributeUsage(System.AttributeTargets.Class)>   
Class A2  
    Inherits System.Attribute  
End Class      
  
<AttributeUsage(System.AttributeTargets.Class, AllowMultiple:=True)>   
Class A3  
    Inherits System.Attribute  
End Class  
  
' Apply custom attributes to classes:  
<A1(), A2()>   
Class BaseClass  
  
End Class  
  
<A3(), A3()>   
Class DerivedClass  
    Inherits BaseClass  
End Class  
  
Public Class TestAttributeUsage  
    Sub Main()  
        Dim b As New BaseClass  
        Dim d As New DerivedClass  
        ' Display custom attributes for each class.  
        Console.WriteLine("Attributes on Base Class:")  
        Dim attrs() As Object = b.GetType().GetCustomAttributes(True)  
  
        For Each attr In attrs  
            Console.WriteLine(attr)  
        Next  
  
        Console.WriteLine("Attributes on Derived Class:")  
        attrs = d.GetType().GetCustomAttributes(True)  
        For Each attr In attrs  
            Console.WriteLine(attr)  
        Next              
    End Sub  
End Class  
```  
  
## <a name="sample-output"></a>샘플 출력  
  
```console  
Attributes on Base Class:  
A1  
A2  
Attributes on Derived Class:  
A3  
A3  
A2  
```  
  
## <a name="see-also"></a>참조

- <xref:System.Attribute>
- <xref:System.Reflection>
- [Visual Basic 프로그래밍 가이드](../../../../visual-basic/programming-guide/index.md)
- [특성](../../../../standard/attributes/index.md)
- [리플렉션(Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)
- [특성(Visual Basic)](../../../../visual-basic/language-reference/attributes.md)
- [사용자 지정 특성 만들기(Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/creating-custom-attributes.md)
- [리플렉션을 사용하여 특성 액세스(Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)
