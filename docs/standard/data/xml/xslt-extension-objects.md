---
title: XSLT 확장명 개체
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: a4ebdbad-087c-4cfe-acc0-17c48142f81a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 25c9c1c81db0bb6775aa9226318d7ec726a93e09
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924933"
---
# <a name="xslt-extension-objects"></a>XSLT 확장명 개체
확장 개체를 사용하여 스타일시트의 기능을 확장할 수 있습니다. 확장명 개체는 <xref:System.Xml.Xsl.XsltArgumentList> 클래스를 사용하여 유지 관리합니다.  
  
 포함 스크립트를 사용하는 대신 확장명 개체를 사용하면 다음과 같은 이점을 활용할 수 있습니다.  
  
- 클래스의 캡슐화 및 재사용에 효과적입니다.  
  
- 스타일시트를 더 작게 유지하고 보다 쉽게 관리할 수 있습니다.  
  
 <xref:System.Xml.Xsl.XsltArgumentList> 메서드를 사용하여 <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> 개체에 XSLT 확장 개체를 추가합니다. 이 때 정규화된 이름과 네임스페이스 URI가 확장 개체와 연결됩니다.  
  
> [!NOTE]
> <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> 메서드를 호출하려면 FullTrust 권한 집합이 필요합니다. 자세한 내용은 [코드 액세스 보안](../../../../docs/framework/misc/code-access-security.md) 및 [명명된 권한 세트](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/4652tyx7(v=vs.100))를 참조하세요.  
  
 확장명 개체에서 반환된 데이터 형식은 네 가지 기본 XPath 데이터 형식인 `number`, `string`, `Boolean` 및 `node set` 중 하나입니다.  
  
 전달할 매개 변수 수를 지정하지 않아도 되는 `params` 키워드로 정의한 메서드는 현재 <xref:System.Xml.Xsl.XslCompiledTransform> 클래스에서 지원되지 않습니다. 그러므로 `params` 키워드로 정의한 메서드를 사용하는 XSLT 스타일시트는 제대로 작동하지 않습니다. 자세한 내용은 [params](../../../csharp/language-reference/keywords/params.md)를 참조하세요.  
  
### <a name="to-use-an-xslt-extension-object"></a>XSLT 확장명 개체를 사용하려면  
  
1. <xref:System.Xml.Xsl.XsltArgumentList> 개체를 만들고 <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> 메서드를 사용하여 확장 개체를 추가합니다.  
  
2. 스타일시트에서 확장명 개체를 호출합니다.  
  
3. <xref:System.Xml.Xsl.XsltArgumentList> 개체를 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 메서드에 전달합니다.  
  
## <a name="see-also"></a>참고 항목

- [XSLT 변환](../../../../docs/standard/data/xml/xslt-transformations.md)
- [XSLT 보안 고려 사항](../../../../docs/standard/data/xml/xslt-security-considerations.md)
