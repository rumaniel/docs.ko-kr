---
title: '방법: 데이터에 ListBox 바인딩'
ms.date: 03/30/2017
helpviewer_keywords:
- ListBox controls [WPF], binding data to
- data binding [WPF], ListBox control
- binding data [WPF], to ListBox control
ms.assetid: de93a907-709a-44a7-84bf-578b846a3d8b
ms.openlocfilehash: 4dea53a524247d18628b3e7e7b2c06906dced53d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911159"
---
# <a name="how-to-bind-a-listbox-to-data"></a>방법: 데이터에 ListBox 바인딩
응용 프로그램 개발자가 만들 수 있습니다 <xref:System.Windows.Controls.ListBox> 각각의 내용을 지정 하지 않고 컨트롤 <xref:System.Windows.Controls.ListBoxItem> 개별적으로 합니다. 개별 항목에 데이터를 바인딩할 데이터 바인딩을 사용할 수 있습니다.  
  
 다음 예제에서는 만드는 방법을 보여 줍니다.는 <xref:System.Windows.Controls.ListBox> 채우는 합니다 <xref:System.Windows.Controls.ListBoxItem> 라는 데이터 원본에 데이터 바인딩하여 요소 *색*합니다. 사용 하 여 필요 없는 경우 <xref:System.Windows.Controls.ListBoxItem> 각 항목의 내용을 지정 하는 태그입니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[ListBoxEvent#7](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxEvent/CSharp/Pane1.xaml#7)]  
[!code-xaml[ListBoxEvent#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxEvent/CSharp/Pane1.xaml#3)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ListBox>
- <xref:System.Windows.Controls.ListBoxItem>
- [컨트롤](../advanced/optimizing-performance-controls.md)
