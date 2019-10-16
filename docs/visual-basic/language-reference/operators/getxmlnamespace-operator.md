---
title: GetXmlNamespace 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.GetXmlNamespace
- GetXmlNamespace
helpviewer_keywords:
- GetXmlNamespace operator [Visual Basic]
- GetXmlNamespace keyword [Visual Basic]
ms.assetid: d0d28cfd-0755-4896-ae0b-4981aa35517c
ms.openlocfilehash: bfccdcd9b5d35418b206dfa9fefffb5ddab69c66
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71592163"
---
# <a name="getxmlnamespace-operator-visual-basic"></a>GetXmlNamespace 연산자(Visual Basic)
지정 된 XML 네임 스페이스 접두사에 해당 하는 @no__t 0 개체를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
GetXmlNamespace(xmlNamespacePrefix)  
```  
  
## <a name="parts"></a>요소  
 `xmlNamespacePrefix`  
 (선택 사항) XML 네임 스페이스 접두사를 식별 하는 문자열입니다. 제공 되는 경우이 문자열은 올바른 XML 식별자 여야 합니다. 자세한 내용은 [선언 된 XML 요소 및 특성의 이름](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)을 참조 하세요. 접두사가 지정 되지 않은 경우에는 기본 네임 스페이스가 반환 됩니다. 기본 네임 스페이스를 지정 하지 않으면 빈 네임 스페이스가 반환 됩니다.  
  
## <a name="return-value"></a>반환 값  
 XML 네임 스페이스 접두사에 해당 하는 <xref:System.Xml.Linq.XNamespace> 개체입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 연산자는 XML 네임 스페이스 접두사 `xmlNamespacePrefix`에 해당 하는 @no__t 1 개체를 가져옵니다.  
  
 Xml 리터럴 및 XML 축 속성에 XML 네임 스페이스 접두사를 직접 사용할 수 있습니다. 그러나 `GetXmlNamespace` 연산자를 사용 하 여 코드에서 사용할 수 있도록 네임 스페이스 접두사를 <xref:System.Xml.Linq.XNamespace> 개체로 변환 해야 합니다. @No__t-0 개체에 정규화 되지 않은 요소 이름을 추가 하 여 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 개 메서드에 필요한 정규화 된 @no__t 1 개체를 가져올 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `ns`을 XML 네임 스페이스 접두사로 가져옵니다. 그런 다음 네임 스페이스의 접두사를 사용 하 여 XML 리터럴을 만들고 정규화 된 이름이 `ns:phone` 인 첫 번째 자식 노드에 액세스 합니다. 그런 다음 해당 자식 노드를 `ShowName` 서브루틴으로 전달 합니다 .이 서브루틴은 `GetXmlNamespace` 연산자를 사용 하 여 정규화 된 이름을 생성 합니다. 그러면 `ShowName` 서브루틴이 정규화 된 이름을 <xref:System.Xml.Linq.XNode.Ancestors%2A> 메서드로 전달 하 여 부모 `ns:contact` 노드를 가져옵니다.  
  
 [!code-vb[VbXMLSamples#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/GetXmlNamespace.vb#38)]  
  
 @No__t-0을 호출 하면 다음 텍스트를 포함 하는 메시지 상자가 표시 됩니다.  
  
 `Name: Patrick Hines`  
  
## <a name="see-also"></a>참조

- [Imports 문(XML 네임스페이스)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)
- [Visual Basic에서 XML에 액세스](../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)
