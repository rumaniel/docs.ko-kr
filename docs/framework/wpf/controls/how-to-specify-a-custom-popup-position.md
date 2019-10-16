---
title: '방법: 사용자 지정 팝업 위치 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Popup control [WPF], specifying custom position
ms.assetid: 28c24f39-d3aa-4ee2-b950-384b4a5dab92
ms.openlocfilehash: dc516f0eb1cfcbac6662497eb4019041eefec2a9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911211"
---
# <a name="how-to-specify-a-custom-popup-position"></a>방법: 사용자 지정 팝업 위치 지정
이 예제에 대 한 사용자 지정 위치를 지정 하는 방법을 보여 줍니다를 <xref:System.Windows.Controls.Primitives.Popup> 시기를 제어 합니다 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 속성이 <xref:System.Windows.Controls.Primitives.PlacementMode.Custom>.  
  
## <a name="example"></a>예제  
 경우는 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 속성이로 설정 되어 <xref:System.Windows.Controls.Primitives.PlacementMode.Custom>, <xref:System.Windows.Controls.Primitives.Popup> 의 정의 된 인스턴스를 호출 합니다 <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> 대리자. 대상 영역의 왼쪽된 위 모퉁이와 왼쪽된 위 모퉁이 있는 가능한 점의 집합을 반환 하는이 대리자는 <xref:System.Windows.Controls.Primitives.Popup>합니다. <xref:System.Windows.Controls.Primitives.Popup> 최상의 가시성을 제공 하는 지점에 배치 됩니다.  
  
 다음 예제에서는 위치를 정의 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.Primitives.Popup> 설정 하 여 합니다 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 속성을 <xref:System.Windows.Controls.Primitives.PlacementMode.Custom>입니다. 또한 만들고 할당 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> 배치 하기 위해 대리자는 <xref:System.Windows.Controls.Primitives.Popup>합니다.  두 콜백 대리자 반환 <xref:System.Windows.Controls.Primitives.CustomPopupPlacement> 개체입니다.  경우는 <xref:System.Windows.Controls.Primitives.Popup> 화면 가장자리에 첫 번째 위치에 의해 숨겨져는 <xref:System.Windows.Controls.Primitives.Popup> 두 번째 위치에 배치 됩니다.  
  
 [!code-xaml[PopupCustomPlacement#CustomPlacement](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml#customplacement)]  
  
 [!code-csharp[PopupCustomPlacement#DelegateInstance](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml.cs#delegateinstance)]
 [!code-vb[PopupCustomPlacement#DelegateInstance](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PopupCustomPlacement/visualbasic/window1.xaml.vb#delegateinstance)]  
  
 [!code-csharp[PopupCustomPlacement#DelegateDefinition](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml.cs#delegatedefinition)]
 [!code-vb[PopupCustomPlacement#DelegateDefinition](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PopupCustomPlacement/visualbasic/window1.xaml.vb#delegatedefinition)]  
  
 전체 샘플을 참조 하세요 [Popup 배치 샘플](https://go.microsoft.com/fwlink/?LinkID=160032)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Primitives.Popup>
- [팝업 개요](popup-overview.md)
- [방법 항목](popup-how-to-topics.md)
