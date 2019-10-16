---
title: 디버거 표시 특성을 사용하여 디버깅 향상
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- debugger, display attributes
- DebuggerTypeProxyAttribute attribute
- debugging [.NET Framework], debugger display attributes
- DebuggerDisplayAttribute attribute
- display attributes for debugger
- DebuggerBrowsableAttribute attribute
ms.assetid: 72bb7aa9-459b-42c4-9163-9312fab4c410
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c27732de448e19c4227062706c7a7d73c98e5f19
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966869"
---
# <a name="enhancing-debugging-with-the-debugger-display-attributes"></a>디버거 표시 특성을 사용하여 디버깅 향상

디버거 표시 특성을 통해 해당 형식의 런타임 동작을 지정하고 가장 잘 이해하는 형식의 개발자는 해당 형식이 디버거에 표시될 때 무엇이 표시되는지 지정할 수도 있습니다. 또한 `Target` 속성을 제공하는 디버거 표시 특성의 경우 소스 코드를 모르는 사용자도 어셈블리 수준에서 적용할 수 있습니다. <xref:System.Diagnostics.DebuggerDisplayAttribute> 특성은 형식 또는 멤버가 디버거 변수 창에 표시되는 방식을 제어합니다. <xref:System.Diagnostics.DebuggerBrowsableAttribute> 특성은 필드 또는 속성이 디버거 변수 창에 표시되는지 결정합니다. <xref:System.Diagnostics.DebuggerTypeProxyAttribute> 특성은 형식에 대한 대체 형식 또는 프록시를 지정하고 디버거 창에 표시되는 방식을 변경합니다. 프록시 또는 대체 형식이 있는 변수를 볼 때 프록시는 디버거 표시 창에서 원래 형식에 대 한를 나타냅니다. 디버거 변수 창에는 프록시 형식의 공용 멤버만 표시됩니다. 개인 멤버는 표시되지 않습니다.  
  
## <a name="using-the-debuggerdisplayattribute"></a>DebuggerDisplayAttribute 사용  

<xref:System.Diagnostics.DebuggerDisplayAttribute.%23ctor%2A> 생성자에는 형식 인스턴스에 대한 값 열에 표시되는 문자열인 단일 인수가 있습니다. 이 문자열에는 중괄호({ 및 })가 포함될 수 있습니다. 중괄호 쌍 안의 텍스트는 식으로 확인됩니다. 예를 들어 더하기 기호(+)를 선택하여 `MyHashtable` 인스턴스에 대한 디버거 표시를 확장하면 다음 C# 코드로 인해 “Count = 4”가 표시됩니다.  

```csharp
[DebuggerDisplay("Count = {count}")]
class MyHashtable
{
    public int count = 4;
}
```

식에서 참조되는 속성에 적용된 특성은 처리되지 않습니다. C# 컴파일러의 경우 대상 형식의 현재 인스턴스에 대한 이 참조에만 암시적으로 액세스할 수 있는 일반 식이 허용됩니다. 식은 제한되고 별칭, 로컬 항목 또는 포인터에는 액세스할 수 없습니다. C# 코드에서 중괄호 사이에 대상 형식의 현재 인스턴스에 대한 `this` 포인터에만 암시적으로 액세스할 수 있는 일반 식을 사용할 수 있습니다.

예를 들어 C# 개체에 재정의된 `ToString()`이 있는 경우 디버거는 이 재정의를 호출하여 표준 `{<typeName>}.` 대신 재정의의 결과를 보여 줍니다. 따라서 `ToString()` 메서드를 재정의한 경우 <xref:System.Diagnostics.DebuggerDisplayAttribute>를 사용할 필요가 없습니다. 둘 모두 사용하는 경우에는 <xref:System.Diagnostics.DebuggerDisplayAttribute> 특성이 `ToString()` 재정의보다 우선합니다.

## <a name="using-the-debuggerbrowsableattribute"></a>DebuggerBrowsableAttribute 사용
 필드 또는 속성에 <xref:System.Diagnostics.DebuggerBrowsableAttribute>를 적용하여 필드나 속성이 디버거 창에 표시되는 방식을 지정합니다. 이 특성에 대한 생성자는 다음 상태 중 하나를 지정하는 <xref:System.Diagnostics.DebuggerBrowsableState> 열거형 값 중 하나를 사용합니다.

- <xref:System.Diagnostics.DebuggerBrowsableState.Never>는 멤버가 데이터 창에 표시되지 않음을 나타냅니다.  예를 들어 필드에서 <xref:System.Diagnostics.DebuggerBrowsableAttribute>에 이 값을 사용하면 계층 구조에서 필드가 제거됩니다. 형식 인스턴스에 대한 더하기 기호(+)를 클릭하여 바깥쪽 형식을 확장하면 필드가 표시되지 않습니다.

- <xref:System.Diagnostics.DebuggerBrowsableState.Collapsed>는 멤버가 표시되지만 기본적으로 확장되지 않음을 나타냅니다.  이것은 기본적인 동작입니다.

- <xref:System.Diagnostics.DebuggerBrowsableState.RootHidden>은 멤버 자체가 표시되지 않지만 배열이나 컬렉션인 경우 해당 요소 개체가 표시됨을 나타냅니다.

> [!NOTE]
> <xref:System.Diagnostics.DebuggerBrowsableAttribute>는 .NET Framework 버전 2.0의 Visual Basic에서 지원되지 않습니다.

다음 코드 예제에서는 <xref:System.Diagnostics.DebuggerBrowsableAttribute>를 사용하여 클래스에 대한 디버그 창에서 해당 특성 뒤에 속성이 나타나지 않도록 하는 방법을 보여 줍니다.

```csharp
[DebuggerBrowsable(DebuggerBrowsableState.Never)]
public static string y = "Test String";
```

## <a name="using-the-debuggertypeproxy"></a>DebuggerTypeProxy 사용
 형식의 디버깅 뷰를 완전히 변경하지만 형식 자체는 변경하지 않아야 할 경우 <xref:System.Diagnostics.DebuggerTypeProxyAttribute> 특성을 사용합니다. <xref:System.Diagnostics.DebuggerTypeProxyAttribute> 특성은 개발자가 형식에 맞게 뷰를 조정할 수 있도록 형식에 대한 표시 프록시를 지정하는 데 사용됩니다.  <xref:System.Diagnostics.DebuggerDisplayAttribute>처럼 이 특성은 어셈블리 수준에서 사용될 수 있습니다. 이 경우 <xref:System.Diagnostics.DebuggerTypeProxyAttribute.Target%2A> 속성은 프록시가 사용될 형식을 지정합니다. 이 특성을 사용하여 특성이 적용되는 형식 내에서 발생하는 전용 중첩 형식을 지정하는 것이 좋습니다.  형식 뷰어를 지원하는 식 평가기는 형식이 표시될 때 이 특성을 확인합니다. 특성이 발견된 경우 식 평가기는 특성이 적용되는 형식을 표시 프록시 형식으로 대체합니다.

 <xref:System.Diagnostics.DebuggerTypeProxyAttribute>가 있는 경우 디버거 변수 창에는 프록시 형식의 공용 멤버만 표시됩니다. 개인 멤버는 표시되지 않습니다. 데이터 창의 동작은 특성이 향상된 뷰를 통해 변경되지 않습니다.

 불필요한 성능 저하를 피하기 위해 표시 프록시의 특성은 데이터 창에서 형식 옆의 더하기 기호(+)를 클릭하는 사용자를 통해 또는 <xref:System.Diagnostics.DebuggerBrowsableAttribute> 특성 적용을 통해 개체가 확장될 때까지 처리되지 않습니다. 따라서 표시 형식에는 특성을 적용하지 않는 것이 좋습니다. 특성은 표시 형식 본문 내에서 적용할 수 있고 적용해야 합니다.

 다음 코드 예제에서는 <xref:System.Diagnostics.DebuggerTypeProxyAttribute>를 사용하여 디버거 표시 프록시로 사용할 형식을 지정하는 방법을 보여 줍니다.

```csharp
[DebuggerTypeProxy(typeof(HashtableDebugView))]
class MyHashtable : Hashtable
{
    private const string TestString =
        "This should not appear in the debug window.";

    internal class HashtableDebugView
    {
        private Hashtable hashtable;
        public const string TestStringProxy =
            "This should appear in the debug window.";

        // The constructor for the type proxy class must have a
        // constructor that takes the target type as a parameter.
        public HashtableDebugView(Hashtable hashtable)
        {
            this.hashtable = hashtable;
        }
    }
}
```

## <a name="example"></a>예제

### <a name="description"></a>설명

다음 코드 예제는 Visual Studio에서 볼 수 있으며 <xref:System.Diagnostics.DebuggerDisplayAttribute>, <xref:System.Diagnostics.DebuggerBrowsableAttribute>및 <xref:System.Diagnostics.DebuggerTypeProxyAttribute> 특성을 적용 한 결과를 볼 수 있습니다.

### <a name="code"></a>코드

[!code-cpp[System.Diagnostics.DebuggerBrowsableAttribute#1](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Diagnostics.DebuggerBrowsableAttribute/cpp/program.cpp#1)]
[!code-csharp[System.Diagnostics.DebuggerBrowsableAttribute#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Diagnostics.DebuggerBrowsableAttribute/CS/program.cs#1)]
[!code-vb[System.Diagnostics.DebuggerBrowsableAttribute#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Diagnostics.DebuggerBrowsableAttribute/VB/module1.vb#1)]

## <a name="see-also"></a>참고자료

- <xref:System.Diagnostics.DebuggerDisplayAttribute>
- <xref:System.Diagnostics.DebuggerBrowsableAttribute>
- <xref:System.Diagnostics.DebuggerTypeProxyAttribute>
