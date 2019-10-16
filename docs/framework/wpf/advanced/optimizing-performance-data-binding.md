---
title: '성능 최적화: 데이터 바인딩'
ms.date: 03/30/2017
helpviewer_keywords:
- binding data [WPF], performance
- data binding [WPF], performance
ms.assetid: 1506a35d-c009-43db-9f1e-4e230ad5be73
ms.openlocfilehash: 25c0906e9f23948476732b10b2c5fb10fe4eb55f
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68401459"
---
# <a name="optimizing-performance-data-binding"></a>성능 최적화: 데이터 바인딩
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 데이터 바인딩은 응용 프로그램이 데이터를 제공하고 상호 작용할 수 있는 간단하고 일관된 방법을 제공합니다. 요소는 다양 한 데이터 소스의 데이터에 CLR 개체 및 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)]형식의 데이터에 바인딩될 수 있습니다.  
  
 이 항목에서는 데이터 바인딩과 관련된 성능 권장 사항을 제공합니다.  

<a name="HowDataBindingReferencesAreResolved"></a>   
## <a name="how-data-binding-references-are-resolved"></a>데이터 바인딩 참조를 확인하는 방법  
 데이터 바인딩 성능 문제를 다루기 전에 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 데이터 바인딩 엔진에서 바인딩의 개체 참조를 확인하는 방법을 살펴보는 것이 좋습니다.  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 데이터 바인딩의 소스는 임의의 CLR 개체 일 수 있습니다. CLR 개체의 속성, 하위 속성 또는 인덱서에 바인딩할 수 있습니다. Microsoft .NET Framework 리플렉션 또는를 <xref:System.ComponentModel.ICustomTypeDescriptor>사용 하 여 바인딩 참조를 확인 합니다. 다음은 바인딩의 개체 참조를 확인하는 세 가지 방법입니다.  
  
 첫 번째 방법에서는 리플렉션을 사용합니다. 이 경우 <xref:System.Reflection.PropertyInfo> 개체는 속성의 특성을 검색 하 고 속성 메타 데이터에 대 한 액세스를 제공 하는 데 사용 됩니다. <xref:System.ComponentModel.ICustomTypeDescriptor> 인터페이스를 사용 하는 경우 데이터 바인딩 엔진은이 인터페이스를 사용 하 여 속성 값에 액세스 합니다. 인터페이스 <xref:System.ComponentModel.ICustomTypeDescriptor> 는 개체에 정적 속성 집합이 없는 경우에 특히 유용 합니다.  
  
 인터페이스를 <xref:System.ComponentModel.INotifyPropertyChanged> 구현 하거나 <xref:System.ComponentModel.TypeDescriptor>와 연결 된 변경 알림을 사용 하 여 속성 변경 알림을 제공할 수 있습니다. 그러나 속성 변경 알림을 구현 하는 기본 전략은를 사용 <xref:System.ComponentModel.INotifyPropertyChanged>하는 것입니다.  
  
 원본 개체가 clr 개체이 고 소스 속성이 clr 속성인 경우 데이터 바인딩 엔진은 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 먼저 원본 개체에서 리플렉션을 사용 하 여를 <xref:System.ComponentModel.TypeDescriptor>가져온 다음를 <xref:System.ComponentModel.PropertyDescriptor>쿼리해야 합니다. 이러한 일련의 리플렉션 작업은 너무 많은 시간을 소비할 수 있으므로 성능 면에서 좋지 않습니다.  
  
 개체 참조를 확인 하는 두 번째 방법에는 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스를 구현 하는 clr 소스 개체와 clr 속성인 소스 속성이 포함 됩니다. 이 경우 데이터 바인딩 엔진에서는 소스 형식에 대해 직접 리플렉션을 사용하여 필요한 속성을 가져옵니다. 이 또한 최적의 방법은 아니지만 첫 번째 방법보다 작업 집합 요구 사항이 적어 비용이 적게 듭니다.  
  
 개체 참조를 확인 하는 세 번째 방법에는 인 소스 개체 <xref:System.Windows.DependencyObject> 와 인 소스 속성이 <xref:System.Windows.DependencyProperty>포함 됩니다. 이 경우 데이터 바인딩 엔진에서 리플렉션을 사용할 필요가 없습니다. 대신 속성 엔진과 데이터 바인딩 엔진이 함께 속성 참조를 독립적으로 확인합니다. 이것이 데이터 바인딩에서 사용되는 개체 참조를 확인하는 최적의 방법입니다.  
  
 다음 표에서는 이러한 세 가지 방법을 사용 하 여 <xref:System.Windows.Controls.TextBlock.Text%2A> 1000 <xref:System.Windows.Controls.TextBlock> 요소의 속성에 대 한 데이터 바인딩 속도를 비교 합니다.  
  
|**TextBlock의 Text 속성 바인딩 대상**|**바인딩 시간(ms)**|**렌더링 시간 -- 바인딩 시간 포함(ms)**|  
|--------------------------------------------------|-----------------------------|--------------------------------------------------|  
|CLR 개체의 속성으로|115|314|  
|을 구현 하는 CLR 개체의 속성에<xref:System.ComponentModel.INotifyPropertyChanged>|115|305|  
|의에 대 한입니다. <xref:System.Windows.DependencyObject> <xref:System.Windows.DependencyProperty>|90|263|  
  
<a name="Binding_to_Large_CLR_Objects"></a>   
## <a name="binding-to-large-clr-objects"></a>대형 CLR 개체에 바인딩  
 수천 개의 속성이 있는 단일 CLR 개체에 데이터를 바인딩할 때 성능에 상당한 영향을 줍니다. 단일 개체를 속성이 작은 여러 CLR 개체로 나누면 이러한 영향을 최소화할 수 있습니다. 이 표에서는 단일의 작은 CLR 개체와 여러 개의 작은 개체에 대 한 데이터 바인딩의 바인딩 및 렌더링 시간을 보여 줍니다.  
  
|**1000개의 TextBlock 개체 데이터 바인딩 대상**|**바인딩 시간(ms)**|**렌더링 시간 -- 바인딩 시간 포함(ms)**|  
|---------------------------------------------|-----------------------------|--------------------------------------------------|  
|1000 속성이 있는 CLR 개체로|950|1200|  
|하나의 속성을 사용 하는 1000 CLR 개체|115|314|  
  
<a name="Binding_to_an_ItemsSource"></a>   
## <a name="binding-to-an-itemssource"></a>ItemsSource에 바인딩  
 에 표시 하려는 직원 목록이 포함 된 CLR <xref:System.Collections.Generic.List%601> 개체가 있는 시나리오를 고려해 보세요. <xref:System.Windows.Controls.ListBox> 이러한 두 개체 간의 대응을 만들려면 employee 목록을 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> <xref:System.Windows.Controls.ListBox>의 속성에 바인딩합니다. 그런데 그룹에 새 직원이 가입했다고 가정합니다. 이 새 사용자를 바인딩된 <xref:System.Windows.Controls.ListBox> 값에 삽입 하기 위해이 사용자를 직원 목록에 추가 하 고이 변경 내용이 데이터 바인딩 엔진에서 자동으로 인식 될 것으로 예상 합니다. 이 가정에서는 false를 증명 합니다. 실제로 변경 내용은에 <xref:System.Windows.Controls.ListBox> 자동으로 반영 되지 않습니다. 이는 CLR <xref:System.Collections.Generic.List%601> 개체가 컬렉션 변경 이벤트를 자동으로 발생 시 키 지 않기 때문입니다. 에서 <xref:System.Windows.Controls.ListBox> 변경 내용을 가져오도록 하려면 직원 목록을 다시 만든 다음의 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> <xref:System.Windows.Controls.ListBox>속성에 다시 연결 해야 합니다 (). 이 솔루션은 효과는 있지만 성능에 큰 영향을 줍니다. <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 의 <xref:System.Windows.Controls.ListBox> 를 새 개체에 재할당할 때마다 첫 번째는 이전 항목을 throw 하 고 전체 목록을 다시 생성 합니다. <xref:System.Windows.Controls.ListBox> 가 복잡 <xref:System.Windows.Controls.ListBox> <xref:System.Windows.DataTemplate>하 게 매핑되면 성능 영향이 확대 됩니다.  
  
 이 문제에 대 한 매우 효율적인 해결책은 직원 목록을 <xref:System.Collections.ObjectModel.ObservableCollection%601>으로 만드는 것입니다. 개체 <xref:System.Collections.ObjectModel.ObservableCollection%601> 는 데이터 바인딩 엔진이 받을 수 있는 변경 알림을 발생 시킵니다. 이벤트는 전체 목록을 다시 생성할 필요 <xref:System.Windows.Controls.ItemsControl> 없이에서 항목을 추가 하거나 제거 합니다.  
  
 다음 표에서는 한 항목을 추가할 때를 <xref:System.Windows.Controls.ListBox> 업데이트 하는 데 걸리는 시간을 보여 줍니다 (UI 가상화가 꺼져 있음). 첫 번째 행의 숫자는 CLR <xref:System.Collections.Generic.List%601> 개체가 요소의 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>에 <xref:System.Windows.Controls.ListBox> 바인딩되는 경과 시간을 나타냅니다. 두 번째 행의 숫자는 <xref:System.Collections.ObjectModel.ObservableCollection%601> 가 <xref:System.Windows.Controls.ListBox> 요소의 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>에 바인딩될 때 경과 된 시간을 나타냅니다. 데이터 바인딩 전략을 <xref:System.Collections.ObjectModel.ObservableCollection%601> 사용 하 여 상당한 시간 절약 효과를 확인 합니다.  
  
|**ItemsSource 데이터 바인딩 대상**|**1개 항목의 업데이트 시간(ms)**|  
|--------------------------------------|---------------------------------------|  
|CLR <xref:System.Collections.Generic.List%601> 개체로|1656|  
|로<xref:System.Collections.ObjectModel.ObservableCollection%601>|20|  
  
<a name="Binding_IList_to_ItemsControl_not_IEnumerable"></a>   
## <a name="bind-ilist-to-itemscontrol-not-ienumerable"></a>IList를 IEnumerable이 아닌 ItemsControl에 바인딩  
 <xref:System.Collections.Generic.IList%601> <xref:System.Collections.Generic.IList%601> 개체 에<xref:System.Collections.IEnumerable> 또는을 바인딩하는 중 하나를 선택 하는 경우 개체를 선택 합니다. <xref:System.Windows.Controls.ItemsControl> 에 바인딩하여 <xref:System.Collections.IEnumerable> 래퍼<xref:System.Collections.Generic.IList%601> 개체를 만들게 됩니다. 즉, 성능이 두 번째 개체의 불필요 한 오버 헤드로 인해 영향을 받습니다. <xref:System.Windows.Controls.ItemsControl> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]  
  
<a name="Do_not_Convert_CLR_objects_to_Xml_Just_For_Data_Binding"></a>   
## <a name="do-not-convert-clr-objects-to-xml-just-for-data-binding"></a>데이터 바인딩만을 위해 CLR 개체를 XML로 변환 안 함  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]내용에 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 데이터를 바인딩할 수 있지만 내용에 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 대 한 데이터 바인딩은 CLR 개체에 대 한 데이터 바인딩에 비해 속도가 느립니다. 데이터 바인딩을 위한 유일한 용도 이면 CLR 개체 데이터를 XML로 변환 하지 마십시오.  
  
## <a name="see-also"></a>참고자료

- [WPF 응용 프로그램 성능 최적화](optimizing-wpf-application-performance.md)
- [애플리케이션 성능 계획](planning-for-application-performance.md)
- [하드웨어 이용](optimizing-performance-taking-advantage-of-hardware.md)
- [레이아웃 및 디자인](optimizing-performance-layout-and-design.md)
- [2차원 그래픽 및 이미징](optimizing-performance-2d-graphics-and-imaging.md)
- [개체 동작](optimizing-performance-object-behavior.md)
- [애플리케이션 리소스](optimizing-performance-application-resources.md)
- [텍스트](optimizing-performance-text.md)
- [기타 성능 권장 사항](optimizing-performance-other-recommendations.md)
- [데이터 바인딩 개요](../data/data-binding-overview.md)
- [연습: WPF 응용 프로그램에서 응용 프로그램 데이터 캐싱](walkthrough-caching-application-data-in-a-wpf-application.md)
