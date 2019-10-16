---
title: 사용자 지정 컨트롤에서 메서드 구현
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- user controls [Windows Forms], method implementation
- custom controls [Windows Forms], overloading methods
- custom controls [Windows Forms], method implementation
- methods [Windows Forms]
- methods [Windows Forms], custom controls
ms.assetid: 35d14fca-4bb4-4a27-8211-1f7a98ea27de
ms.openlocfilehash: 867bf97ea13654de6f9c0209c64b9320824f9665
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69931745"
---
# <a name="method-implementation-in-custom-controls"></a>사용자 지정 컨트롤에서 메서드 구현
메서드는 다른 구성 요소에서 구현되는 것과 같은 방식으로 컨트롤에서 구현됩니다.  
  
 Visual Basic에서 값을 반환해야 하는 메서드는 `Public Function`으로 구현됩니다. 값이 반환되지 않는 경우 메서드는 `Public Sub`로 구현됩니다. 메서드는 다음 구문을 사용하여 선언됩니다.  
  
```vb  
Public Function ConvertMatterToEnergy(Matter as Integer) As Integer  
   ' Conversion code goes here.  
End Function  
```  
  
 함수는 값을 반환하므로 정수, 문자열, 개체 등의 반환 형식을 지정해야 합니다. `Function` 또는 `Sub` 프로시저에서 사용하는 인수도 지정해야 합니다.  
  
 C#에서는 Visual Basic에서처럼 함수와 프로시저를 구분하지 않습니다. 메서드는 값이나 `void`를 반환합니다. C# 공용 메서드를 선언하는 구문은 다음과 같습니다.  
  
```csharp  
public int ConvertMatterToEnergy(int matter)  
{  
   // Conversion code goes here.  
}  
```  
  
 메서드를 선언할 때는 가능하면 항상 모든 인수를 명시적 데이터 형식으로 선언합니다. 개체 참조를 사용하는 인수는 `As Widget`가 아닌 `As Object`과 같이 특정 클래스 형식으로 선언해야 합니다. Visual Basic에서 기본 설정인 `Option Strict`는 이 규칙을 자동으로 적용합니다.  
  
 형식이 지정된 인수를 사용하면 런타임이 아닌 컴파일러에서 대부분의 개발자 오류를 찾아낼 수 있습니다. 컴파일러는 항상 오류를 찾아내는 반면 런타임 테스트에서는 테스트 가능한 오류만 찾아낼 수 있습니다.  
  
## <a name="overloaded-methods"></a>오버로드된 메서드  
 컨트롤 사용자가 메서드에 서로 다른 매개 변수 조합을 제공할 수 있도록 하려면 명시적 데이터 형식을 사용하여 메서드의 여러 오버로드를 제공합니다. 모든 데이터 형식을 포함할 수 있는 `As Object`로 선언된 매개 변수는 만들지 않아야 합니다. 이러한 매개 변수를 만들면 오류가 발생해도 테스트에서 확인되지 않을 수 있습니다.  
  
> [!NOTE]
> 공용 언어 런타임의 유니버설 데이터 형식은 `Object`가 아닌 `Variant`입니다. `Variant`는 언어에서 제거되었습니다.  
  
 예를 들어 가상 `Spin` 컨트롤의 `Widget` 메서드에서는 회전 방향과 속도를 직접 지정할 수도 있고 각운동량을 가져올 다른 `Widget` 개체를 지정할 수도 있습니다.  
  
```vb  
Overloads Public Sub Spin( _  
   ByVal SpinDirection As SpinDirectionsEnum, _  
   ByVal RevolutionsPerSecond As Double)  
   ' Implementation code here.  
End Sub  
Overloads Public Sub Spin(ByVal Driver As Widget) _  
   ' Implementation code here.  
End Sub  
```  
  
```csharp  
public void Spin(SpinDirectionsEnum spinDirection, double revolutionsPerSecond)  
{  
   // Implementation code here.  
}  
  
public void Spin(Widget driver)  
{  
   // Implementation code here.  
}  
```  
  
## <a name="see-also"></a>참고자료

- [이벤트](../../../standard/events/index.md)
- [Windows Forms 컨트롤의 속성](properties-in-windows-forms-controls.md)
