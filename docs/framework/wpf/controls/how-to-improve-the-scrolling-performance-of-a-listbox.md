---
title: '방법: ListBox의 스크롤 성능 향상'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListBox control [WPF], reusing item containers
- ListBox control [WPF], improving scrolling performance
ms.assetid: 1e2bf8f3-c8ce-47f7-a400-a7fe11d1a848
ms.openlocfilehash: a9d1ca1d8ac2ef830984408f3052eb0ed0987c5d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770866"
---
# <a name="how-to-improve-the-scrolling-performance-of-a-listbox"></a>방법: ListBox의 스크롤 성능 향상
경우는 <xref:System.Windows.Controls.ListBox> 많은 항목이 사용자가 스크롤할 때 사용자 인터페이스가 응답 속도가 느려질 수 있습니다는 <xref:System.Windows.Controls.ListBox> 마우스 휠을 사용 하거나, 스크롤 막대의 엄지 단추를 끌어 합니다. 성능을 향상 시킬 수 있습니다 합니다 <xref:System.Windows.Controls.ListBox> 설정 하 여 사용자가 스크롤할 때 합니다 `VirtualizingStackPanel.VirtualizationMode` 연결 된 속성을 <xref:System.Windows.Controls.VirtualizationMode.Recycling?displayProperty=nameWithType>입니다.  
  
## <a name="example"></a>예제  
  
## <a name="description"></a>설명  
다음 예제에서는 <xref:System.Windows.Controls.ListBox> 가져오거나 설정 합니다 `VirtualizingStackPanel.VirtualizationMode` 연결 된 속성을 <xref:System.Windows.Controls.VirtualizationMode.Recycling?displayProperty=nameWithType> 스크롤 하는 동안 성능 향상을 위해.  
  
## <a name="code"></a>코드  
 [!code-xaml[RecycleItemContainerShippets#VirtualizationMode](~/samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml#virtualizationmode)]  
  
 다음 예제에서는 이전 예제에 사용 데이터를 보여 줍니다.  
  
 [!code-csharp[RecycleItemContainerShippets#ListBoxData](~/samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml.cs#listboxdata)]
 [!code-vb[RecycleItemContainerShippets#ListBoxData](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RecycleItemContainerShippets/visualbasic/window1.xaml.vb#listboxdata)]
