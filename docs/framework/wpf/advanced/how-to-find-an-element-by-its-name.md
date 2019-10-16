---
title: '방법: 이름에 따라 요소 찾기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- elements [WPF], finding by name
ms.assetid: cfa7cf35-8aa2-4060-9454-872ed4af3f0e
ms.openlocfilehash: 7405f9ba8db5d4db0ce35ca250f13e456685f39b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61757848"
---
# <a name="how-to-find-an-element-by-its-name"></a>방법: 이름에 따라 요소 찾기
이 예제를 사용 하는 방법에 설명 합니다 <xref:System.Windows.FrameworkElement.FindName%2A> 메서드는 요소를 해당 <xref:System.Windows.FrameworkElement.Name%2A> 값.  
  
## <a name="example"></a>예제  
 이 예제에서는 이름을 사용 하 여 특정 요소를 찾는 방법 단추 이벤트 처리기로 기록 됩니다. `stackPanel` <xref:System.Windows.FrameworkElement.Name%2A> 루트 <xref:System.Windows.FrameworkElement> 검색 중인 문서를 나타내고 예제 메서드에서 다음 시각적으로 찾은 요소의 캐스팅 하 여 <xref:System.Windows.Controls.TextBlock> 중 하나를 변경 하 고를 <xref:System.Windows.Controls.TextBlock> 표시 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 속성.  
  
 [!code-csharp[FEFindName#Find](~/samples/snippets/csharp/VS_Snippets_Wpf/FEFindName/CSharp/default.xaml.cs#find)]
 [!code-vb[FEFindName#Find](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FEFindName/VisualBasic/default.xaml.vb#find)]
