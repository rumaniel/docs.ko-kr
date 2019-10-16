---
title: '방법: ToolStrip 컨트롤에서 설정/해제 단추 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- toggle buttons [Windows Forms], creating
- examples [Windows Forms], toolbars
- ToolStrip control [Windows Forms], creating toggle buttons
ms.assetid: d9c197df-4c65-43f2-beee-b68b52b2befc
ms.openlocfilehash: 6a003b91cd4db5db2790a20db97dbaa4d8925e96
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68972357"
---
# <a name="how-to-create-toggle-buttons-in-toolstrip-controls"></a>방법: ToolStrip 컨트롤에서 설정/해제 단추 만들기

사용자가 토글 단추를 클릭 하면 오목 하 게 나타나고 사용자가 단추를 다시 클릭할 때까지 오목 하 게 유지 됩니다.

## <a name="to-create-a-toggling-toolstripbutton"></a>전환 ToolStripButton을 만들려면

- 다음 코드 예제와 같은 코드를 사용 합니다. 이 코드 <xref:System.Windows.Forms.ToolStrip> 에서는 폼에 컨트롤이 포함 되어 있고 해당 <xref:System.Windows.Forms.ToolStrip.Items%2A> 컬렉션에 <xref:System.Windows.Forms.ToolStripButton> 호출 `toolStripButton1`된이 포함 되어 있다고 가정 합니다. 또한 이라는 `toolStripButton1_CheckedChanged`이벤트 처리기가 있는 것으로 가정 합니다.

    ```vb
    toolStripButton1.CheckOnClick = True
    toolStripButton1.CheckedChanged AddressOf _
    EventHandler(toolStripButton1_CheckedChanged);
    ```

    ```csharp
    toolStripButton1.CheckOnClick = true;
    toolStripButton1.CheckedChanged += new _
    EventHandler(toolStripButton1_CheckedChanged);
    ```

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStripButton>
- [ToolStrip 컨트롤 개요](toolstrip-control-overview-windows-forms.md)
