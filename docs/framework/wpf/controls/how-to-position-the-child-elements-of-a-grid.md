---
title: '방법: Grid의 자식 요소 위치 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Grid control [WPF], positioning child elements
ms.assetid: 27b3ba9b-ad32-44e2-bcab-a79d573a463c
ms.openlocfilehash: c508f45c1ea3d0925503d6fe5600498a0558d5ad
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770804"
---
# <a name="how-to-position-the-child-elements-of-a-grid"></a>방법: Grid의 자식 요소 위치 지정
이 예제에서는 get을 사용 하 고에 정의 된 메서드를 설정 하는 방법을 보여 줍니다 <xref:System.Windows.Controls.Grid> 자식 요소의 위치입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 부모 <xref:System.Windows.Controls.Grid> 요소 (`grid1`)는 세 개의 열과 행이 3입니다. 자식 <xref:System.Windows.Shapes.Rectangle> 요소 (`rect1`)에 추가 되는 <xref:System.Windows.Controls.Grid> 열 위치 0의에서 행 위치 0입니다. <xref:System.Windows.Controls.Button> 요소 위치를 변경 하기 위해 호출할 수 있는 메서드를 나타냅니다 합니다 <xref:System.Windows.Shapes.Rectangle> 내의 요소는 <xref:System.Windows.Controls.Grid>합니다. 사용자가 단추를 클릭 하면 관련된 메서드가 활성화 됩니다.  
  
 [!code-xaml[gridGetSetMethods](~/samples/snippets/csharp/VS_Snippets_Wpf/gridGetSetMethods/CSharp/Window1.xaml)]  
  
 다음 코드 숨김 예제에서는 메서드를 처리 하는 단추 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트를 발생 시킵니다. 이 예제에서는 이러한 메서드 호출을 기록 <xref:System.Windows.Controls.TextBlock> 사용 하 여 관련 요소를 새 속성 값을 문자열로 출력 하는 메서드를 가져옵니다.  
  
 [!code-csharp[gridGetSetMethods#2](~/samples/snippets/csharp/VS_Snippets_Wpf/gridGetSetMethods/CSharp/Window1.xaml.cs#2)]
 [!code-vb[gridGetSetMethods#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/gridGetSetMethods/VisualBasic/Window1.xaml.vb#2)]  
 최종된 결과 다음과 같습니다.
 
 ![스크린 샷 두 개의 열을 사용 하 여 WPF 사용자 인터페이스, 오른쪽 3x3 격자에 보여 주며 왼쪽에 열과 그리드의 행 색이 지정 된 사각형을 이동 하는 단추가 있습니다.](././media/grid-methods-sample.png) 
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Grid>
- [패널 개요](panels-overview.md)
