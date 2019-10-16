---
title: '방법: BindingSource ResetItem 메서드를 사용하여 변경 알림 발생'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- change notifications [Windows Forms], raising
- data binding [Windows Forms], change notifications
- BindingSource component [Windows Forms], raising change notifications with
- data sources [Windows Forms], detecting changes
- change notifications
ms.assetid: ab8b4096-37ff-4e30-aabc-de79a2f2e972
ms.openlocfilehash: 39beb5c7162fb01a51360330216687c158ff433c
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65583715"
---
# <a name="how-to-raise-change-notifications-using-the-bindingsource-resetitem-method"></a>방법: BindingSource ResetItem 메서드를 사용하여 변경 알림 발생
컨트롤에 대한 일부 데이터 소스는 항목이 변경, 추가 또는 삭제될 때 변경 알림을 발생시키지 않습니다. <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용하여 이러한 데이터 소스에 바인딩하고 코드에서 변경 알림을 발생시킬 수 있습니다.  
  
## <a name="example"></a>예제  
 이 폼은 <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용하여 목록을 <xref:System.Windows.Forms.DataGridView> 컨트롤에 바인딩하는 방법을 보여 줍니다. 목록에서 변경 알림이 발생하지 않으므로 <xref:System.Windows.Forms.BindingSource>의 <xref:System.Windows.Forms.BindingSource.ResetItem%2A> 메서드는 목록의 항목이 변경될 때 호출됩니다. .  
  
 [!code-cpp[System.Windows.Forms.DataConnector.ResetItem#1](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataConnector.ResetItem/CPP/form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.DataConnector.ResetItem#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnector.ResetItem/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.DataConnector.ResetItem#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnector.ResetItem/VB/form1.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System, System.Data, System.Drawing 및 System.Windows.Forms 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.BindingNavigator>
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.BindingSource>
- [BindingSource 구성 요소](bindingsource-component.md)
- [방법: 형식에는 Windows Forms 컨트롤 바인딩](how-to-bind-a-windows-forms-control-to-a-type.md)
