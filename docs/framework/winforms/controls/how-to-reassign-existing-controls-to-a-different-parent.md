---
title: '방법: 다른 부모에 기존 컨트롤 다시 할당'
ms.date: 03/30/2017
helpviewer_keywords:
- container controls [Windows Forms], Windows Forms
- layout [Windows Forms], resizing
- layout [Windows Forms], child controls
ms.assetid: 5a5723ff-34e0-4b6f-a57b-be4ebe35cb34
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 84e662e0bd2689115abe128c6442e4462eed3e18
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987041"
---
# <a name="how-to-reassign-existing-controls-to-a-different-parent"></a>방법: 다른 부모에 기존 컨트롤 다시 할당

폼에 있는 컨트롤을 새 컨테이너 컨트롤에 할당할 수 있습니다.

1. Visual Studio에서 **도구 상자** 의 <xref:System.Windows.Forms.Button> 세 컨트롤을 폼으로 끌어옵니다. 서로 정렬되지 않은 상태로 근처에 배치합니다.

2. **도구 상자**에서 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤 아이콘을 클릭합니다. (아이콘을 폼으로 끌어 오지 마세요.)

3. 마우스 포인터를 세 <xref:System.Windows.Forms.Button> 컨트롤 쪽으로 이동합니다.

   포인터가 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤 아이콘이 연결된 십자형으로 바뀝니다.

4. 마우스 단추를 길게 클릭합니다.

5. 마우스 포인터를 끌어 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤의 윤곽선을 그립니다.

6. 세 <xref:System.Windows.Forms.Button> 컨트롤 주위에 윤곽선을 그립니다.

7. 마우스 단추를 놓습니다.

   이제 세 <xref:System.Windows.Forms.Button> 컨트롤이 <xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤에 삽입됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.FlowLayoutPanel>
- <xref:System.Windows.Forms.TableLayoutPanel>
- [연습: TableLayoutPanel를 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)
- [연습: 맞춤선을 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)
