---
title: '방법: Grid 요소 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Grid control [WPF], creating [WPF], grid instance
ms.assetid: b2f07626-9df8-43b8-8d36-492f3cb42837
ms.openlocfilehash: ebb9369da73bd595338e5b6ef42bda639bde6ed4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001364"
---
# <a name="how-to-create-a-grid-element"></a>방법: Grid 요소 만들기
## <a name="example"></a>예제  
 다음 예제에서는 만들고의 인스턴스를 사용 하는 방법을 보여 줍니다 <xref:System.Windows.Controls.Grid> 중 하나를 사용 하 여 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 또는 코드입니다. 이 예제에서는 세 <xref:System.Windows.Controls.ColumnDefinition> 개체 및 3 <xref:System.Windows.Controls.RowDefinition> 9에 있는 표를 만들려면 셀, 워크시트와 같이 개체입니다. 각 셀을 포함을 <xref:System.Windows.Controls.TextBlock> 데이터 및 맨 위 행을 나타내는 요소에 포함 되어는 <xref:System.Windows.Controls.TextBlock> 사용 하 여를 <xref:System.Windows.Controls.Grid.ColumnSpan%2A> 적용 하는 속성입니다. 각 셀의 경계를 표시 하는 <xref:System.Windows.Controls.Grid.ShowGridLines%2A> 속성을 사용할 수 있습니다.  
  
 [!code-csharp[Grid#3](~/samples/snippets/csharp/VS_Snippets_Wpf/Grid/CSharp/Grid_Code.cs#3)]
 [!code-vb[Grid#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Grid/VisualBasic/grid_vb.vb#3)]
 [!code-xaml[Grid#3](~/samples/snippets/xaml/VS_Snippets_Wpf/Grid/XAML/default.xaml#3)]  
  
  어느 방법이 든 아래와 같이 동일한 훨씬 보이는 사용자 인터페이스를 생성 합니다.

  ![스크린샷 세 개의 열을 분할할 표를 포함 하는 WPF 사용자 인터페이스를 보여 줍니다.  ' 2018 제공 되는 제품은 ' 맨 위 행의 모든 열에 걸친 제목 되 게 하 고 판매 수치를 사용 하 여 세 열 특정 사분기에 합니다.  아래쪽 행에 텍스트 메시지를 사용 하 여 두 열에 걸친 ' 총 단위: 300,000'](././media/how-to-create-a-grid-element/how-to-create-a-grid-element.png)
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Grid>
- [패널 개요](panels-overview.md)
