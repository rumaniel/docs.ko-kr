---
title: 중첩된 Graphics 컨테이너 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [Windows Forms], nested containers
- graphics [Windows Forms], clipping
- graphics [Windows Forms], transformations in nested objects
ms.assetid: a0d9f178-43a4-4323-bb5a-d3e3f77ae6c1
ms.openlocfilehash: 4533fbba62c36714f55cd8bd55fde7a1c8f6c9e6
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505052"
---
# <a name="using-nested-graphics-containers"></a>중첩된 Graphics 컨테이너 사용
GDI +-임시로 바꾸거나의 상태 부분을 보강 하는 데 사용할 수 있는 컨테이너를 제공 하는 중에 <xref:System.Drawing.Graphics> 개체입니다. 호출 하 여 컨테이너를 만들어야 합니다 <xref:System.Drawing.Graphics.BeginContainer%2A> 메서드는 <xref:System.Drawing.Graphics> 개체입니다. 호출할 수 있습니다 <xref:System.Drawing.Graphics.BeginContainer%2A> 반복 하 여 중첩 된 컨테이너를 구성 합니다. 호출할 때마다 <xref:System.Drawing.Graphics.BeginContainer%2A> 를 호출 하 여 이루어야 <xref:System.Drawing.Graphics.EndContainer%2A>합니다.  
  
## <a name="transformations-in-nested-containers"></a>중첩 된 컨테이너에서 변환  
 다음 예제는 <xref:System.Drawing.Graphics> 개체 및 해당 컨테이너 <xref:System.Drawing.Graphics> 개체입니다. 월드 변형을 <xref:System.Drawing.Graphics> 개체가 x 방향의 변환 100 단위 및 y 방향의 80 단위입니다. 컨테이너의 월드 변형을 30도 회전입니다. 코드에서는 호출 `DrawRectangle(pen, -60, -30, 120, 60)` 두 번입니다. 첫 번째 호출은 <xref:System.Drawing.Graphics.DrawRectangle%2A> ; 컨테이너 내부 즉, 호출에 대 한 호출 사이는 <xref:System.Drawing.Graphics.BeginContainer%2A> 고 <xref:System.Drawing.Graphics.EndContainer%2A>입니다. 두 번째 호출은 <xref:System.Drawing.Graphics.DrawRectangle%2A> 호출 후 <xref:System.Drawing.Graphics.EndContainer%2A>합니다.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#61](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#61)]
 [!code-vb[System.Drawing.MiscLegacyTopics#61](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#61)]  
  
 위의 코드에서 컨테이너 내에서 그린 사각형은 변환 먼저 컨테이너 (회전)의 전역 변형 한 후의 월드 변형을 여는 <xref:System.Drawing.Graphics> 개체 (translation). 컨테이너 외부에서 그릴 사각형의 월드 변형을 의해서만 변환 되는 <xref:System.Drawing.Graphics> 개체 (translation). 다음 그림에서는 두 개의 사각형을 보여 줍니다. 
  
 ![중첩 된 컨테이너를 보여 주는 그림입니다.](./media/using-nested-graphics-containers/nested-containers-illustration.png)  
  
## <a name="clipping-in-nested-containers"></a>중첩 된 컨테이너의 클리핑  
 다음 예제에서는 어떻게 중첩 된 컨테이너 클리핑 영역을 처리 합니다. 코드는 만듭니다는 <xref:System.Drawing.Graphics> 개체와 해당 컨테이너 <xref:System.Drawing.Graphics> 개체입니다. 클립 영역을 <xref:System.Drawing.Graphics> 개체는 사각형을 및 컨테이너의 클리핑 영역 타원입니다. 코드를 두 번 호출에서는 <xref:System.Drawing.Graphics.DrawLine%2A> 메서드. 첫 번째 호출은 <xref:System.Drawing.Graphics.DrawLine%2A> 컨테이너 및 두 번째 호출은 내부 <xref:System.Drawing.Graphics.DrawLine%2A> 컨테이너를 벗어납니다 (호출 후 <xref:System.Drawing.Graphics.EndContainer%2A>). 첫 번째 줄은 두 클리핑 영역의 교집합에 의해 잘립니다. 두 번째 줄의 클리핑 사각형 영역에 의해서만 잘리는지를 <xref:System.Drawing.Graphics> 개체입니다.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#62](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#62)]
 [!code-vb[System.Drawing.MiscLegacyTopics#62](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#62)]  
  
 다음 그림에서는 두 잘린된 줄을 보여 줍니다.
  
 ![잘린된 줄을 사용 하 여 중첩 된 컨테이너를 보여 주는 그림입니다.](./media/using-nested-graphics-containers/nested-container-clipped-lines.png)  
  
 위의 두 예제 같이 변환과 클리핑 영역에 중첩 된 컨테이너에 누적 됩니다. 컨테이너의 세계 변환을 설정 하는 경우 및 <xref:System.Drawing.Graphics> 개체를 둘 다 컨테이너 내에서 그리는 항목에 적용 됩니다. 먼저 적용된 되며 변환 컨테이너의 변환 수를 <xref:System.Drawing.Graphics> 개체가 두 번째 적용 됩니다. 컨테이너의 클리핑 영역을 설정 하는 경우 및 <xref:System.Drawing.Graphics> 개체, 컨테이너 내에서 가져온 항목 두 클리핑 영역의 교집합에 의해 잘립니다.  
  
## <a name="quality-settings-in-nested-containers"></a>중첩 된 컨테이너에 대 한 품질 설정  
 품질 설정 (<xref:System.Drawing.Graphics.SmoothingMode%2A>, <xref:System.Drawing.Graphics.TextRenderingHint%2A>, 등)에 중첩 된 컨테이너 누적은 컨테이너의 품질 설정이 품질 설정을 일시적으로 대체 되는 대신는 <xref:System.Drawing.Graphics> 개체입니다. 새 컨테이너를 만들어야 하는 경우 해당 컨테이너에 대 한 품질 설정은 기본값으로 설정 됩니다. 예를 들어 있다고 가정 된 <xref:System.Drawing.Graphics> 다듬기 모드를 사용 하 여 개체 <xref:System.Drawing.Drawing2D.SmoothingMode.AntiAlias>합니다. 컨테이너를 만들면 컨테이너 안의 다듬기 모드 모드를 다듬기 기본값입니다. 컨테이너의 다듬기 모드를 설정 하는 무료 이며 설정한 모드에 따라 컨테이너 내에서 그리는 항목을 가져오게 됩니다. 항목에 대 한 호출 후 그린 <xref:System.Drawing.Graphics.EndContainer%2A> 다듬기 모드에 따라 그려집니다 (<xref:System.Drawing.Drawing2D.SmoothingMode.AntiAlias>) 호출 하기 전에 진행 된 <xref:System.Drawing.Graphics.BeginContainer%2A>합니다.  
  
## <a name="several-layers-of-nested-containers"></a>중첩 된 컨테이너의 여러 계층  
 하나의 컨테이너에 제한 되지 않습니다는 <xref:System.Drawing.Graphics> 개체입니다. 시퀀스 컨테이너를 만들 수 있습니다 하 고 앞에 중첩 된 각 세계 변환, 클리핑 영역 및 중첩된 된 컨테이너의 각 품질 설정을 지정할 수 있습니다. 가장 안쪽 컨테이너에서 그리기 메서드를 호출 하는 경우 변환은 안쪽 컨테이너 시작 및 끝 가장 바깥쪽 컨테이너를 사용 하 여 순서 대로 적용 됩니다. 항목 안쪽에 있는 컨테이너 내에서 가져온 모든 클리핑 영역의 교집합에 의해 잘립니다.  
  
 다음 예에서는 <xref:System.Drawing.Graphics> 개체와 해당 텍스트 렌더링 힌팅 설정 <xref:System.Drawing.Drawing2D.SmoothingMode.AntiAlias>합니다. 코드는 다른 중첩 된 두 개의 컨테이너를 만듭니다. 외부 컨테이너의 텍스트 렌더링 힌트로 설정 됩니다 <xref:System.Drawing.Text.TextRenderingHint.SingleBitPerPixel>, 내부 컨테이너의 텍스트 렌더링 힌트로 설정 됩니다 및 <xref:System.Drawing.Drawing2D.SmoothingMode.AntiAlias>합니다. 코드를 세 개의 문자열을 그립니다: 내부 컨테이너에서 외부 컨테이너에서 하나에서 하나를 <xref:System.Drawing.Graphics> 개체 자체입니다.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#63](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#63)]
 [!code-vb[System.Drawing.MiscLegacyTopics#63](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#63)]  
  
 다음 그림에서는 3 개의 문자열을 보여 줍니다. 내부 컨테이너에서 그리는 문자열을 <xref:System.Drawing.Graphics> 앤티앨리어싱 하 여 개체 다듬어집니다. 외부 컨테이너에서 가져온 문자열 앤티 앨리어싱 여 그라데이션이 없습니다 때문에 합니다 <xref:System.Drawing.Graphics.TextRenderingHint%2A> 속성이 <xref:System.Drawing.Text.TextRenderingHint.SingleBitPerPixel>합니다.  
  
 ![중첩 된 컨테이너에서 가져온 문자열을 보여 주는 그림입니다.](./media/using-nested-graphics-containers/nested-containers-three-strings.png)  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Graphics>
- [Graphics 개체의 상태 관리](managing-the-state-of-a-graphics-object.md)
