---
title: XML 하위 항목 축 속성(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyDescendantsAxis
helpviewer_keywords:
- Visual Basic code, accessing XML
- XML descendant axis property [Visual Basic]
- descendant axis property [Visual Basic]
- XML axis [Visual Basic], descendant
- XML [Visual Basic], accessing
ms.assetid: a178f85b-5d54-438f-8479-40b62af6fe76
ms.openlocfilehash: bc1dff6dc3b580079087f370212b7d3acd30e4fb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61938673"
---
# <a name="xml-descendant-axis-property-visual-basic"></a>XML 하위 항목 축 속성(Visual Basic)

다음의 하위 항목에 액세스할 수:는 <xref:System.Xml.Linq.XElement> 개체를 <xref:System.Xml.Linq.XDocument> 개체의 컬렉션인 <xref:System.Xml.Linq.XElement> 개체나 컬렉션 <xref:System.Xml.Linq.XDocument> 개체입니다.

## <a name="syntax"></a>구문

```
object...<descendant>
```

## <a name="parts"></a>요소

`object` 필수입니다. <xref:System.Xml.Linq.XElement> 개체, <xref:System.Xml.Linq.XDocument> 개체, <xref:System.Xml.Linq.XElement> 개체의 컬렉션 또는 <xref:System.Xml.Linq.XDocument> 개체의 컬렉션입니다.

`...<` 필수입니다. 하위 축 속성의 시작을 나타냅니다.

`descendant` 필수입니다. 폼에 액세스 하려면 하위 노드의 이름을 [`prefix:]name`합니다.

|파트|설명|
|----------|-----------------|
|`prefix`|선택 사항입니다. 하위 노드에 대 한 XML 네임 스페이스 접두사입니다. 사용 하 여 정의 된 전역 XML 네임 스페이스 여야는 `Imports` 문입니다.|
|`name`|필수 요소. 하위 노드의 로컬 이름입니다. 참조 [선언 된 XML 요소 및 특성의 이름을](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)입니다.|

`>` 필수입니다. 하위 축 속성의 끝을 나타냅니다.

## <a name="return-value"></a>반환 값

<xref:System.Xml.Linq.XElement> 개체의 컬렉션입니다.

## <a name="remarks"></a>설명

이름으로 하위 노드에 액세스 하는 XML 하위 축 속성을 사용할 수는 <xref:System.Xml.Linq.XElement> 또는 <xref:System.Xml.Linq.XDocument> 개체 또는 컬렉션 <xref:System.Xml.Linq.XElement> 또는 <xref:System.Xml.Linq.XDocument> 개체입니다. XML을 사용 하 여 `Value` 반환된 된 컬렉션의 첫 번째 하위 노드의 값에 액세스 하는 속성입니다. 자세한 내용은 [XML 값 속성](../../../visual-basic/language-reference/xml-axis/xml-value-property.md)합니다.

Visual Basic 컴파일러는 하위 항목 축 속성에 대 한 호출으로 변환 합니다는 <xref:System.Xml.Linq.XContainer.Descendants%2A> 메서드.

## <a name="xml-namespaces"></a>XML 네임스페이스

하위 축 속성의 이름을 사용 하 여 전역적으로 선언 된 XML 네임 스페이스만 사용할 수는 `Imports` 문입니다. XML 요소 리터럴 내에서 로컬로 선언 된 XML 네임 스페이스를 사용할 수 없습니다. 자세한 내용은 [Imports 문 (XML Namespace)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)합니다.

## <a name="example"></a>예제

다음 예제에서는 명명 된 첫 번째 하위 노드의 값에 액세스 하는 방법을 보여 줍니다 `name` 이라는 모든 하위 노드의 값 `phone` 에서 `contacts` 개체입니다.

[!code-vb[VbXMLSamples#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples11.vb#25)]

이 코드의 텍스트는 다음과 같습니다.

`Name: Patrick Hines`

`Home Phone = 206-555-0144`

## <a name="example"></a>예제

다음 예제에서는 `ns`를 XML 네임스페이스 접두사로 선언한 다음 다음 네임 스페이스의 접두사는 XML 리터럴을 만들고 정규화 된 이름 사용 하 여 첫 번째 자식 노드의 값에 액세스를 사용 하 여 `ns:name`입니다.

[!code-vb[VbXMLSamples#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples12.vb#26)]

이 코드의 텍스트는 다음과 같습니다.

`Name: Patrick Hines`

## <a name="see-also"></a>참고자료

- <xref:System.Xml.Linq.XElement>
- [XML 축 속성](../../../visual-basic/language-reference/xml-axis/index.md)
- [XML 리터럴](../../../visual-basic/language-reference/xml-literals/index.md)
- [Visual Basic에서 XML 만들기](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [선언된 XML 요소 및 특성의 이름](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
