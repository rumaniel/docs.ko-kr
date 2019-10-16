---
title: '방법: 비주얼 스타일 요소 렌더링'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- visual themes [Windows Forms], applying to elements of Windows Forms applications
- professional appearance [Windows Forms], applying to elements of Windows Forms applications
- visual styles [Windows Forms], rendering Windows Forms controls
ms.assetid: a207781b-1baa-4ce9-b788-1e951bd4b5df
ms.openlocfilehash: a2b9524b6a3e3c77d3c68c4d9e138b8c0e2a9373
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662302"
---
# <a name="how-to-render-a-visual-style-element"></a>방법: 비주얼 스타일 요소 렌더링
합니다 <xref:System.Windows.Forms.VisualStyles?displayProperty=nameWithType> 네임 스페이스는 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> Windows 사용자를 나타내는 개체 인터페이스 (UI) 요소 비주얼 스타일에서 지원 합니다. 이 항목에서는 사용 하는 방법에 설명 합니다 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 렌더링 하는 클래스를 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 나타내는 **로그 오프** 및 **종료** 시작 메뉴의 단추입니다.  
  
### <a name="to-render-a-visual-style-element"></a>비주얼 스타일 요소 렌더링  
  
1. 만들기는 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 그릴 원하는 요소를 설정 합니다. 사용 된 <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A?displayProperty=nameWithType> 속성 및 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer.IsElementDefined%2A?displayProperty=nameWithType> 메서드, <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer.%23ctor%2A> 생성자 비주얼 스타일을 사용할 수 없거나 정의 되어 있지 않은 경우 예외가 throw 됩니다.  
  
     [!code-cpp[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#4](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/cpp/form1.cpp#4)]
     [!code-csharp[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/CS/form1.cs#4)]
     [!code-vb[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/VB/form1.vb#4)]  
  
2. 호출을 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer.DrawBackground%2A> 메서드를 요소는 렌더링는 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 현재 나타냅니다.  
  
     [!code-cpp[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#6](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/cpp/form1.cpp#6)]
     [!code-csharp[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#6](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/CS/form1.cs#6)]
     [!code-vb[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#6](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/VB/form1.vb#6)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- 파생 되는 사용자 지정 컨트롤을 <xref:System.Windows.Forms.Control> 클래스입니다.  
  
- <xref:System.Windows.Forms.Form> 사용자 지정 컨트롤을 호스팅하는 합니다.  
  
- 에 대 한 참조를 <xref:System?displayProperty=nameWithType>, <xref:System.Drawing?displayProperty=nameWithType>를 <xref:System.Windows.Forms?displayProperty=nameWithType>, 및 <xref:System.Windows.Forms.VisualStyles?displayProperty=nameWithType> 네임 스페이스입니다.  
  
## <a name="see-also"></a>참고자료

- [비주얼 스타일을 사용하여 컨트롤 렌더링](rendering-controls-with-visual-styles.md)
