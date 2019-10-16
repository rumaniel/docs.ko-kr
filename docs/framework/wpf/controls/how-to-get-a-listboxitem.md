---
title: '방법: ListBoxItem 가져오기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListBox controls [WPF], getting a ListBoxItem
- ListBoxItem [WPF]
ms.assetid: da877c6f-5fd8-40cb-8909-225cbfd99aa5
ms.openlocfilehash: 27a435feb4a941c77af221ab25bd63ea98b16e92
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910327"
---
# <a name="how-to-get-a-listboxitem"></a>방법: ListBoxItem 가져오기
특정 준비 해야 하는 경우 <xref:System.Windows.Controls.ListBoxItem> 특정 인덱스에는 <xref:System.Windows.Controls.ListBox>를 사용할 수 있습니다는 <xref:System.Windows.Controls.ItemContainerGenerator>.  
  
## <a name="example"></a>예제  
 다음 예제는 <xref:System.Windows.Controls.ListBox> 와 해당 항목입니다.  
  
 [!code-xaml[ListBoxItems#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxItems/CSharp/Window1.xaml#1)]  
  
 다음 예제에 있는 항목의 인덱스를 지정 하 여 항목을 검색 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Controls.ItemContainerGenerator.ContainerFromIndex%2A> 의 속성을 <xref:System.Windows.Controls.ItemContainerGenerator>합니다.  
  
 [!code-csharp[ListBoxItems#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxItems/CSharp/Window1.xaml.cs#2)]
 [!code-vb[ListBoxItems#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListBoxItems/VisualBasic/Window1.xaml.vb#2)]  
  
 목록 상자 항목을 검색 한 후에 다음 예제에서와 같이 항목의 내용을 표시할 수 있습니다.  
  
 [!code-csharp[ListBoxItems#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxItems/CSharp/Window1.xaml.cs#3)]
 [!code-vb[ListBoxItems#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListBoxItems/VisualBasic/Window1.xaml.vb#3)]
