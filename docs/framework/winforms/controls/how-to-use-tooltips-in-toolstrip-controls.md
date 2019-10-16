---
title: '방법: ToolStrip 컨트롤에서 도구 설명 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- ToolStrip control [Windows Forms], adding tooltips
- toolbars [Windows Forms], adding tooltips
- tooltips [Windows Forms], adding
ms.assetid: c5d86024-a7c5-44ee-8b3f-2daf53d80d3e
ms.openlocfilehash: 3f383b6cccba7825637ea65a0e13280b91b406c9
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939727"
---
# <a name="how-to-use-tooltips-in-toolstrip-controls"></a>방법: ToolStrip 컨트롤에서 도구 설명 사용
<xref:System.Windows.Forms.ToolTip> 컨트롤의 <xref:System.Windows.Forms.ToolStrip> 속성을`true`로 설정 하 여 원하는 컨트롤의를 표시할 수 있습니다. <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A>  
  
### <a name="to-display-a-tooltip"></a>도구 설명을 표시 하려면  
  
- `true`컨트롤의 <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A> 속성을로 설정 합니다.  
  
     의 <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A?displayProperty=nameWithType> 기본값은이 `true`고, 및 <xref:System.Windows.Forms.MenuStrip.ShowItemToolTips%2A?displayProperty=nameWithType> <xref:System.Windows.Forms.StatusStrip.ShowItemToolTips%2A?displayProperty=nameWithType> 의`false`기본값은입니다.  
  
### <a name="to-use-the-tooltiptext-property-for-the-tooltip-text-of-a-toolstripbutton"></a>ToolStripButton의 도구 설명 텍스트에 ToolTipText 속성을 사용 하려면  
  
1. 단추의 속성을로 `true`설정 합니다. <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A>  
  
2. 단추의 속성을로 `false`설정 합니다. <xref:System.Windows.Forms.ToolStripButton.AutoToolTip%2A?displayProperty=nameWithType>  
  
     <xref:System.Windows.Forms.ToolStripButton> 속성은<xref:System.Windows.Forms.ToolStripSplitButton>기본적 `true` 으로 ,<xref:System.Windows.Forms.ToolStripDropDownButton>및에 대해입니다. `AutoToolTip`  
  
     는 <xref:System.Windows.Forms.ToolStripButton> 기본적으로 `Text` <xref:System.Windows.Forms.ToolTip> 텍스트에 대해 해당 속성을 사용 합니다. 이 절차를 사용 하 여에 <xref:System.Windows.Forms.ToolStripButton> <xref:System.Windows.Forms.ToolTip>사용자 지정 텍스트를 표시할 수 있습니다.  
  
> [!NOTE]
> 를 또는 <xref:System.Windows.Forms.ToolStripItemDisplayStyle> 로<xref:System.Windows.Forms.ToolStripItemDisplayStyle.Image>설정 하면 단추에 텍스트가 표시 되지 않지만 도구 설명이 계속 표시 됩니다. <xref:System.Windows.Forms.ToolStripItemDisplayStyle.None>  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A>
- <xref:System.Windows.Forms.ToolStripButton>
- <xref:System.Windows.Forms.ToolStripDropDownButton>
- <xref:System.Windows.Forms.ToolStripSplitButton>
- [ToolStrip 컨트롤 개요](toolstrip-control-overview-windows-forms.md)
