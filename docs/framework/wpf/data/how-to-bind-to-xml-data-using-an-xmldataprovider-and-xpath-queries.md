---
title: '방법: XMLData Provider 및 XPath 쿼리를 사용하여 XML 데이터에 바인딩'
ms.date: 03/30/2017
helpviewer_keywords:
- XmlDataProvider [WPF], binding to XML data
- data binding [WPF], binding to XML data using XmlDataProvider queries
- binding [WPF], to XML data using XmlDataProvider queries
ms.assetid: 7dcd018f-16aa-4870-8e47-c1b4ea31e574
ms.openlocfilehash: d92b01c453a9e07a5d4a6d1900d54e8c86210041
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005686"
---
# <a name="how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries"></a>방법: XMLData Provider 및 XPath 쿼리를 사용하여 XML 데이터에 바인딩
이 예제에서는 <xref:System.Windows.Data.XmlDataProvider>을 사용 하 여 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 데이터에 바인딩하는 방법을 보여 줍니다.  
  
 @No__t-0을 사용 하면 응용 프로그램에서 데이터 바인딩을 통해 액세스할 수 있는 기본 데이터는 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 노드의 트리가 될 수 있습니다. 즉, <xref:System.Windows.Data.XmlDataProvider>은 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 노드의 트리를 바인딩 소스로 사용 하는 편리한 방법을 제공 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서 데이터는 <xref:System.Windows.FrameworkElement.Resources%2A> 섹션에 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] *데이터 아일랜드* 로 직접 포함 됩니다. [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 데이터 고립 영역은 `<x:XData>` 태그로 래핑되어야 하며, 항상 단일 루트 노드가 있어야 합니다. 이 예에서는 *인벤토리*입니다.  
  
> [!NOTE]
> [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 데이터의 루트 노드에는 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 네임스페이스를 빈 문자열로 설정하는 **xmlns** 특성이 있습니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 페이지에 인라인인 데이터 고립 영역에 XPath 쿼리를 적용하기 위한 요구 사항입니다. 이 인라인 경우 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]이 고, 따라서 데이터 아일랜드는 <xref:System.Windows> 네임 스페이스를 상속 합니다. 이로 인해 XPath 쿼리가 <xref:System.Windows> 네임 스페이스로 한정 되지 않도록 하 여 쿼리를 잘못 전달 하는 것을 방지 하기 위해 네임 스페이스를 비워 두어야 합니다.  
  
 [!code-xaml[XMLDataSource#1](~/samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSource/CS/Window1.xaml#1)]  
  
 이 예에 표시된 대로 특성 구문에서 동일한 바인딩 선언을 만들기 위해 특수 문자를 적절하게 이스케이프 처리해야 합니다. 자세한 내용은 [XML 문자 엔터티 및 XAML](../../xaml-services/xml-character-entities-and-xaml.md)을 참조하세요.  
  
 이 예제가 실행 되 면 <xref:System.Windows.Controls.ListBox>은 다음 항목을 표시 합니다. *재고* 값이 “*out*”이거나 *숫자* 값이 3이상 또는 8과 동일한 *책* 아래에 있는 모든 요소의 *제목*입니다. @No__t-2에 설정 된 @no__t 1 값은 *Books* 요소만 노출 되어야 함을 나타내므로 (기본적으로 필터 설정) *CD* 항목이 반환 되지 않습니다.  
  
 ![4 권의 책의 제목을 보여 주는 XPath 예제의 스크린샷](./media/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries/xpath-example-listbox-details.png)  
  
 이 예에서는 <xref:System.Windows.DataTemplate>에 있는 <xref:System.Windows.Controls.TextBlock> 바인딩의 <xref:System.Windows.Data.Binding.XPath%2A>이 "*Title*"로 설정 되어 있기 때문에 책 제목이 표시 됩니다. *ISBN*과 같은 특성의 값을 표시 하려면 <xref:System.Windows.Data.Binding.XPath%2A> 값을 "`@ISBN`"로 설정 합니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 **XPath** 속성은 XmlNode.SelectNodes 메서드를 통해 처리됩니다. **XPath** 쿼리를 수정하여 다른 결과를 얻을 수 있습니다. 다음은 이전 예제에서 바인딩된 <xref:System.Windows.Controls.ListBox>에 대 한 <xref:System.Windows.Data.Binding.XPath%2A> 쿼리에 대 한 몇 가지 예입니다.  
  
- `XPath="Book[1]"`은 첫 번째 책 요소를 반환합니다(“작동 중인 XML”). **XPath** 색인은 0이 아니라 1을 기반으로 합니다.  
  
- `XPath="Book[@*]"`에서는 모든 특성이 있는 모든 책 요소를 반환합니다.  
  
- `XPath="Book[last()-1]"`은 끝에서 두 번째인 책 요소를 반환합니다(“Microsoft .NET 소개”).  
  
- `XPath="*[position()>3]"`에서는 처음 3개를 제외한 모든 책 요소를 반환합니다.  
  
 **XPath** 쿼리를 실행 하면 <xref:System.Xml.XmlNode> 또는 XmlNodes 목록이 반환 됩니다. <xref:System.Xml.XmlNode>은 CLR (공용 언어 런타임) 개체입니다. 즉, <xref:System.Windows.Data.Binding.Path%2A> 속성을 사용 하 여 CLR (공용 언어 런타임) 속성에 바인딩할 수 있습니다. 이전 예를 다시 살펴보겠습니다. 예제의 나머지 부분이 동일 하 게 유지 되 고 <xref:System.Windows.Controls.TextBlock> 바인딩을 다음과 같이 변경 하면 <xref:System.Windows.Controls.ListBox>에 반환 된 XmlNodes 이름이 표시 됩니다. 이 경우 반환된 모든 노드의 이름은 "*Book*"입니다.  
  
 [!code-xaml[XmlDataSourceVariation#XmlNodePath](~/samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSourceVariation/CS/Page1.xaml#xmlnodepath)]  
  
 컴파일 시 데이터의 정확한 콘텐츠를 알아야 하므로, 일부 애플리케이션에서 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]를 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 페이지 소스의 데이터 고립 영역으로 포함하면 불편할 수 있습니다. 따라서 다음 예에서와 같이 외부 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 파일에서 데이터 가져오기도 지원됩니다.  
  
 [!code-xaml[XMLDataSource2#XmlFileExample](~/samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSource2/CS/Window1.xaml#xmlfileexample)]  
  
 @No__t-0 데이터가 원격 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 파일에 있는 경우 다음과 같이 <xref:System.Windows.Data.XmlDataProvider.Source%2A> 특성에 적절 한 URL을 할당 하 여 데이터에 대 한 액세스를 정의 합니다.  
  
```xml  
<XmlDataProvider x:Key="BookData" Source="http://MyUrl" XPath="Books"/>  
```  
  
## <a name="see-also"></a>참조

- <xref:System.Windows.Data.ObjectDataProvider>
- [XDocument, XElement 또는 LINQ for XML 쿼리 결과에 바인딩](how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results.md)
- [계층적 XML 데이터에 마스터-세부 패턴 사용](how-to-use-the-master-detail-pattern-with-hierarchical-xml-data.md)
- [바인딩 소스 개요](binding-sources-overview.md)
- [데이터 바인딩 개요](data-binding-overview.md)
- [방법 항목](data-binding-how-to-topics.md)
