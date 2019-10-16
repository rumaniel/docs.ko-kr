---
title: XML 요소 리터럴(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlLiteralElement
helpviewer_keywords:
- XML element literal [Visual Basic]
- element literal [Visual Basic]
- XML literals [Visual Basic], element
ms.assetid: 95039642-7893-48b7-b23f-45a6c55d8f67
ms.openlocfilehash: 3431ad32809e1f15eb8473d5af7660367cca04de
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64751958"
---
# <a name="xml-element-literal-visual-basic"></a>XML 요소 리터럴(Visual Basic)

나타내는 리터럴입니다는 <xref:System.Xml.Linq.XElement> 개체입니다.

## <a name="syntax"></a>구문

```xml
<name [ attributeList ] />
-or-
<name [ attributeList ] > [ elementContents ] </[ name ]>
```

## <a name="parts"></a>요소

- `<`

  필수 요소. 시작 요소 태그를 엽니다.

- `name`

  필수 요소. 요소 이름입니다. 형식에는 다음 중 하나입니다.

  - 폼의 요소 이름에 대 한 리터럴 텍스트 `[ePrefix:]eName`여기서:

    |파트|설명|
    |---|---|
    |`ePrefix`|선택 사항입니다. 요소에 대 한 XML 네임 스페이스 접두사입니다. 전역으로 정의 된 XML 네임 스페이스에 있어야는 `Imports` 파일 또는 프로젝트 수준 또는 로컬이 요소 또는 부모 요소에 정의 된 XML 네임 스페이스 문입니다.|
    |`eName`|필수 요소. 요소 이름입니다. 형식에는 다음 중 하나입니다.<br /><br /> -리터럴 텍스트입니다. 참조 [선언 된 XML 요소 및 특성의 이름을](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)입니다.<br />포함 형식의 식을 `<%= eNameExp %>`합니다. 유형의 `eNameExp` 있어야 `String` 이거나 암시적으로 변환할 수 있는 유형 <xref:System.Xml.Linq.XName>합니다.|

  - 포함 식 형식의 `<%= nameExp %>`합니다. 유형의 `nameExp` 있어야 `String` 또는 형식으로 암시적으로 변환할 <xref:System.Xml.Linq.XName>합니다. 포함된 식은 요소의 닫는 태그에 허용 되지 않습니다.

- `attributeList`

  선택 사항입니다. 리터럴에서 특성 목록을 선언 합니다.

  `attribute [ attribute ... ]`

  각 `attribute` 다음 구문 중 하나:

  - 특성 형식의 할당이 `[aPrefix:]aName=aValue`여기서:

    |파트|설명|
    |---|---|
    |`aPrefix`|선택 사항입니다. 특성에 대 한 XML 네임 스페이스 접두사입니다. 전역으로 정의 된 XML 네임 스페이스에 있어야는 `Imports` 문이나이 요소 또는 부모 요소에 정의 된 로컬 XML 네임 스페이스입니다.|
    |`aName`|필수 요소. 특성의 이름입니다. 형식에는 다음 중 하나입니다.<br /><br /> -리터럴 텍스트입니다. 참조 [선언 된 XML 요소 및 특성의 이름을](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)입니다.<br />포함 형식의 식을 `<%= aNameExp %>`합니다. 유형의 `aNameExp` 있어야 `String` 이거나 암시적으로 변환할 수 있는 유형 <xref:System.Xml.Linq.XName>합니다.|
    |`aValue`|선택 사항입니다. 특성의 값입니다. 형식에는 다음 중 하나입니다.<br /><br /> -리터럴 텍스트를 따옴표로 묶어야 합니다.<br />포함 형식의 식을 `<%= aValueExp %>`합니다. 모든 형식이 허용 됩니다.|

  - 포함 식 형식의 `<%= aExp %>`합니다.

- `/>`

  선택 사항입니다. 요소 콘텐츠가 없는 빈 요소를 나타냅니다.

- `>`

  필수 요소. 이상 버전 또는 빈 요소 태그를 종료합니다.

- `elementContents`

  선택 사항입니다. 콘텐츠 요소입니다.

  `content [ content ... ]`

  각 `content` 다음 중 하나일 수 있습니다.

  - 리터럴 텍스트입니다. 모든 공백을 `elementContents` 리터럴 텍스트 경우 의미를 갖습니다.

  - 포함 식 형식의 `<%= contentExp %>`합니다.

  - XML 요소 리터럴입니다.

  - XML 주석 리터럴입니다. 참조 [XML 주석 리터럴](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md)합니다.

  - XML 처리 명령 리터럴입니다. 참조 [XML 처리 명령 리터럴](../../../visual-basic/language-reference/xml-literals/xml-processing-instruction-literal.md)합니다.

  - XML CDATA 리터럴입니다. 참조 [XML CDATA 리터럴](../../../visual-basic/language-reference/xml-literals/xml-cdata-literal.md)합니다.

- `</[name]>`

  선택 사항입니다. 요소의 닫는 태그를 나타냅니다. 선택적 `name` 포함 된 식의 결과 매개 변수가 잘못 되었습니다.

## <a name="return-value"></a>반환 값

<xref:System.Xml.Linq.XElement> 개체입니다.

## <a name="remarks"></a>설명

XML 요소 리터럴 구문을 사용 하 여 만들려는 <xref:System.Xml.Linq.XElement> 코드에서 개체입니다.

> [!NOTE]
> XML 리터럴을 줄 연속 문자를 사용 하지 않고 여러 줄을 확장할 수 있습니다. 이 기능을 사용 하면 XML 문서에서 콘텐츠를 복사 하 고 Visual Basic 프로그램에 직접 붙여넣을 수 있습니다.

포함 형식의 식이 `<%= exp %>` XML 요소 리터럴에에 동적 정보를 추가할 수 있습니다. 자세한 내용은 [XML의 포함 식](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)합니다.

Visual Basic 컴파일러는 XML 요소 리터럴에 호출으로 변환 합니다 <xref:System.Xml.Linq.XElement.%23ctor%2A> 생성자 및 필요한 경우는 <xref:System.Xml.Linq.XAttribute.%23ctor%2A> 생성자입니다.

## <a name="xml-namespaces"></a>XML 네임스페이스

XML 네임 스페이스 접두사는 코드에서 여러 번 동일한 네임 스페이스에서 요소를 사용 하 여 XML 리터럴을 만들 수 있는 경우에 유용 합니다. 사용 하 여 정의 하는 전역 XML 네임 스페이스 접두사를 사용할 수는 `Imports` 문 또는 로컬 접두사를 사용 하 여 정의 하는 `xmlns:xmlPrefix="xmlNamespace"` 특성 구문입니다. 자세한 내용은 [Imports 문 (XML Namespace)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)합니다.

XML 네임 스페이스에 대 한 범위 지정 규칙에 따라 로컬 접두사 전역 접두사 보다 우선합니다. 그러나 XML 리터럴의 XML 네임 스페이스를 정의 하는 경우 해당 네임 스페이스가 아닙니다 포함된 식에 표시 되는 식에 사용할 수 있습니다. 포함된 된 식에는 전역 XML 네임 스페이스만 액세스할 수 있습니다.

Visual Basic 컴파일러는 XML 리터럴이 생성된 된 코드에서 하나의 로컬 네임 스페이스 정의로 사용 되는 각 전역 XML 네임 스페이스를 변환 합니다. 사용 되지 않는 전역 XML 네임 스페이스는 생성된 된 코드에 표시 되지 않습니다.

## <a name="example"></a>예제

다음 예제에서는 두 중첩 된 빈 요소가 포함 된 간단한 XML 요소를 만드는 방법을 보여 줍니다.

[!code-vb[VbXMLSamples#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples9.vb#20)]

다음 텍스트를 표시합니다. 리터럴 빈 요소의 구조를 유지 됨을 알 수 있습니다.

```xml
<outer>
  <inner1></inner1>
  <inner2 />
</outer>
```

## <a name="example"></a>예제

다음 예제에서는 포함 된 식을 사용 하 여 요소 이름과 특성을 만드는 방법을 보여 줍니다.

[!code-vb[VbXMLSamples#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples9.vb#21)]

이 코드의 텍스트는 다음과 같습니다.

```xml
<book isbn="1234" author="My Author" year="1999" title="My Book" />
```

## <a name="example"></a>예제

다음 예제에서는 `ns`를 XML 네임스페이스 접두사로 선언한 다음 XML 리터럴 만들려는 네임 스페이스의 접두사를 사용 하 고 요소의 마지막 폼을 표시 합니다.

[!code-vb[VbXMLSamples#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples10.vb#22)]

이 코드의 텍스트는 다음과 같습니다.

```xml
<ns:outer xmlns:ns="http://SomeNamespace">
  <ns:middle xmlns:ns="http://NewNamespace">
    <ns:inner1 />
    <inner2 xmlns="http://SomeNamespace" />
  </ns:middle>
</ns:outer>
```

컴파일러가 XML 네임 스페이스에 대 한 접두사 정의에 전역 XML 네임 스페이스의 접두사를 변환 하는 주의 하십시오. 합니다 \<ns:middle >에 대 한 XML 네임 스페이스 접두사를 재정의 하는 요소는 \<ns:inner1 > 요소입니다. 그러나 합니다 \<ns:inner2 > 정의한 네임 스페이스를 사용 하는 요소는 `Imports` 문입니다.

## <a name="see-also"></a>참고자료

- <xref:System.Xml.Linq.XElement>
- [선언된 XML 요소 및 특성의 이름](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
- [XML 주석 리터럴](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md)
- [XML CDATA 리터럴](../../../visual-basic/language-reference/xml-literals/xml-cdata-literal.md)
- [XML 리터럴](../../../visual-basic/language-reference/xml-literals/index.md)
- [Visual Basic에서 XML 만들기](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [XML의 포함 식](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)
- [Imports 문(XML 네임스페이스)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)
