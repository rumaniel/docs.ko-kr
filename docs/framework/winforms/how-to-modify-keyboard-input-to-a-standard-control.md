---
title: '방법: 표준 컨트롤로 키보드 입력 수정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- keyboard input [Windows Forms], modifying
- modifying keyboard input
- Windows Forms, modifying keyboard input
- keyboards [Windows Forms], keyboard input
ms.assetid: 626d3712-d866-4988-bcda-a2d5b36ec0ba
ms.openlocfilehash: 1aa22501eb3d15b30be4ea4918473cf5a48cfe94
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964286"
---
# <a name="how-to-modify-keyboard-input-to-a-standard-control"></a>방법: 표준 컨트롤로 키보드 입력 수정
Windows Forms는 키보드 입력을 사용 및 수정할 수 있는 기능을 제공합니다. 키 사용은 메시지 큐 아래의 다른 메서드 및 이벤트가 키 값을 수신하지 않도록 메서드 또는 이벤트 처리기 내에서 키를 처리하는 것을 가리킵니다. 키 수정은 메시지 큐 아래의 메서드 및 이벤트 처리기가 다른 키 값을 수신하도록 키 값을 수정하는 것을 가리킵니다. 이 항목에서는 이러한 작업을 수행하는 방법을 보여 줍니다.  
  
### <a name="to-consume-a-key"></a>키를 사용하려면  
  
- <xref:System.Windows.Forms.Control.KeyPress> 이벤트 처리기에서 <xref:System.Windows.Forms.KeyPressEventArgs> 클래스의 <xref:System.Windows.Forms.KeyPressEventArgs.Handled%2A> 속성을 `true`로 설정합니다.  
  
     또는  
  
     <xref:System.Windows.Forms.Control.KeyDown> 이벤트 처리기에서 <xref:System.Windows.Forms.KeyEventArgs> 클래스의 <xref:System.Windows.Forms.KeyEventArgs.Handled%2A> 속성을 `true`로 설정합니다.  
  
    > [!NOTE]
    > <xref:System.Windows.Forms.Control.KeyDown> 이벤트 처리기에서 <xref:System.Windows.Forms.KeyEventArgs.Handled%2A> 속성을 설정해도 <xref:System.Windows.Forms.Control.KeyPress> 및 <xref:System.Windows.Forms.Control.KeyUp> 이벤트가 현재 키 입력에 대해 발생하지 않도록 차단되지는 않습니다. 이렇게 하려면 <xref:System.Windows.Forms.KeyEventArgs.SuppressKeyPress%2A> 속성을 사용합니다.  
  
     다음 예제는 <xref:System.Windows.Forms.Control.KeyPress> 이벤트 처리기가 수신한 <xref:System.Windows.Forms.KeyPressEventArgs>의 <xref:System.Windows.Forms.KeyPressEventArgs.KeyChar%2A> 속성을 검사하는 `switch` 문에서 발췌한 내용입니다. 이 코드는 'A' 및 'a' 문자 키를 사용합니다.  
  
     [!code-csharp[System.Windows.Forms.KeyBoardInput#6](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#6)]
     [!code-vb[System.Windows.Forms.KeyBoardInput#6](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#6)]  
  
### <a name="to-modify-a-standard-character-key"></a>표준 문자 키를 수정하려면  
  
- <xref:System.Windows.Forms.Control.KeyPress> 이벤트 처리기에서 <xref:System.Windows.Forms.KeyPressEventArgs> 클래스의 <xref:System.Windows.Forms.KeyPressEventArgs.KeyChar%2A> 속성을 새 문자 키의 값으로 설정합니다.  
  
     다음 예제는 'B'를 'A’로 수정하고 'b'를 'a'로 수정하는 `switch` 문에서 발췌한 내용입니다. 새로운 키 값이 메시지 큐의 다른 메서드 및 이벤트에 전파되도록 <xref:System.Windows.Forms.KeyPressEventArgs> 매개 변수의 <xref:System.Windows.Forms.KeyPressEventArgs.Handled%2A> 속성은 `false`로 설정됩니다.  
  
     [!code-csharp[System.Windows.Forms.KeyBoardInput#7](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#7)]
     [!code-vb[System.Windows.Forms.KeyBoardInput#7](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#7)]  
  
### <a name="to-modify-a-noncharacter-key"></a>문자가 아닌 키를 수정하려면  
  
- Windows 메시지를 처리하는 <xref:System.Windows.Forms.Control> 메서드를 재정의하고, WM_KEYDOWN 또는 WM_SYSKEYDOWN 메시지를 검색하고, <xref:System.Windows.Forms.Message> 매개 변수의 <xref:System.Windows.Forms.Message.WParam%2A> 속성을 문자가 아닌 새 키를 나타내는 <xref:System.Windows.Forms.Keys> 값으로 설정합니다.  
  
     다음 코드 예제에서는 컨트롤의 <xref:System.Windows.Forms.Control.PreProcessMessage%2A> 메서드를 재정의하여 F1-F9 키를 검색하고 F3 키 누름을 F1로 수정하는 방법을 보여 줍니다. 키보드 메시지를 가로채기 <xref:System.Windows.Forms.Control> 위해 재정의할 수 있는 메서드에 대 한 자세한 내용은 [Windows Forms 응용 프로그램의 사용자 입력](user-input-in-a-windows-forms-application.md) 및 [키보드 입력 작동 방식](how-keyboard-input-works.md)을 참조 하세요.  
  
     [!code-csharp[System.Windows.Forms.KeyBoardInput#12](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#12)]
     [!code-vb[System.Windows.Forms.KeyBoardInput#12](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#12)]  
  
## <a name="example"></a>예제  
 다음 코드 예제는 이전 섹션의 코드 예제에 대한 전체 애플리케이션입니다. 응용 프로그램은 <xref:System.Windows.Forms.TextBox> 클래스에서 파생된 사용자 지정 컨트롤을 통해 키보드 입력을 사용 및 수정합니다.  
  
 [!code-csharp[System.Windows.Forms.KeyBoardInput#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#0)]
 [!code-vb[System.Windows.Forms.KeyBoardInput#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#0)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System, System.Drawing 및 System.Windows.Forms 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- [Windows Forms 응용 프로그램의 키보드 입력](keyboard-input-in-a-windows-forms-application.md)
- [Windows Forms 응용 프로그램의 사용자 입력](user-input-in-a-windows-forms-application.md)
- [키보드 입력 작동 방식](how-keyboard-input-works.md)
