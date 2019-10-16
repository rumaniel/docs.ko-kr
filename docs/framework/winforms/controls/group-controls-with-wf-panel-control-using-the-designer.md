---
title: '방법: 디자이너를 사용하여 Windows Forms 패널 컨트롤에서 컨트롤 그룹화'
ms.date: 03/30/2017
helpviewer_keywords:
- Panel control [Windows Forms], grouping controls
- controls [Windows Forms], grouping
- Windows Forms controls, grouping
ms.assetid: 7e1cd708-fdb1-49d8-9ca2-5640b276bf2e
ms.openlocfilehash: cadfa715b140c63b216ec0ca2e6d6a6589ae3458
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040383"
---
# <a name="how-to-group-controls-with-the-windows-forms-panel-control-using-the-designer"></a>방법: 디자이너를 사용하여 Windows Forms 패널 컨트롤에서 컨트롤 그룹화
Windows Forms <xref:System.Windows.Forms.Panel> 컨트롤은 다른 컨트롤을 그룹화 하는 데 사용 됩니다. 컨트롤을 그룹화 하는 이유는 세 가지가 있습니다. 하나는 일반 사용자 인터페이스에 대 한 관련 폼 요소의 시각적 그룹화입니다. 또 다른 예로는 라디오 단추와 같은 프로그래밍 방식 그룹화가 있습니다. 마지막은 디자인 타임에 컨트롤을 하나의 단위로 이동 하기 위한 것입니다.

## <a name="to-create-a-group-of-controls"></a>컨트롤 그룹을 만들려면

1. 도구 상자 <xref:System.Windows.Forms.Panel> 의 **Windows Forms** 탭에서 컨트롤을 폼으로 끌어 놓습니다.

2. 패널에 다른 컨트롤을 추가 하 고 패널 내부에 그립니다.

     패널에 포함 하려는 기존 컨트롤이 있는 경우 모든 컨트롤을 선택 하 고 클립보드로 잘라내고 <xref:System.Windows.Forms.Panel> 컨트롤을 선택한 다음 패널에 붙여 넣을 수 있습니다. 이러한 항목을 패널로 끌어올 수도 있습니다.

3. 필드 패널에 테두리를 추가 하려면 해당 <xref:System.Windows.Forms.BorderStyle> 속성을 설정 합니다. <xref:System.Windows.Forms.BorderStyle.Fixed3D> ,<xref:System.Windows.Forms.BorderStyle.FixedSingle>및 의<xref:System.Windows.Forms.BorderStyle.None>세 가지 옵션을 선택할 수 있습니다.

## <a name="see-also"></a>참고자료

- [Panel 컨트롤](panel-control-windows-forms.md)
- [Panel 컨트롤 개요](panel-control-overview-windows-forms.md)
- [방법: 패널의 배경 설정](how-to-set-the-background-of-a-windows-forms-panel.md)
