---
title: '방법: XML 리터럴 (Visual Basic)를 수정 합니다.'
ms.date: 07/20/2015
helpviewer_keywords:
- XML axis [Visual Basic], Value
- XML literals [Visual Basic]
- XML literals [Visual Basic], modifying
ms.assetid: 4e864522-a37a-43a2-8236-af80277c5482
ms.openlocfilehash: 003715b04f3a5c0fb41e846beb189f117378ea58
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62053030"
---
# <a name="how-to-modify-xml-literals-visual-basic"></a>방법: XML 리터럴 (Visual Basic)를 수정 합니다.

Visual Basic XML 리터럴 수정 하는 편리한 방법을 제공 합니다. 추가 및 요소 및 특성을 삭제할 수도 있고, 새 XML 요소를 사용 하 여 기존 요소를 바꿀 수도 있습니다. 이 항목에서는 기존 XML 리터럴 수정 하는 방법의 몇 가지 예를 제공 합니다.

### <a name="to-modify-the-value-of-an-xml-literal"></a>XML 리터럴의 값을 수정 하려면

1. XML 리터럴의 값을 수정 하려면 XML 리터럴 및 설정에 대 한 참조를 가져올는 `Value` 속성을 원하는 값입니다.

    모든 값을 업데이트 하는 다음 코드 예제는 \<가격 > XML 문서의 요소입니다.

    [!code-vb[VbXmlSamples2#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#4)]

    다음은 샘플 소스 XML 및이 코드 예제에서 XML을 수정 합니다.

    XML 원본:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
    </Catalog>
    ```

    수정 된 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>47.20</Price>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>48.25</Price>
      </Book>
    </Catalog>
    ```

    > [!NOTE]
    > `Value` 속성 컬렉션의 첫 번째 XML 요소를 가리킵니다. 컬렉션에 동일한 이름을 가진 요소가 둘 이상 있으면 설정 된 `Value` 속성 컬렉션의 첫 번째 요소에만 영향을 줍니다.

### <a name="to-add-an-attribute-to-an-xml-literal"></a>XML 리터럴에서 특성을 추가 하려면

1. 리터럴 xml 특성을 추가 하려면 먼저 리터럴 XML에 대 한 참조를 가져옵니다. 그런 다음 새 XML 특성 축 속성을 추가 하 여 특성을 추가할 수 있습니다. 새 추가할 수도 있습니다 <xref:System.Xml.Linq.XAttribute> 개체를 사용 하 여 리터럴 XML <xref:System.Xml.Linq.XContainer.Add%2A> 메서드. 다음 예제에서는 두 옵션을 보여 줍니다.

    [!code-vb[VbXmlSamples2#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#5)]

    다음은 샘플 소스 XML 및이 코드 예제에서 XML을 수정 합니다.

    XML 원본:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" >
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
    </Catalog>
    ```

    수정 된 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" genre="Computer" editorEmail="someone@example.com">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk331" genre="Computer" editorEmail="someone@example.com">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
    </Catalog>
    ```

    XML 특성 축 속성에 대 한 자세한 내용은 참조 하세요. [XML 특성 축 속성](../../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)합니다.

### <a name="to-add-an-element-to-an-xml-literal"></a>XML 리터럴에서 요소를 추가 하려면

1. XML 리터럴 요소에 추가 하려면 먼저 리터럴 XML에 대 한 참조를 가져옵니다. 추가할 수 있습니다 새 <xref:System.Xml.Linq.XElement> 개체를 사용 하 여 요소의 마지막 하위 요소로 <xref:System.Xml.Linq.XContainer.Add%2A> 메서드. 새 추가할 수 있습니다 <xref:System.Xml.Linq.XElement> 개체를 사용 하 여 첫 번째 하위 요소로 <xref:System.Xml.Linq.XContainer.AddFirst%2A> 메서드.

    다른 하위 요소를 기준으로 특정 위치에 새 요소를 추가 하려면 먼저 인접 한 하위 요소에 대 한 참조를 가져옵니다. 추가할 수 있습니다 새 <xref:System.Xml.Linq.XElement> 개체를 사용 하 여 인접 한 하위 요소 앞의 <xref:System.Xml.Linq.XNode.AddBeforeSelf%2A> 메서드. 새 추가할 수도 있습니다 <xref:System.Xml.Linq.XElement> 개체를 사용 하 여 인접 한 하위 요소 뒤의 <xref:System.Xml.Linq.XNode.AddAfterSelf%2A> 메서드.

    다음 예제에서는 각이 방법을의 예를 보여 줍니다.

    [!code-vb[VbXmlSamples2#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#6)]

    다음은 샘플 소스 XML 및이 코드 예제에서 XML을 수정 합니다.

    XML 원본:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" >
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
    </Catalog>
    ```

    수정 된 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" >
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk000"></Book>
      <Book id="bk331">
        <Publisher>Microsoft Press</Publisher>
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
        <PublishDate>2005-2-14</PublishDate>
      </Book>
      <Book id="bk999"></Book>
    </Catalog>
    ```

### <a name="to-remove-an-element-or-attribute-from-an-xml-literal"></a>XML 리터럴 요소 또는 특성을 제거 하려면

1. XML 리터럴에서 요소 또는 특성을 제거 하 여 요소 또는 특성 및 호출에 대 한 참조를 가져올는 `Remove` 메서드를 다음 예제에서와 같이 합니다.

    [!code-vb[VbXmlSamples2#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#7)]

    다음은 샘플 소스 XML 및이 코드 예제에서 XML을 수정 합니다.

    XML 원본:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" genre="Computer" editorEmail="someone@example.com">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk000"></Book>
      <Book id="bk331" genre="Computer" editorEmail="someone@example.com">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
      <Book id="bk999"></Book>
    </Catalog>
    ```

    수정 된 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" editorEmail="someone@example.com">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk000"></Book>
      <Book id="bk331" editorEmail="someone@example.com">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book></Catalog>
    ```

    제거할 모든 요소나 특성에서 XML 리터럴의 xml 리터럴에 대 한 참조를 가져오고 호출을 <xref:System.Xml.Linq.XElement.RemoveAll%2A> 메서드.

### <a name="to-modify-an-xml-literal"></a>XML 리터럴 수정

1. XML 요소의 이름을 변경 하려면 먼저 요소에 대 한 참조를 가져옵니다. 만들 수 있습니다 새 <xref:System.Xml.Linq.XElement> 새 이름을 지정 하 고 새 전달 된 개체 <xref:System.Xml.Linq.XElement> 개체를 <xref:System.Xml.Linq.XNode.ReplaceWith%2A> 기존 메서드의 <xref:System.Xml.Linq.XElement> 개체입니다.

    대체 하는 요소에 유지 해야 하는 하위 요소가 있으면 새 값을 설정 <xref:System.Xml.Linq.XElement> 개체는 <xref:System.Xml.Linq.XContainer.Nodes%2A> 기존 요소의 속성입니다. 기존 요소의 내부 XML을 새 요소의 값을 설정 합니다. 새 요소의 값을 설정할 수이 고, 그렇지는 `Value` 기존 요소의 속성입니다.

    다음 코드 예제에서는 모든 바꿉니다 \<설명 > 요소는 \<추상 > 요소입니다. 내용의 \<설명 > 요소는 새 유지 \<추상 > 요소를 사용 하 여를 <xref:System.Xml.Linq.XContainer.Nodes%2A> 의 속성을 \<설명 > <xref:System.Xml.Linq.XElement> 개체입니다.

    [!code-vb[VbXmlSamples2#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#8)]

    다음은 샘플 소스 XML 및이 코드 예제에서 XML을 수정 합니다.

    XML 원본:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
        <Description>
          An in-depth look at creating applications
          with <technology>XML</technology>. For
          <audience>beginners</audience> or
          <audience>advanced</audience> developers.
        </Description>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
        <Description>
          Get the expert insights, practical code samples, and best
          practices you need to advance your expertise with
          <technology>Visual Basic .NET</technology>.
          Learn how to create faster, more reliable applications
          based on professional, pragmatic guidance by today's top
          <audience>developers</audience>.
        </Description>
      </Book>
    </Catalog>
    ```

    수정 된 XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <MSRP>44.95</MSRP>    <Abstract>
          An in-depth look at creating applications
          with <technology>XML</technology>. For
          <audience>beginners</audience> or
          <audience>advanced</audience> developers.
        </Abstract>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <MSRP>45.95</MSRP>    <Abstract>
          Get the expert insights, practical code samples, and best
          practices you need to advance your expertise with
          <technology>Visual Basic .NET</technology>.
          Learn how to create faster, more reliable applications
          based on professional, pragmatic guidance by today's top
          <audience>developers</audience>.
        </Abstract>
      </Book>
    </Catalog>
    ```

## <a name="see-also"></a>참고자료

- [Visual Basic에서 XML 조작](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)
- [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)
- [방법: 파일, 문자열 또는 Stream에서 XML 로드](../../../../visual-basic/programming-guide/language-features/xml/how-to-load-xml-from-a-file-string-or-stream.md)
- [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
- [Visual Basic의 LINQ 소개](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
