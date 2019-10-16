---
title: ToolBar 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- ToolBar
helpviewer_keywords:
- toolbars [Windows Forms], about toolbars
- ToolBar control [Windows Forms], about ToolBar controls
ms.assetid: d426b203-0216-4dbe-b834-1641e50a9c29
ms.openlocfilehash: c7c19783963bb315a0356979797c6f4d4e3b9e08
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69929587"
---
# <a name="toolbar-control-overview-windows-forms"></a>ToolBar 컨트롤 개요(Windows Forms)
> [!NOTE]
> <xref:System.Windows.Forms.ToolStrip> 컨트롤은 <xref:System.Windows.Forms.ToolBar> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.ToolBar> 컨트롤을 계속 유지하도록 선택할 수 있습니다.  
  
 Windows Forms <xref:System.Windows.Forms.ToolBar> 컨트롤은 폼에서 드롭다운 메뉴 및 명령을 활성화하는 비트맵 단추가 포함된 한 행을 표시하는 컨트롤 막대로 사용됩니다. 따라서 도구 모음 단추를 클릭하는 것은 메뉴 명령을 선택하는 것과 같을 수 있습니다. 단추는 누름 단추, 드롭다운 메뉴 또는 구분 기호로 표시 되고 동작하도록 구성할 수 있습니다. 일반적으로 도구 모음에는 애플리케이션 메뉴 구조의 항목에 해당하는 단추 및 메뉴가 포함되며, 애플리케이션에서 자주 사용되는 함수 및 명령에 대한 빠른 액세스를 제공합니다.  
  
## <a name="working-with-the-toolbar-control"></a>ToolBar 컨트롤 사용  
 <xref:System.Windows.Forms.ToolBar> 컨트롤은 일반적으로 부모 창의 위쪽에 "도킹" 되지만 창의 어느 쪽에도 도킹할 수 있습니다. 도구 모음에서 사용자가 마우스 포인터로 도구 모음 단추를 가리키면 도구 설명을 표시할 수 있습니다. 도구 설명은 단추 또는 메뉴의 기능을 간략하게 설명하는 작은 팝업 창입니다. 도구 설명을 <xref:System.Windows.Forms.ToolBar.ShowToolTips%2A> 표시 하려면 속성을로 `true`설정 해야 합니다.  
  
> [!NOTE]
> 특정 애플리케이션은 애플리케이션 창 위에서 "고정 해제"되어 위치를 변경할 수 있는 도구 모음과 매우 비슷한 기능이 있는 컨트롤을 제공합니다. Windows Forms ToolBar 컨트롤은 이러한 동작을 수행할 수 없습니다.  
  
 <xref:System.Windows.Forms.ToolBar.Appearance%2A> 속성이 로<xref:System.Windows.Forms.ToolBarAppearance>설정 되 면 도구 모음 단추가 볼록 및 3 차원으로 표시 됩니다. 도구 모음의 <xref:System.Windows.Forms.ToolBar.Appearance%2A> 속성을로 <xref:System.Windows.Forms.ToolBarAppearance> 설정 하 여 도구 모음과 단추의 단추를 평면 모양으로 지정할 수 있습니다. 마우스 포인터를 평면 모양의 단추 위로 움직이면 단추 모양이 3차원 모양으로 바뀝니다. 도구 모음 단추는 구분 기호를 사용하여 논리 그룹으로 나눌 수 있습니다. 구분 기호는 도구 모음 단추를 <xref:System.Windows.Forms.ToolBarButton.Style%2A> 속성이 설정 <xref:System.Windows.Forms.ToolBarButtonStyle>합니다. 도구 모음에서 빈 공간으로 나타납니다. 도구 모음이 평면 모양이면 단추 구분 기호는 단추 사이의 공간이 아니라 선으로 나타납니다.  
  
 컨트롤을 사용 하면 <xref:System.Windows.Forms.ToolBar.Buttons%2A> 컬렉션에 개체를 추가 <xref:System.Windows.Forms.Button> 하 여 도구 모음을 만들 수 있습니다. <xref:System.Windows.Forms.ToolBar> 컬렉션 편집기를 사용 하 여 <xref:System.Windows.Forms.ToolBar> 컨트롤에 단추를 추가할 수 있습니다. 각 <xref:System.Windows.Forms.Button> 개체에는 텍스트 또는 이미지가 할당 되어야 하지만 둘 다 할당할 수 있습니다. 이미지는 연결된 [ImageList](imagelist-component-windows-forms.md) 구성 요소에서 제공됩니다. 런타임에 <xref:System.Windows.Forms.ToolBar.ToolBarButtonCollection> <xref:System.Windows.Forms.ToolBar.ToolBarButtonCollection.Add%2A> 및 메서드<xref:System.Windows.Forms.ToolBar.ToolBarButtonCollection.Remove%2A> 를 사용 하 여에서 단추를 추가 하거나 제거할 수 있습니다. 의 <xref:System.Windows.Forms.ToolBar>단추를 프로그래밍 하려면 <xref:System.Windows.Forms.ToolBar.ButtonClick> <xref:System.Windows.Forms.ToolBar> 클래스<xref:System.Windows.Forms.ToolBarButtonClickEventArgs> 의 <xref:System.Windows.Forms.ToolBarButtonClickEventArgs.Button%2A> 속성을 사용 하 여의 이벤트에 코드를 추가 하 여 어떤 단추를 클릭 했는지 확인 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolBar>
- [ToolBar 컨트롤](toolbar-control-windows-forms.md)
- [방법: ToolBar 컨트롤에 단추 추가](how-to-add-buttons-to-a-toolbar-control.md)
- [방법: 도구 모음 단추의 아이콘 정의](how-to-define-an-icon-for-a-toolbar-button.md)
- [방법: 도구 모음 단추에 대 한 트리거 메뉴 이벤트](how-to-trigger-menu-events-for-toolbar-buttons.md)
