---
title: '방법: ContextMenuOpening 이벤트 처리'
ms.date: 03/30/2017
helpviewer_keywords:
- ContextMenuOpening properties [WPF]
ms.assetid: 789652fb-1951-4217-934a-7843e355adf4
ms.openlocfilehash: b3d0f5c77ebf8527e4854d4edf12d6fa8a4b5f0c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614638"
---
# <a name="how-to-handle-the-contextmenuopening-event"></a>방법: ContextMenuOpening 이벤트 처리
합니다 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 는 기존 상황에 맞는 메뉴 표시 하기 전에 설정 하 여 표시 되는 메뉴를 표시 하지 않으려면를 조정 하거나 응용 프로그램에서 이벤트를 처리할 수 있습니다 합니다 <xref:System.Windows.RoutedEventArgs.Handled%2A> 속성을 `true` 이벤트 데이터의 합니다. 설정에 대 한 일반적인 이유 <xref:System.Windows.RoutedEventArgs.Handled%2A> 하 `true` 전적으로 사용 하 여 새 메뉴를 바꾸려면 데이터가 이벤트 <xref:System.Windows.Controls.ContextMenu> 개체, 경우에 따라 요구 하는 작업을 취소 하 고 새로운 열기를 시작 합니다. 에 대 한 처리기를 작성 하는 경우를 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 이벤트 알아야 사이의 타이밍 문제에 대 한 <xref:System.Windows.Controls.ContextMenu> 컨트롤과 열고 일반적 컨트롤에 대 한 상황에 맞는 메뉴의 위치를 지정 하는 일을 담당 하는 서비스. 이 항목에서는 다양 한 상황에 맞는 메뉴 열기 시나리오에 대 한 코드 기술 중 일부를 보여 줍니다 및 타이밍 문제를 고려해 야 하는 있는 경우를 보여 줍니다.  
  
 일부의 시나리오 처리에 대 한는 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 이벤트:  
  
- 메뉴 항목을 먼저 호출한 다음 표시를 조정합니다.  
  
- 표시 하기 전에 전체 메뉴를 대체합니다.  
  
- 완전히 모든 기존 상황에 맞는 메뉴를 표시 안 함 및 없는 상황에 맞는 메뉴를 표시 합니다.  
  
## <a name="example"></a>예제  
  
## <a name="adjusting-the-menu-items-before-display"></a>메뉴 항목을 먼저 호출한 다음 표시를 조정합니다.  
 기존 메뉴 항목을 조정 매우 간단 하 고 가장 일반적인 시나리오 일 것입니다. 에 더하거나 뺄 상황에 맞는 메뉴 또는 상황에 맞는 메뉴를 요청 하는 개체의 속성으로 사용할 수 있는 특정 상태 정보에 응용 프로그램의 현재 상태 정보에 대 한 응답 하기 위해이 수행할 수 있습니다.  
  
 일반적인 방법은 마우스 오른쪽 단추로 클릭는 특정 컨트롤 상태인 이벤트의 소스를 가져오고 가져오는 <xref:System.Windows.FrameworkElement.ContextMenu%2A> 속성을 합니다. 일반적으로 확인 하려는 합니다 <xref:System.Windows.Controls.ItemsControl.Items%2A> 컬렉션을 이미 메뉴에 존재 하 고 다음 추가 하거나 제거 적절 한 새 상황에 맞는 메뉴 항목을 참조 <xref:System.Windows.Controls.MenuItem> 하거나 컬렉션에서 항목입니다.  
  
 [!code-csharp[ContextMenuOpeningHandlers#AddItemNoHandle](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#additemnohandle)]  
  
## <a name="replacing-the-entire-menu-before-display"></a>표시 하기 전에 전체 메뉴를 대체합니다.  
 다른 시나리오는 전체 상황에 맞는 메뉴를 대체 하려는 경우. 물론 위의 코드에서의 변형 기존 상황에 맞는 메뉴의 모든 항목을 제거 하 고 항목 0부터 시작 하는 새 템플릿을 추가할에 사용할 수 있습니다. 새 상황에 맞는 메뉴에서 모든 항목을 바꾸는 보다 직관적인 방법 이지만 <xref:System.Windows.Controls.ContextMenu>항목으로 채울, 설정한 후 합니다 <xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=nameWithType> 속성을 새 컨트롤의 <xref:System.Windows.Controls.ContextMenu>.  
  
 다음은 대체 하는 것에 대 한 간단한 처리기 코드는 <xref:System.Windows.Controls.ContextMenu>합니다. 코드는 사용자 지정 참조 `BuildMenu` 분산 되어 있는 호출 되므로 둘 이상의 예제 처리기 메서드.  
  
 [!code-csharp[ContextMenuOpeningHandlers#ReplaceNoReopen](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#replacenoreopen)]  
  
 [!code-csharp[ContextMenuOpeningHandlers#BuildMenu](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#buildmenu)]  
  
 그러나 이러한 처리기에 대 한이 스타일을 사용 하는 경우 <xref:System.Windows.FrameworkElement.ContextMenuOpening>, 경우 타이밍 문제가 노출 될 가능성이 있습니다 설정 하는 개체는 <xref:System.Windows.Controls.ContextMenu> 기존 상황에 맞는 메뉴가 없습니다. 사용자 컨트롤을 마우스 오른쪽 단추로 클릭할 때 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 발생 하는 경우에 기존 <xref:System.Windows.Controls.ContextMenu> 비어 있거나 null입니다. 하지만 경우에 새 <xref:System.Windows.Controls.ContextMenu> 원본에 설정한 요소 표시할 너무 늦게 도착 합니다. 또한 사용자를 두 번째로 마우스 오른쪽 단추로 클릭 경우 이번 새 <xref:System.Windows.Controls.ContextMenu> 나타나면 값이 null이 아닌 하 고 처리기를 제대로 바꾸고 처리기를 두 번째로 실행 될 때 메뉴를 표시 합니다. 이 두 가지 가능한 해결 방법을 제안합니다.  
  
1. 되도록 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 항상 하나 이상의 자리 표시자 컨트롤에 대해 실행 하는 처리기 <xref:System.Windows.Controls.ContextMenu> 사용 가능한 처리기 코드를 교체 하려고 하는 합니다. 이 경우 이전 예에서 같이 처리기를 여전히 사용할 수 있지만 일반적으로 자리 표시자를 할당 하려는 <xref:System.Windows.Controls.ContextMenu> 초기 태그에서:  
  
     [!code-xaml[ContextMenuOpeningHandlers#XAMLWithInitCM](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml#xamlwithinitcm)]  
  
2. 가정 초기 <xref:System.Windows.Controls.ContextMenu> 값 null 일 수 있음, 일부 예비 논리를 기반으로 합니다. 할 수 있는지 확인 하거나 <xref:System.Windows.Controls.ContextMenu> null 또는 처리기 되었는지 여부를 확인 하는 플래그를 사용 하 여 한 번 이상를 실행 합니다. 한다고 가정 하기 때문에 <xref:System.Windows.Controls.ContextMenu> 다음을 설정 하는 방법에 대 한 수를 표시, 처리기 <xref:System.Windows.RoutedEventArgs.Handled%2A> 에 `true` 이벤트 데이터에서입니다. 에 <xref:System.Windows.Controls.ContextMenuService> 상황에 맞는 메뉴 표시를 담당 하는 `true` 에 대 한 값 <xref:System.Windows.RoutedEventArgs.Handled%2A> 이벤트 데이터는 상황에 맞는 메뉴에 대 한 표시를 취소 / 컨트롤 이벤트를 발생 시킨 조합 요청을 나타냅니다.  
  
 다음 단계 새 대시보드를 제공 하는 잠재적으로 의심 스러운 상황에 맞는 메뉴 표시 되지 않는 했으므로 표시 합니다. 하나는 기본적으로 이전 처리기로 동일한 새 설정: 새 빌드하면 <xref:System.Windows.Controls.ContextMenu> 컨트롤 소스를 설정 하 고 <xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=nameWithType> 속성을 합니다. 추가 단계는 첫 번째 시도 억제 하기 때문에 이제 강제 해야 상황에 맞는 메뉴를 표시 합니다. 표시 하도록 설정 합니다 <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A?displayProperty=nameWithType> 속성을 `true` 처리기 내에서. 주의이 작업을 수행 하는 경우 처리기에서 상황에 맞는 메뉴를 열고 발생 하기 때문에 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 이벤트 다시 합니다. 처리기를 다시 입력 하는 경우 재귀 됩니다 무한 합니다. 이것이 항상 확인 해야 하는 이유 `null` 내에서 상황에 맞는 메뉴를 열면 플래그를 사용 하 여 또는 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 이벤트 처리기입니다.  
  
## <a name="suppressing-any-existing-context-menu-and-displaying-no-context-menu"></a>모든 기존 상황에 맞는 메뉴를 표시 안 함 및 상황에 맞는 메뉴 표시  
 메뉴를 완전히를 억제 하는 처리기를 작성 하는 마지막 시나리오는 흔하지 않습니다. 지정된 된 컨트롤 상황에 맞는 메뉴를 표시 하지 않는, 경우에이 보장 하기 보다는 사용자가 요청할 때 메뉴를 억제 하 여 보다 적합할 가지가 있습니다. 처리기를 사용 하 여 상황에 맞는 메뉴를 표시 하지 않으려면를 아무 것도 표시 하려는 경우 처리기를 설정 하기만 해야 하지만 <xref:System.Windows.RoutedEventArgs.Handled%2A> 에 `true` 이벤트 데이터에서입니다. <xref:System.Windows.Controls.ContextMenuService> 하는 상황에 맞는 메뉴를 표시 하는 컨트롤에서 발생 시킨 이벤트의 이벤트 데이터를 확인 합니다. 이벤트로 표시 되어 있으면 <xref:System.Windows.RoutedEventArgs.Handled%2A> 어디서 나 경로 따르는 다음 이벤트를 시작한 상황에 맞는 메뉴 열기 작업 표시 되지 않습니다.  
  
 [!code-csharp[ContextMenuOpeningHandlers#ReplaceReopen](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#replacereopen)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ContextMenu>
- <xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=nameWithType>
- [기본 요소 개요](base-elements-overview.md)
- [ContextMenu 개요](../controls/contextmenu-overview.md)
