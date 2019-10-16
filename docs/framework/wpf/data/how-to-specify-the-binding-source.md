---
title: '방법: 바인딩 소스 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- binding data [WPF], binding sources
- data binding [WPF], binding source
- binding sources [WPF]
ms.assetid: 55d47757-2648-4a52-987f-b767953f168c
ms.openlocfilehash: 418dc77ce7638698d4850b06dafcea57787e1015
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69959695"
---
# <a name="how-to-specify-the-binding-source"></a>방법: 바인딩 소스 지정
데이터 바인딩에서 바인딩 소스 개체는 데이터를 가져온 개체를 참조합니다. 이 항목에서는 바인딩 소스를 지정하는 여러 가지 방법을 설명합니다.  
  
## <a name="example"></a>예제  
 하나의 공용 소스에 여러 개의 속성을 바인딩하는 경우 `DataContext` 속성을 사용할 수 있습니다. 이 속성은 모든 데이터 바인딩된 속성이 공용 소스를 상속받게 되는 범위를 설정하는 편리한 방법을 제공합니다.  
  
 다음 예제에서 데이터 컨텍스트는 애플리케이션의 루트 요소에 설정됩니다. 따라서 모든 자식 요소가 해당 데이터 컨텍스트를 상속받을 수 있습니다. 바인딩할 데이터는 사용자 지정 데이터 클래스, 즉 매핑과 `incomeDataSource`의 지정한 리소스 키를 통해 직접 참조되는 `NetIncome`에서 옵니다.  
  
 [!code-xaml[DirectionalBinding#DataContext1](~/samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml#datacontext1)]  
[!code-xaml[DirectionalBinding#DataContext2](~/samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml#datacontext2)]  
  
 다음 예제에서는 `NetIncome` 클래스의 정의를 보여 줍니다.  
  
 [!code-csharp[DirectionalBinding#DataObject](~/samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/billsdata.cs#dataobject)]
 [!code-vb[DirectionalBinding#DataObject](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DirectionalBinding/VisualBasic/NetIncome.vb#dataobject)]  
  
> [!NOTE]
> 위의 예제는 태그에서 개체를 인스턴스화하며 개체를 리소스로 사용합니다. 코드에서 이미 인스턴스화된 개체에 바인딩하려는 경우 `DataContext` 속성을 프로그래밍 방식으로 설정해야 합니다. 예제는 [XAML의 바인딩에 사용할 수 있는 데이터 만들기](how-to-make-data-available-for-binding-in-xaml.md)를 참조하세요.  
  
 또는 개별 바인딩에서 소스를 명시적으로 지정하려는 경우 다음 옵션을 사용할 수 있습니다. 이러한 옵션은 상속된 데이터 컨텍스트보다 우선합니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Windows.Data.Binding.Source%2A>|이 속성을 사용하여 소스를 개체의 인스턴스로 설정합니다. 범위를 설정 하는 기능을 수행 해야 하는 경우 동일한 데이터 컨텍스트를 상속 하는 몇 가지 속성, 사용할 수는 <xref:System.Windows.Data.Binding.Source%2A> 속성 대신는 `DataContext` 속성입니다. 자세한 내용은 <xref:System.Windows.Data.Binding.Source%2A>을 참조하세요.|  
|<xref:System.Windows.Data.Binding.RelativeSource%2A>|이는 바인딩 대상이 있는 위치와 상대적인 소스를 지정할 때 유용합니다. 이 속성을 사용할 수 있는 몇 가지 일반 시나리오 중 요소의 한 속성을 같은 요소의 다른 속성에 바인딩하거나 스타일 또는 템플릿에서 바인딩을 정의하는 경우가 이에 해당합니다. 자세한 내용은 <xref:System.Windows.Data.Binding.RelativeSource%2A>을 참조하세요.|  
|<xref:System.Windows.Data.Binding.ElementName%2A>|바인딩할 요소를 나타내는 문자열을 지정합니다. 이는 애플리케이션에서 다른 요소의 속성에 바인딩하려고 할 때 유용합니다. 예를 들어 사용 하려는 경우를 <xref:System.Windows.Controls.Slider> 애플리케이션에서 다른 컨트롤의 높이 제어 하 바인딩하려는 경우 또는 <xref:System.Windows.Controls.ContentControl.Content%2A> 컨트롤을 <xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A> 의 속성에 <xref:System.Windows.Controls.ListBox> 컨트롤. 자세한 내용은 <xref:System.Windows.Data.Binding.ElementName%2A>을 참조하세요.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.FrameworkElement.DataContext%2A?displayProperty=nameWithType>
- <xref:System.Windows.FrameworkContentElement.DataContext%2A?displayProperty=nameWithType>
- [속성 값 상속](../advanced/property-value-inheritance.md)
- [데이터 바인딩 개요](data-binding-overview.md)
- [바인딩 선언 개요](binding-declarations-overview.md)
- [방법 항목](data-binding-how-to-topics.md)
