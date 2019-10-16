---
title: '방법: 단색 브러시 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- solid color brushes
- brushes [Windows Forms], examples
- brushes [Windows Forms], creating solid
ms.assetid: 85c3fe7d-fb1d-4591-8a9f-d75b556b90af
ms.openlocfilehash: ed9ec1f52b41c83b3cc6e36dedf97f1c00db42e6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61937711"
---
# <a name="how-to-create-a-solid-brush"></a>방법: 단색 브러시 만들기
이 예제에서는 만듭니다는 <xref:System.Drawing.SolidBrush> 에서 사용할 수 있는 개체를 <xref:System.Drawing.Graphics> 모양을 채우는 개체입니다.  
  
## <a name="example"></a>예제  
 [!code-cpp[System.Drawing.ConceptualHowTos#1](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#1)]
 [!code-csharp[System.Drawing.ConceptualHowTos#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#1)]
 [!code-vb[System.Drawing.ConceptualHowTos#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#1)]  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 호출 해야 사용을 완료 한 후 <xref:System.IDisposable.Dispose%2A> 브러시 개체와 같은 시스템 리소스를 사용 하는 개체입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.SolidBrush>
- <xref:System.Drawing.Brush>
- [그래픽 프로그래밍 시작](getting-started-with-graphics-programming.md)
- [GDI+의 브러시 및 채워진 도형](brushes-and-filled-shapes-in-gdi.md)
- [브러시를 사용하여 도형 채우기](using-a-brush-to-fill-shapes.md)
