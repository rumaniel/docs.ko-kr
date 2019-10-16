---
title: 끌어서 놓기 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- drag-and-drop [WPF], implementing
- drag sources [WPF], drag-and-drop
- data transfer [WPF], drag-and-drop
- drag-and-drop [WPF], about
- drag-and-drop [WPF], events
- drop targets [WPF], drag-and-drop
ms.assetid: 1a5b27b0-0ac5-4cdf-86c0-86ac0271fa64
ms.openlocfilehash: 72dc443e5653b9871c3f67b003bd1af0536d5993
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291479"
---
# <a name="drag-and-drop-overview"></a>끌어서 놓기 개요
이 항목에서는 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 애플리케이션의 끌어서 놓기 지원에 대해 개괄적으로 설명합니다. 끌어서 놓기는 일반적으로 마우스(또는 다른 포인팅 디바이스)를 사용하여 하나 이상의 개체를 선택하고 이러한 개체를 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]에서 원하는 놓기 대상 위로 끌어서 놓는 데이터 전송 방법을 가리킵니다.  

<a name="Drag_and_Drop_Support"></a>   
## <a name="drag-and-drop-support-in-wpf"></a>WPF의 끌어서 놓기 지원  
 끌어서 놓기 작업은 일반적으로 끌어온 개체가 시작되는 끌기 소스와 놓은 개체를 받는 놓기 대상의 두 부분으로 이루어집니다.  끌기 소스와 놓기 대상은 동일한 애플리케이션이나 다른 애플리케이션의 UI 요소일 수 있습니다.  
  
 끌어서 놓기로 조작할 수 있는 개체의 유형과 개수는 완전히 임의로 지정됩니다. 예를 들어 파일, 폴더 및 선택한 콘텐츠는 끌어서 놓기 작업을 통해 조작되는 보다 일반적인 개체 중 일부입니다.  
  
 끌어서 놓기 작업 중 수행되는 특정 작업은 애플리케이션과 관련이 있으며 컨텍스트에 의해 결정되는 경우가 많습니다.  예를 들어 동일한 저장 장치의 한 폴더에서 다른 폴더로 선택 된 파일을 끌어서 놓으면 기본적으로 파일이 이동 하는 반면, UNC (범용 명명 규칙) 공유에서 로컬 폴더로 파일을 끌어서 놓으면 기본적으로 파일이 복사 됩니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 제공하는 끌어서 놓기 기능은 다양한 끌어서 놓기 시나리오를 지원하도록 매우 유연하고 사용자 지정 가능하도록 설계되었습니다.  끌어서 놓기는 단일 응용 프로그램 내에서 또는 서로 다른 응용 프로그램 간에 개체 조작을 지원합니다. @No__t-0 응용 프로그램과 다른 Windows 응용 프로그램 간의 끌어서 놓기도 완전히 지원 됩니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 모든 <xref:System.Windows.UIElement> 또는 <xref:System.Windows.ContentElement>가 끌어서 놓기에 참여할 수 있습니다. 끌어서 놓기 작업에 필요한 이벤트와 메서드는 <xref:System.Windows.DragDrop> 클래스에서 정의됩니다. <xref:System.Windows.UIElement> 또는 <xref:System.Windows.ContentElement>가 기본 요소로 상속될 때 이벤트가 클래스 멤버에 표시되도록 <xref:System.Windows.DragDrop> 및 <xref:System.Windows.UIElement> 클래스에는 <xref:System.Windows.ContentElement> 연결된 이벤트에 대한 별칭이 포함됩니다. 이러한 이벤트에 연결된 이벤트 처리기는 내부 <xref:System.Windows.DragDrop> 연결된 이벤트에 연결되며 동일한 이벤트 데이터 인스턴스를 받습니다. 자세한 내용은 <xref:System.Windows.UIElement.Drop?displayProperty=nameWithType> 이벤트를 참조하세요.  
  
> [!IMPORTANT]
> 인터넷 영역에서는 OLE 끌어서 놓기가 작동하지 않습니다.  
  
<a name="Data_Transfer"></a>   
## <a name="data-transfer"></a>데이터 전송  
 끌어서 놓기는 보다 일반적인 데이터 전송 영역의 일부입니다. 데이터 전송에는 끌어서 놓기 작업과 복사 및 붙여넣기 작업이 포함됩니다. 끌어서 놓기 작업은 시스템 클립보드를 사용하여 개체 또는 애플리케이션 간에 데이터를 전송하는 데 사용되는 복사 및 붙여넣기 작업이나 잘라내기 및 붙여넣기 작업과 비슷합니다. 두 작업 유형에는 모두 다음이 필요합니다.  
  
- 데이터를 제공하는 소스 개체  
  
- 전송된 데이터를 일시적으로 저장하는 방법  
  
- 데이터를 받는 대상 개체  
  
 복사 및 붙여넣기 작업에서는 시스템 클립보드를 사용하여 전송된 데이터를 일시적으로 저장하고, 끌어서 놓기 작업에서는 <xref:System.Windows.DataObject>를 사용하여 데이터를 저장합니다. 개념적으로, 데이터 개체는 실제 데이터를 포함하는 하나 이상의 <xref:System.Object> 쌍과 해당 데이터 형식 식별자로 구성됩니다.  
  
 끌기 소스는 정적 <xref:System.Windows.DragDrop.DoDragDrop%2A?displayProperty=nameWithType> 메서드를 호출하고 전송된 데이터를 전달하여 끌어서 놓기 작업을 시작합니다. <xref:System.Windows.DragDrop.DoDragDrop%2A> 메서드는 필요한 경우 데이터를 자동으로 <xref:System.Windows.DataObject>에 래핑합니다. 데이터 형식을 보다 효율적으로 제어하기 위해 데이터를 <xref:System.Windows.DragDrop.DoDragDrop%2A> 메서드에 전달하기 전에 <xref:System.Windows.DataObject>에 래핑할 수 있습니다. 놓기 대상은 <xref:System.Windows.DataObject>에서 데이터를 추출해야 합니다. 데이터 개체 작업에 대한 자세한 내용은 [데이터 및 데이터 개체](data-and-data-objects.md)를 참조하세요.  
  
 끌어서 놓기 작업의 소스 및 대상은 UI 요소입니다. 그러나 실제로 전송되는 데이터는 일반적으로 시각적 표현이 없습니다. Windows 탐색기에서 파일을 끌 때 발생하는 것과 같이 끌어온 데이터의 시각적 표현을 제공하는 코드를 작성할 수 있습니다. 기본적으로 커서를 변경하여 끌어서 놓기 작업이 데이터에 주는 효과(예: 데이터가 이동 또는 복사되는지 여부)를 나타내 사용자에게 피드백을 제공합니다.  
  
### <a name="drag-and-drop-effects"></a>끌어서 놓기 효과  
 끌어서 놓기 작업은 전송된 데이터에 여러 가지 효과를 줄 수 있습니다. 예를 들어 데이터를 복사하거나 데이터를 이동할 수 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 끌어서 놓기 작업의 효과를 지정하는 데 사용할 수 있는 <xref:System.Windows.DragDropEffects> 열거형을 정의합니다. 끌기 소스의 <xref:System.Windows.DragDrop.DoDragDrop%2A> 메서드에서 소스가 허용하는 효과를 지정할 수 있습니다. 놓기 대상에서 <xref:System.Windows.DragEventArgs.Effects%2A> 클래스의 <xref:System.Windows.DragEventArgs> 속성에 대상의 의도한 효과를 지정할 수 있습니다. <xref:System.Windows.DragDrop.DragOver> 이벤트에 놓기 대상의 의도한 효과를 지정하는 경우 해당 정보가 <xref:System.Windows.DragDrop.GiveFeedback> 이벤트에서 끌기 소스로 다시 전달됩니다. 끌기 소스는 이 정보를 사용하여 놓기 대상이 데이터에 주려는 효과를 사용자에게 알립니다. 데이터를 놓을 때 놓기 대상은 <xref:System.Windows.DragDrop.Drop> 이벤트에 실제 효과를 지정합니다. 해당 정보는 <xref:System.Windows.DragDrop.DoDragDrop%2A> 메서드의 반환 값으로 끌기 소스에 다시 전달됩니다. 놓기 대상이 `allowedEffects`의 끌기 소스 목록에 없는 효과를 반환하는 경우 데이터 전송 없이 끌어서 놓기 작업이 취소됩니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 <xref:System.Windows.DragDropEffects> 값은 끌어서 놓기 작업의 효과와 관련해서 끌기 소스와 놓기 대상 간에 통신을 제공하는 데만 사용됩니다. 끌어서 놓기 작업의 실제 효과는 애플리케이션에서 적절한 코드를 작성하는지에 따라 달라집니다.  
  
 예를 들어 놓기 대상에서 데이터를 놓을 때의 효과를 데이터 이동으로 지정할 수 있습니다. 그러나 데이터를 이동하려면 대상 요소에 추가하고 소스 요소에서 제거해야 합니다. 소스 요소에서 데이터 이동이 허용됨을 나타낼 수도 있지만 소스 요소에서 데이터를 제거하는 코드를 제공하지 않으면 최종 결과로 데이터가 이동되지 않고 복사됩니다.  
  
<a name="Drag_and_Drop_Events"></a>   
## <a name="drag-and-drop-events"></a>끌어서 놓기 이벤트  
 끌어서 놓기 작업은 이벤트 기반 모델을 지원합니다.  끌기 소스와 놓기 대상은 둘 다 표준 이벤트 집합을 사용하여 끌어서 놓기 작업을 처리합니다.  다음 표에는 표준 끌어서 놓기 이벤트가 요약되어 있습니다. 이러한 이벤트는 <xref:System.Windows.DragDrop> 클래스의 연결된 이벤트입니다. 연결된 이벤트에 대한 자세한 내용은 [연결된 이벤트 개요](attached-events-overview.md)를 참조하세요.  
  
### <a name="drag-source-events"></a>끌기 소스 이벤트  
  
|이벤트|요약|  
|-----------|-------------|  
|<xref:System.Windows.DragDrop.GiveFeedback>|이 이벤트는 끌어서 놓기 작업 중에 지속적으로 발생하며 놓기 소스가 피드백 정보를 사용자에게 제공할 수 있게 합니다. 이 피드백은 일반적으로 마우스 포인터 모양 변경을 통해 놓기 대상에서 허용하는 효과를 표시하여 제공됩니다.  이는 버블링 이벤트입니다.|  
|<xref:System.Windows.DragDrop.QueryContinueDrag>|이 이벤트는 끌어서 놓기 작업 중 변경에 키보드 또는 마우스 단추의 상태가 변경될 때 발생하며 놓기 소스가 키/단추 상태에 따라 끌어서 놓기 작업을 취소할 수 있게 합니다. 이는 버블링 이벤트입니다.|  
|<xref:System.Windows.DragDrop.PreviewGiveFeedback>|<xref:System.Windows.DragDrop.GiveFeedback>의 터널링(tunneling) 버전입니다.|  
|<xref:System.Windows.DragDrop.PreviewQueryContinueDrag>|<xref:System.Windows.DragDrop.QueryContinueDrag>의 터널링(tunneling) 버전입니다.|  
  
### <a name="drop-target-events"></a>놓기 대상 이벤트  
  
|이벤트|요약|  
|-----------|-------------|  
|<xref:System.Windows.DragDrop.DragEnter>|이 이벤트는 개체를 놓기 대상의 경계로 끌 때 발생합니다. 이는 버블링 이벤트입니다.|  
|<xref:System.Windows.DragDrop.DragLeave>|이 이벤트는 개체를 놓기 대상의 경계에서 끌 때 발생합니다.  이는 버블링 이벤트입니다.|  
|<xref:System.Windows.DragDrop.DragOver>|이 이벤트는 놓기 대상의 경계 내에서 개체를 끄는(이동하는) 동안 지속적으로 발생합니다. 이는 버블링 이벤트입니다.|  
|<xref:System.Windows.DragDrop.Drop>|이 이벤트는 개체를 놓기 대상에 놓을 때 발생합니다.  이는 버블링 이벤트입니다.|  
|<xref:System.Windows.DragDrop.PreviewDragEnter>|<xref:System.Windows.DragDrop.DragEnter>의 터널링(tunneling) 버전입니다.|  
|<xref:System.Windows.DragDrop.PreviewDragLeave>|<xref:System.Windows.DragDrop.DragLeave>의 터널링(tunneling) 버전입니다.|  
|<xref:System.Windows.DragDrop.PreviewDragOver>|<xref:System.Windows.DragDrop.DragOver>의 터널링(tunneling) 버전입니다.|  
|<xref:System.Windows.DragDrop.PreviewDrop>|<xref:System.Windows.DragDrop.Drop>의 터널링(tunneling) 버전입니다.|  
  
 개체 인스턴스에 대해 끌어서 놓기 이벤트를 처리하려면 앞의 표에 나열된 이벤트에 대한 처리기를 추가합니다. 클래스 수준에서 끌어서 놓기 이벤트를 처리하려면 해당 가상 On*Event 및 On\*PreviewEvent 메서드를 재정의합니다. 자세한 내용은 [컨트롤 기본 클래스를 통해 라우트된 이벤트의 클래스 처리](marking-routed-events-as-handled-and-class-handling.md#Class_Handling_of_Routed_Events)를 참조하세요.  
  
<a name="Implementing_Drag_And_Drop"></a>   
## <a name="implementing-drag-and-drop"></a>끌어서 놓기 구현  
 UI 요소는 끌기 소스, 놓기 대상 또는 둘 다일 수 있습니다. 기본 끌어서 놓기를 구현하려면 끌어서 놓기 작업을 시작하고 놓은 데이터를 처리하는 코드를 작성합니다. 선택적 끌어서 놓기 이벤트를 처리하여 끌어서 놓기 경험을 향상시킬 수 있습니다.  
  
 기본 끌어서 놓기를 구현하려면 다음 작업을 완료합니다.  
  
- 끌기 소스가 될 요소를 식별합니다. 끌기 소스는 <xref:System.Windows.UIElement> 또는 <xref:System.Windows.ContentElement>일 수 있습니다.  
  
- 끌어서 놓기 작업을 시작할 끌기 소스에 이벤트 처리기를 만듭니다. 이벤트는 일반적으로 <xref:System.Windows.UIElement.MouseMove> 이벤트입니다.  
  
- 끌기 소스 이벤트 처리기에서 <xref:System.Windows.DragDrop.DoDragDrop%2A> 메서드를 호출하여 끌어서 놓기 작업을 시작합니다. <xref:System.Windows.DragDrop.DoDragDrop%2A> 호출에서 끌기 소스, 전송할 데이터 및 허용되는 효과를 지정합니다.  
  
- 놓기 대상이 될 요소를 식별합니다. 놓기 대상은 <xref:System.Windows.UIElement> 또는 <xref:System.Windows.ContentElement>일 수 있습니다.  
  
- 놓기 대상에서 <xref:System.Windows.UIElement.AllowDrop%2A> 속성을 `true`로 설정합니다.  
  
- 놓기 대상에서 <xref:System.Windows.DragDrop.Drop> 이벤트 처리기를 만들어 놓은 데이터를 처리합니다.  
  
- <xref:System.Windows.DragDrop.Drop> 이벤트 처리기에서 <xref:System.Windows.DragEventArgs> 및 <xref:System.Windows.DataObject.GetDataPresent%2A> 메서드를 사용하여 <xref:System.Windows.DataObject.GetData%2A>에서 데이터를 추출합니다.  
  
- <xref:System.Windows.DragDrop.Drop> 이벤트 처리기에서 데이터를 사용하여 원하는 끌어서 놓기 작업을 수행합니다.  
  
 사용자 지정 <xref:System.Windows.DataObject>를 만들고 다음 작업과 같이 선택적 끌기 소스 및 놓기 대상 이벤트를 처리하여 끌어서 놓기 구현을 향상시킬 수 있습니다.  
  
- 사용자 지정 데이터 또는 여러 데이터 항목을 전송하려면 <xref:System.Windows.DataObject> 메서드에 전달할 <xref:System.Windows.DragDrop.DoDragDrop%2A>를 만듭니다.  
  
- 끌기 중 추가 작업을 수행하려면 놓기 대상에서 <xref:System.Windows.DragDrop.DragEnter>, <xref:System.Windows.DragDrop.DragOver> 및 <xref:System.Windows.DragDrop.DragLeave> 이벤트를 처리합니다.  
  
- 마우스 포인터의 모양을 변경하려면 끌기 소스에서 <xref:System.Windows.DragDrop.GiveFeedback> 이벤트를 처리합니다.  
  
- 끌어서 놓기 작업을 취소하는 방법을 변경하려면 끌기 소스에서 <xref:System.Windows.DragDrop.QueryContinueDrag> 이벤트를 처리합니다.  
  
<a name="Drag_And_Drop_Example"></a>   
## <a name="drag-and-drop-example"></a>끌어서 놓기 예제  
 이 섹션에서는 <xref:System.Windows.Shapes.Ellipse> 요소에 대해 끌어서 놓기를 구현하는 방법을 설명합니다. <xref:System.Windows.Shapes.Ellipse>는 끌기 소스인 동시에 놓기 대상입니다. 전송된 데이터는 타원의 <xref:System.Windows.Shapes.Shape.Fill%2A> 속성에 대한 문자열 표현입니다. 다음 XAML은 <xref:System.Windows.Shapes.Ellipse> 요소 및 이 요소가 처리하는 끌어서 놓기 관련 이벤트를 보여 줍니다. 끌어서 놓기를 구현 하는 방법에 대 한 전체 단계는 [ 연습: 사용자 정의 컨트롤에서 끌어서 놓기를 사용 하도록 설정 @ no__t-0.  
  
 [!code-xaml[DragDropSnippets#EllipseXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml#ellipsexaml)]  
  
### <a name="enabling-an-element-to-be-a-drag-source"></a>요소를 끌기 소스로 사용할 수 있도록 설정  
 끌기 소스인 개체는 다음 작업을 수행해야 합니다.  
  
- 끌기가 발생하는 시기 식별  
  
- 끌어서 놓기 작업 시작  
  
- 전송할 데이터 식별  
  
- 끌어서 놓기 작업이 전송된 데이터에 미칠 수 있는 효과 지정  
  
 끌기 소스는 허용되는 작업(이동, 복사, 없음)과 관련된 피드백을 사용자에게 제공할 수도 있으며, 끌기 중 Esc 키를 누르는 것과 같은 추가 사용자 입력에 따라 끌어서 놓기 작업을 취소할 수 있습니다.  
  
 애플리케이션은 끌기가 발생하는 시기를 확인한 다음 <xref:System.Windows.DragDrop.DoDragDrop%2A> 메서드를 호출하여 끌어서 놓기 작업을 시작해야 합니다. 일반적으로 이 시기는 마우스 단추를 누르고 있는 동안 끄는 요소에서 <xref:System.Windows.UIElement.MouseMove> 이벤트가 발생할 때입니다. 다음 예제에서는 <xref:System.Windows.Shapes.Ellipse> 요소의 <xref:System.Windows.UIElement.MouseMove> 이벤트 처리기에서 끌어서 놓기 작업을 시작하여 끌기 소스로 만드는 방법을 보여 줍니다. 전송된 데이터는 타원의 <xref:System.Windows.Shapes.Shape.Fill%2A> 속성에 대한 문자열 표현입니다.  
  
 [!code-csharp[DragDropSnippets#DoDragDrop](~/samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#dodragdrop)]
 [!code-vb[DragDropSnippets#DoDragDrop](~/samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#dodragdrop)]  
  
 <xref:System.Windows.UIElement.MouseMove> 이벤트 처리기 내에서 <xref:System.Windows.DragDrop.DoDragDrop%2A> 메서드를 호출하여 끌어서 놓기 작업을 시작합니다. <xref:System.Windows.DragDrop.DoDragDrop%2A> 메서드는 다음 세 개의 매개 변수를 사용합니다.  
  
- `dragSource` - 전송된 데이터의 소스인 종속성 개체에 대한 참조입니다. 일반적으로 <xref:System.Windows.UIElement.MouseMove> 이벤트의 소스입니다.  
  
- `data` - <xref:System.Windows.DataObject>에 래핑되고 전송된 데이터를 포함하는 개체입니다.  
  
- `allowedEffects` - 끌어서 놓기 작업의 허용되는 효과를 지정하는 <xref:System.Windows.DragDropEffects> 열거형 값 중 하나입니다.  
  
 `data` 매개 변수를 통해 직렬화 가능한 개체를 전달할 수 있습니다. 데이터가 아직 <xref:System.Windows.DataObject>에 래핑되지 않은 경우 자동으로 새 <xref:System.Windows.DataObject>에 래핑됩니다. 여러 데이터 항목을 전달하려면 직접 <xref:System.Windows.DataObject>를 만들어 <xref:System.Windows.DragDrop.DoDragDrop%2A> 메서드에 전달해야 합니다. 자세한 내용은 [데이터 및 데이터 개체](data-and-data-objects.md)를 참조하세요.  
  
 `allowedEffects` 매개 변수는 끌기 소스에서 놓기 대상이 전송된 데이터로 수행할 수 있게 하려는 작업을 지정하는 데 사용됩니다. 끌기 소스에 대한 일반적인 값은 <xref:System.Windows.DragDropEffects.Copy>, <xref:System.Windows.DragDropEffects.Move> 및 <xref:System.Windows.DragDropEffects.All>입니다.  
  
> [!NOTE]
> 놓기 대상은 놓은 데이터에 대한 응답으로 의도한 효과를 지정할 수도 있습니다. 예를 들어 놓기 대상이 놓을 데이터 형식을 인식할 수 없는 경우 허용되는 효과를 <xref:System.Windows.DragDropEffects.None>으로 설정하여 데이터를 거부할 수 있습니다. 일반적으로 이 작업은 해당 <xref:System.Windows.DragDrop.DragOver> 이벤트 처리기에서 수행합니다.  
  
 끌기 소스는 선택적으로 <xref:System.Windows.DragDrop.GiveFeedback> 및 <xref:System.Windows.DragDrop.QueryContinueDrag> 이벤트를 처리할 수 있습니다. 이러한 이벤트에는 이벤트를 처리된 것으로 표시하지 않을 경우 사용되는 기본 처리기가 있습니다. 일반적으로 기본 동작을 특별히 변경해야 하는 경우가 아니면 이 이벤트는 무시됩니다.  
  
 <xref:System.Windows.DragDrop.GiveFeedback> 이벤트는 끌기 소스를 끄는 동안 지속적으로 발생합니다. 이 이벤트에 대한 기본 처리기는 끌기 소스가 유효한 놓기 대상 위에 있는지 여부를 확인합니다. 있을 경우 놓기 대상의 허용되는 효과를 확인합니다. 그런 다음 허용되는 놓기 효과와 관련된 피드백을 최종 사용자에게 제공합니다. 이 작업은 일반적으로 마우스 커서를 놓기 없음, 복사 또는 이동 커서로 변경하여 수행됩니다. 사용자 지정 커서를 통해 사용자에게 피드백을 제공해야 하는 경우에만 이 이벤트를 처리해야 합니다. 이 이벤트를 처리하는 경우 기본 처리기가 해당 처리기를 재정의하지 않도록 이벤트를 처리된 것으로 표시해야 합니다.  
  
 <xref:System.Windows.DragDrop.QueryContinueDrag> 이벤트는 끌기 소스를 끄는 동안 지속적으로 발생합니다. 이 이벤트를 처리하여 Esc, Shift, Ctrl 및 Alt 키의 상태에 따라 끌어서 놓기 작업을 종료하는 작업 및 마우스 단추의 상태를 확인할 수 있습니다. 이 이벤트에 대한 기본 처리기는 Esc 키를 누를 경우 끌어서 놓기 작업을 취소하고 마우스 단추를 놓을 경우 데이터를 놓습니다.  
  
> [!CAUTION]
> 이러한 이벤트는 끌어서 놓기 작업 중에 지속적으로 발생합니다. 따라서 리소스를 많이 사용하는 작업은 이벤트 처리기에서 피해야 합니다.  예를 들어 <xref:System.Windows.DragDrop.GiveFeedback> 이벤트가 발생할 때마다 새 커서를 만드는 대신 캐시된 커서를 사용합니다.  
  
### <a name="enabling-an-element-to-be-a-drop-target"></a>요소를 놓기 대상으로 사용할 수 있도록 설정  
 놓기 대상인 개체는 다음 작업을 수행해야 합니다.  
  
- 유효한 놓기 대상으로 지정  
  
- 대상 위로 끌 때 끌기 소스에 응답  
  
- 전송된 데이터가 받을 수 있는 형식인지 확인  
  
- 놓인 데이터 처리  
  
 요소를 놓기 대상으로 지정하려면 해당 <xref:System.Windows.UIElement.AllowDrop%2A> 속성을 `true`로 설정합니다. 그러면 요소에서 놓기 대상 이벤트가 발생하여 처리할 수 있습니다. 끌어서 놓기 작업 중에 다음 이벤트 시퀀스가 놓기 대상에서 발생합니다.  
  
1. <xref:System.Windows.DragDrop.DragEnter>  
  
2. <xref:System.Windows.DragDrop.DragOver>  
  
3. <xref:System.Windows.DragDrop.DragLeave> 또는 <xref:System.Windows.DragDrop.Drop>  
  
 <xref:System.Windows.DragDrop.DragEnter> 이벤트는 데이터를 놓기 대상의 경계로 끌 때 발생합니다. 응용 프로그램에 적절한 경우 일반적으로 이 이벤트를 처리하여 끌어서 놓기 작업의 효과 미리 보기를 제공합니다. <xref:System.Windows.DragDrop.DragEnter> 이벤트에서 <xref:System.Windows.DragEventArgs.Effects%2A?displayProperty=nameWithType> 속성을 설정하지 마세요. <xref:System.Windows.DragDrop.DragOver> 이벤트를 덮어쓰게 됩니다.  
  
 다음 예제에서는 <xref:System.Windows.Shapes.Ellipse> 요소에 대한 <xref:System.Windows.DragDrop.DragEnter> 이벤트 처리기를 보여 줍니다. 이 코드는 현재 <xref:System.Windows.Shapes.Shape.Fill%2A> 브러시를 저장하여 끌어서 놓기 작업의 효과를 미리 봅니다. 그런 다음 <xref:System.Windows.DataObject.GetDataPresent%2A> 메서드를 사용하여 타원 위로 끄는 <xref:System.Windows.DataObject>에 <xref:System.Windows.Media.Brush>로 변환될 수 있는 문자열 데이터가 포함되어 있는지 여부를 확인합니다. 포함되어 있는 경우 <xref:System.Windows.DataObject.GetData%2A> 메서드를 사용하여 데이터가 추출됩니다. 그런 다음 <xref:System.Windows.Media.Brush>로 변환되어 타원에 적용됩니다. 변경 내용이 <xref:System.Windows.DragDrop.DragLeave> 이벤트 처리기에서 취소됩니다. 데이터를 <xref:System.Windows.Media.Brush>로 변환할 수 없는 경우 아무 작업도 수행되지 않습니다.  
  
 [!code-csharp[DragDropSnippets#DragEnter](~/samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#dragenter)]
 [!code-vb[DragDropSnippets#DragEnter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#dragenter)]  
  
 <xref:System.Windows.DragDrop.DragOver> 이벤트는 데이터를 놓기 대상 위로 끄는 동안 지속적으로 발생합니다. 이 이벤트는 끌기 소스의 <xref:System.Windows.DragDrop.GiveFeedback> 이벤트와 쌍을 이룹니다. <xref:System.Windows.DragDrop.DragOver> 이벤트 처리기에서 일반적으로 <xref:System.Windows.DataObject.GetDataPresent%2A> 및 <xref:System.Windows.DataObject.GetData%2A> 메서드를 사용하여 전송된 데이터가 놓기 대상에서 처리할 수 있는 형식인지 여부를 확인합니다. 보조키를 눌렀는지 여부를 확인할 수도 있습니다. 이는 일반적으로 사용자가 이동 또는 복사 작업을 의도하는지를 나타냅니다. 이러한 검사가 수행된 후 <xref:System.Windows.DragEventArgs.Effects%2A?displayProperty=nameWithType> 속성을 설정하여 끌기 소스에 데이터를 놓을 때의 효과를 알립니다. 끌기 소스는 <xref:System.Windows.DragDrop.GiveFeedback> 이벤트 인수를 통해 이 정보를 받으며, 적절한 커서를 설정하여 사용자에게 피드백을 제공할 수 있습니다.  
  
 다음 예제에서는 <xref:System.Windows.Shapes.Ellipse> 요소에 대한 <xref:System.Windows.DragDrop.DragOver> 이벤트 처리기를 보여 줍니다. 이 코드는 타원 위로 끄는 <xref:System.Windows.DataObject>에 <xref:System.Windows.Media.Brush>로 변환될 수 있는 문자열 데이터가 포함되어 있는지 여부를 확인합니다. 포함되어 있는 경우 <xref:System.Windows.DragEventArgs.Effects%2A?displayProperty=nameWithType> 속성을 <xref:System.Windows.DragDropEffects.Copy>로 설정합니다. 이는 데이터를 타원에 복사할 수 있음을 끌기 소스에 나타냅니다. 데이터를 <xref:System.Windows.Media.Brush>로 변환할 수 없는 경우 <xref:System.Windows.DragEventArgs.Effects%2A?displayProperty=nameWithType> 속성이 <xref:System.Windows.DragDropEffects.None>으로 설정됩니다. 이는 타원이 데이터에 유효한 놓기 대상이 아님을 끌기 소스에 나타냅니다.  
  
 [!code-csharp[DragDropSnippets#DragOver](~/samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#dragover)]
 [!code-vb[DragDropSnippets#DragOver](~/samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#dragover)]  
  
 <xref:System.Windows.DragDrop.DragLeave> 이벤트는 데이터를 놓지 않고 대상의 경계에서 끌 때 발생합니다. 이 이벤트를 처리하여 <xref:System.Windows.DragDrop.DragEnter> 이벤트 처리기에서 수행한 작업을 모두 실행 취소합니다.  
  
 다음 예제에서는 <xref:System.Windows.Shapes.Ellipse> 요소에 대한 <xref:System.Windows.DragDrop.DragLeave> 이벤트 처리기를 보여 줍니다. 이 코드는 저장된 <xref:System.Windows.Media.Brush>를 타원에 적용하여 <xref:System.Windows.DragDrop.DragEnter> 이벤트 처리기에서 수행된 미리 보기를 실행 취소합니다.  
  
 [!code-csharp[DragDropSnippets#DragLeave](~/samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#dragleave)]
 [!code-vb[DragDropSnippets#DragLeave](~/samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#dragleave)]  
  
 <xref:System.Windows.DragDrop.Drop> 이벤트는 놓기 대상 위에 데이터를 놓을 때 발생합니다. 기본적으로 이 이벤트는 마우스 단추를 놓을 때 발생합니다. <xref:System.Windows.DragDrop.Drop> 이벤트 처리기에서 <xref:System.Windows.DataObject.GetData%2A> 메서드를 사용하여 <xref:System.Windows.DataObject>에서 전송된 데이터를 추출하고 애플리케이션에 필요한 데이터 처리를 모두 수행합니다. <xref:System.Windows.DragDrop.Drop> 이벤트는 끌어서 놓기 작업을 종료합니다.  
  
 다음 예제에서는 <xref:System.Windows.Shapes.Ellipse> 요소에 대한 <xref:System.Windows.DragDrop.Drop> 이벤트 처리기를 보여 줍니다. 이 코드는 끌어서 놓기 작업의 효과를 적용하며 <xref:System.Windows.DragDrop.DragEnter> 이벤트 처리기의 코드와 비슷합니다. 타원 위로 끄는 <xref:System.Windows.DataObject>에 <xref:System.Windows.Media.Brush>로 변환될 수 있는 문자열 데이터가 포함되어 있는지 여부를 확인합니다. 포함되어 있는 경우 <xref:System.Windows.Media.Brush>가 타원에 적용됩니다. 데이터를 <xref:System.Windows.Media.Brush>로 변환할 수 없는 경우 아무 작업도 수행되지 않습니다.  
  
 [!code-csharp[DragDropSnippets#Drop](~/samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#drop)]
 [!code-vb[DragDropSnippets#Drop](~/samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#drop)]  
  
## <a name="see-also"></a>참조

- <xref:System.Windows.Clipboard>
- [연습: 사용자 정의 컨트롤에서 끌어서 놓기 사용 @ no__t-0
- [방법 항목](drag-and-drop-how-to-topics.md)
- [끌어서 놓기](drag-and-drop.md)
