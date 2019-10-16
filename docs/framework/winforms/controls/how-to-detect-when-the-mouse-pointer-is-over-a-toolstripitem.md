---
title: '방법: 마우스 포인터가 ToolStripItem 위에 있는 시점 감지'
ms.date: 03/30/2017
helpviewer_keywords:
- toolbars [Windows Forms], detecting mouse movement
- ToolStrip control [Windows Forms], detecting mouse movement
- ToolStripItem class [Windows Forms], detecting mouse movement
- mouse [Windows Forms], detecting movement on toolbars
ms.assetid: d38b5082-aba7-4f6c-841b-bd9714e307fd
ms.openlocfilehash: f01a9acb3a566be40d65fb075c8487d4e9cb6e73
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623637"
---
# <a name="how-to-detect-when-the-mouse-pointer-is-over-a-toolstripitem"></a>방법: 마우스 포인터가 ToolStripItem 위에 있는 시점 감지
다음 절차를 사용 하 여 마우스 포인터가 위에 있는 시기를 감지 하는 <xref:System.Windows.Forms.ToolStripItem>합니다.  
  
### <a name="to-detect-when-the-pointer-is-over-a-toolstripitem"></a>포인터가 toolstripitem을 가리키는 시점 감지 하려면  
  
- 사용 된 <xref:System.Windows.Forms.ToolStripItem.Selected%2A> 는 항목에 대 한 속성 <xref:System.Windows.Forms.ToolStripItem.CanSelect%2A> 는 `true`합니다.  
  
     동기화 할 필요가 없도록 그러면 합니다 <xref:System.Windows.Forms.ToolStripItem.MouseEnter> 및 <xref:System.Windows.Forms.ToolStripItem.MouseLeave> 이벤트입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStripItem>
- <xref:System.Windows.Forms.ToolStripItem.Selected%2A>
- [ToolStrip 컨트롤 개요](toolstrip-control-overview-windows-forms.md)
