---
title: '방법: 빗살 무늬로 도형 채우기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- patterns [Windows Forms], adding to shapes
- shapes [Windows Forms], filling with patterns
- brushes [Windows Forms], using hatch brushes
ms.assetid: 9c8300ff-187b-404f-af1f-ebd499f5b16f
ms.openlocfilehash: b9ecefb82aaaf896c4ed39733f1e8d7bd65c16d4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645479"
---
# <a name="how-to-fill-a-shape-with-a-hatch-pattern"></a>방법: 빗살 무늬로 도형 채우기
빗살 무늬 두 색으로에서 이루어집니다: 배경색 및 배경 위에 패턴을 형성 하는 줄에 대 한 하나입니다. 빗살 무늬를 사용 하 여 닫힌된 도형 채우기를 사용 하 여를 <xref:System.Drawing.Drawing2D.HatchBrush> 개체입니다. 다음 예제에서는 빗살 무늬를 사용 하 여 타원을 채우는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 <xref:System.Drawing.Drawing2D.HatchBrush.%23ctor%2A> 생성자에는 세 가지 인수: 해치 스타일, 빗살 무늬 선의 색 및 배경색입니다. 빗살 무늬 스타일 인수로 사용할 수 있는 모든 값은 <xref:System.Drawing.Drawing2D.HatchStyle> 열거형입니다. 에 50 개 이상의 요소가 <xref:System.Drawing.Drawing2D.HatchStyle> 열거형; 몇 가지 요소는 다음 목록에 표시 합니다.  
  
- <xref:System.Drawing.Drawing2D.HatchStyle.Horizontal>  
  
- <xref:System.Drawing.Drawing2D.HatchStyle.Vertical>  
  
- <xref:System.Drawing.Drawing2D.HatchStyle.ForwardDiagonal>  
  
- <xref:System.Drawing.Drawing2D.HatchStyle.BackwardDiagonal>  
  
- <xref:System.Drawing.Drawing2D.HatchStyle.Cross>  
  
- <xref:System.Drawing.Drawing2D.HatchStyle.DiagonalCross>  
  
 다음 그림은 채워진된 타원을 보여 줍니다.  
  
 ![패턴을 해치](./media/hatch1.png "hatch1")  
  
 [!code-csharp[System.Drawing.UsingABrush#41](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.UsingABrush#41](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#41)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.PaintEventArgs> 이벤트 처리기의 매개 변수인 `e`<xref:System.Windows.Forms.Control.Paint>가 필요합니다.  
  
## <a name="see-also"></a>참고자료

- [브러시를 사용하여 도형 채우기](using-a-brush-to-fill-shapes.md)
