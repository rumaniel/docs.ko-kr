---
title: XML Value 속성(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyExtensionValue
helpviewer_keywords:
- Value property [Visual Basic]
- Visual Basic code, accessing XML
- XML axis [Visual Basic], Value
- XML Value property [Visual Basic]
ms.assetid: 7ddd057a-a195-4e9b-ad8b-2ee0e615a20f
ms.openlocfilehash: 46f81e39686da30270cd67edeb4c9f2d43e048b3
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71592010"
---
# <a name="xml-value-property-visual-basic"></a>XML Value 속성(Visual Basic)

@No__t-0 개체 컬렉션의 첫 번째 요소 값에 대 한 액세스를 제공 합니다.

## <a name="syntax"></a>구문

```vb
object.Value
```

## <a name="parts"></a>요소

|용어|정의|  
|---|---|  
|`object`|필수. <xref:System.Xml.Linq.XElement> 개체의 컬렉션입니다.|  

## <a name="return-value"></a>반환 값

 컬렉션의 첫 번째 요소 값을 포함 하는 `String` 이거나, 컬렉션이 비어 있는 경우-1 @no__t입니다.

## <a name="remarks"></a>설명

 @No__t-0 속성을 사용 하면 <xref:System.Xml.Linq.XElement> 개체 컬렉션의 첫 번째 요소 값에 쉽게 액세스할 수 있습니다. 이 속성은 먼저 컬렉션에 하나 이상의 개체가 포함 되어 있는지 여부를 확인 합니다. 컬렉션이 비어 있으면이 속성은 `Nothing`을 반환 합니다. 그렇지 않으면이 속성은 컬렉션에 있는 첫 번째 요소의 <xref:System.Xml.Linq.XElement.Value%2A> 속성 값을 반환 합니다.

> [!NOTE]
> ' @No__t-0 ' 식별자를 사용 하 여 XML 특성의 값에 액세스 하는 경우 특성 값이 `String`로 반환 되며 <xref:System.Xml.Linq.XAttribute.Value%2A> 속성을 명시적으로 지정할 필요가 없습니다.

 컬렉션의 다른 요소에 액세스 하려면 XML 확장 인덱서 속성을 사용 하면 됩니다. 자세한 내용은 [확장 인덱서 속성](extension-indexer-property.md)을 참조 하세요.

## <a name="inheritance"></a>상속

 대부분의 사용자는 <xref:System.Collections.Generic.IEnumerable%601>을 구현할 필요가 없으므로이 섹션을 무시할 수 있습니다.

 @No__t-0 속성은 `IEnumerable(Of XElement)`을 구현 하는 형식에 대 한 확장 속성입니다. 이 확장 속성의 바인딩은 확장 메서드의 바인딩과 유사 합니다. 형식이 인터페이스 중 하나를 구현 하 고 이름이 "Value" 인 속성을 정의 하는 경우 해당 속성은 확장 속성 보다 우선 합니다. 즉, `IEnumerable(Of XElement)`을 구현 하는 클래스에서 새 속성을 정의 하 여이 <xref:System.Xml.Linq.XElement.Value%2A> 속성을 재정의할 수 있습니다.

## <a name="example"></a>예제

 다음 예에서는 <xref:System.Xml.Linq.XElement.Value%2A> 속성을 사용 하 여 <xref:System.Xml.Linq.XElement> 개체의 컬렉션에 있는 첫 번째 노드에 액세스 하는 방법을 보여 줍니다. 이 예제에서는 자식 축 속성을 사용 하 여 `contact` 개체에 있는 `phone` 이라는 모든 자식 노드의 컬렉션을 가져옵니다.

 [!code-vb[VbXMLSamples#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#15)]

 이 코드의 텍스트는 다음과 같습니다.

 `Phone number: 206-555-0144`

## <a name="example"></a>예제

 다음 예에서는 <xref:System.Xml.Linq.XAttribute> 개체의 컬렉션에서 XML 특성의 값을 가져오는 방법을 보여 줍니다. 이 예에서는 특성 축 속성을 사용 하 여 모든 `phone` 요소에 대 한 `type` 특성의 값을 표시 합니다.

 [!code-vb[VbXMLSamples#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#16)]

 이 코드의 텍스트는 다음과 같습니다.

 ```console
 home
 work
```

## <a name="see-also"></a>참조

- <xref:System.Xml.Linq.XElement>
- <xref:System.Collections.Generic.IEnumerable%601>
- [XML 축 속성](index.md)
- [XML 리터럴](../xml-literals/index.md)
- [Visual Basic에서 XML 만들기](../../programming-guide/language-features/xml/creating-xml.md)
- [확장명 메서드](../../programming-guide/language-features/procedures/extension-methods.md)
- [확장명 인덱서 속성](extension-indexer-property.md)
- [XML Child 축 속성](xml-child-axis-property.md)
- [XML Attribute 축 속성](xml-attribute-axis-property.md)
