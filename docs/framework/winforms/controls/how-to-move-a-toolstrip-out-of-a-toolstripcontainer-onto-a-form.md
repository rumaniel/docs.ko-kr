---
title: '방법: ToolStripContainer에서 양식으로 ToolStrip 이동'
ms.date: 03/30/2017
helpviewer_keywords:
- ToolStrip control [Windows Forms], parenting to forms
- Windows Forms, parenting ToolStrip controls
ms.assetid: a1c94a7f-6fc5-4e4c-84cf-ff11dc573d33
ms.openlocfilehash: c6519add6789485d41146633abb5e11f80913649
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69039821"
---
# <a name="how-to-move-a-toolstrip-out-of-a-toolstripcontainer-onto-a-form"></a>방법: ToolStripContainer에서 양식으로 ToolStrip 이동
다음 절차를 사용 하 여를 <xref:System.Windows.Forms.ToolStrip> 에서 <xref:System.Windows.Forms.ToolStripContainer> 폼으로 이동할 수 있습니다.

## <a name="to-move-a-toolstrip-out-of-a-toolstripcontainer-onto-a-form"></a>ToolStripContainer의 ToolStrip을 폼으로 이동 하려면

1. <xref:System.Windows.Forms.ToolStrip>를 선택합니다.

2. CTRL + <xref:System.Windows.Forms.ToolStrip> X를 눌러를 자르거나,를 <xref:System.Windows.Forms.ToolStrip> 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 **잘라내기** 를 선택 합니다.

3. 양식을 선택 합니다.

4. CTRL + <xref:System.Windows.Forms.ToolStrip> V를 눌러를 붙여넣거나 **편집** 메뉴에서 **붙여넣기** 를 선택 합니다.

5. 의 속성을 **Top**으로 설정 합니다. <xref:System.Windows.Forms.ToolStrip> <xref:System.Windows.Forms.ToolStrip.Dock%2A>

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.ToolStripContainer>
- [ToolStrip 컨트롤 개요](toolstrip-control-overview-windows-forms.md)
