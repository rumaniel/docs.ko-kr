---
title: '방법: 커서 형식 변경'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- mouse pointer [WPF], cursor type
- cursor (mouse pointer)
ms.assetid: 08c945a7-8ab0-4320-acf3-0b4955a344c2
ms.openlocfilehash: 5c9e6931f6addb62a51e44b06a159d4e7b1e5f8a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776677"
---
# <a name="how-to-change-the-cursor-type"></a>방법: 커서 형식 변경
변경 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Input.Cursor> 특정 요소 및 응용 프로그램에 대 한 마우스 포인터의 합니다.  
  
 이 예제는 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 파일과 코드 숨김 파일입니다.  
  
## <a name="example"></a>예제  
 사용자 인터페이스를 만든 후 구성 되는 <xref:System.Windows.Controls.ComboBox> 원하는 선택 <xref:System.Windows.Input.Cursor>, 한 쌍의 <xref:System.Windows.Controls.RadioButton> 커서 변경 요소를 하나만 적용할 또는 전체 응용 프로그램에 적용 하는 경우를 결정 하는 개체 및 <xref:System.Windows.Controls.Border> 새 커서에 적용 되는 요소입니다.  
  
 [!code-xaml[cursors#ChangeCursorsXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/cursors/CSharp/Window1.xaml#changecursorsxaml)]  
  
 다음 코드 숨김 만듭니다는 <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> 에서 커서 유형이 변경 될 때 호출 되는 이벤트 처리기를 <xref:System.Windows.Controls.ComboBox>합니다.  집합과 커서 이름으로 필터링 하는 switch 문 합니다 <xref:System.Windows.FrameworkElement.Cursor%2A> 속성에는 <xref:System.Windows.Controls.Border> 이라는 *DisplayArea*합니다.  
  
 커서 변경 "전체 application"으로 설정 된 경우는 <xref:System.Windows.Input.Mouse.OverrideCursor%2A> 속성을 <xref:System.Windows.FrameworkElement.Cursor%2A> 의 속성은 <xref:System.Windows.Controls.Border> 컨트롤.  이렇게 하면 커서 전체 응용 프로그램에 대 한 변경입니다.  
  
 [!code-csharp[cursors#ChangeCursorsSample](~/samples/snippets/csharp/VS_Snippets_Wpf/cursors/CSharp/Window1.xaml.cs#changecursorssample)]
 [!code-vb[cursors#ChangeCursorsSample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/cursors/VisualBasic/Window1.xaml.vb#changecursorssample)]  
  
## <a name="see-also"></a>참고자료

- [입력 개요](input-overview.md)
