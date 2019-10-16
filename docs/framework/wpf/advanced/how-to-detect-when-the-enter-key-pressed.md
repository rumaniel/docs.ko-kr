---
title: '방법: Enter 키를 눌렀을 때 검색'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Enter key [WPF], detecting
- keys [WPF], Enter
ms.assetid: a66f39d2-ef4a-43a5-b454-a4ea0fe88655
ms.openlocfilehash: e2337826077c836696937f91541d6d261f1270aa
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004816"
---
# <a name="how-to-detect-when-the-enter-key-pressed"></a>방법: Enter 키를 눌렀을 때 검색
이 예제에서는 키보드에서 <xref:System.Windows.Input.Key.Enter> 키를 누르는 시기를 검색 하는 방법을 보여 줍니다.  
  
 이 예제는 @no__t 파일 및 코드 숨김으로 구성 된 파일로 구성 되어 있습니다.  
  
## <a name="example"></a>예제  
 사용자가 <xref:System.Windows.Controls.TextBox>에서 <xref:System.Windows.Input.Key.Enter> 키를 누르면 텍스트 상자의 입력이 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]의 다른 영역에 나타납니다.  
  
 다음 XAML은 <xref:System.Windows.Controls.StackPanel>, <xref:System.Windows.Controls.TextBlock> 및 <xref:System.Windows.Controls.TextBox>로 구성 되는 사용자 인터페이스를 만듭니다.  
  
 [!code-xaml[keydown#KeyDownUI](~/samples/snippets/csharp/VS_Snippets_Wpf/KeyDown/CSharp/Window1.xaml#keydownui)]  
  
 다음 코드는 <xref:System.Windows.UIElement.KeyDown> 이벤트 처리기를 만듭니다.  누른 키가 @no__t 0 인 경우 <xref:System.Windows.Controls.TextBlock>에 메시지가 표시 됩니다.  
  
 [!code-csharp[keydown#KeyDownSample](~/samples/snippets/csharp/VS_Snippets_Wpf/KeyDown/CSharp/Window1.xaml.cs#keydownsample)]
 [!code-vb[keydown#KeyDownSample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/KeyDown/VisualBasic/Window1.xaml.vb#keydownsample)]  
  
## <a name="see-also"></a>참조

- [입력 개요](input-overview.md)
- [라우트된 이벤트 개요](routed-events-overview.md)
