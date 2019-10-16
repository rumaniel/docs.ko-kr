---
title: '방법: 색 회전'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- colors [Windows Forms], rotating
- examples [Windows Forms], rotating colors
ms.assetid: e2e4c300-159c-4f4a-9b56-103b0f7cbc05
ms.openlocfilehash: d251a223fca50eebc3a959ea694242992c4a1dbe
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65590316"
---
# <a name="how-to-rotate-colors"></a>방법: 색 회전
4 차원 색 공간에서 회전은 시각화 하기가 어렵습니다. 에서는 수 쉽게 동의 고정 색 구성 요소 중 하나를 유지 하 여 회전을 시각화 합니다. 1 자리 알파 구성 요소 (완전 불투명) 한다고 가정 합니다. 그런 다음 다음 그림에 나와 있는 것 처럼 빨강, 녹색 및 파랑 축이 있는 3 차원 색 공간을를 시각화할 수 있습니다 했습니다.  
  
 ![빨간색, 녹색 및 파란색 축 회전을 보여 주는 그림입니다.](./media/how-to-rotate-colors/rotation-red-green-blue-axes.gif)  
  
 색을 3 차원 공간에서 지점으로 생각할 수 있습니다. 예를 들어 공간의 점 (1, 0, 0) 빨강을 나타내고 녹색 공간의 점 (0, 1, 0)을 나타냅니다.  
  
 다음 그림에서는 빨간색-녹색 평면에서 60도의 각도 통해 (1, 0, 0) 색을 회전 하는 것을 보여 줍니다. 빨강-녹색 평면 평행한 평면에서 회전 파란색 축 회전으로 생각할 수 있습니다.  
  
 ![파란색 축 회전을 보여 주는 그림입니다.](./media/how-to-rotate-colors/rotation-about-blue-axis.gif)  
  
 다음 그림에서는 각각 세 개의 좌표 축 (빨간색, 녹색, 파랑)에 대 한 회전을 수행 하기 위해 색 매트릭스를 초기화 하는 방법을 보여 줍니다.  
  
 ![3 개의 축 중심으로 회전 하는 데 색 매트릭스를 초기화 합니다.](./media/how-to-rotate-colors/rotation-about-three-axes.gif)  
  
## <a name="example"></a>예제  
 다음 예제에서는 (1, 0, 0.6) 모두 같은 색은 파란색 축에 대 한 60도 회전을 적용 하는 이미지입니다. 회전은 빨강-녹색 평면에 병렬 되는 평면에서 이루어집니다.  
  
 다음 그림에서는 왼쪽 및 오른쪽에 있는 색 회전 이미지에 원본 이미지를 보여 줍니다.  
  
 ![원래 이미지와 색 회전 이미지를 보여 주는 그림입니다.](./media/how-to-rotate-colors/original-color-rotated-images.png)  
  
 다음 그림에서는 다음 코드에서 수행 되는 색 회전 시각화를 보여 줍니다.
  
 ![색 회전 시각화를 보여 주는 그림입니다.](./media/how-to-rotate-colors/visualization-color-rotation.gif)  
  
 [!code-csharp[System.Drawing.RotateColors#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RotateColors/CS/Form1.cs#1)]
 [!code-vb[System.Drawing.RotateColors#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RotateColors/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다. 대체 `RotationInput.bmp` 와 경로 시스템에서 사용할 이미지 파일 이름입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Imaging.ColorMatrix>
- <xref:System.Drawing.Imaging.ImageAttributes>
- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
- [이미지 다시 칠하기](recoloring-images.md)
