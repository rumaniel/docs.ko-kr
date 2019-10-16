---
title: '방법: 모눈 간 크기 조정 속성 공유'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Grid control [WPF], sharing sizing data of columns
- sizing data in Grid controls [WPF]
- Grid control [WPF], sharing sizing data of rows
ms.assetid: a0535a6f-ff04-4b25-9912-7dd856e11044
ms.openlocfilehash: d5ab2ac612d55c8cbc34ae6d7d9d63b9f8aa23e7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910587"
---
# <a name="how-to-share-sizing-properties-between-grids"></a>방법: 모눈 간 크기 조정 속성 공유
이 예제에서는 열 크기 조정 데이터를 공유 하는 방법을 보여 줍니다 및 간에 행 <xref:System.Windows.Controls.Grid> 일관 된 크기 조정 유지 하기 위해 요소입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 개의 <xref:System.Windows.Controls.Grid> 부모의 자식 요소로 요소 <xref:System.Windows.Controls.DockPanel>합니다. 합니다 <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A> 연결 속성 <xref:System.Windows.Controls.Grid> 부모에서 정의 된 <xref:System.Windows.Controls.DockPanel>합니다.  
  
 이 예제에서는 두 개를 사용 하 여 속성 값을 조작 <xref:System.Windows.Controls.Button> 요소; 부울 속성 값의 각 요소 하나 나타냅니다. 경우는 <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A> 속성 값으로 설정 됩니다 `true`의 각 열 또는 행 멤버는 <xref:System.Windows.Controls.DefinitionBase.SharedSizeGroup%2A> 행 또는 열의 콘텐츠에 관계 없이 크기 조정 정보를 공유 합니다.  
  
 [!code-xaml[gridIssharedsizescopeProp#1](~/samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#1)]  
  
 ...  
  
 [!code-xaml[gridIssharedsizescopeProp#2](~/samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#2)]  
  
 다음 코드 숨김 예제에서는 메서드를 처리 하는 단추 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트를 발생 시킵니다. 이러한 메서드 호출의 결과 작성 하는 예제 <xref:System.Windows.Controls.TextBlock> 사용 하 여 관련 요소를 새 속성 값을 문자열로 출력 하는 메서드를 가져옵니다.  
  
 [!code-csharp[gridIssharedsizescopeProp#3](~/samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml.cs#3)]
 [!code-vb[gridIssharedsizescopeProp#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/gridIssharedsizescopeProp/VisualBasic/Window1.xaml.vb#3)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Grid>
- <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A>
- [패널 개요](panels-overview.md)
