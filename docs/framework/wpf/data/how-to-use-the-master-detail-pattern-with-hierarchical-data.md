---
title: '방법: 계층적 데이터에서 마스터-세부 정보 패턴 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- data binding [WPF], Master-Detail data paradigm
- Master-Detail data paradigm
ms.assetid: 11429b9e-058d-4084-bfb6-2cf209c8ddf7
ms.openlocfilehash: e0bbb24b07fdc1c362e2be43d69d189defbc27a4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61931896"
---
# <a name="how-to-use-the-master-detail-pattern-with-hierarchical-data"></a>방법: 계층적 데이터에서 마스터-세부 정보 패턴 사용
이 예제에는 마스터-세부 시나리오를 구현 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 이 예에서 `LeagueList` 컬렉션인 `Leagues`합니다. 각 `League` 에 `Name` 의 컬렉션과 `Divisions`, 및 각 `Division` 에 이름 및 컬렉션 `Teams`합니다. 각 `Team` 팀 이름이 있습니다.  
  
 [!code-xaml[MasterDetail#HowTo1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MasterDetail/VisualBasic/Page1.xaml#howto1)]  
[!code-xaml[MasterDetail#HowTo2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MasterDetail/VisualBasic/Page1.xaml#howto2)]  
  
 예제 스크린샷은 다음과 같습니다. 합니다 `Divisions` <xref:System.Windows.Controls.ListBox> 자동으로 선택 항목을 추적 합니다 `Leagues` <xref:System.Windows.Controls.ListBox> 해당 데이터를 표시 합니다. 합니다 `Teams` <xref:System.Windows.Controls.ListBox> 다른 두에서 선택 항목을 추적 <xref:System.Windows.Controls.ListBox> 컨트롤입니다.  
  
 ![마스터를 보여주는 스크린 샷&#45;세부 정보 시나리오 예제입니다.](./media/how-to-use-the-master-detail-pattern-with-hierarchical-data/databinding-master-detail-scenario.png)  
  
 이 예제에서 주의 해야 할 두 가지 사항은 다음과 같습니다.  
  
1. 세 가지 <xref:System.Windows.Controls.ListBox> 컨트롤 같은 소스에 바인딩합니다. 설정한 합니다 <xref:System.Windows.Data.Binding.Path%2A> 하려는 데이터의 수준을 지정에 대 한 바인딩 속성을 <xref:System.Windows.Controls.ListBox> 표시할 합니다.  
  
2. 설정 해야 합니다는 <xref:System.Windows.Controls.Primitives.Selector.IsSynchronizedWithCurrentItem%2A> 속성을 `true` 에 <xref:System.Windows.Controls.ListBox> 컨트롤의 추적 하는 선택 합니다. 이 속성을 설정 하면 선택한 항목으로 항상 설정 되어 있는지를 <xref:System.Windows.Controls.ItemCollection.CurrentItem%2A>입니다. 또는 경우는 <xref:System.Windows.Controls.ListBox> 에서 데이터를 가져오는 <xref:System.Windows.Data.CollectionViewSource>, 선택 및 통화 자동으로 동기화 합니다.  
  
 때 사용 하는 방법은 약간 다른 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 데이터입니다. 예를 들어 참조 [계층적 XML 데이터에 마스터-세부 패턴 사용](how-to-use-the-master-detail-pattern-with-hierarchical-xml-data.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.HierarchicalDataTemplate>
- [선택에 따라 수집 및 표시 정보에 바인딩](how-to-bind-to-a-collection-and-display-information-based-on-selection.md)
- [데이터 바인딩 개요](data-binding-overview.md)
- [데이터 템플릿 개요](data-templating-overview.md)
- [방법 항목](data-binding-how-to-topics.md)
