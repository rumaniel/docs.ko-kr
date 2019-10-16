---
title: '방법: XAML에서 바인딩에 사용할 수 있는 데이터 만들기'
ms.date: 01/29/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], making data available for binding
- binding data [WPF], making data available for
ms.assetid: 7103c2e8-0e31-4a13-bf12-ca382221a8d5
ms.openlocfilehash: 3487a160cc49ab6b779a20157668915c2da33900
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68401499"
---
# <a name="how-to-make-data-available-for-binding-in-xaml"></a>방법: XAML에서 바인딩에 사용할 수 있는 데이터 만들기
이 항목에서는 응용 프로그램의 요구 사항에 따라에서 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]바인딩에 사용할 수 있는 데이터를 만들 수 있는 다양 한 방법에 대해 설명 합니다.  
  
## <a name="example"></a>예제  
 에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]바인딩할 CLR (공용 언어 런타임) 개체를 사용 하는 경우 개체를 바인딩할 수 있도록 하는 한 가지 방법은 해당 개체를 리소스로 정의 하 고 `x:Key`이를에 제공 하는 것입니다. 다음 예제 `Person` 에서는 라는 `PersonName`문자열 속성이 있는 개체가 있습니다. 요소를 `Person` `SDKSample`포함 하는 강조 표시 된 줄의 개체는 라는 네임 스페이스에 정의 됩니다. `<src>`  
  
 [!code-xaml[SimpleBinding#Instantiation](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml?highlight=9,37)]  
  
 그런 다음 `<TextBlock>` 요소를 포함 <xref:System.Windows.Controls.TextBlock> 하는 강조 표시 된 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]줄에 표시 된 대로 컨트롤을의 개체에 바인딩할 수 있습니다. 
  
 또는 다음 예제와 같이 <xref:System.Windows.Data.ObjectDataProvider> 클래스를 사용할 수 있습니다.  
  
 [!code-xaml[ObjectDataProvider}](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Page1.xaml?highlight=10-14,42)]  
  
 `<TextBlock>` 요소를 포함 하는 강조 표시 된 줄에 표시 되는 것과 동일한 방식으로 바인딩을 정의 합니다.  
  
 이 특정 예제에서 결과는 동일 합니다. 텍스트 콘텐츠가 <xref:System.Windows.Controls.TextBlock> `Joe`있는가 있습니다. 그러나 클래스는 <xref:System.Windows.Data.ObjectDataProvider> 메서드의 결과에 바인딩하는 기능과 같은 기능을 제공 합니다. 제공 하는 기능이 필요한 경우 <xref:System.Windows.Data.ObjectDataProvider> 클래스를 사용 하도록 선택할 수 있습니다.  
  
 그러나 이미 생성 된 개체에 바인딩하는 경우에는 다음 예제와 같이 코드 `DataContext` 에서를 설정 해야 합니다.  
  
 [!code-csharp[ADODataSet#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ADODataSet/CSharp/Window1.xaml.cs#1)]
 [!code-vb[ADODataSet#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ADODataSet/VisualBasic/Window1.xaml.vb#1)]  
  
 클래스<xref:System.Windows.Data.XmlDataProvider> 를 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 사용 하 여 바인딩에 대 한 데이터에 액세스 하려면 [xmldataprovider 및 XPath 쿼리를 사용 하 여 XML 데이터에 바인딩](how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)을 참조 하세요. 클래스<xref:System.Windows.Data.ObjectDataProvider> 를 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 사용 하 여 바인딩에 대 한 데이터에 액세스 하려면 [XDocument, XElement 또는 LINQ for XML 쿼리 결과에 바인딩](how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results.md)을 참조 하세요.  
  
 바인딩할 데이터를 지정할 수 있는 여러 가지 방법에 대 한 자세한 내용은 [바인딩 소스 지정](how-to-specify-the-binding-source.md)을 참조 하세요. 바인딩할 수 있는 데이터 형식에 대 한 자세한 내용 또는 바인딩을 위한 고유한 CLR (공용 언어 런타임) 개체를 구현 하는 방법에 대 한 자세한 내용은 [바인딩 소스 개요](binding-sources-overview.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [데이터 바인딩 개요](data-binding-overview.md)
- [방법 항목](data-binding-how-to-topics.md)
