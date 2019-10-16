---
title: '방법: 디자이너를 사용하여 Windows Forms 단추를 적용 단추로 지정'
ms.date: 03/30/2017
helpviewer_keywords:
- buttons [Windows Forms], default on Windows Forms
- Accept button on Windows Forms
- Button control [Windows Forms], designating as default
- Windows Forms controls, default button on form
ms.assetid: a1da0590-755f-49f2-aca7-609fac6351bf
ms.openlocfilehash: 27ecb26c493232bcfb996d012f9760b7ef91e5b2
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69039653"
---
# <a name="how-to-designate-a-windows-forms-button-as-the-accept-button-using-the-designer"></a>방법: 디자이너를 사용하여 Windows Forms 단추를 적용 단추로 지정
Windows Form에서 컨트롤을 <xref:System.Windows.Forms.Button> 기본 단추 라고도 하는 허용 단추로 지정할 수 있습니다. 사용자가 ENTER 키를 누를 때마다 폼의 다른 컨트롤에 포커스가 있는지 여부에 관계 없이 기본 단추가 클릭 됩니다. 이에 대 한 예외는 포커스가 있는 컨트롤이 다른 단추인 경우입니다 .이 경우 포커스가 있는 단추를 클릭 하거나 여러 줄 텍스트 상자를 클릭 하거나 ENTER 키를 트래핑 하는 사용자 지정 컨트롤을 클릭 합니다.

## <a name="to-designate-the-accept-button"></a>수락 단추를 지정 하려면

1. 단추가 있는 폼을 선택 합니다.

2. **속성** 창에서 폼의 <xref:System.Windows.Forms.Form.AcceptButton%2A> 속성을 <xref:System.Windows.Forms.Button> 컨트롤의 이름으로 설정 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Form.AcceptButton%2A>
- [Button 컨트롤 개요](button-control-overview-windows-forms.md)
- [Windows Forms Button 컨트롤 선택 방법](ways-to-select-a-windows-forms-button-control.md)
- [방법: Windows Forms 단추 클릭에 응답](how-to-respond-to-windows-forms-button-clicks.md)
- [방법: 디자이너를 사용 하 여 Windows Forms 단추를 취소 단추로 지정](designate-a-wf-button-as-the-cancel-button-using-the-designer.md)
- [Button 컨트롤](button-control-windows-forms.md)
