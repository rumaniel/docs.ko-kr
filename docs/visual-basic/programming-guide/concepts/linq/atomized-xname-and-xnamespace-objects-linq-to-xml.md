---
title: 원자화 명령의 xname 및 XNamespace 개체 (LINQ to XML) (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 21ee7585-7df9-40b4-8c76-a12bb5f29bb3
ms.openlocfilehash: ae6d21c21aac4455e7932015c131fb4295673056
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71351835"
---
# <a name="atomized-xname-and-xnamespace-objects-linq-to-xml-visual-basic"></a>원자화 명령의 xname 및 XNamespace 개체 (LINQ to XML) (Visual Basic)

<xref:System.Xml.Linq.XName> 및 <xref:System.Xml.Linq.XNamespace> 개체는 *원자화*됩니다. 즉, 이들 개체의 정규화된 이름이 같으면 같은 개체를 참조합니다. 이를 통해 쿼리 성능이 향상될 수 있습니다. 두 개의 원자화된 이름이 같은지 비교하는 경우 기본 중간 언어에서 이 두 개의 참조가 같은 개체를 가리키는지 여부만 확인하면 됩니다. 기본 코드는 시간이 많이 걸리는 문자열 비교를 수행할 필요가 없습니다.

## <a name="atomization-semantics"></a>원자화 의미 체계

원자화는 두 <xref:System.Xml.Linq.XName> 개체가 같은 로컬 이름을 갖고 있고 동일한 네임스페이스에 있는 경우 동일한 인스턴스를 공유함을 의미합니다. 마찬가지로 두 <xref:System.Xml.Linq.XNamespace> 개체가 같은 네임스페이스 URI를 갖고 있으면 같은 인스턴스를 공유합니다.

클래스가 원자화된 개체를 사용하려면 클래스에 대한 생성자가 public이 아니라 private이어야 합니다. 이는 생성자가 public인 경우 원자화되지 않은 개체를 생성할 수 있기 때문입니다. <xref:System.Xml.Linq.XName> 및 <xref:System.Xml.Linq.XNamespace> 클래스는 문자열을 <xref:System.Xml.Linq.XName> 또는 <xref:System.Xml.Linq.XNamespace>로 변환하는 암시적 변환 연산자를 구현합니다. 이를 통해 이러한 개체의 인스턴스를 가져올 수 있습니다. 생성자는 액세스할 수 없으므로 생성자를 사용하여 인스턴스를 가져올 수 없습니다.

<xref:System.Xml.Linq.XName> 및 <xref:System.Xml.Linq.XNamespace>는 비교하는 두 개체가 같은 인스턴스를 참조하는지 확인하기 위해 같음 연산자 및 같지 않음 연산자도 구현합니다.

## <a name="example"></a>예제

다음 코드에서는 몇 가지 <xref:System.Xml.Linq.XElement> 개체를 만들어 동일한 이름이 같은 인스턴스를 공유함을 보여 줍니다.

```vb
Dim r1 As New XElement("Root", "data1")
Dim r2 As XElement = XElement.Parse("<Root>data2</Root>")

If DirectCast(r1.Name, Object) = DirectCast(r2.Name, Object) Then
    Console.WriteLine("r1 and r2 have names that refer to the same instance.")
Else
    Console.WriteLine("Different")
End If

Dim n As XName = "Root"

If DirectCast(n, Object) = DirectCast(r1.Name, Object) Then
    Console.WriteLine("The name of r1 and the name in 'n' refer to the same instance.")
Else
    Console.WriteLine("Different")
End If
```

이 예제는 다음과 같은 출력을 생성합니다.

```console
r1 and r2 have names that refer to the same instance.
The name of r1 and the name in 'n' refer to the same instance.
```

앞에서 설명했듯이 원자화된 개체의 이점은 <xref:System.Xml.Linq.XName>을 매개 변수로 사용하는 축 메서드를 사용하는 경우 축 메서드에서 두 이름이 원하는 요소를 선택하는 같은 인스턴스를 참조하는지 여부만 확인하면 된다는 것입니다.

다음 예제에서는 <xref:System.Xml.Linq.XName>을 <xref:System.Xml.Linq.XContainer.Descendants%2A> 메서드 호출로 전달합니다. 그러면 원자화 패턴으로 인해 성능이 향상됩니다.

```vb
Dim root As New XElement("Root", New XElement("C1", 1), New XElement("Z1", New XElement("C1", 2), New XElement("C1", 1)))

Dim query = From e In root.Descendants("C1") Where CInt(e) = 1e

For Each z As var In query
    Console.WriteLine(z)
Next
```

이 예제는 다음과 같은 출력을 생성합니다.

```xml
<C1>1</C1>
<C1>1</C1>
```

## <a name="see-also"></a>참조

- [성능 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/performance-linq-to-xml.md)
