---
title: '방법: 썸네일 이미지 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- thumbnail images [Windows Forms], creating
- images [Windows Forms], creating thumbnails
ms.assetid: e956242a-1e5b-4217-a3cf-5f3fb45d00ba
ms.openlocfilehash: 786a92d99f5e7a0c27f502efa9a5fe617ac4d4d6
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923750"
---
# <a name="how-to-create-thumbnail-images"></a>방법: 썸네일 이미지 만들기
축소판 이미지는 이미지의 작은 버전입니다. 개체의 메서드를 <xref:System.Drawing.Image.GetThumbnailImage%2A> 호출 하 여 미리 보기 이미지를 만들 수 있습니다. <xref:System.Drawing.Image>  
  
## <a name="example"></a>예제  
 다음 예제에서는 JPG 파일 <xref:System.Drawing.Image> 에서 개체를 생성 합니다. 원래 이미지의 너비는 640 픽셀이 고 높이는 479 픽셀입니다. 이 코드는 너비가 100 픽셀이 고 높이가 100 픽셀인 축소판 이미지를 만듭니다.  
  
 다음 그림은 축소판 이미지를 보여 줍니다.  
  
 ![출력 축소판 그림을 보여 주는 스크린샷](./media/how-to-create-thumbnail-images/construct-thumbnail-image.png)  
  
> [!NOTE]
> 이 예제에서는 콜백 메서드가 선언 되었지만 사용 되지 않았습니다. 모든 버전의 GDI +를 지원 합니다.  
  
 [!code-csharp[System.Drawing.WorkingWithImages#71](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#71)]
 [!code-vb[System.Drawing.WorkingWithImages#71](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#71)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다. 예제를 실행 하려면 다음이 단계를 수행 합니다.  
  
1. 새 Windows Forms 애플리케이션을 만듭니다.  
  
2. 예제 코드를 폼에 추가 합니다.  
  
3. 폼의 <xref:System.Windows.Forms.Control.Paint> 이벤트에 대 한 처리기 만들기  
  
4. 처리기에서 `GetThumbnail` 메서드를 호출 하 고에 대해 `e` <xref:System.Windows.Forms.PaintEventArgs>를 전달 합니다. <xref:System.Windows.Forms.Control.Paint>  
  
5. 축소판 그림으로 만들 이미지 파일을 찾습니다.  
  
6. `GetThumbnail` 메서드에서 이미지에 대 한 경로와 파일 이름을 지정 합니다.  
  
7. F5 키를 눌러 예제를 실행 합니다.  
  
     100 x 100 축소판 이미지는 폼에 표시 됩니다.  
  
## <a name="see-also"></a>참고자료

- [이미지, 비트맵 및 메타파일](images-bitmaps-and-metafiles.md)
- [이미지, 비트맵, 아이콘 및 메타파일 사용](working-with-images-bitmaps-icons-and-metafiles.md)
