---
title: '방법: 컨트롤에 투명한 배경 적용'
ms.date: 03/30/2017
helpviewer_keywords:
- transparent backgrounds [Windows Forms], custom controls
- custom controls [Windows Forms], transparent background
- transparency [Windows Forms], Windows Forms custom controls
ms.assetid: 32433e63-f4e9-4305-9857-6de3edeb944a
ms.openlocfilehash: a82807ea3873b2217d1f05f6c720c599ea79abdd
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966648"
---
# <a name="how-to-give-your-control-a-transparent-background"></a>방법: 컨트롤에 투명한 배경 적용
.NET Framework의 이전 버전에서는 양식 생성자에 먼저 <xref:System.Windows.Forms.Control.SetStyle%2A> 메서드를 설정하지 않으면 컨트롤이 투명 배경색 설정을 지원하지 않았습니다. 현재 프레임워크 버전에서는 대부분의 컨트롤에 대한 배경색을 디자인 타임에 <xref:System.Drawing.Color.Transparent%2A> 속성 **창 또는 양식 생성자의 코드에서** 으로 설정할 수 있습니다.  
  
> [!NOTE]
> Windows Forms 컨트롤은 진정한 투명성을 지원하지 않습니다. 투명한 Windows Forms 컨트롤의 배경은 해당 부모가 색칠합니다.  
  
> [!NOTE]
> <xref:System.Windows.Controls.Button> 속성이 <xref:System.Windows.Forms.ButtonBase.BackColor%2A> 으로 설정된 경우에도 <xref:System.Drawing.Color.Transparent%2A>컨트롤은 투명한 배경색을 지원하지 않습니다.  
  
### <a name="to-give-your-control-a-transparent-backcolor"></a>컨트롤에 투명한 배경색을 적용하려면  
  
- 속성 창에서 <xref:System.Windows.Forms.ButtonBase.BackColor%2A> 속성을 선택하고 <xref:System.Drawing.Color.Transparent%2A>으로 설정합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Color.FromArgb%2A>
- [.NET Framework에서 사용자 지정 Windows Forms 컨트롤 개발](developing-custom-windows-forms-controls.md)
- [관리되는 그래픽 클래스 사용](../advanced/using-managed-graphics-classes.md)
- [방법: 불투명 및 반투명 선 그리기](../advanced/how-to-draw-opaque-and-semitransparent-lines.md)
