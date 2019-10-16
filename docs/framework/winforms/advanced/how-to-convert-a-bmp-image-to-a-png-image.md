---
title: '방법: BMP 이미지를 PNG 이미지로 변환'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- BMP images [Windows Forms], converting to PNG
- image formats [Windows Forms], converting between
ms.assetid: 9d4a692d-73ac-4ce3-9e05-9ec321e8fbd6
ms.openlocfilehash: 59200941aa0f872a0bd99510bfaa8a8b878a9061
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64648299"
---
# <a name="how-to-convert-a-bmp-image-to-a-png-image"></a>방법: BMP 이미지를 PNG 이미지로 변환
이미지 파일 형식 간에 변환하려는 경우가 많습니다. <xref:System.Drawing.Image> 클래스의 <xref:System.Drawing.Image.Save%2A> 메서드를 호출하고 원하는 이미지 파일 형식에 대해 <xref:System.Drawing.Imaging.ImageFormat>을 지정하여 이 변환을 쉽게 수행할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 형식에서 BMP 이미지를 로드하고 PNG 형식으로 이미지를 저장합니다.  
  
 [!code-csharp[UsingImageEncodersDecoders#4](~/samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#4)]
 [!code-vb[UsingImageEncodersDecoders#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#4)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- Windows Forms 애플리케이션  
  
- `System.Drawing.Imaging` 네임스페이스에 대한 참조  
  
## <a name="see-also"></a>참고자료

- [방법: 설치 된 인코더 나열](how-to-list-installed-encoders.md)
- [관리되는 GDI+에서 이미지 인코더 및 디코더 사용](using-image-encoders-and-decoders-in-managed-gdi.md)
- [비트맵의 유형](types-of-bitmaps.md)
