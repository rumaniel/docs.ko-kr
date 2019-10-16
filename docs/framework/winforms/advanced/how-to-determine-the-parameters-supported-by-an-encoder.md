---
title: '방법: 인코더에서 지원하는 매개 변수 확인'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- encoder parameters [Windows Forms], determining supported
ms.assetid: f47ae459-e3ce-4d41-a140-2f6c6aea3f44
ms.openlocfilehash: 3e5345180e0ff3321b9ef0b885b836d3e9456f28
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64643330"
---
# <a name="how-to-determine-the-parameters-supported-by-an-encoder"></a>방법: 인코더에서 지원하는 매개 변수 확인
품질 및 압축 수준 등의 이미지 매개 변수를 조정할 수 있지만 매개 변수는 지정 된 이미지 인코더가 지 알고 있어야 합니다. 합니다 <xref:System.Drawing.Image> 클래스를 제공 합니다 <xref:System.Drawing.Image.GetEncoderParameterList%2A> 메서드 특정 인코더에 대 한 지원 되는 이미지 매개 변수를 확인할 수 있도록 합니다. GUID를 사용 하 여 인코더를 지정 합니다. 합니다 <xref:System.Drawing.Image.GetEncoderParameterList%2A> 메서드는 배열을 반환 <xref:System.Drawing.Imaging.EncoderParameter> 개체입니다.  
  
## <a name="example"></a>예제  
 다음 예제 코드는 JPEG 인코더에 대 한 지원 되는 매개 변수를 출력합니다. 매개 변수 범주 및 연관 된 Guid의 목록을 사용 하 여는 <xref:System.Drawing.Imaging.Encoder> 클래스 개요 각 매개 변수에 대 한 범주를 결정 합니다.  
  
 [!code-csharp[UsingImageEncodersDecoders#3](~/samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#3)]
 [!code-vb[UsingImageEncodersDecoders#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#3)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- Windows Forms 애플리케이션  
  
- A <xref:System.Windows.Forms.PaintEventArgs>에서의 매개 변수인 <xref:System.Windows.Forms.PaintEventHandler>합니다.   
  
## <a name="see-also"></a>참고자료

- [방법: 설치 된 인코더 나열](how-to-list-installed-encoders.md)
- [비트맵의 유형](types-of-bitmaps.md)
- [관리되는 GDI+에서 이미지 인코더 및 디코더 사용](using-image-encoders-and-decoders-in-managed-gdi.md)
