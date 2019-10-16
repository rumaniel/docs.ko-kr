---
title: ToolStrip 기술 요약
ms.date: 03/30/2017
helpviewer_keywords:
- ToolStrip control [Windows Forms], technology summary
- status bars [Windows Forms], technology summary
- toolbars [Windows Forms], technology summary
- menus [Windows Forms], technology summary
ms.assetid: e8d61973-7af9-429f-9df5-05a899c15a7b
ms.openlocfilehash: d447f78a6b6d8a71ea2e67d4c991655eb4712199
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64654704"
---
# <a name="toolstrip-technology-summary"></a>ToolStrip 기술 요약
이 항목에서는 `ToolStrip` 제어 및 이를 사용하도록 지원하는 클래스에 대한 정보를 요약하여 설명합니다.  
  
 `ToolStrip` 컨트롤과 연결된 클래스는 도구 모음, 상태 표시줄 및 메뉴를 만드는 완벽한 솔루션을 제공합니다.  
  
## <a name="namespaces"></a>네임스페이스  
 <xref:System.Windows.Forms?displayProperty=nameWithType>  
  
## <a name="background"></a>배경  
 `ToolStrip` 컨트롤과 연결된 클래스를 사용하여 일관되고 전문적인 모양 및 동작을 제공하는 고급 도구 모음 기능을 만들 수 있습니다. `ToolStrip` 컨트롤 및 클래스는 이전 컨트롤에 비해 다음과 같은 향상된 기능을 제공합니다.  
  
- 더 일관된 이벤트 모델.  
  
- 작업 목록 및 항목 컬렉션 편집기가 포함된 더 일관된 디자인 타임 동작.  
  
- `ToolStripManager` 및 `ToolStripRenderer`를 사용한 사용자 지정 렌더링.  
  
- `ToolStripContainer` 및 `ToolStripPanel`을 사용한 기본 제공 래프팅(도킹된 경우 도구 영역 내에서 가로 또는 세로 공간 공유).  
  
- <xref:System.Windows.Forms.ToolStrip.AllowItemReorder%2A> 속성을 사용한 디자인 타임 및 런타임 항목 다시 정렬.  
  
- <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A> 속성을 사용한 오버플로 메뉴 항목에 대한 항목 위치 변경.  
  
- `ToolStripContainer`, `ToolStripPanel` 및 `ToolStripContentPanel`을 통해 완전히 구성 가능한 컨트롤 위치.  
  
- `ToolStripControlHost`를 사용하여 `ToolStrip`, 기본 컨트롤 및 사용자 지정 컨트롤 호스트.  
  
- `ToolStripPanel`을 사용하여 `ToolStrip` 컨트롤 병합.  
  
 `ToolStrip`는 `MenuStrip`, `ContextMenuStrip` 및 `StatusStrip`의 확장 가능한 기본 클래스입니다. 이들 컨트롤은 각 구현이 적절한 동작을 처리하도록 확장된, 일반 동작 및 이벤트 처리를 상속하는 <xref:System.Windows.Forms.ToolStripItem> 컨테이너입니다. <xref:System.Windows.Forms.ToolStripItem>에서 파생되는 컨트롤이 다음 표에 나와 있습니다. 기본 `ToolStrip` 클래스는 이들 컨트롤에 대한 그리기, 사용자 입력 및 끌어서 놓기 이벤트를 처리합니다.  
  
 `ToolStrip`, `MenuStrip`, `ContextMenuStrip` 및 `StatusStrip` 컨트롤은 이전 도구 모음, 메뉴, 바로 가기 메뉴 및 상태 표시줄 컨트롤을 대체합니다. 이전 버전과의 호환성을 위해 해당 컨트롤이 유지되는 경우에도 마찬가지입니다.  
  
## <a name="toolstrip-classes-at-a-glance"></a>ToolStrip 클래스 개요  
 다음 표에서는 기술 영역별로 그룹화된 ToolStrip 클래스를 보여 줍니다.  
  
|기술 영역|클래스|  
|---------------------|-----------|  
|도구 모음, 상태 및 메뉴 컨테이너|<xref:System.Windows.Forms.ToolStrip><br /><br /> <xref:System.Windows.Forms.MenuStrip><br /><br /> <xref:System.Windows.Forms.ContextMenuStrip><br /><br /> <xref:System.Windows.Forms.StatusStrip><br /><br /> <xref:System.Windows.Forms.ToolStripDropDownMenu>|  
|ToolStrip 항목|<xref:System.Windows.Forms.ToolStripLabel><br /><br /> <xref:System.Windows.Forms.ToolStripDropDownItem><br /><br /> <xref:System.Windows.Forms.ToolStripMenuItem><br /><br /> <xref:System.Windows.Forms.ToolStripButton><br /><br /> <xref:System.Windows.Forms.ToolStripStatusLabel><br /><br /> <xref:System.Windows.Forms.ToolStripSeparator><br /><br /> <xref:System.Windows.Forms.ToolStripControlHost><br /><br /> <xref:System.Windows.Forms.ToolStripComboBox><br /><br /> <xref:System.Windows.Forms.ToolStripTextBox><br /><br /> <xref:System.Windows.Forms.ToolStripProgressBar><br /><br /> <xref:System.Windows.Forms.ToolStripDropDownButton><br /><br /> <xref:System.Windows.Forms.ToolStripSplitButton>|  
|위치|<xref:System.Windows.Forms.ToolStripContainer><br /><br /> <xref:System.Windows.Forms.ToolStripContentPanel><br /><br /> <xref:System.Windows.Forms.ToolStripPanel>|  
|프레젠테이션 및 렌더링|<xref:System.Windows.Forms.ToolStripManager><br /><br /> <xref:System.Windows.Forms.ToolStripRenderer><br /><br /> <xref:System.Windows.Forms.ToolStripProfessionalRenderer><br /><br /> <xref:System.Windows.Forms.ToolStripRenderMode><br /><br /> <xref:System.Windows.Forms.ToolStripManagerRenderMode>|  
  
## <a name="toolstrip-design-time-features"></a>ToolStrip 디자인 타임 기능  
 컨트롤의 <xref:System.Windows.Forms.ToolStrip> 패밀리는 작업 애플리케이션을 빠르게 만들 수 있도록 사용자 인터페이스의 기본 사항을 내부 편집하고 정의하기 위한 다양한 도구 및 템플릿 집합을 제공합니다.  
  
### <a name="task-dialog-boxes"></a>작업 대화 상자  
 Visual Studio에서는 디자이너의 컨트롤에서 스마트 태그를 클릭하면 자주 사용되는 대부분 명령에 편리하게 액세스할 수 있는 작업 목록이 표시됩니다.  
  
- [MenuStrip 작업 대화 상자](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233645(v=vs.100))  
  
- [ToolStrip 작업 대화 상자](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233648(v=vs.100))  
  
- [ContextMenuStrip 작업 대화 상자](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233646(v=vs.100))  
  
- [StatusStrip 작업 대화 상자](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233642(v=vs.100))  
  
- [ToolStripContainer 작업 대화 상자](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233647(v=vs.100))  
  
### <a name="items-collection-editors"></a>항목 컬렉션 편집기  
 클릭 하면 Visual Studio에서 **항목 편집** 태스크의 목록 또는 선택한 컨트롤을 마우스 오른쪽 단추로 클릭 **항목 편집** 바로 가기 메뉴의 컨트롤에 대 한 컬렉션 편집기가 표시 됩니다. 컬렉션 편집기를 통해 컨트롤에 포함된 항목을 추가, 제거, 다시 정렬할 수 있습니다. 컨트롤 및 컨트롤 항목에 대한 속성을 보고 변경할 수도 있습니다.  
  
- [MenuStrip 항목 컬렉션 편집기](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233625(v=vs.100))  
  
- [StatusStrip 항목 컬렉션 편집기](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233631(v=vs.100))  
  
- [ContextMenuStrip 항목 컬렉션 편집기](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233641(v=vs.100))  
  
- [ToolStrip 항목 컬렉션 편집기](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233643(v=vs.100))  
  
## <a name="hosting-controls"></a>컨트롤 호스트  
 <xref:System.Windows.Forms.ToolStripControlHost> 클래스는 <xref:System.Windows.Forms.ToolStripComboBox>, <xref:System.Windows.Forms.ToolStripTextBox> 및 <xref:System.Windows.Forms.ToolStripProgressBar> 컨트롤에 대한 기본 제공 래퍼를 제공합니다. 다른 기존 컨트롤이나 COM 컨트롤을 <xref:System.Windows.Forms.ToolStripControlHost>에서 호스트할 수도 있습니다.  
  
 컨트롤 호스팅의 예제를 참조 하세요. [방법: ToolStripControlHost 사용 하 여 Windows Forms 컨트롤 래핑](how-to-wrap-a-windows-forms-control-with-toolstripcontrolhost.md)합니다.  
  
## <a name="rendering"></a>렌더링  
 <xref:System.Windows.Forms.ToolStrip> 클래스는 기타 Windows Forms 컨트롤과 크게 다른 렌더링 체계를 구현합니다. 이 체계를 사용하여 스타일과 테마를 쉽게 적용할 수 있습니다.  
  
 <xref:System.Windows.Forms.ToolStrip> 및 여기에 포함된 모든 <xref:System.Windows.Forms.ToolStripItem> 개체에 스타일을 적용하려면 각 항목에 대한 <xref:System.Windows.Forms.ToolStripItem.Paint> 이벤트를 처리할 필요가 없습니다. 대신에 <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> 속성을 <xref:System.Windows.Forms.ToolStripRenderMode.Custom>이 아닌 <xref:System.Windows.Forms.ToolStripRenderMode> 값의 하나로 설정할 수 있습니다. 또는 <xref:System.Windows.Forms.ToolStrip.Renderer%2A>를 직접 <xref:System.Windows.Forms.ToolStripRenderer> 클래스에서 상속되는 클래스로 설정할 수 있습니다. 이 속성을 설정하면 자동으로 <xref:System.Windows.Forms.ToolStrip.RenderMode%2A>가 설정됩니다.  
  
 <xref:System.Windows.Forms.ToolStrip.RenderMode%2A>를 <xref:System.Windows.Forms.ToolStripRenderMode.ManagerRenderMode>로 설정하거나 <xref:System.Windows.Forms.ToolStripManager.RenderMode%2A> 또는 <xref:System.Windows.Forms.ToolStripManager.Renderer%2A> 속성을 각각 원하는 <xref:System.Windows.Forms.ToolStripManagerRenderMode> 또는 <xref:System.Windows.Forms.ToolStripRenderer> 값으로 설정하여 같은 애플리케이션의 여러 <xref:System.Windows.Forms.ToolStrip> 개체에 같은 스타일을 적용할 수 있습니다.  
  
 렌더링의 예 참조 [방법: 만들기 및 ToolStrip 컨트롤에 Windows Forms에 대 한 사용자 지정 렌더러를 설정](create-and-set-a-custom-renderer-for-the-toolstrip-control-in-wf.md)합니다.  
  
## <a name="styles-and-themes"></a>스타일 및 테마  
 <xref:System.Windows.Forms.ToolStrip> 및 연결된 클래스를 사용하면 각 항목에 대한 <xref:System.Windows.Forms.ToolStripItem.OnPaint%2A> 메서드를 재정의할 필요 없이 시각적 스타일과 사용자 지정 모양을 쉽게 지원할 수 있습니다. <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A>과 <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> 및 <xref:System.Windows.Forms.ToolStrip.Renderer%2A> 속성을 사용합니다.  
  
## <a name="rafting-and-docking"></a>래프팅 및 도킹  
 <xref:System.Windows.Forms.ToolStrip> 컨트롤을 래프팅, 도킹 또는 절대적으로 배치할 수 있습니다. <xref:System.Windows.Forms.ToolStrip> 항목은 컨테이너의 <xref:System.Windows.Forms.ToolStrip.LayoutEngine%2A>에 의해 배치됩니다.  
  
 *래프팅* 기능은 도구 모음의 가로 또는 세로 공간을 공유 합니다. Windows 폼에는 <xref:System.Windows.Forms.ToolStripContainer>가 포함될 수 있고, 이 컨테이너에는 폼의 왼쪽, 오른쪽, 위쪽, 아래쪽에 <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.MenuStrip> 및 <xref:System.Windows.Forms.StatusStrip> 컨트롤을 배치 및 래프팅할 패널이 있습니다. 왼쪽 또는 오른쪽 <xref:System.Windows.Forms.ToolStripContainer>에 여러 <xref:System.Windows.Forms.ToolStrip> 컨트롤을 배치하면 컨트롤이 세로로 쌓입니다. 위쪽 또는 아래쪽 <xref:System.Windows.Forms.ToolStripContainer>에 배치하면 가로로 쌓입니다. <xref:System.Windows.Forms.ToolStripContainer>의 가운데 <xref:System.Windows.Forms.ToolStripContentPanel>을 사용하여 기존 컨트롤을 폼에 배치할 수 있습니다.  
  
 임의 또는 모든 <xref:System.Windows.Forms.ToolStripContainer> 컨트롤은 디자인 타임에 직접 선택할 수 있고 삭제할 수 있습니다. <xref:System.Windows.Forms.ToolStripContainer>는 확장 및 축소 가능하고 포함된 컨트롤을 사용하여 크기가 조정됩니다.  
  
 *도킹* 폼의 왼쪽, 오른쪽, 위쪽 또는 아래쪽에는 컨트롤의 단순 위치 지정 됩니다.  
  
 도킹을 통해 래프팅하는 이점은 <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.MenuStrip> 및 <xref:System.Windows.Forms.StatusStrip> 컨트롤이 다른 컨트롤과 가로 또는 세로 공간을 공유할 수 있다는 점입니다.  
  
 대부분 <xref:System.Windows.Forms.ToolStrip> 컨트롤은 래프팅을 사용하는 대신 다른 컨트롤 같이 폼에 도킹될 수 있습니다. <xref:System.Windows.Forms.ToolStrip> 컨트롤을 <xref:System.Windows.Forms.ToolStripContainer>에서 제거하고 해당 `Dock` 속성을 `None`으로 설정하여 해당 컨트롤이 폼에 자유롭게 배치되도록 지정하거나, 각 <xref:System.Windows.Forms.Control.Location%2A> 속성을 설정하여 절대 위치를 지정할 수 있습니다. [방법: 폼에 ToolStripContainer의 ToolStrip 이동](how-to-move-a-toolstrip-out-of-a-toolstripcontainer-onto-a-form.md)합니다.  
  
 더 큰 유연성, 특히 MDI(다중 문서 인터페이스) 애플리케이션을 위해 또는 <xref:System.Windows.Forms.ToolStripContainer>가 필요하지 않을 경우 <xref:System.Windows.Forms.ToolStripPanel> 컨트롤을 하나 이상 사용합니다. <xref:System.Windows.Forms.ToolStripPanel>에서는 <xref:System.Windows.Forms.ToolStrip> 컨트롤을 배치 및 래프팅할 도킹 가능한 공간을 제공하지만 기존 컨트롤에 사용할 공간을 제공하지 않습니다. 기본적으로 <xref:System.Windows.Forms.ToolStripPanel> 디자이너에 표시 되지 않습니다 **도구 상자**를 마우스 오른쪽 단추로 클릭 하 여 하를 전환할 수 있습니다 하지만 **도구 상자**, 클릭 하 고 **항목 선택**합니다. 다른 클래스처럼 <xref:System.Windows.Forms.ToolStripPanel>에 프로그래밍 방식으로 액세스할 수도 있습니다.  
  
 <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.MenuStrip> 및 <xref:System.Windows.Forms.StatusStrip>을 통해 항목이 오버플로될 수 있습니다. 이는 이들 항목이 Microsoft Office 도구 모음에서 동작하는 방식과 비슷합니다.  
  
## <a name="see-also"></a>참고자료

- [ToolStrip 컨트롤 개요](toolstrip-control-overview-windows-forms.md)
- [ToolStrip 컨트롤 아키텍처](toolstrip-control-architecture.md)
