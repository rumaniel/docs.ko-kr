---
title: '방법: 배율 조정 시 보간 모드를 사용하여 이미지 품질 관리'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- interpolation mode [Windows Forms], controlling image quality
- images [Windows Forms], scaling
- images [Windows Forms], controlling quality
ms.assetid: fde9bccf-8aa5-4b0d-ba4b-788740627b02
ms.openlocfilehash: ab0ff93b3ee26467c0de448efd31b698167f95c2
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505719"
---
# <a name="how-to-use-interpolation-mode-to-control-image-quality-during-scaling"></a>방법: 배율 조정 시 보간 모드를 사용하여 이미지 품질 관리
보간 모드를 <xref:System.Drawing.Graphics> 방법은 GDI + 확장 (확장 및 축소) 이미지에 영향을 미칩니다. <xref:System.Drawing.Drawing2D.InterpolationMode> 열거형은 다음 목록에 나와 있는 여러 보간 모드를 정의 합니다.  
  
- <xref:System.Drawing.Drawing2D.InterpolationMode.NearestNeighbor>  
  
- <xref:System.Drawing.Drawing2D.InterpolationMode.Bilinear>  
  
- <xref:System.Drawing.Drawing2D.InterpolationMode.HighQualityBilinear>  
  
- <xref:System.Drawing.Drawing2D.InterpolationMode.Bicubic>  
  
- <xref:System.Drawing.Drawing2D.InterpolationMode.HighQualityBicubic>  
  
 이미지를 확대 하려면 원본 이미지의 각 픽셀의 더 큰 이미지 픽셀 그룹에 매핑해야 합니다. 이미지를 축소 하려면 원래 이미지의 픽셀의 그룹을 더 작은 이미지의 단일 픽셀에 매핑해야 합니다. 이러한 매핑을 수행 하는 알고리즘의 효과 배율 조정 된 이미지의 품질을 결정 합니다. 처리 시간이 더 높은 배율 조정 된 이미지를 생성 하는 알고리즘은 경향이 있습니다. 위의 목록에서 <xref:System.Drawing.Drawing2D.InterpolationMode.NearestNeighbor> 최저 품질 모드 및 <xref:System.Drawing.Drawing2D.InterpolationMode.HighQualityBicubic> 최고 품질 모드입니다.  
  
 보간 모드를 설정 하려면의 구성원 중 하나를 할당 합니다 <xref:System.Drawing.Drawing2D.InterpolationMode> 열거형을를 <xref:System.Drawing.Graphics.InterpolationMode%2A> 의 속성을 <xref:System.Drawing.Graphics> 개체입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 이미지를 그린 다음 세 가지 서로 다른 보간 모드를 사용 하 여 이미지를 축소 합니다.  
  
 다음 그림에서는 원본 이미지와 3 개의 더 작은 이미지를 보여 줍니다.  
  
 ![다양 한 보간 설정을 사용 하 여 이미지를 보여 주는 스크린샷.](./media/how-to-use-interpolation-mode-to-control-image-quality-during-scaling/varied-interpolation-settings.png)  
  
 [!code-csharp[System.Drawing.WorkingWithImages#81](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#81)]
 [!code-vb[System.Drawing.WorkingWithImages#81](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#81)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다.  
  
## <a name="see-also"></a>참고자료

- [이미지, 비트맵 및 메타파일](images-bitmaps-and-metafiles.md)
- [이미지, 비트맵, 아이콘 및 메타파일 사용](working-with-images-bitmaps-icons-and-metafiles.md)
