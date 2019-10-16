---
title: '방법: 끌어온 GridView 열 머리글에 대한 스타일 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- ListView controls [WPF], styling
ms.assetid: 0b999645-0313-4b33-80b9-19ece08b5459
ms.openlocfilehash: dbcdd38e0397b8e637aff962420a2959f33203df
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910886"
---
# <a name="how-to-create-a-style-for-a-dragged-gridview-column-header"></a>방법: 끌어온 GridView 열 머리글에 대한 스타일 만들기
이 예제는 끌어 온된 모양의 변경 하는 방법을 보여 줍니다 <xref:System.Windows.Controls.GridViewColumnHeader> 사용자가 열의 위치를 변경 하는 경우.  
  
## <a name="example"></a>예제  
 다른 위치로 열 머리글을 끌면를 <xref:System.Windows.Controls.ListView> 를 사용 하는 <xref:System.Windows.Controls.GridView> 보기 모드에 대 한 열을 새 위치로 이동 합니다. 열 머리글을 끄는 동안 헤더의 움직이는 복사본이 원래 머리글 외에도 표시 됩니다. 열 머리글을 <xref:System.Windows.Controls.GridView> 으로 표시 됩니다는 <xref:System.Windows.Controls.GridViewColumnHeader> 개체입니다.  
  
 부동 및 원래 머리글 모두의 모양을 사용자 지정 하려면 설정할 수 있습니다 <xref:System.Windows.Controls.ControlTemplate.Triggers%2A> 수정 하는 <xref:System.Windows.Controls.GridViewColumnHeader> <xref:System.Windows.Style>합니다. 이러한 <xref:System.Windows.Controls.ControlTemplate.Triggers%2A> 때 적용 되는 <xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> 속성 값이 `true` 하며 <xref:System.Windows.Controls.GridViewColumnHeader.Role%2A> 속성 값이 <xref:System.Windows.Controls.GridViewColumnHeaderRole.Floating>합니다.  
  
 사용자의 마우스 단추를 누를 누르고 위에 마우스를 일시 중지할 경우 합니다 <xref:System.Windows.Controls.GridViewColumnHeader>의 <xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> 속성 값이 변경 `true`합니다. 마찬가지로, 사용자가 시작할 때 끌기 작업을 <xref:System.Windows.Controls.GridViewColumnHeader.Role%2A> 속성 변경 <xref:System.Windows.Controls.GridViewColumnHeaderRole.Floating>합니다.  
  
 다음 예제에서는 설정 하는 방법을 보여 줍니다 <xref:System.Windows.Controls.ControlTemplate.Triggers%2A> 변경 하는 <xref:System.Windows.Controls.Control.Foreground%2A> 및 <xref:System.Windows.Controls.Control.Background%2A> 사용자가 열을 새 위치로 끌 때 원래 머리글과 부동 머리글의 색입니다.  
  
 [!code-xaml[ListViewHeaderRoleStyle#GVCHControlTemplateStart](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#gvchcontroltemplatestart)]  
[!code-xaml[ListViewHeaderRoleStyle#ControlTemplateTriggersStart](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#controltemplatetriggersstart)]  
[!code-xaml[ListViewHeaderRoleStyle#IsPressed](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#ispressed)]  
[!code-xaml[ListViewHeaderRoleStyle#Floating](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#floating)]  
[!code-xaml[ListViewHeaderRoleStyle#ControlTemplateTriggersEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#controltemplatetriggersend)]  
[!code-xaml[ListViewHeaderRoleStyle#GVCHControlTemplateEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#gvchcontroltemplateend)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.GridViewColumnHeader>
- <xref:System.Windows.Controls.GridViewColumnHeaderRole>
- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [방법 항목](listview-how-to-topics.md)
- [ListView 개요](listview-overview.md)
- [GridView 개요](gridview-overview.md)
