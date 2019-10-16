---
title: '방법: 자동 배율 조정 없이 성능 향상'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- automatic scaling
- images [Windows Forms], improving performance
- images [Windows Forms], using without automatic scaling
- performance [Windows Forms], improving image
ms.assetid: 5fe2c95d-8653-4d55-bf0d-e5afa28f223b
ms.openlocfilehash: dd1a1545dce33de1ce11938db8495ebf311dadda
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67506211"
---
# <a name="how-to-improve-performance-by-avoiding-automatic-scaling"></a>방법: 자동 배율 조정 없이 성능 향상
GDI + 그리면, 성능 저하가 발생 하는 이미지를 확장 자동으로 수 있습니다. 대상 사각형의 크기를 전달 하 여 이미지의 크기 조정은 제어할 수는 또는 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드.  
  
 다음을 호출 하는 예를 들어를 <xref:System.Drawing.Graphics.DrawImage%2A> 의 왼쪽 위 모퉁이 지정 하는 메서드 (50, 30) 하지만 대상 사각형을 지정 하지 않습니다.  
  
 [!code-csharp[System.Drawing.WorkingWithImages#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.WorkingWithImages#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#31)]  
  
 이 가장 쉬운 버전의는 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드 반드시 가장 효율적인 있지 필요한 인수 개수를 기준으로 합니다. GDI + (일반적으로 인치당 96 도트)에서 사용 하는 해상도에 저장 된 해상도와 다른 경우는 <xref:System.Drawing.Image> 개체는 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드 이미지 크기를 조정 합니다. 예를 들어는 <xref:System.Drawing.Image> 216 픽셀 너비, 72 인치당 저장된 수평 해상도 값 개체에 있습니다. 216/72 3 이므로 <xref:System.Drawing.Graphics.DrawImage%2A> 3 인치 너비 인치당 96 도트의 해상도로 포함 되도록 이미지 크기 조정 됩니다. 즉, <xref:System.Drawing.Graphics.DrawImage%2A> 96 x 3 = 288 개의 너비는 이미지가 표시 됩니다 (픽셀)입니다.  
  
 화면 해상도 96dpi 인 다른, 경우에 GDI +는 아마도 이미지 배율을 조정 화면 해상도 96dpi 인 경우. 있기 때문입니다 GDI + <xref:System.Drawing.Graphics> 개체가 연결 된 장치 컨텍스트에 및 화면 해상도 대 한 장치 컨텍스트에 GDI + 쿼리 하는 경우 결과 일반적으로 실제 화면 해상도 관계 없이 96입니다. 대상 사각형을 지정 하 여 자동 크기 조정 하지 않아도 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드.  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 번 동일한 이미지를 그립니다. 첫 번째 경우, 대상 사각형의 높이 너비를 지정 하지 않으면 및 이미지 자동으로 크기가 조정 됩니다. 두 번째 경우에서 너비와 대상 사각형의 높이 (픽셀)을 원본 이미지의 높이 너비와 동일 하 게 지정 됩니다. 다음 그림에서는 두 번 렌더링 되는 이미지를 보여 줍니다.  
  
 ![배율 조정 된 질감을 사용 하 여 이미지를 보여 주는 스크린샷.](./media/how-to-improve-performance-by-avoiding-automatic-scaling/two-scaled-texture-images.png)  
  
 [!code-csharp[System.Drawing.WorkingWithImages#32](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.WorkingWithImages#32](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#32)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다. Texture.jpg을 이미지 이름 및 시스템에 유효한 경로 바꿉니다.  
  
## <a name="see-also"></a>참고자료

- [이미지, 비트맵 및 메타파일](images-bitmaps-and-metafiles.md)
- [이미지, 비트맵, 아이콘 및 메타파일 사용](working-with-images-bitmaps-icons-and-metafiles.md)
