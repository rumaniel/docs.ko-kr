---
title: '방법: 포커스 이벤트를 사용하여 요소의 색 변경'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- focus events [WPF], changing element color for
- colors of elements [WPF], changing
- elements [WPF], changing color of
ms.assetid: 7e246802-3625-47a7-ae9d-c8a2a40fd040
ms.openlocfilehash: 5c59dc5f2f8f26fac69933f9ef641a3a51306619
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004828"
---
# <a name="how-to-change-the-color-of-an-element-using-focus-events"></a>방법: 포커스 이벤트를 사용하여 요소의 색 변경
이 예제에서는 <xref:System.Windows.UIElement.GotFocus> 및 <xref:System.Windows.UIElement.LostFocus> 이벤트를 사용 하 여 요소의 포커스를 얻거나 잃을 때 요소의 색을 변경 하는 방법을 보여 줍니다.  
  
 이 예제는 @no__t 파일 및 코드 숨김으로 구성 된 파일로 구성 되어 있습니다.  
  
## <a name="example"></a>예제  
 다음 XAML은 두 <xref:System.Windows.Controls.Button> 개체로 구성 된 사용자 인터페이스를 만들고 <xref:System.Windows.UIElement.GotFocus> 및 <xref:System.Windows.UIElement.LostFocus> 이벤트의 이벤트 처리기를 <xref:System.Windows.Controls.Button> 개체에 연결 합니다.  
  
 [!code-xaml[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/CSharp/Window1.xaml#gotlostfocussamplexaml)]  
  
 다음 코드는 <xref:System.Windows.UIElement.GotFocus> 및 <xref:System.Windows.UIElement.LostFocus> 이벤트 처리기를 만듭니다.  @No__t-0이 키보드 포커스를 얻으면 <xref:System.Windows.Controls.Button>의 @no__t 1이 빨강으로 변경 됩니다.  @No__t-0이 키보드 포커스를 잃으면 <xref:System.Windows.Controls.Button>의 @no__t 1이 다시 흰색으로 변경 됩니다.  
  
 [!code-csharp[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleEventHandlers](~/samples/snippets/csharp/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/CSharp/Window1.xaml.cs#gotlostfocussampleeventhandlers)]
 [!code-vb[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleEventHandlers](~/samples/snippets/visualbasic/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/VisualBasic/Window1.xaml.vb#gotlostfocussampleeventhandlers)]  
  
## <a name="see-also"></a>참조

- [입력 개요](input-overview.md)
