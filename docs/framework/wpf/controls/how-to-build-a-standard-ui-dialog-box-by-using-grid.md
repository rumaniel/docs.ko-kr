---
title: '방법: Grid를 사용하여 표준 UI 대화 상자 빌드'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dialog boxes [WPF], creating
- Grid control [WPF], creating [WPF], dialog box
ms.assetid: d6ac3d51-844b-4d29-96d8-81a696a7b960
ms.openlocfilehash: 68c9653e616388374aad2ad33ac7dab68446241d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923417"
---
# <a name="how-to-build-a-standard-ui-dialog-box-by-using-grid"></a>방법: Grid를 사용하여 표준 UI 대화 상자 빌드
이 예제에서는 요소를 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] <xref:System.Windows.Controls.Grid> 사용 하 여 표준 대화 상자를 만드는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 Windows 운영 체제에서 **실행** 대화 상자와 같은 대화 상자를 만듭니다.  
  
 이 예제에서는를 <xref:System.Windows.Controls.Grid> 만들고 <xref:System.Windows.Controls.ColumnDefinition> 및 <xref:System.Windows.Controls.RowDefinition> 클래스를 사용 하 여 5 개의 열과 4 개의 행을 정의 합니다.  
  
 그런 다음이 예제에서는 대화 상자 <xref:System.Windows.Controls.Image>에 `RunIcon.png`있는 이미지를 나타내기 위해,를 추가 하 고 배치 합니다. 이미지는의 <xref:System.Windows.Controls.Grid> 첫 번째 열과 행 (왼쪽 위 모퉁이)에 배치 됩니다.  
  
 그런 다음 첫 번째 행의 <xref:System.Windows.Controls.TextBlock> 나머지 열을 포함 하는 첫 번째 열에 요소를 추가 합니다. 첫 번째 열의 <xref:System.Windows.Controls.TextBlock> 두 번째 행에 다른 요소를 추가 하 여 **열린** 텍스트 상자를 나타냅니다. 는 <xref:System.Windows.Controls.TextBlock> 데이터 입력 영역을 나타내는와 같습니다.  
  
 마지막으로,이 예에서는 <xref:System.Windows.Controls.Button> **확인**, **취소**및 **찾아보기** 이벤트를 나타내는 세 개의 요소를 최종 행에 추가 합니다.  
  
 [!code-csharp[GridRunDialog#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridRunDialog/CSharp/window1.xaml.cs#1)]
 [!code-vb[GridRunDialog#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GridRunDialog/VisualBasic/grid_vb.vb#1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Grid>
- <xref:System.Windows.GridUnitType>
- [패널 개요](panels-overview.md)
- [방법 항목](grid-how-to-topics.md)
