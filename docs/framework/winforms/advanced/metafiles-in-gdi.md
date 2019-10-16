---
title: GDI+의 메타파일
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [Windows Forms], metafiles
- GDI+, metafiles
- metafiles
ms.assetid: 51da872c-c783-440f-8bf6-1e580a966c31
ms.openlocfilehash: df54289722cf12bad840722c6eafdaa43279a5dc
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67504592"
---
# <a name="metafiles-in-gdi"></a>GDI+의 메타파일
GDI + 제공은 <xref:System.Drawing.Imaging.Metafile> 클래스를 기록 하 고 메타 파일을 표시할 수 있도록 합니다. 벡터 이미지 라고도 불리는 메타 파일 이미지 그리기 명령 및 설정의 시퀀스로 저장 되어 있는 경우 명령 및 설정에 기록를 <xref:System.Drawing.Imaging.Metafile> 개체를 메모리에 저장 하거나 파일 또는 스트림에 저장할 수 있습니다.  
  
## <a name="metafile-formats"></a>메타 파일 형식  
 GDI +에서는 다음 형식으로 저장 된 메타 파일을 표시할 수 있습니다.  
  
- Windows 메타 파일 (WMF)  
  
- EMF(확장 메타파일)  
  
- EMF+  
  
 GDI +를 기록할 수 메타 파일 EMF, EMF + 형식으로 있지만 WMF 형식에 없습니다.  
  
 EMF +는 GDI + 레코드를 저장할 수 있는 EMF 확장 합니다. EMF + 형식에 두 가지 변형이 있습니다. EMF +만 및 EMF + 복합 합니다. EMF + 전용 메타 파일에는 GDI + 레코드만 포함합니다. GDI는 아니라 GDI +에서 이러한 메타 파일을 표시할 수 있습니다. EMF + 복합 메타 파일 GDI 및 GDI + 레코드를 포함 합니다. EMF + 복합 메타 파일의 각 GDI + 레코드를 대체 GDI 레코드를 이룹니다. 이러한 메타 파일은 GDI 또는 GDI +에서 표시할 수 있습니다.  
  
 다음 예제에서는 이전에 파일로 저장 된 메타 파일을 표시 합니다. 메타 파일에서 왼쪽 위 모퉁이 표시 됩니다 (100, 100).  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#21)]  
  
## <a name="see-also"></a>참고자료

- [이미지, 비트맵 및 메타파일](images-bitmaps-and-metafiles.md)
