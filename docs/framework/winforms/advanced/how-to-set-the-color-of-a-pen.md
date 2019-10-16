---
title: '방법: 펜 색 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- pens [Windows Forms], setting color
- colored pens
ms.assetid: a9df06f9-a6d5-4d9b-a2d1-583943540775
ms.openlocfilehash: ee2d3f8cdf6dd10ca2a9ff0dd3e66b164c84f21b
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64637011"
---
# <a name="how-to-set-the-color-of-a-pen"></a>방법: 펜 색 설정
이 예제에서는 기존 색이 달라 <xref:System.Drawing.Pen> 개체  
  
## <a name="example"></a>예제  
 [!code-cpp[System.Drawing.ConceptualHowTos#9](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#9)]
 [!code-csharp[System.Drawing.ConceptualHowTos#9](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#9)]
 [!code-vb[System.Drawing.ConceptualHowTos#9](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#9)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- A <xref:System.Drawing.Pen> 개체인 `myPen`합니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 호출 해야 <xref:System.Drawing.Pen.Dispose%2A> 시스템 리소스를 사용 하는 개체에 (같은 <xref:System.Drawing.Pen> 개체)을 사용 하 여 작업을 마친 후 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Pen>
- [그래픽 프로그래밍 시작](getting-started-with-graphics-programming.md)
- [방법: 펜 만들기](how-to-create-a-pen.md)
- [펜을 사용하여 선과 도형 그리기](using-a-pen-to-draw-lines-and-shapes.md)
- [GDI+의 펜, 선 및 사각형](pens-lines-and-rectangles-in-gdi.md)
