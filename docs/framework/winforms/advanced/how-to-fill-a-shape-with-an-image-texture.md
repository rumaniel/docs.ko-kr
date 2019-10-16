---
title: '방법: 이미지 질감으로 도형 채우기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [Windows Forms], using with brushes
- bitmaps [Windows Forms], using texture
- shapes [Windows Forms], filling with images
ms.assetid: 508da5a6-2433-4d2b-9680-eaeae4e96e3b
ms.openlocfilehash: 42c456137f84c6fa657ba5a09727eae052a45376
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69911683"
---
# <a name="how-to-fill-a-shape-with-an-image-texture"></a>방법: 이미지 질감으로 도형 채우기
<xref:System.Drawing.Image> 클래스<xref:System.Drawing.TextureBrush> 와 클래스를 사용 하 여 닫힌 셰이프를 질감으로 채울 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 이미지를 사용 하 여 타원을 채웁니다. 이 코드에서는 <xref:System.Drawing.Image> 개체를 생성 한 다음 해당 <xref:System.Drawing.Image> 개체의 주소를 <xref:System.Drawing.TextureBrush.%23ctor%2A> 생성자에 인수로 전달 합니다. 세 번째 문은 이미지의 크기를 조정 하 고 네 번째 문은 타원을 배율이 조정 된 이미지의 반복 된 복사본으로 채웁니다.  
  
 다음 코드에서 속성은 <xref:System.Drawing.TextureBrush.Transform%2A> 그리기 전에 이미지에 적용 되는 변환을 포함 합니다. 원래 이미지의 너비는 640 픽셀이 고 높이는 480 픽셀 이라고 가정 합니다. 변환은 가로 및 세로 크기 조정 값을 설정 하 여 이미지를 75 × 75로 축소 합니다.  
  
> [!NOTE]
> 다음 예제에서 이미지 크기는 75 x 75이 고, 타원 크기는 150 × 250입니다. 이미지가 채우는 타원 보다 작으므로 타원이 이미지를 사용 하 여 바둑판식으로 배열 됩니다. 바둑판식 배열은 모양의 경계에 도달할 때까지 이미지가 가로 및 세로로 반복 됨을 의미 합니다. 바둑판식 배열 [에 대 한 자세한 내용은 방법: 이미지](how-to-tile-a-shape-with-an-image.md)를 사용 하 여 셰이프를 바둑판식으로 배열 합니다.  
  
 [!code-csharp[System.Drawing.UsingABrush#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.UsingABrush#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#21)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다.  
  
## <a name="see-also"></a>참고자료

- [브러시를 사용하여 도형 채우기](using-a-brush-to-fill-shapes.md)
