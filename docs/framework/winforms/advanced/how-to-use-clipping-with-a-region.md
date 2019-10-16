---
title: '방법: 영역에 클리핑 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- regions [Windows Forms], clipping
- regions [Windows Forms], restricting drawing surface
ms.assetid: 43d121b4-e14c-4901-b25c-2d6c25ba4e29
ms.openlocfilehash: e62be137b36a2f369c02151466154f6b3bab090b
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65063845"
---
# <a name="how-to-use-clipping-with-a-region"></a>방법: 영역에 클리핑 사용
속성 중 하나는 <xref:System.Drawing.Graphics> 클래스의 클립 영역입니다. 수행한 모든 그리기는 주어진 <xref:System.Drawing.Graphics> 개체의 클립 영역으로 제한 됩니다 <xref:System.Drawing.Graphics> 개체입니다. 호출 하 여 클립 영역을 설정할 수 있습니다는 <xref:System.Drawing.Graphics.SetClip%2A> 메서드.  
  
## <a name="example"></a>예제  
 다음 예제에서는 단일 다각형으로 구성 된 경로 생성 합니다. 다음 코드를 해당 경로 기반으로 영역을 생성 합니다. 지역에 전달 되는 <xref:System.Drawing.Graphics.SetClip%2A> 메서드는 <xref:System.Drawing.Graphics> 개체와 다음 두 문자열을 그릴 합니다.  
  
 다음 그림은 잘린된 문자열을 보여 줍니다.  
  
 ![잘린된 문자열을 보여 주는 스크린샷.](./media/how-to-use-clipping-with-a-region/clipped-strings-polygon.png)  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#41](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.MiscLegacyTopics#41](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#41)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows Forms에서 사용 하도록 설계 되었으며 필요 <xref:System.Windows.Forms.PaintEventArgs> `e`의 매개 변수인 <xref:System.Windows.Forms.PaintEventHandler>합니다.  
  
## <a name="see-also"></a>참고자료

- [GDI+의 영역](regions-in-gdi.md)
- [영역 사용](using-regions.md)
