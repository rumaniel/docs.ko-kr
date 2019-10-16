---
title: '방법: Windows Forms에서 ToolStrip 컨트롤에 대한 사용자 지정 렌더러 만들기 및 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolStrip control [Windows Forms], custom rendering
- toolbars [Windows Forms], rendering
- examples [Windows Forms], toolbars
- ToolStrip control [Windows Forms], rendering
ms.assetid: 88a804ba-679f-4ba3-938a-0dc396199c5b
ms.openlocfilehash: c354ace3a7d3ce43f549dd1295a85fbee004eb22
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69929737"
---
# <a name="how-to-create-and-set-a-custom-renderer-for-the-toolstrip-control-in-windows-forms"></a>방법: Windows Forms에서 ToolStrip 컨트롤에 대한 사용자 지정 렌더러 만들기 및 설정
<xref:System.Windows.Forms.ToolStrip>컨트롤을 통해 테마와 스타일을 쉽게 지원할 수 있습니다. <xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=nameWithType> 속성<xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=nameWithType> 또는 속성 중 하나를 사용자 지정 렌더러에서 설정 하 여 사용자 지정 모양 및 동작 (모양 및 느낌)을 구현할 수 있습니다.  
  
 각 <xref:System.Windows.Forms.ToolStrip>개별 <xref:System.Windows.Forms.ToolStripRenderMode.ManagerRenderMode?displayProperty=nameWithType>, <xref:System.Windows.Forms.MenuStrip> <xref:System.Windows.Forms.ToolStrip.RenderMode%2A?displayProperty=nameWithType> , <xref:System.Windows.Forms.ContextMenuStrip> 또는<xref:System.Windows.Forms.StatusStrip>컨트롤 에 렌더러를 할당 하거나 속성을로 설정 하 여 모든 개체에 영향을 주는 속성을사용할수있습니다.<xref:System.Windows.Forms.ToolStripManager.Renderer%2A>  
  
> [!NOTE]
> <xref:System.Windows.Forms.ToolStrip.RenderMode%2A>`null`의 <xref:System.Windows.Forms.ToolStripRenderMode.Custom> 값<xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=nameWithType> 이이 아닌 경우에만를 반환 합니다.  
  
### <a name="to-create-a-custom-renderer"></a>사용자 지정 렌더러를 만들려면  
  
1. 클래스를 <xref:System.Windows.Forms.ToolStripRenderer> 확장 합니다.  
  
2. 적절 한를 재정의 하 여 원하는 사용자 지정 렌더링 *을* 구현 합니다. 멤버  
  
    ```vb  
    Public Class RedTextRenderer  
        Inherits System.Windows.Forms.ToolStripRenderer  
        Protected Overrides Sub OnRenderItemText(ByVal e As _  
            ToolStripItemTextRenderEventArgs)   
            e.TextColor = Color.Red  
            e.TextFont = New Font("Helvetica", 7, FontStyle.Bold)  
            MyBase.OnRenderItemText(e)  
        End Sub  
    End Class  
    ```  
  
    ```csharp  
    public class RedTextRenderer : _  
        System.Windows.Forms.ToolStripRenderer  
    {  
        protected override void _  
            OnRenderItemText(ToolStripItemTextRenderEventArgs e)  
        {  
            e.TextColor = Color.Red;  
            e.TextFont = new Font("Helvetica", 7, FontStyle.Bold);  
           base.OnRenderItemText(e);  
        }  
    }  
    ```  
  
### <a name="to-set-the-custom-renderer-to-be-the-current-renderer"></a>사용자 지정 렌더러를 현재 렌더러에서 설정 하려면  
  
1. 하나 <xref:System.Windows.Forms.ToolStrip>에 대 한 사용자 지정 렌더러를 설정 하려면 <xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=nameWithType> 속성을 사용자 지정 렌더러로 설정 합니다.  
  
    ```vb  
    toolStrip1.Renderer = New RedTextRenderer()  
    ```  
  
    ```csharp  
    toolStrip1.Renderer = new RedTextRenderer();  
    ```  
  
2. 또는 응용 프로그램에 포함 된 모든 <xref:System.Windows.Forms.ToolStrip> 클래스에 대 한 사용자 지정 렌더러를 설정 하려면 다음을 수행 합니다. 속성을 사용자 지정 렌더러로 설정 하 고 <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> 속성을로 <xref:System.Windows.Forms.ToolStripRenderMode.ManagerRenderMode>설정 합니다. <xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=nameWithType>  
  
    ```vb  
    toolStrip1.RenderMode = ToolStripRenderMode.ManagerRenderMode  
    ToolStripManager.Renderer = New RedTextRenderer()  
    ```  
  
    ```csharp  
    toolStrip1.RenderMode = ToolStripRenderMode.ManagerRenderMode;  
    ToolStripManager.Renderer = new RedTextRenderer();  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStripManager.Renderer%2A>
- <xref:System.Windows.Forms.ToolStripRenderer>
- <xref:System.Windows.Forms.ToolStrip.RenderMode%2A>
- [ToolStrip 컨트롤 개요](toolstrip-control-overview-windows-forms.md)
- [ToolStrip 컨트롤 아키텍처](toolstrip-control-architecture.md)
- [ToolStrip 기술 요약](toolstrip-technology-summary.md)
