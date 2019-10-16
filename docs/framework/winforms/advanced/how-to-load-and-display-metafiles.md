---
title: '방법: 메타파일 로드 및 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- examples [Windows Forms], metafiles
- metafiles [Windows Forms], displaying
ms.assetid: 60af1714-f148-4d85-a739-0557965ffa73
ms.openlocfilehash: 39b7251b2789c7410e1d59b4aa7990a2f73055fe
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61723218"
---
# <a name="how-to-load-and-display-metafiles"></a>방법: 메타파일 로드 및 표시
<xref:System.Drawing.Imaging.Metafile> 클래스에서 상속 되는 <xref:System.Drawing.Image> 클래스, 기록, 표시 및 벡터 이미지 검사에 대 한 메서드를 제공 합니다.  
  
## <a name="example"></a>예제  
 화면에 벡터 이미지 (메타 파일)를 표시할 필요는 <xref:System.Drawing.Imaging.Metafile> 개체 및 <xref:System.Drawing.Graphics> 개체입니다. 파일 (또는 스트림)의 이름을 전달 하는 <xref:System.Drawing.Imaging.Metafile> 생성자입니다. 만든 후는 <xref:System.Drawing.Imaging.Metafile> 개체를 전달 <xref:System.Drawing.Imaging.Metafile> 개체를 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드의 <xref:System.Drawing.Graphics> 개체입니다.  
  
 이 예에서는 만듭니다는 <xref:System.Drawing.Imaging.Metafile> EMF (확장된 메타 파일) 파일에서 개체 다음에 왼쪽 위 모퉁이 사용 하 여 이미지를 그립니다 (60, 10).  
  
 다음 그림에서는 지정된 된 위치에 그릴 메타 파일을 보여 줍니다.  
  
 ![이미지 위치](./media/imageposition2.png "imageposition2")  
  
 [!code-csharp[System.Drawing.WorkingWithImages#41](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.WorkingWithImages#41](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#41)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다.  
  
## <a name="see-also"></a>참고자료

- [이미지, 비트맵, 아이콘 및 메타파일 사용](working-with-images-bitmaps-icons-and-metafiles.md)
