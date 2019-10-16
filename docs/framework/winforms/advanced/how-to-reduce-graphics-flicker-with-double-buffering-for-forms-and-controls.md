---
title: '방법: 양식과 컨트롤에 이중 버퍼링을 사용하여 그래픽 깜빡임 줄이기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- flicker [Windows Forms], reducing in Windows Forms
- graphics [Windows Forms], reducing double-buffered flicker
ms.assetid: 91083d3a-653f-4f15-a467-0f37b2aa39d6
ms.openlocfilehash: d143d7ec87a214a900264e069b329ea28a92c3e9
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65590386"
---
# <a name="how-to-reduce-graphics-flicker-with-double-buffering-for-forms-and-controls"></a>방법: 양식과 컨트롤에 이중 버퍼링을 사용하여 그래픽 깜빡임 줄이기
이중 버퍼링은 메모리 버퍼를 사용하여 여러 그리기 작업과 관련된 깜박임 문제를 해결합니다. 이중 버퍼링을 사용하면 모든 그리기 작업이 그리기 화면 대신 메모리 버퍼에 먼저 렌더링됩니다. 모든 그리기 작업이 완료되면 메모리 버퍼가 연결된 그리기 화면에 직접 복사됩니다. 하나의 그래픽 작업만 화면에서 수행 되므로 복잡 한 그리기 작업과 관련 된 이미지 깜빡임이 제거 됩니다. 대부분의 응용 프로그램에 대 한.NET Framework에서 제공 하는 기본 이중 버퍼링 최상의 결과 제공 합니다. 표준 Windows Forms 컨트롤은 기본적으로 버퍼링 된 double입니다. 두 가지 방법으로 컨트롤을 작성 한 폼에서 기본 이중 버퍼링을 사용 하도록 설정할 수 있습니다. 설정 하거나 합니다 <xref:System.Windows.Forms.Control.DoubleBuffered%2A> 속성을 `true`, 하거나 호출할 수 있습니다는 <xref:System.Windows.Forms.Control.SetStyle%2A> 설정 하는 방법을 <xref:System.Windows.Forms.ControlStyles.OptimizedDoubleBuffer> 플래그를 `true`합니다. 두 방법 모두 양식이 나 컨트롤에 기본 이중 버퍼링을 사용 하도록 설정 되며 깜박임 그래픽 렌더링을 제공 합니다. 호출 된 <xref:System.Windows.Forms.Control.SetStyle%2A> 메서드는 모든 렌더링 코드를 작성 하는 사용자 지정 컨트롤에만 권장 됩니다.  
  
 애니메이션 또는 고급 메모리 관리와 같은 고급 이중 버퍼링 시나리오에 대 한 사용자 고유의 이중 버퍼링 논리를 구현할 수 있습니다. 자세한 내용은 [방법: 버퍼링 된 그래픽 수동 관리](how-to-manually-manage-buffered-graphics.md)합니다.  
  
### <a name="to-reduce-flicker"></a>깜빡임을 줄이기 위해  
  
- <xref:System.Windows.Forms.Control.DoubleBuffered%2A> 속성을 `true`으로 설정합니다.  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#31)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#31)]  
  
 \- 또는 -  
  
- 호출을 <xref:System.Windows.Forms.Control.SetStyle%2A> 설정 하는 메서드를 <xref:System.Windows.Forms.ControlStyles.OptimizedDoubleBuffer> 플래그를 `true`.  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#32](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#32)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#32](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#32)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Control.DoubleBuffered%2A>
- <xref:System.Windows.Forms.Control.SetStyle%2A>
- [이중 버퍼링 그래픽](double-buffered-graphics.md)
- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
