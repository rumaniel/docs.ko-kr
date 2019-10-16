---
title: AttributeUsage(C#)
ms.date: 04/25/2018
ms.openlocfilehash: a3a82e33d7259ec56ec3e907bc3d4d9f8a01167d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54589313"
---
# <a name="attributeusage-c"></a>AttributeUsage(C#)

사용자 지정 특성 클래스를 사용하는 방법을 결정합니다. <xref:System.AttributeUsageAttribute>는 사용자 지정 특성 정의에 적용되는 특성입니다. `AttributeUsage` 특성을 사용하면 다음을 제어할 수 있습니다.

- 적용할 수 있는 프로그램 요소 특성 사용을 제한하지 않는 한, 다음과 같은 프로그램 요소 중 하나에 특성을 적용할 수 있습니다.
  - 어셈블리(assembly)
  - 모듈(module)
  - 필드(field)
  - 이벤트(event)
  - 메서드(method)
  - 매개변수(param)
  - 속성(property)
  - 반환값(return)
  - 형식(type)
- 특성을 단일 프로그램 요소에 여러 번 적용할 수 있는지 여부
- 특성이 파생 클래스에게 상속되는지 여부

기본 설정을 명시적으로 적용할 경우 다음 예제와 같이 작성합니다.

[!code-csharp[Define a new attribute](../../../../../samples/snippets/csharp/attributes/NewAttribute.cs#1)]

이 예제에서 `NewAttribute` 클래스는 모든 지원되는 프로그램 요소에 적용할 수 있습니다. 하지만 각 엔터티에 한 번만 적용할 수 있습니다. 이 특성은 기본 클래스에 적용될 때 파생 클래스에게 상속됩니다.

<xref:System.AttributeUsageAttribute.AllowMultiple> 및 <xref:System.AttributeUsageAttribute.Inherited> 인수는 선택 사항이므로 다음 코드는 동일한 효과를 가집니다.

[!code-csharp[Omit optional attributes](../../../../../samples/snippets/csharp/attributes/NewAttribute.cs#2)]

첫 번째 <xref:System.AttributeUsageAttribute> 인수는 <xref:System.AttributeTargets> 열거형의 요소가 하나 이상이어야 합니다. 다음 예제와 같이 OR 연산자를 사용하여 여러 대상 형식을 함께 연결할 수 있습니다.

[!code-csharp[Create an attribute for fields or properties](../../../../../samples/snippets/csharp/attributes/NewPropertyOrFieldAttribute.cs#1)]

C# 7.3부터 특성은 속성 또는 자동 구현 속성의 지원 필드에 적용할 수 있습니다. 특성에 `field` 지정자를 지정하지 않는 한 특성이 속성에 적용됩니다. 두 경우 모두 다음 예제에서 표시됩니다.

[!code-csharp[Create an attribute for fields or properties](../../../../../samples/snippets/csharp/attributes/NewPropertyOrFieldAttribute.cs#2)]

<xref:System.AttributeUsageAttribute.AllowMultiple> 인수가 `true`인 경우 다음 예제와 같이 결과 특성을 단일 엔터티에 두 번 이상 적용할 수 있습니다.

[!code-csharp[Create and use an attribute that can be applied multiple times](../../../../../samples/snippets/csharp/attributes/MultiUseAttribute.cs#1)]

이 경우 `AllowMultiple`이 `true`로 설정되므로 `MultiUseAttribute`를 반복적으로 적용할 수 있습니다. 여러 특성을 적용하기 위해 표시된 두 형식이 모두 유효합니다.

<xref:System.AttributeUsageAttribute.Inherited>이 `false`인 경우 특성은 특성 클래스에서 파생된 클래스에서 상속하지 않습니다. 예를 들어:

[!code-csharp[Create and use an attribute that can be applied multiple times](../../../../../samples/snippets/csharp/attributes/NonInheritedAttribute.cs#1)]

이 경우에 `NonInheritedAttribute`은 상속을 통해 `DClass`에 적용되지 않습니다.

## <a name="remarks"></a>주의

`AttributeUsage` 특성은 단일 사용 특성입니다. 같은 클래스에 두 번 이상 적용될 수 없습니다. `AttributeUsage`는 <xref:System.AttributeUsageAttribute>의 별칭입니다.

자세한 내용은 [리플렉션을 사용하여 특성 액세스(C#)](accessing-attributes-by-using-reflection.md)를 참조하세요.

## <a name="example"></a>예제

다음 예제에서는 <xref:System.AttributeUsageAttribute> 특성에 대한 <xref:System.AttributeUsageAttribute.Inherited> 및 <xref:System.AttributeUsageAttribute.AllowMultiple>의 영향과 클래스에 적용되는 사용자 지정 특성을 열거하는 방법을 보여 줍니다.

[!code-csharp[Applying and querying attributes](../../../../../samples/snippets/csharp/attributes/Program.cs#1)]

## <a name="sample-output"></a>샘플 출력

```text
Attributes on Base Class:
FirstAttribute
SecondAttribute
Attributes on Derived Class:
ThirdAttribute
ThirdAttribute
SecondAttribute
```

## <a name="see-also"></a>참고 항목

- <xref:System.Attribute>
- <xref:System.Reflection>
- [C# 프로그래밍 가이드](../..//index.md)
- [특성](../../../..//standard/attributes/index.md)
- [리플렉션(C#)](../reflection.md)
- [특성](index.md)
- [사용자 지정 특성 만들기(C#)](creating-custom-attributes.md)
- [리플렉션을 사용하여 특성 액세스(C#)](accessing-attributes-by-using-reflection.md)
