---
title: '방법: 이벤트를 사용하여 롤오버 효과 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- colors of elements [WPF], changing
- rollover effect [WPF]
- element colors [WPF], changing
ms.assetid: 3b20d028-6f1c-4b25-95d2-fa68cefbdb4c
ms.openlocfilehash: 806056397200fa5c567e83227499ba721544f523
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005186"
---
# <a name="how-to-create-a-rollover-effect-using-events"></a>방법: 이벤트를 사용하여 롤오버 효과 만들기
이 예제에서는 마우스 포인터가 들어가거나 요소가 차지 하는 영역을 벗어날 때 요소의 색을 변경 하는 방법을 보여 줍니다.  
  
 이 예제는 @no__t 파일 및 코드 숨김으로 구성 된 파일로 구성 되어 있습니다.  
  
> [!NOTE]
> 이 예제에서는 이벤트를 사용 하는 방법을 보여 주지만 동일한 효과를 얻기 위한 권장 방법은 스타일에 <xref:System.Windows.Trigger>을 사용 하는 것입니다. 자세한 내용은 [스타일 지정 및 템플릿](../controls/styling-and-templating.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 XAML은 <xref:System.Windows.Controls.TextBlock>의 <xref:System.Windows.Controls.Border>으로 구성 된 사용자 인터페이스를 만들고 <xref:System.Windows.Input.Mouse.MouseEnter> 및 <xref:System.Windows.UIElement.MouseLeave> 이벤트 처리기를 <xref:System.Windows.Controls.Border>에 연결 합니다.  
  
 [!code-xaml[mouseenterMouseleave#MouseEnterLeaveSampleXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/mouseenterMouseleave/CSharp/Window1.xaml#mouseenterleavesamplexaml)]  
  
 다음 코드는 <xref:System.Windows.UIElement.MouseEnter> 및 <xref:System.Windows.UIElement.MouseLeave> 이벤트 처리기를 만듭니다.  마우스 포인터가 <xref:System.Windows.Controls.Border>에 들어가면 <xref:System.Windows.Controls.Border>의 배경이 빨강으로 변경 됩니다.  마우스 포인터가 <xref:System.Windows.Controls.Border>을 벗어나면 <xref:System.Windows.Controls.Border>의 배경은 다시 흰색으로 변경 됩니다.  
  
 [!code-csharp[mouseenterMouseleave#MouseEnterLeaveSampleEventHandlers](~/samples/snippets/csharp/VS_Snippets_Wpf/mouseenterMouseleave/CSharp/Window1.xaml.cs#mouseenterleavesampleeventhandlers)]
 [!code-vb[mouseenterMouseleave#MouseEnterLeaveSampleEventHandlers](~/samples/snippets/visualbasic/VS_Snippets_Wpf/mouseenterMouseleave/VisualBasic/Window1.xaml.vb#mouseenterleavesampleeventhandlers)]
