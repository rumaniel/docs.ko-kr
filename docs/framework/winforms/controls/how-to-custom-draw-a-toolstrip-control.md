---
title: '방법: ToolStrip 컨트롤 그리기 사용자 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- toolbars [Windows Forms], custom drawing
- drawing [Windows Forms], owner
- ProfessionalColorTable class [Windows Forms], overriding
- examples [Windows Forms], toolbars
- drawing [Windows Forms], custom
- toolbars [Windows Forms], changing colors
- ToolStrip control [Windows Forms], drawing
- ToolStrip control [Windows Forms], changing colors
- custom drawing
- owner drawing
ms.assetid: 94e7d7bd-a752-441c-b5b3-7acf98881163
ms.openlocfilehash: 810a680a1a9d9065e80ed87453a728fe628a953d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69935362"
---
# <a name="how-to-custom-draw-a-toolstrip-control"></a>방법: ToolStrip 컨트롤 그리기 사용자 지정
<xref:System.Windows.Forms.ToolStrip> 컨트롤에는 다음과 같은 연결된 렌더링(그리기) 클래스가 있습니다.  
  
- <xref:System.Windows.Forms.ToolStripSystemRenderer>는 운영 체제의 모양 및 스타일을 제공합니다.  
  
- <xref:System.Windows.Forms.ToolStripProfessionalRenderer>는 Microsoft Office의 모양 및 스타일을 제공합니다.  
  
- <xref:System.Windows.Forms.ToolStripRenderer>는 다른 두 렌더링 클래스에 대한 추상 기본 클래스입니다.  
  
 <xref:System.Windows.Forms.ToolStrip>에 대한 사용자 지정 그리기(소유자 그리기라고도 함)를 수행하기 위해 렌더러 클래스 중 하나를 재정의하고 렌더링 논리의 한 측면을 변경할 수 있습니다.  
  
 다음 절차에서는 사용자 지정 그리기의 다양한 측면을 설명합니다.  
  
### <a name="to-switch-between-the-provided-renderers"></a>제공된 렌더러 간에 전환하려면  
  
- <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> 속성을 원하는 <xref:System.Windows.Forms.ToolStripRenderMode> 값으로 설정합니다.  
  
     <xref:System.Windows.Forms.ToolStripRenderMode.ManagerRenderMode>에서는 정적 <xref:System.Windows.Forms.ToolStrip.RenderMode%2A>가 애플리케이션에 대한 렌더러를 결정합니다. <xref:System.Windows.Forms.ToolStripRenderMode>의 다른 값은 <xref:System.Windows.Forms.ToolStripRenderMode.Custom>, <xref:System.Windows.Forms.ToolStripRenderMode.Professional> 및 <xref:System.Windows.Forms.ToolStripRenderMode.System>입니다.  
  
### <a name="to-change-the-microsoft-officestyle-borders-to-straight"></a>Microsoft Office 스타일 테두리를 직선으로 변경하려면  
  
- <xref:System.Windows.Forms.ToolStripProfessionalRenderer.OnRenderToolStripBorder%2A?displayProperty=nameWithType>를 재정의하지만 기본 클래스를 호출하지 않습니다.  
  
> [!NOTE]
> <xref:System.Windows.Forms.ToolStripRenderer>, <xref:System.Windows.Forms.ToolStripSystemRenderer> 및 <xref:System.Windows.Forms.ToolStripProfessionalRenderer>에 대한 이 메서드의 버전이 있습니다.  
  
### <a name="to-change-the-professionalcolortable"></a>ProfessionalColorTable을 변경하려면  
  
- <xref:System.Windows.Forms.ProfessionalColorTable>을 재정의하고 원하는 색을 변경합니다.  
  
    ```vb  
    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As _  
    System.EventArgs) Handles Me.Load  
        Dim t As MyColorTable = New MyColorTable  
        ToolStrip1.Renderer = New ToolStripProfessionalRenderer(t)  
    End Sub  
  
    Class MyColorTable   
    Inherits ProfessionalColorTable  
  
    Public Overrides ReadOnly Property ButtonPressedGradientBegin() As Color  
        Get  
            Return Color.Red  
        End Get  
    End Property  
  
    Public Overrides ReadOnly Property ButtonPressedGradientMiddle() _  
    As System.Drawing.Color  
        Get  
            Return Color.Blue  
        End Get  
            End Property  
  
    Public Overrides ReadOnly Property ButtonPressedGradientEnd() _  
    As System.Drawing.Color  
        Get  
            Return Color.Green  
        End Get  
    End Property  
  
    Public Overrides ReadOnly Property ButtonSelectedGradientBegin() _  
    As Color  
        Get  
            Return Color.Yellow  
        End Get  
    End Property  
  
    Public Overrides ReadOnly Property ButtonSelectedGradientMiddle() As System.Drawing.Color  
        Get  
            Return Color.Orange  
        End Get  
    End Property  
  
    Public Overrides ReadOnly Property ButtonSelectedGradientEnd() _  
    As System.Drawing.Color  
        Get  
            Return Color.Violet  
        End Get  
    End Property  
    End Class  
    ```  
  
### <a name="to-change-the-rendering-for-all-toolstrip-controls-in-your-application"></a>애플리케이션의 모든 ToolStrip 컨트롤에 대한 렌더링을 변경하려면  
  
1. <xref:System.Windows.Forms.ToolStripManager.RenderMode%2A?displayProperty=nameWithType> 속성을 사용하여 제공된 렌더러 중 하나를 선택합니다.  
  
2. <xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=nameWithType>를 사용하여 사용자 지정 렌더러를 할당합니다.  
  
3. <xref:System.Windows.Forms.ToolStrip.RenderMode%2A?displayProperty=nameWithType>가 기본값인 <xref:System.Windows.Forms.ToolStripRenderMode.ManagerRenderMode>로 설정되었는지 확인합니다.  
  
### <a name="to-turn-off-the-microsoft-office-colors-for-the-entire-application"></a>전체 애플리케이션에 대해 Microsoft Office 색을 해제하려면  
  
- <xref:System.Windows.Forms.ToolStripManager.VisualStylesEnabled%2A?displayProperty=nameWithType>를 `false`로 설정합니다.  
  
### <a name="to-turn-off-the-microsoft-office-colors-for-one-toolstrip-control"></a>하나의 ToolStrip 컨트롤에 대해 Microsoft Office 색을 해제하려면  
  
- 다음 코드 예제와 유사한 코드를 사용합니다.  
  
    ```vb  
    Dim colorTable As ProfessionalColorTable()  
    colorTable.UseSystemColors = True  
    Dim toolStrip.Renderer As ToolStripProfessionalRenderer(colorTable)  
    ```  
  
    ```csharp  
    ProfessionalColorTable colorTable = new ProfessionalColorTable();  
    colorTable.UseSystemColors = true;  
    toolStrip.Renderer = new ToolStripProfessionalRenderer(colorTable);  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStripSystemRenderer>
- <xref:System.Windows.Forms.ToolStripProfessionalRenderer>
- <xref:System.Windows.Forms.ToolStripRenderer>
- [소유자 그리기 지원이 기본 제공되는 컨트롤](controls-with-built-in-owner-drawing-support.md)
- [방법: Windows Forms의 ToolStrip 컨트롤에 대 한 사용자 지정 렌더러 만들기 및 설정](create-and-set-a-custom-renderer-for-the-toolstrip-control-in-wf.md)
- [ToolStrip 컨트롤 개요](toolstrip-control-overview-windows-forms.md)
