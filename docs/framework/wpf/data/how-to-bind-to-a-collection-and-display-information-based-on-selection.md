---
title: '방법: 선택 영역에 따라 컬렉션 및 표시 정보에 바인딩'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data collections [WPF], selecting data for views
- data binding [WPF], creating views of data collections
- data binding [WPF], selecting data for views
- data binding [WPF], binding to collections
ms.assetid: 952a7d76-dd29-49e5-86f5-32c4530e70eb
ms.openlocfilehash: bb7d4c89e63982a3052857dcb50d04d36d9517dd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61967947"
---
# <a name="how-to-bind-to-a-collection-and-display-information-based-on-selection"></a>방법: 선택 영역에 따라 컬렉션 및 표시 정보에 바인딩
간단한 마스터-세부 시나리오에 데이터 바인딩된 <xref:System.Windows.Controls.ItemsControl> 와 같은 <xref:System.Windows.Controls.ListBox>합니다. 선택한 항목에 대 한 자세한 정보를 표시할 사용자 선택에 따라 있습니다. 이 예제에서는이 시나리오를 구현 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 이 예에서 `People` 되는 <xref:System.Collections.ObjectModel.ObservableCollection%601> 의 `Person` 클래스입니다. 이 `Person` 클래스에는 세 가지 속성이 포함: `FirstName`, `LastName`, 및 `HomeTown`, 모든 형식의 `string`합니다.  
  
 [!code-xaml[CollectionBinding#Source](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#source)]  
[!code-xaml[CollectionBinding#UI](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#ui)]  
  
 합니다 <xref:System.Windows.Controls.ContentControl> 다음을 사용 하 여 <xref:System.Windows.DataTemplate> 정의 하는 방법의 정보를는 `Person` 표시 됩니다:  
  
 [!code-xaml[CollectionBinding#DetailTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#detailtemplate)]  
  
 다음은 예제에서 생성 하는 스크린샷입니다. <xref:System.Windows.Controls.ContentControl> 선택한 사용자의 다른 속성을 보여 줍니다.  
  
 ![컬렉션에 바인딩](./media/databinding-collectionbindingsample.png "DataBinding_CollectionBindingSample")  
  
 이 예제에서 주의 해야 할 두 가지 사항은 다음과 같습니다.  
  
1. 합니다 <xref:System.Windows.Controls.ListBox> 하며 <xref:System.Windows.Controls.ContentControl> 동일한 소스에 바인딩합니다. <xref:System.Windows.Data.Binding.Path%2A> 두 바인딩은 모두의 속성에는 두 컨트롤의 전체 컬렉션 개체에 바인딩하는 때문에 지정 되지 않은 합니다.  
  
2. 설정 해야 합니다 <xref:System.Windows.Controls.Primitives.Selector.IsSynchronizedWithCurrentItem%2A> 속성을 `true` 이 작업을 수행 하려면. 이 속성을 설정 하면 선택한 항목으로 항상 설정 되어 있는지를 <xref:System.Windows.Controls.ItemCollection.CurrentItem%2A>입니다. 또는 경우는 <xref:System.Windows.Controls.ListBox> 에서 데이터를 가져오는 <xref:System.Windows.Data.CollectionViewSource>, 선택 및 통화 자동으로 동기화 합니다.  
  
 합니다 `Person` 재정의 클래스를 `ToString` 메서드는 다음과 같이 합니다. 기본적으로 <xref:System.Windows.Controls.ListBox> 호출 `ToString` 바인딩된 컬렉션에 있는 각 개체의 문자열 표현을 표시 합니다. 이유는 각 `Person` 첫 번째 이름으로 표시 되는 <xref:System.Windows.Controls.ListBox>합니다.  
  
 [!code-csharp[CollectionBinding#ToString](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Data.cs#tostring)]
 [!code-vb[CollectionBinding#ToString](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CollectionBinding/VisualBasic/Person.vb#tostring)]  
  
## <a name="see-also"></a>참고자료

- [계층적 데이터에 마스터-세부 패턴 사용](how-to-use-the-master-detail-pattern-with-hierarchical-data.md)
- [계층적 XML 데이터에 마스터-세부 패턴 사용](how-to-use-the-master-detail-pattern-with-hierarchical-xml-data.md)
- [데이터 바인딩 개요](data-binding-overview.md)
- [데이터 템플릿 개요](data-templating-overview.md)
- [방법 항목](data-binding-how-to-topics.md)
