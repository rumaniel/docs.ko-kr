---
title: '방법: 디자이너를 사용하여 Windows Forms 패널 배경 설정'
ms.date: 03/30/2017
helpviewer_keywords:
- background colors [Windows Forms], Windows Forms Panel controls
- background images [Windows Forms], Windows Forms Panel controls
- Panel control [Windows Forms], background
- colors [Windows Forms], Windows Forms Panel controls
ms.assetid: db83cf54-3c69-4b08-ac6c-25b9b5abb1b0
ms.openlocfilehash: 6927a7118c43ced03623a9764a3ef1e0814c95cb
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211638"
---
# <a name="how-to-set-the-background-of-a-windows-forms-panel-using-the-designer"></a>방법: 디자이너를 사용 하 여 Windows Forms 패널의 배경 설정

Windows Forms <xref:System.Windows.Forms.Panel> 컨트롤 배경색 및 배경 이미지를 표시할 수 있습니다. <xref:System.Windows.Forms.Control.BackColor%2A> 속성 패널 레이블 등에서 포함 된 라디오 단추를 컨트롤에 대 한 배경색을 설정 합니다. 경우는 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 속성을 설정 하지 않으면는 <xref:System.Windows.Forms.Control.BackColor%2A> 선택 패널의 모든 입력 됩니다. 경우는 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 속성이 설정 되 면 이미지 패널에 포함 된 컨트롤 뒤에 표시 됩니다.

다음 절차를 수행 하려면을 **Windows 응용 프로그램** 포함 된 폼을 사용 하 여 프로젝트를 <xref:System.Windows.Forms.Panel> 제어 합니다. Visual Studio에서 이러한 프로젝트를 설정 하는 방법에 대 한 정보를 참조 하세요. [방법: Windows Forms 응용 프로그램 프로젝트를 만듭니다](/visualstudio/ide/step-1-create-a-windows-forms-application-project) 고 [방법: Windows Forms에 컨트롤 추가](how-to-add-controls-to-windows-forms.md)합니다.

## <a name="set-the-background-in-the-windows-forms-designer"></a>Windows Forms 디자이너의 배경 설정

1. Visual Studio에서 프로젝트를 열고 선택 된 <xref:System.Windows.Forms.Panel> 제어 합니다.

2. 에 **속성** 창, 화살표 옆의 단추 클릭을 <xref:System.Windows.Forms.Control.BackColor%2A> 속성 창을 표시 하는 세 개의 탭을 사용 하 여 합니다.

3. 선택 된 **사용자 지정** 색상표를 표시 하려면 탭 합니다.

4. 선택 된 **웹** 또는 **시스템** 미리 정의 된 색 이름 목록을 표시 하려면 탭 및 색을 선택 합니다.

5. 에 **속성** 창, 화살표 옆의 단추 클릭을 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 속성입니다.

6. 에 **열려** 대화 상자를 표시 하려는 파일을 선택 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Control.BackColor%2A>
- <xref:System.Windows.Forms.Control.BackgroundImage%2A>
- [Panel 컨트롤](panel-control-windows-forms.md)
- [Panel 컨트롤 개요](panel-control-overview-windows-forms.md)
- [방법: 디자이너를 사용 하 여 Windows Forms 패널 컨트롤을 사용 하 여 그룹 컨트롤](group-controls-with-wf-panel-control-using-the-designer.md)
