---
title: '방법: 선, 곡선 및 도형으로 그림 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- figures [Windows Forms], creating from shapes
- figures [Windows Forms], creating from lines
ms.assetid: 82fd56c7-b443-4765-9b7c-62ce030656ec
ms.openlocfilehash: c8cf7a7e08bed56fb704bba4e30ff369bc3fcf89
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64643465"
---
# <a name="how-to-create-figures-from-lines-curves-and-shapes"></a>방법: 선, 곡선 및 도형으로 그림 만들기
그림을 만들려면 생성을 <xref:System.Drawing.Drawing2D.GraphicsPath>와 같은 메서드를 호출 하 고 <xref:System.Drawing.Drawing2D.GraphicsPath.AddLine%2A> 및 <xref:System.Drawing.Drawing2D.GraphicsPath.AddCurve%2A>기본 경로에 추가 합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 그림이 포함 된 경로 만듭니다.  
  
- 첫 번째 예제에서는 단일 그림 포함 된 경로 만듭니다. 그림은 단일 호 이루어져 있습니다. 호에는 기본 좌표계에서 시계 반대 방향으로 180도 스윕 각도 합니다.  
  
- 두 번째 예제에서는 두 그림에 포함 된 경로 만듭니다. 첫 번째 그림에는 뒤에 줄 호입니다. 두 번째 그림은 뒤에 줄 뒤에 곡선을 줄입니다. 첫 번째 그림을 남겨 하 고 두 번째 그림 닫힙니다.  
  
 [!code-csharp[System.Drawing.ConstructingDrawingPaths#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.ConstructingDrawingPaths#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/VB/Class1.vb#21)]  
  
 [!code-csharp[System.Drawing.ConstructingDrawingPaths#22](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/CS/Class1.cs#22)]
 [!code-vb[System.Drawing.ConstructingDrawingPaths#22](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/VB/Class1.vb#22)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제에서는 Windows Forms에서 사용 하도록 설계 되었으며 필요할 <xref:System.Windows.Forms.PaintEventArgs> `e`의 매개 변수는 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Drawing2D.GraphicsPath>
- [경로 구성 및 그리기](constructing-and-drawing-paths.md)
- [펜을 사용하여 선과 도형 그리기](using-a-pen-to-draw-lines-and-shapes.md)
