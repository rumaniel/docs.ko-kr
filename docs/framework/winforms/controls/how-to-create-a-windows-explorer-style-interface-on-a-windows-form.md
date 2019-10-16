---
title: '방법: Windows Form에 Windows 탐색기 스타일 인터페이스 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Explorer [Windows Forms], creating with Windows Forms
- SplitContainer control [Windows Forms], Explorer-style interface
- forms [Windows Forms], Windows Explorer type
ms.assetid: 9a3d5f4f-5dda-4350-9ad5-57ce5976dc47
ms.openlocfilehash: 34a5cd735c350688d9e83003806668e213932c85
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960621"
---
# <a name="how-to-create-a-windows-explorerstyle-interface-on-a-windows-form"></a>방법: Windows Form에 Windows 탐색기 스타일 인터페이스 만들기
Windows 탐색기는 친숙 한 응용 프로그램에 대 한 일반적인 사용자 인터페이스 선택입니다.

 Windows 탐색기는 기본적으로 <xref:System.Windows.Forms.TreeView> 개별 패널의 컨트롤 <xref:System.Windows.Forms.ListView> 및 컨트롤입니다. 분할자에 의해 패널의 크기를 조정할 수 있습니다. 이러한 컨트롤 정렬은 정보를 표시 하 고 검색 하는 데 매우 효과적입니다.

 다음 단계에서는 Windows 탐색기와 같은 양식에서 컨트롤을 정렬 하는 방법을 보여 줍니다. Windows 탐색기 응용 프로그램의 파일 검색 기능을 추가 하는 방법은 표시 되지 않습니다.

## <a name="to-create-a-windows-explorer-style-windows-form"></a>Windows 탐색기 스타일의 Windows Form을 만들려면

1. 새 Windows 응용 프로그램 프로젝트 만들기 (**파일** > **새로** > 만들기**프로젝트** > **시각적 개체 C#**  또는**클래식 데스크톱** **Visual Basic** >  >  **Windows Forms 응용 프로그램**).

2. **도구 상자**에서:

    1. 컨트롤을 <xref:System.Windows.Forms.SplitContainer> 폼으로 끌어 옵니다.

    2. 컨트롤을 <xref:System.Windows.Forms.TreeView> **SplitterPanel1** ( <xref:System.Windows.Forms.SplitContainer> **Panel1**로 표시 된 컨트롤의 패널)로 끕니다.

    3. 컨트롤을 <xref:System.Windows.Forms.ListView> **SplitterPanel2** ( <xref:System.Windows.Forms.SplitContainer> **Panel2**로 표시 된 컨트롤의 패널)로 끕니다.

3. CTRL 키를 누른 채 차례로 클릭 하 여 세 개의 컨트롤을 모두 선택 합니다. 컨트롤을 선택 하 <xref:System.Windows.Forms.SplitContainer> 는 경우 패널 대신 분할자 막대를 클릭 합니다.

    > [!NOTE]
    > **편집** 메뉴에서 **모두 선택** 명령을 사용 하지 마십시오. 이렇게 하면 다음 단계에 필요한 속성은 **속성** 창에 표시 되지 않습니다.

4. **속성** 창에서 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 속성을 <xref:System.Windows.Forms.DockStyle.Fill>로 설정합니다.

5. F5 키를 눌러 애플리케이션을 실행합니다.

     이 폼에는 Windows 탐색기와 유사한 두 부분으로 구성 된 사용자 인터페이스가 표시 됩니다.

    > [!NOTE]
    > 분할자를 끌면 패널의 크기가 자동으로 조정 됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.SplitContainer>
- [방법: Windows Forms를 사용 하 여 다중 창 사용자 인터페이스 만들기](how-to-create-a-multipane-user-interface-with-windows-forms.md)
- [방법: 분할 창에서 크기 조정 및 위치 지정 동작 정의](how-to-define-resize-and-positioning-behavior-in-a-split-window.md)
- [방법: 가로로 창 분할](how-to-split-a-window-horizontally.md)
- [SplitContainer 컨트롤](splitcontainer-control-windows-forms.md)
