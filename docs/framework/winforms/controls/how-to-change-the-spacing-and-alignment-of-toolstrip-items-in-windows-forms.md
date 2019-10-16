---
title: '방법: Windows Forms에서 ToolStrip 항목의 간격 및 맞춤 변경'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolStrip control [Windows Forms], aligning items
- examples [Windows Forms], toolbars
- toolbars [Windows Forms], aligning items
ms.assetid: cd483466-0f49-43df-addf-e2b5fcd64027
ms.openlocfilehash: c7a874659be8dbaec66b78e1e065bcbec21da3b4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64650873"
---
# <a name="how-to-change-the-spacing-and-alignment-of-toolstrip-items-in-windows-forms"></a>방법: Windows Forms에서 ToolStrip 항목의 간격 및 맞춤 변경
합니다 <xref:System.Windows.Forms.ToolStrip> 컨트롤 크기 조정 간격 등의 레이아웃 기능을 완벽 하 게 지원 <xref:System.Windows.Forms.ToolStripItem> 의 서로 상대적인, 컨트롤 배열을 컨트롤에 <xref:System.Windows.Forms.ToolStrip>, 및 간격을 기준으로 컨트롤의는 <xref:System.Windows.Forms.ToolStrip>합니다.  
  
 때문에 기본값인 합니다 <xref:System.Windows.Forms.ToolStripItem.AutoSize%2A> 속성은 `true`, 컨트롤의 크기가 자동으로 설정 하지 않으면를 <xref:System.Windows.Forms.ToolStripItem.AutoSize%2A> 속성을 `false`입니다.  
  
### <a name="to-manually-size-a-toolstripitem"></a>ToolStripItem의 크기를 수동으로 조정 하려면  
  
1. 설정 된 <xref:System.Windows.Forms.ToolStripItem.AutoSize%2A> 속성을 `false` 연결된 된 컨트롤에 대 한 합니다.  
  
    ```vb  
    ToolStripButton1.AutoSize = False  
    ```  
  
    ```csharp  
    toolStripButton1.AutoSize = false;  
    ```  
  
2. 설정 된 <xref:System.Windows.Forms.ToolStripItem.Size%2A> 관련 된 원하는 방식으로 속성 <xref:System.Windows.Forms.ToolStripItem>합니다.  
  
### <a name="to-set-the-spacing-of-a-toolstripitem"></a>ToolStripItem의 간격을 설정 하려면  
  
1. 픽셀을 원하는 값을 삽입 합니다 <xref:System.Windows.Forms.ToolStripItem.Margin%2A> 연결된 된 컨트롤의 속성입니다.  
  
     값을 <xref:System.Windows.Forms.ToolStripItem.Margin%2A> 순서로 항목과 인접 항목 사이의 간격을 지정 하는 속성: 왼쪽, 위쪽, 오른쪽 및 아래입니다.  
  
    ```vb  
    ToolStripTextBox1.Margin = New System.Windows.Forms.Padding _  
        (3, 0, 3, 0)  
    ```  
  
    ```csharp  
    toolStripTextBox1.Margin = new System.Windows.Forms.Padding   
        (3, 0, 3, 0);  
    ```  
  
### <a name="to-align-a-toolstripitem-to-the-right-side-of-the-toolstrip"></a>오른쪽 ToolStrip에 toolstripitem을 가리키는 맞게  
  
1. 설정 된 <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 속성을 <xref:System.Windows.Forms.ToolStripItemAlignment.Right> 연결된 된 컨트롤에 대 한 합니다. 기본적으로 <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 로 설정 된 <xref:System.Windows.Forms.ToolStripItemAlignment.Left>, 컨트롤의 왼쪽에 맞춰집니다는 <xref:System.Windows.Forms.ToolStrip>합니다.  
  
    ```vb  
    ToolStripSplitButton1.Alignment = _  
        System.Windows.Forms.ToolStripItemAlignment.Right  
    ```  
  
    ```csharp  
    toolStripSplitButton1.Alignment =   
        System.Windows.Forms.ToolStripItemAlignment.Right;  
    ```  
  
### <a name="to-arrange-toolstrip-items-on-the-toolstrip"></a>ToolStrip에서 ToolStrip 항목을 정렬 하려면  
  
- 설정 된 <xref:System.Windows.Forms.ToolStrip.LayoutStyle%2A> 속성의 값을 <xref:System.Windows.Forms.ToolStripLayoutStyle> 원하는 합니다.  
  
    ```vb  
    ToolStripDropDown1.LayoutStyle = _  
        System.Windows.Forms.ToolStripLayoutStyle.Flow  
    ```  
  
    ```csharp  
    toolStripDropDown1.LayoutStyle =   
        System.Windows.Forms.ToolStripLayoutStyle.Flow;  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.Control.Layout>
- <xref:System.Windows.Forms.ToolStrip.LayoutCompleted>
- <xref:System.Windows.Forms.ToolStrip.LayoutSettings%2A>
- <xref:System.Windows.Forms.ToolStripItem.TextImageRelation%2A>
- <xref:System.Windows.Forms.ToolStripItem.Placement%2A>
- <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A>
- [ToolStrip 컨트롤 개요](toolstrip-control-overview-windows-forms.md)
- [ToolStrip 컨트롤 아키텍처](toolstrip-control-architecture.md)
- [ToolStrip 기술 요약](toolstrip-technology-summary.md)
