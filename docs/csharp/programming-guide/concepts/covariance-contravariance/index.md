---
title: 공변성(Covariance) 및 반공변성(Contravariance)(C#)
ms.date: 07/20/2015
ms.assetid: 066d9a3c-aab7-4ea6-826d-0b1a85399c74
ms.openlocfilehash: 1d5a1de1825e585512f694a0cd72cee9b37cda36
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69595279"
---
# <a name="covariance-and-contravariance-c"></a>공변성(Covariance) 및 반공변성(Contravariance)(C#)
C#에서 공변성(Covariance)과 반공변성(Contravariance)은 배열 형식, 대리자 형식 및 제네릭 형식 인수에 대한 암시적 참조 변환을 가능하게 합니다. 공변성(Covariance)은 할당 호환성을 유지하고 반공변성(Contravariance)은 할당 호환성을 유지하지 않습니다.  
  
 다음 코드에서는 할당 호환성, 공변성(Covariance) 및 반공변성(Contravariance) 간의 차이를 보여 줍니다.  
  
```csharp  
// Assignment compatibility.   
string str = "test";  
// An object of a more derived type is assigned to an object of a less derived type.   
object obj = str;  
  
// Covariance.   
IEnumerable<string> strings = new List<string>();  
// An object that is instantiated with a more derived type argument   
// is assigned to an object instantiated with a less derived type argument.   
// Assignment compatibility is preserved.   
IEnumerable<object> objects = strings;  
  
// Contravariance.             
// Assume that the following method is in the class:   
// static void SetObject(object o) { }   
Action<object> actObject = SetObject;  
// An object that is instantiated with a less derived type argument   
// is assigned to an object instantiated with a more derived type argument.   
// Assignment compatibility is reversed.   
Action<string> actString = actObject;  
```  
  
 배열에 대한 공변성(Covariance)은 더 많이 파생된 형식의 배열을 더 적게 파생된 형식의 배열로 암시적 변환을 가능하게 합니다. 하지만 다음 코드 예제와 같이 이 작업은 형식이 안전하지 않습니다.  
  
```csharp  
object[] array = new String[10];  
// The following statement produces a run-time exception.  
// array[0] = 10;  
```  
  
 메서드 그룹에 대한 공변성(Covariance) 및 반공변성(Contravariance) 지원으로 대리자 형식과 메서드 시그니처를 일치시킬 수 있습니다. 일치하는 시그니처가 있는 메서드뿐만이 아니라 더 많이 파생된 형식(공변성(covariance))을 반환하는 메서드 또는 대리자 형식에 지정된 것보다 더 적게 파생된 형식(반공변성(contravariance))을 가지고 있는 매개 변수를 수락하는 메서드도 대리자에 할당할 수 있습니다. 자세한 내용은 [대리자의 가변성(C#)](./variance-in-delegates.md) 및 [대리자의 가변성 사용(C#)](./using-variance-in-delegates.md)을 참조하세요.  
  
 다음 코드 예제에서는 메서드 그룹에 대한 공변성(Covariance) 및 반공변성(Contravariance) 지원을 보여 줍니다.  
  
```csharp  
static object GetObject() { return null; }  
static void SetObject(object obj) { }  
  
static string GetString() { return ""; }  
static void SetString(string str) { }  
  
static void Test()  
{  
    // Covariance. A delegate specifies a return type as object,  
    // but you can assign a method that returns a string.  
    Func<object> del = GetString;  
  
    // Contravariance. A delegate specifies a parameter type as string,  
    // but you can assign a method that takes an object.  
    Action<string> del2 = SetObject;  
}  
```  
  
 .NET Framework 4 이상에서 C#는 제네릭 인터페이스 및 대리자의 공변성(Covariance) 및 반공변성(Contravariance)을 지원하고 제네릭 형식 매개 변수를 암시적으로 변환할 수 있습니다. 자세한 내용은 [제네릭 인터페이스의 가변성(C#)](./variance-in-generic-interfaces.md) 및 [대리자의 가변성(C#)](./variance-in-delegates.md)을 참조하세요.  
  
 다음 코드 예제에서는 제네릭 인터페이스에 대한 암시적 참조 변환을 보여 줍니다.  
  
```csharp  
IEnumerable<String> strings = new List<String>();  
IEnumerable<Object> objects = strings;  
```  
  
 제네릭 매개 변수가 선언된 공변(covariant) 또는 반공변(contravariant)인 경우 제네릭 인터페이스 또는 대리자를 *variant*라고 합니다. C#에서는 사용자 고유의 variant 인터페이스 및 대리자를 만들 수 있습니다. 자세한 내용은 [Variant 제네릭 인터페이스 만들기(C#)](./creating-variant-generic-interfaces.md) 및 [대리자의 가변성(C#)](./variance-in-delegates.md)을 참조하세요.  
  
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[제네릭 인터페이스의 가변성(C#)](./variance-in-generic-interfaces.md)|제네릭 인터페이스의 공분산 및 반공분산에 대해 설명하고 .NET Framework의 Variant 제네릭 인터페이스의 목록을 제공합니다.|  
|[Variant 제네릭 인터페이스 만들기(C#)](./creating-variant-generic-interfaces.md)|사용자 지정 variant 인터페이스를 만드는 방법을 보여 줍니다.|  
|[제네릭 컬렉션용 인터페이스의 가변성 사용(C#)](./using-variance-in-interfaces-for-generic-collections.md)|<xref:System.Collections.Generic.IEnumerable%601> 및 <xref:System.IComparable%601> 인터페이스의 공변성(Covariance) 및 반공변성(Contravariance) 지원을 통해 코드를 다시 사용하는 방법을 보여 줍니다.|  
|[대리자의 가변성(C#)](./variance-in-delegates.md)|제네릭 및 제네릭이 아닌 대리자의 공변성(Covariance) 및 반공변성(Contravariance)을 설명하고 .NET Framework의 Variant 제네릭 인터페이스의 목록을 제공합니다.|  
|[대리자의 가변성 사용(C#)](./using-variance-in-delegates.md)|제네릭이 아닌 대리자의 공변성(Covariance) 및 반공변성(Contravariance) 지원을 사용하여 메서드 시그니처를 대리자 형식과 일치시키는 방법을 보여 줍니다.|  
|[Func 및 Action 제네릭 대리자에 가변성 사용(C#)](./using-variance-for-func-and-action-generic-delegates.md)|`Func` 및 `Action` 대리자의 공변성(Covariance) 및 반공변성(Contravariance) 지원을 통해 코드를 다시 사용하는 방법을 보여 줍니다.|
