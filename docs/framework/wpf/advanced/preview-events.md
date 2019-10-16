---
title: 미리 보기 이벤트
ms.date: 03/30/2017
helpviewer_keywords:
- Preview events [WPF]
- suppressing events [WPF]
- events [WPF], Preview
- events [WPF], suppressing
ms.assetid: b5032308-aa9c-4d02-af11-630ecec8df7e
ms.openlocfilehash: 75165df94aa8b508ef85cf970933efb98b9d62ca
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61772881"
---
# <a name="preview-events"></a>미리 보기 이벤트
터널링 이벤트, 라고도 미리 보기 이벤트는 라우트된 이벤트에서 이벤트를 발생 시킨 및 이벤트 데이터에서 소스로 보고 되는 요소에 대해 응용 프로그램 루트 경로 방향 이동 하는 위치입니다. 일부 이벤트 시나리오를 지원 또는 미리 보기 이벤트; 필요 이 항목에서는 미리 보기 이벤트 있는, 응용 프로그램 또는 구성 요소 처리 하는 방법을 하는 경우 및 사용자 지정 구성 요소 또는 클래스에서 미리 보기 이벤트를 만들 수 있는 적절 한 사례를 설명 합니다.  
  
## <a name="preview-events-and-input"></a>미리 보기 이벤트 및 입력  
 이벤트는 일반적으로 주의 해야 하는 미리 보기를 처리 하는 경우 이벤트를 표시 합니다. 처리 된 이벤트 데이터. 이외의 모든 요소에 대해 미리 보기 이벤트를 처리 (이벤트 데이터의 소스로 보고 되는 요소)이 발생 하는 요소는 효과가 발생 하는 이벤트를 처리 하는 요소를 제공 하지 않는 합니다. 경우에 따라 컨트롤의 합치기 내에서 관계에 해당 요소가 존재 하는 경우에 특히 원하는 결과입니다.  
  
 입력된 이벤트에 대 한 특히 미리 보기 이벤트를 공유할 수도 이벤트 데이터 인스턴스는 해당 하는 버블링 이벤트. 입력된 이벤트를 처리를 표시 하는 미리 보기 이벤트 클래스 처리기를 사용 하는 경우 버블링 입력된 이벤트 클래스 처리기가 호출 되지 않습니다. 또는 미리 보기 이벤트 인스턴스 처리기를 사용 하 여 표시할 이벤트를 처리 하는 경우 버블링 이벤트에 대 한 처리기 일반적으로 호출 되지 않습니다. 클래스 처리기 나 인스턴스 처리기를 등록 또는 기술은 일반적으로 사용 되지 않습니다 하지만 해당 이벤트가 처리 됨으로 표시 됩니다 하는 경우에 호출 될 옵션을 사용 하 여 연결할 수 있습니다.  
  
 한 클래스 처리 및 미리 보기 이벤트의 관계에 대 한 자세한 내용은 참조 [라우트된 이벤트 것으로 표시를 처리 및 클래스 처리](marking-routed-events-as-handled-and-class-handling.md)합니다.  
  
### <a name="working-around-event-suppression-by-controls"></a>컨트롤에서 억제하는 이벤트 문제 해결  
 미리 보기 이벤트 일반적으로 사용 되는 시나리오 중 하나는 입력된 이벤트를 처리할 복합 컨트롤입니다. 경우에 따라 컨트롤의 작성자가 컨트롤에서 자세한 정보를 전달 하거나 더 구체적인 동작 하는 구성 요소에서 정의한 이벤트를 대체 하기 위해 원래에서 특정 이벤트를 표시 하지 않습니다. 예를 들어를 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] <xref:System.Windows.Controls.Button> 를 표시 하지 않습니다 <xref:System.Windows.UIElement.MouseLeftButtonDown> 및 <xref:System.Windows.UIElement.MouseRightButtonDown> 버블링 이벤트에 의해 발생 합니다 <xref:System.Windows.Controls.Button> 또는 마우스를 캡처 및 발생 시키기 위해 복합 요소를 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 에서 항상 발생 시키는 이벤트를 <xref:System.Windows.Controls.Button> 자체입니다. 이벤트 및 해당 데이터 경로 따라 계속 하지만 합니다 <xref:System.Windows.Controls.Button> 이벤트 데이터를 표시 <xref:System.Windows.RoutedEventArgs.Handled%2A>, 명시 다음에서 작동 해야 하는 이벤트 처리기만는 `handledEventsToo` 경우 호출 됩니다.  다른 응용 프로그램의 루트 요소가 컨트롤 억제 이벤트를 처리할 수 있게 하려는, 한 가지 대안은 사용 하 여 코드의 처리기를 연결할 `handledEventsToo` 로 지정 된 `true`합니다. 하지만 미리 보기에 해당 하는 입력된 이벤트를 처리 하는 라우팅 방향을 변경 하려면 더 간단한 방법 표시 되는 경우가 있습니다. 예를 들어 컨트롤에서 억제 하는 경우 <xref:System.Windows.UIElement.MouseLeftButtonDown>에 대 한 처리기를 연결 해 보세요 <xref:System.Windows.UIElement.PreviewMouseLeftButtonDown> 대신 합니다. 이 기술에만 기본 요소 입력된 이벤트와 같은 <xref:System.Windows.UIElement.MouseLeftButtonDown>합니다. 이러한 입력된 이벤트 터널/버블 쌍을 사용 하 여 두 이벤트를 발생 하며 이벤트 데이터를 공유 합니다.  
  
 이러한 각 기법에는 의도 하지 않은 또는 제한 사항 미리 보기 이벤트를 처리 하는 부작용이 버블링 이벤트를 처리 해야 하는 처리기를 비활성화할 수 있습니다 시점 이벤트를 처리 하 고 따라서 제한을는 일반적으로 Previ에 남아 있지만 처리 이벤트를 표시 하는 것이 좋습니다. 활용 하면 초보 부분 경로입니다. 에 대 한 제한 합니다 `handledEventsToo` 지정할 수 없다는 것이 방법은 `handledEventsToo` 처리기에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 특성으로 등록 해야 이벤트 처리기 코드에서 연결 처리기가 있는 요소에 대 한 개체 참조를 가져온 후 합니다.  
  
## <a name="see-also"></a>참고자료

- [라우트된 이벤트를 처리된 것으로 표시 및 클래스 처리](marking-routed-events-as-handled-and-class-handling.md)
- [라우트된 이벤트 개요](routed-events-overview.md)
