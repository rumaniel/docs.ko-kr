---
title: '방법: 데이터 바인딩에서 XML 네임스페이스 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- XML [WPF], namespaces
- data binding [WPF], XML namespaces
- namespaces [WPF], XML
ms.assetid: a47c832f-dc84-48f2-96d5-cde18fc4284b
ms.openlocfilehash: 38bf6e8f88b0325193d49148cd6c33031f7b0a6d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61931913"
---
# <a name="how-to-use-xml-namespaces-in-data-binding"></a>방법: 데이터 바인딩에서 XML 네임스페이스 사용
## <a name="example"></a>예제  
 이 예제에서는 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 바인딩 소스에 지정된 네임스페이스를 처리하는 방법을 보여 줍니다.  
  
 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 데이터에 다음 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 네임스페이스 정의가 있는 경우  
  
 `<rss version="2.0" xmlns:dc="http://purl.org/dc/elements/1.1/">`  
  
 사용할 수는 <xref:System.Windows.Data.XmlNamespaceMapping> 네임 스페이스를 매핑할 요소를 <xref:System.Windows.Data.XmlNamespaceMapping.Prefix%2A>다음 예제와 같이 합니다. 사용할 수 있습니다 합니다 <xref:System.Windows.Data.XmlNamespaceMapping.Prefix%2A> 가리킵니다는 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 네임 스페이스입니다. <xref:System.Windows.Controls.ListBox> 이 예제에 표시 합니다 *제목* 및 *dc:date* 각 *항목*합니다.  
  
 [!code-xaml[XmlnsBindSnippet#XmlNamespaceMapping](~/samples/snippets/csharp/VS_Snippets_Wpf/XmlnsBindSnippet/CS/Window1.xaml#xmlnamespacemapping)]  
  
 <xref:System.Windows.Data.XmlNamespaceMapping.Prefix%2A> 에 사용 되는 것과 일치 하지 않아도 지정할 합니다 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 소스에서 접두사가 변경 하는 경우를 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 매핑은 계속 작동 하는 원본입니다.  
  
 이 특정 예제는 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 웹 서비스에서 데이터가 하지만 <xref:System.Windows.Data.XmlNamespaceMapping> 인라인 요소 에서도 작동 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 또는 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 포함 된 파일에서 데이터.  
  
## <a name="see-also"></a>참고자료

- [XMLDataProvider 및 XPath 쿼리를 사용하여 XML 데이터에 바인딩](how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)
- [데이터 바인딩 개요](data-binding-overview.md)
- [방법 항목](data-binding-how-to-topics.md)
