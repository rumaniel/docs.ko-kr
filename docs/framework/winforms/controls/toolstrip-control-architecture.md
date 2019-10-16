---
title: ToolStrip 컨트롤 아키텍처
ms.date: 03/30/2017
helpviewer_keywords:
- ToolStrip control [Windows Forms], architecture
ms.assetid: 71df2d18-862e-4701-9ff9-c1fe606f94f2
ms.openlocfilehash: d0a1441e9bae8d2c1f938e7399c11e736708da4d
ms.sourcegitcommit: 30a83efb57c468da74e9e218de26cf88d3254597
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2019
ms.locfileid: "68363831"
---
# <a name="toolstrip-control-architecture"></a>ToolStrip 컨트롤 아키텍처

<xref:System.Windows.Forms.ToolStrip> 및<xref:System.Windows.Forms.ToolStripItem> 클래스는 도구 모음, 상태 및 메뉴 항목을 표시 하기 위한 유연 하 고 확장 가능한 시스템을 제공 합니다. 이러한 클래스는 모두 <xref:System.Windows.Forms> 네임 스페이스에 포함 되며 일반적으로 "ToolStrip" 접두사 ( <xref:System.Windows.Forms.ToolStripOverflow>예:) 또는 "스트립 <xref:System.Windows.Forms.MenuStrip>" 접미사 (예:)로 이름이 지정 됩니다.

## <a name="toolstrip"></a>ToolStrip

다음 항목에서는 및 <xref:System.Windows.Forms.ToolStrip> 이 항목에서 파생 되는 컨트롤에 대해 설명 합니다.

<xref:System.Windows.Forms.ToolStrip> 에 대 한 추상 기본 클래스인 <xref:System.Windows.Forms.MenuStrip>, <xref:System.Windows.Forms.StatusStrip>, 및 <xref:System.Windows.Forms.ContextMenuStrip>합니다. 다음 개체 모델에서는 상속 계층 <xref:System.Windows.Forms.ToolStrip> 구조를 보여 줍니다.

![ToolStrip 개체 모델을 보여 주는 다이어그램입니다.](./media/toolstrip-control-architecture/toolstrip-object-model.gif)

컬렉션<xref:System.Windows.Forms.ToolStrip.Items%2A> 을 <xref:System.Windows.Forms.ToolStrip> 통해의 모든 항목에 액세스할 수 있습니다. 컬렉션<xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItems%2A> 을 <xref:System.Windows.Forms.ToolStripDropDownItem> 통해의 모든 항목에 액세스할 수 있습니다. 에서 <xref:System.Windows.Forms.ToolStrip>파생 된 클래스에서 <xref:System.Windows.Forms.ToolStrip.DisplayedItems%2A> 속성을 사용 하 여 현재 표시 된 항목에만 액세스할 수도 있습니다. 다음은 현재 오버플로 메뉴에 없는 항목입니다.

다음 항목을 모두 사용 하 여 원활 하 게 작동 하도록 특별히 설계 된 <xref:System.Windows.Forms.ToolStripSystemRenderer> 고 <xref:System.Windows.Forms.ToolStripProfessionalRenderer> 모든 방향에서. 에 대 한 디자인 타임에 기본적으로 사용할 수는 <xref:System.Windows.Forms.ToolStrip> 제어 합니다.

- <xref:System.Windows.Forms.ToolStripButton>

- <xref:System.Windows.Forms.ToolStripSeparator>

- <xref:System.Windows.Forms.ToolStripLabel>

- <xref:System.Windows.Forms.ToolStripDropDownButton>

- <xref:System.Windows.Forms.ToolStripSplitButton>

- <xref:System.Windows.Forms.ToolStripTextBox>

- <xref:System.Windows.Forms.ToolStripComboBox>

### <a name="menustrip"></a>MenuStrip

<xref:System.Windows.Forms.MenuStrip> 대체 하는 최상위 컨테이너인 <xref:System.Windows.Forms.MainMenu>합니다. 또한 키 처리 및 여러 문서 MDI (인터페이스) 기능도 제공 합니다. 기능적으로 <xref:System.Windows.Forms.ToolStripDropDownItem> 하 고 <xref:System.Windows.Forms.ToolStripMenuItem> 과 함께 작동 <xref:System.Windows.Forms.MenuStrip>이지만에서 파생 되므로 <xref:System.Windows.Forms.ToolStripItem>합니다.

다음 항목을 모두 사용 하 여 원활 하 게 작동 하도록 특별히 설계 된 <xref:System.Windows.Forms.ToolStripSystemRenderer> 고 <xref:System.Windows.Forms.ToolStripProfessionalRenderer> 모든 방향에서. 에 대 한 디자인 타임에 기본적으로 사용할 수는 <xref:System.Windows.Forms.MenuStrip> 제어 합니다.

- <xref:System.Windows.Forms.ToolStripMenuItem>

- <xref:System.Windows.Forms.ToolStripTextBox>

- <xref:System.Windows.Forms.ToolStripComboBox>

### <a name="statusstrip"></a>StatusStrip

<xref:System.Windows.Forms.StatusStrip> 대체는 <xref:System.Windows.Forms.StatusBar> 제어 합니다. 의 <xref:System.Windows.Forms.StatusStrip> 특수 기능으로는 <xref:System.Windows.Forms.ToolStripStatusLabel> 사용자 지정 테이블 레이아웃, 양식의 크기 조정 및 이동 그립 지원 `Spring` 및 속성 (에서 사용 가능한 공간을 자동으로 채울 수 있음)이 포함 됩니다.

다음 항목을 모두 사용 하 여 원활 하 게 작동 하도록 특별히 설계 된 <xref:System.Windows.Forms.ToolStripSystemRenderer> 고 <xref:System.Windows.Forms.ToolStripProfessionalRenderer> 모든 방향에서. 에 대 한 디자인 타임에 기본적으로 사용할 수는 <xref:System.Windows.Forms.StatusStrip> 제어 합니다.

- <xref:System.Windows.Forms.ToolStripStatusLabel>

- <xref:System.Windows.Forms.ToolStripDropDownButton>

- <xref:System.Windows.Forms.ToolStripSplitButton>

- <xref:System.Windows.Forms.ToolStripProgressBar>

### <a name="contextmenustrip"></a>ContextMenuStrip

<xref:System.Windows.Forms.ContextMenuStrip>가 <xref:System.Windows.Forms.ContextMenu>를 대체합니다. 을 <xref:System.Windows.Forms.ContextMenuStrip> 컨트롤과 연결할 수 있으며 마우스 오른쪽 단추를 클릭 하면 상황에 맞는 메뉴 또는 바로 가기 메뉴가 자동으로 표시 됩니다. 표시할 수 있습니다는 <xref:System.Windows.Forms.ContextMenuStrip> 를 사용 하 여 프로그래밍 방식으로 <xref:System.Windows.Forms.ToolStripDropDown.Show%2A> 메서드. <xref:System.Windows.Forms.ContextMenuStrip> 취소할 수 있는 지원 <xref:System.Windows.Forms.ToolStripDropDown.Opening> 고 <xref:System.Windows.Forms.ToolStripDropDown.Closing> 동적 채우기 및 여러 원클릭 시나리오를 처리 하는 이벤트입니다. <xref:System.Windows.Forms.ContextMenuStrip> 이미지, 상태를 확인 하는 메뉴 항목, 텍스트, 액세스 키, 바로 가기 및 계단식 메뉴를 지원합니다.

다음 항목을 모두 사용 하 여 원활 하 게 작동 하도록 특별히 설계 된 <xref:System.Windows.Forms.ToolStripSystemRenderer> 고 <xref:System.Windows.Forms.ToolStripProfessionalRenderer> 모든 방향에서. 에 대 한 디자인 타임에 기본적으로 사용할 수는 <xref:System.Windows.Forms.ContextMenuStrip> 제어 합니다.

- <xref:System.Windows.Forms.ToolStripMenuItem>

- <xref:System.Windows.Forms.ToolStripSeparator>

- <xref:System.Windows.Forms.ToolStripTextBox>

- <xref:System.Windows.Forms.ToolStripComboBox>

### <a name="toolstrip-generic-features"></a>ToolStrip 일반 기능

다음 항목에서는 <xref:System.Windows.Forms.ToolStrip> 및 파생 컨트롤에 대 한 일반적인 기능과 동작에 대해 설명 합니다.

#### <a name="painting"></a>칠하기

사용자 지정 그리기를 수행할 수 있는 <xref:System.Windows.Forms.ToolStrip> 여러 가지 방법으로 제어 합니다. 다른 Windows Forms 컨트롤과 마찬가지로 합니다 <xref:System.Windows.Forms.ToolStrip> 및 <xref:System.Windows.Forms.ToolStripItem> overridable 둘 `OnPaint` 메서드 및 `Paint` 이벤트입니다. 컨트롤의 클라이언트 영역을 기준으로 좌표 시스템은 일반적인 그리기 즉, 컨트롤의 왼쪽 위 모서리는 0, 0입니다. 합니다 `Paint` 이벤트 및 `OnPaint` 에 대 한 메서드는 <xref:System.Windows.Forms.ToolStripItem> 다른 컨트롤 그리기 이벤트 처럼 동작 합니다.

또한 <xref:System.Windows.Forms.ToolStrip> 컨트롤은 배경, 항목 배경, 항목 이미지, 항목 화살표, 항목 텍스트 <xref:System.Windows.Forms.ToolStripRenderer> 및 테두리를 그리기 위한 재정의 가능한 메서드를 포함 하는 클래스를 통해 항목과 컨테이너를 렌더링 하는 데 보다 세부적인 액세스를 제공 합니다. <xref:System.Windows.Forms.ToolStrip>. 이러한 메서드에 대 한 이벤트 인수를 사각형, 색 및 원하는 대로 조정할 수 있는 텍스트 형식 등의 여러 속성을 노출 합니다.

항목을 그리는 방법을의 몇 가지 측면을 조정 하려면 일반적으로 재정의 된 <xref:System.Windows.Forms.ToolStripRenderer>합니다.

새 항목을 작성 하는 그리기의 모든 측면을 제어 하려는 경우 재정의 `OnPaint` 메서드. 내에서 `OnPaint`에서 메서드를 사용할 수는 <xref:System.Windows.Forms.ToolStripRenderer>합니다.

기본적으로 <xref:System.Windows.Forms.ToolStrip> 이중 버퍼링을 활용 하 고 되는지는 <xref:System.Windows.Forms.ControlStyles.OptimizedDoubleBuffer> 설정 합니다.

#### <a name="parenting"></a>상위

컨테이너 소유권과 부모로 이루어진 개념은 다른 Windows Forms 컨테이너 컨트롤 보다 <xref:System.Windows.Forms.ToolStrip> 컨트롤에서 더 복잡 합니다. 오버플로와 같은 동적 시나리오를 지원 하 고, 여러 <xref:System.Windows.Forms.ToolStrip> 항목에서 드롭다운 항목을 공유 하 고, 컨트롤 <xref:System.Windows.Forms.ContextMenuStrip> 에서의 생성을 지 원하는 데 필요 합니다.

다음 목록에서는 부모로 관련 된 멤버를 설명 하 고 사용 방법을 설명 합니다.

- <xref:System.Windows.Forms.ToolStripDropDown.OwnerItem%2A>드롭다운 항목의 원본인 항목에 액세스 합니다. 와 유사 <xref:System.Windows.Forms.ContextMenuStrip.SourceControl%2A>하지만 컨트롤을 반환 하는 대신를 <xref:System.Windows.Forms.ToolStripItem>반환 합니다.

- <xref:System.Windows.Forms.ContextMenuStrip.SourceControl%2A>여러 컨트롤이 동일한 <xref:System.Windows.Forms.ContextMenuStrip> <xref:System.Windows.Forms.ContextMenuStrip>를 공유 하는 경우의 소스로 사용할 컨트롤을 결정 합니다.

- <xref:System.Windows.Forms.ToolStripItem.GetCurrentParent%2A> 에 대 한 읽기 전용 접근자는 <xref:System.Windows.Forms.ToolStripItem.Parent%2A> 속성입니다. 부모와 달리 소유자에서 부모 나타냅니다는 반환 된 현재 <xref:System.Windows.Forms.ToolStrip> 항목이 표시 되는는 오버플로 영역에 있을 수 있습니다.

- <xref:System.Windows.Forms.ToolStripItem.Owner%2A> 반환 된 <xref:System.Windows.Forms.ToolStrip> 해당 항목 컬렉션에 현재 포함 되어 <xref:System.Windows.Forms.ToolStripItem>. 이 참조 하는 가장 좋은 방법은 <xref:System.Windows.Forms.ToolStrip.ImageList%2A> 또는 기타 속성 최상위 <xref:System.Windows.Forms.ToolStrip> 오버플로 처리 하는 특수 코드를 작성 하지 않고도 합니다.

#### <a name="behavior-of-inherited-controls"></a>상속 된 컨트롤의 동작

다음 컨트롤은 상속에 사용 될 때마다 잠깁니다.

- <xref:System.Windows.Forms.ToolStrip>

- <xref:System.Windows.Forms.MenuStrip>

- <xref:System.Windows.Forms.ContextMenuStrip>

- <xref:System.Windows.Forms.StatusStrip>

- <xref:System.Windows.Forms.ToolStripPanel>여기에는 <xref:System.Windows.Forms.ToolStripContainer> 및 개별 <xref:System.Windows.Forms.ToolStripPanel> 컨트롤의 패널도 포함 됩니다.

예를 들어 이전 목록에 있는 하나 이상의 컨트롤을 사용 하 여 새 Windows Forms 응용 프로그램을 만듭니다. 하나 이상의 컨트롤에 대 한 액세스 한정자를 또는 `public` `protected`로 설정 하 고 프로젝트를 빌드합니다. 첫 번째 폼에서 상속 되는 폼을 추가한 다음 상속 된 컨트롤을 선택 합니다. 컨트롤이 잠긴 것으로 표시 되 면 해당 액세스 한정자가 `private`인 것 처럼 동작 합니다.

#### <a name="toolstripcontainer-support-of-inheritance"></a>ToolStripContainer 상속 지원

컨트롤 <xref:System.Windows.Forms.ToolStripContainer> 은 다음 예제와 비슷하게 제한 된 상속 된 시나리오를 지원 합니다.

1. 새 Windows Forms 애플리케이션을 만듭니다.

2. 폼에 <xref:System.Windows.Forms.ToolStripContainer>를 추가합니다.

3. 의 <xref:System.Windows.Forms.ToolStripContainer> 액세스 한정자를 또는 `protected`로 `public` 설정 합니다.

4. , <xref:System.Windows.Forms.ToolStrip> <xref:System.Windows.Forms.ToolStripPanel> 및 컨트롤의 조합을의 영역<xref:System.Windows.Forms.ToolStripContainer>에 추가 합니다. <xref:System.Windows.Forms.ContextMenuStrip> <xref:System.Windows.Forms.MenuStrip>

5. 프로젝트를 빌드합니다.

6. 첫 번째 폼에서 상속 되는 폼을 추가 합니다.

7. 폼에서 상속 <xref:System.Windows.Forms.ToolStripContainer> 된을 선택 합니다.

#### <a name="inherited-behavior-of-child-controls"></a>자식 컨트롤의 상속 된 동작

이전 단계를 완료 한 후에는 다음과 같은 상속 된 동작이 발생 합니다.

- 디자이너에서 컨트롤이 상속 된 아이콘과 함께 표시 됩니다.

- <xref:System.Windows.Forms.ToolStripPanel> 컨트롤이 잠겨 있으므로 해당 콘텐츠를 선택 하거나 다시 정렬할 수 없습니다.

- 에 컨트롤 <xref:System.Windows.Forms.ToolStripContentPanel>을 추가 하 고, 컨트롤을 이동 하 고, 컨트롤을의 자식 컨트롤로 <xref:System.Windows.Forms.ToolStripContentPanel>만들 수 있습니다.

- 양식을 작성 한 후 변경 내용이 유지 됩니다.

  > [!NOTE]
  > 의 일부인 모든 <xref:System.Windows.Forms.ToolStripPanel> 컨트롤에서 액세스 한정자를 제거 합니다.<xref:System.Windows.Forms.ToolStripContainer> 의 <xref:System.Windows.Forms.ToolStripContainer> 액세스 한정자는 전체 컨트롤을 제어 합니다.

#### <a name="partial-trust"></a>부분 신뢰

부분 신뢰의 `ToolStrip`에 대 한 제한 사항은 권한이 없는 사람이 나 서비스에서 사용 될 수 있는 개인 정보를 실수로 입력 하지 않도록 하기 위한 것입니다. 보호 조치는 다음과 같습니다.

- `ToolStripDropDown`컨트롤은 <xref:System.Security.Permissions.UIPermissionWindow.AllWindows> <xref:System.Windows.Forms.ToolStripControlHost>에 항목을 표시 해야 합니다. 이는 <xref:System.Windows.Forms.ToolStripTextBox>,, <xref:System.Windows.Forms.ToolStripProgressBar> 등의 <xref:System.Windows.Forms.ToolStripComboBox>내장 컨트롤과 사용자가 만든 컨트롤에 모두 적용 됩니다. 이 요구 사항이 충족 되지 않으면 이러한 항목이 표시 되지 않습니다. 예외가 throw되지 않습니다.

- 속성을로 `false` 설정 하는 것은 허용 되지 않으며 <xref:System.Windows.Forms.ToolStripDropDown.Closing> , 취소할 수 있는 이벤트 매개 변수는 무시 됩니다. <xref:System.Windows.Forms.ToolStripDropDown.AutoClose%2A> 이렇게 하면 드롭다운 항목을 해제 하지 않고 키를 두 번 이상 입력할 수 없습니다. 이 요구 사항이 충족 되지 않으면 이러한 항목이 표시 되지 않습니다. 예외가 throw되지 않습니다.

- 가 아닌 <xref:System.Security.Permissions.UIPermissionWindow.AllWindows>부분 신뢰 컨텍스트에서 발생 하는 경우 많은 키 입력 처리 이벤트가 발생 하지 않습니다.

- 가 부여 되지 않은 경우 <xref:System.Security.Permissions.UIPermissionWindow.AllWindows> 에는 액세스 키가 처리 되지 않습니다.

#### <a name="usage"></a>사용

다음 사용 패턴은 레이아웃, 키보드 상호 <xref:System.Windows.Forms.ToolStrip> 작용 및 최종 사용자 동작에 대 한 베어링을 포함 합니다.

- 에 조인 됨<xref:System.Windows.Forms.ToolStripPanel>

  는 내에서 <xref:System.Windows.Forms.ToolStripPanel>및에 걸쳐 위치를 변경할 수있습니다.<xref:System.Windows.Forms.ToolStrip> <xref:System.Windows.Forms.ToolStripPanel> `Dock` 속성이 무시 됩니다 경우에 <xref:System.Windows.Forms.ToolStrip.Stretch%2A> 속성은 `false`, 크기를 <xref:System.Windows.Forms.ToolStrip> 에 항목을 추가 함에 따라는 <xref:System.Windows.Forms.ToolStripPanel>합니다. 일반적으로 <xref:System.Windows.Forms.ToolStrip> 탭 순서에 참여 하지 않습니다.

- 도킹됨

  는 <xref:System.Windows.Forms.ToolStrip> 고정 된 위치에 있는 컨테이너의 한쪽에 배치 되 고 크기는 도킹 되는 전체 가장자리를 중심으로 확장 됩니다. 일반적으로 <xref:System.Windows.Forms.ToolStrip> 탭 순서에 참여 하지 않습니다.

- 절대 위치

  는 <xref:System.Windows.Forms.ToolStrip> 다른 컨트롤과 마찬가지로, <xref:System.Windows.Forms.Control.Location%2A> 속성에 의해 배치 되 고 크기가 고정 되어 있으며 일반적으로 탭 순서에 참여 합니다.

#### <a name="keyboard-interaction"></a>키보드 상호 작용

##### <a name="access-keys"></a>액세스 키

ALT 키와 결합 된 액세스 키는 키보드를 사용 하 여 컨트롤을 활성화 하는 한 가지 방법입니다. <xref:System.Windows.Forms.ToolStrip>에서는 명시적 및 암시적 액세스 키를 모두 지원 합니다. 명시적 정의는 문자 앞에 앰퍼샌드 (&) 문자를 사용 합니다. 암시적 정의는 지정 `Text` 된 속성의 문자 순서를 기준으로 일치 하는 항목을 찾으려고 시도 하는 알고리즘을 사용 합니다.

##### <a name="shortcut-keys"></a>바로 가기 키

에서 <xref:System.Windows.Forms.MenuStrip> 사용 하는 바로 가기 키는 <xref:System.Windows.Forms.Keys> 열거형 (순서에 한정 되지 않음)의 조합을 사용 하 여 바로 가기 키를 정의 합니다. 또한 <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeyDisplayString%2A> 속성을 사용 하 여 텍스트를 포함 하는 바로 가기 키를 표시할 수 있습니다. 예를 들어 "삭제" 대신 "Del"을 표시 합니다.

##### <a name="navigation"></a>탐색

ALT 키를 누르면가 <xref:System.Windows.Forms.MenuStrip> 가리키는가 <xref:System.Windows.Forms.Form.MainMenuStrip%2A>활성화 됩니다. 여기에서 CTRL + TAB은 내의 <xref:System.Windows.Forms.ToolStrip> `ToolStripPanel`컨트롤 사이를 탐색 합니다. 숫자 키패드의 TAB 키와 화살표 키는의 <xref:System.Windows.Forms.ToolStrip>항목 간을 탐색 합니다. 특수 알고리즘은 오버플로 영역의 탐색을 처리 합니다. 스페이스바는 <xref:System.Windows.Forms.ToolStripButton>, <xref:System.Windows.Forms.ToolStripDropDownButton>또는 <xref:System.Windows.Forms.ToolStripSplitButton>를 선택 합니다.

##### <a name="focus-and-validation"></a>포커스 및 유효성 검사

ALT 키를 활성화 합니다 <xref:System.Windows.Forms.MenuStrip> 또는 <xref:System.Windows.Forms.ToolStrip> 도 현재 포커스가 있는 컨트롤에서 포커스가 제거 합니다. 내에 호스트 된 컨트롤 인지를 <xref:System.Windows.Forms.MenuStrip> 의 드롭다운 또는 <xref:System.Windows.Forms.MenuStrip>, 컨트롤 사용자가 TAB 키를 누를 때 포커스를 얻습니다. 일반적으로 <xref:System.Windows.Forms.Control.GotFocus>, <xref:System.Windows.Forms.Control.LostFocus>를 <xref:System.Windows.Forms.Control.Enter>, 및 <xref:System.Windows.Forms.Control.Leave> 의 이벤트 <xref:System.Windows.Forms.MenuStrip> 키보드에서 활성화 될 경우 발생할 수 있습니다. 이러한 경우에 사용 된 <xref:System.Windows.Forms.MenuStrip.MenuActivate> 및 <xref:System.Windows.Forms.MenuStrip.MenuDeactivate> 이벤트 대신 합니다.

기본적으로 <xref:System.Windows.Forms.ToolStrip.CausesValidation%2A> 는 `false`합니다. 폼 <xref:System.Windows.Forms.ContainerControl.Validate%2A> 에서 명시적으로를 호출 하 여 유효성 검사를 수행 합니다.

#### <a name="layout"></a>레이아웃

속성을 <xref:System.Windows.Forms.ToolStrip> 사용 <xref:System.Windows.Forms.ToolStripLayoutStyle> 하 여의 멤버 중 하나를 선택 하 여 레이아웃을 제어 합니다. <xref:System.Windows.Forms.ToolStrip.LayoutStyle%2A>

##### <a name="stack-layouts"></a>스택 레이아웃

누적은의 <xref:System.Windows.Forms.ToolStrip>양쪽 끝에 있는 항목을 정렬 하는 것입니다. 다음은 스택 레이아웃을 설명합니다.

- 기본값은 <xref:System.Windows.Forms.ToolStripLayoutStyle.StackWithOverflow>입니다. 이 설정을 <xref:System.Windows.Forms.ToolStrip> <xref:System.Windows.Forms.ToolStrip.Orientation%2A> 사용 하면에서 속성에 따라 끌기 및 도킹 시나리오를 처리 하는 레이아웃을 자동으로 변경 합니다.

- <xref:System.Windows.Forms.ToolStripLayoutStyle.VerticalStackWithOverflow>항목을 <xref:System.Windows.Forms.ToolStrip> 세로로 나란히 렌더링 합니다.

- <xref:System.Windows.Forms.ToolStripLayoutStyle.HorizontalStackWithOverflow>항목을 <xref:System.Windows.Forms.ToolStrip> 가로 방향으로 나란히 렌더링 합니다.

##### <a name="other-features-of-stack-layouts"></a>스택 레이아웃의 다른 기능

<xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 종료를 결정 합니다 <xref:System.Windows.Forms.ToolStrip> 항목 정렬 됩니다.

항목 내에서 적합 하지 않은 경우는 <xref:System.Windows.Forms.ToolStrip>, 오버플로 단추를 자동으로 표시 됩니다. <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> 속성을 설정 하지 않았거나 전혀 필요에 따라 항상 넘침 영역 항목을 표시할지 여부를 결정 합니다.

에 <xref:System.Windows.Forms.ToolStrip.LayoutCompleted> 이벤트를 검사할 수 있습니다 합니다 <xref:System.Windows.Forms.ToolStripItem.Placement%2A> 항목 주에 배치 되었는지 여부를 결정 하는 속성 <xref:System.Windows.Forms.ToolStrip>, 오버플로 <xref:System.Windows.Forms.ToolStrip>, 전혀 표시 되지 않는 경우 또는. 항목이 표시 되지 않습니다 하는 일반적인 이유는 주 항목에는 적합 하지 않은 <xref:System.Windows.Forms.ToolStrip> 및 해당 <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> 속성이 <xref:System.Windows.Forms.ToolStripItemOverflow.Never>합니다.

확인을 <xref:System.Windows.Forms.ToolStrip> 에 배치 하 여 이동할 수는 <xref:System.Windows.Forms.ToolStripPanel> 설정 해당 <xref:System.Windows.Forms.ToolStrip.GripStyle%2A> 에 <xref:System.Windows.Forms.ToolStripGripStyle.Visible>입니다.

##### <a name="other-layout-options"></a>다른 레이아웃 옵션

다른 레이아웃 옵션 <xref:System.Windows.Forms.ToolStripLayoutStyle.Flow> 은 및 <xref:System.Windows.Forms.ToolStripLayoutStyle.Table>입니다.

##### <a name="flow-layout"></a>선형 레이아웃

<xref:System.Windows.Forms.ToolStripLayoutStyle.Flow>레이아웃은, <xref:System.Windows.Forms.ContextMenuStrip> <xref:System.Windows.Forms.ToolStripDropDownMenu>및 <xref:System.Windows.Forms.ToolStripOverflow>에 대 한 기본값입니다. 비슷합니다는 <xref:System.Windows.Forms.FlowLayoutPanel>합니다. 레이아웃의 <xref:System.Windows.Forms.ToolStripLayoutStyle.Flow> 기능은 다음과 같습니다.

- 기능의 일부만 <xref:System.Windows.Forms.FlowLayoutPanel> 에 의해 노출 되는 <xref:System.Windows.Forms.ToolStrip.LayoutSettings%2A> 속성입니다. 캐스팅 해야 합니다 <xref:System.Windows.Forms.LayoutSettings> 클래스는 <xref:System.Windows.Forms.FlowLayoutSettings> 클래스입니다.

- 사용할 수는 <xref:System.Windows.Forms.ToolStripItem.Dock%2A> 고 <xref:System.Windows.Forms.ToolStripItem.Anchor%2A> 행 내에서 항목을 정렬 하려면 코드에서 속성입니다.

- <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 속성은 무시됩니다.

- 에 <xref:System.Windows.Forms.ToolStrip.LayoutCompleted> 이벤트를 검사할 수 있습니다 합니다 <xref:System.Windows.Forms.ToolStripItem.Placement%2A> 주 항목 배치 되었는지 여부를 결정 하는 속성 <xref:System.Windows.Forms.ToolStrip> 에 적합 하지 않은 또는.

- 그립은 렌더링 되지 않으므로의 레이아웃 <xref:System.Windows.Forms.ToolStrip> <xref:System.Windows.Forms.ToolStripPanel> 에서 <xref:System.Windows.Forms.ToolStripLayoutStyle.Flow> 을 이동할 수 없습니다.

- 합니다 <xref:System.Windows.Forms.ToolStrip> 오버플로 단추가 렌더링 되지 않습니다 및 <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> 무시 됩니다.

##### <a name="table-layout"></a>테이블 레이아웃

<xref:System.Windows.Forms.ToolStripLayoutStyle.Table>레이아웃은의 <xref:System.Windows.Forms.StatusStrip>기본값입니다. 비슷합니다 <xref:System.Windows.Forms.TableLayoutPanel>합니다. 레이아웃의 <xref:System.Windows.Forms.ToolStripLayoutStyle.Flow> 기능은 다음과 같습니다.

- 기능의 일부만 <xref:System.Windows.Forms.TableLayoutPanel> 에 의해 노출 되는 <xref:System.Windows.Forms.ToolStrip.LayoutSettings%2A> 속성입니다. 캐스팅 해야 합니다 <xref:System.Windows.Forms.LayoutSettings> 클래스는 <xref:System.Windows.Forms.TableLayoutSettings> 클래스입니다.

- 사용할 수는 <xref:System.Windows.Forms.ToolStripItem.Dock%2A> 고 <xref:System.Windows.Forms.ToolStripItem.Anchor%2A> 테이블 셀 내 항목을 정렬 하려면 코드에서 속성입니다.

- <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 속성은 무시됩니다.

- 에 <xref:System.Windows.Forms.ToolStrip.LayoutCompleted> 이벤트를 검사할 수 있습니다 합니다 <xref:System.Windows.Forms.ToolStripItem.Placement%2A> 주 항목 배치 되었는지 여부를 결정 하는 속성 <xref:System.Windows.Forms.ToolStrip> 에 적합 하지 않은 또는.

- 그립은 렌더링 되지 않으므로의 레이아웃 <xref:System.Windows.Forms.ToolStrip> <xref:System.Windows.Forms.ToolStripPanel> 에서 <xref:System.Windows.Forms.ToolStripLayoutStyle.Table> 을 이동할 수 없습니다.

- 합니다 <xref:System.Windows.Forms.ToolStrip> 오버플로 단추가 렌더링 되지 않습니다 및 <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> 무시 됩니다.

## <a name="toolstripitem"></a>ToolStripItem

다음 항목에서는 및 <xref:System.Windows.Forms.ToolStripItem> 이 항목에서 파생 되는 컨트롤에 대해 설명 합니다.

<xref:System.Windows.Forms.ToolStripItem>는로 이동 <xref:System.Windows.Forms.ToolStrip>하는 모든 항목에 대 한 추상 기본 클래스입니다. 다음 개체 모델에서는 상속 계층 <xref:System.Windows.Forms.ToolStripItem> 구조를 보여 줍니다.

![ToolStripItem 개체 모델을 보여 주는 다이어그램입니다.](./media/toolstrip-control-architecture/toolstripitem-object-model.gif)

<xref:System.Windows.Forms.ToolStripItem> 클래스에서 직접 상속 되거나 <xref:System.Windows.Forms.ToolStripItem>를 간접적으로 상속 됩니다에서 또는 <xref:System.Windows.Forms.ToolStripItem> 를 통해 <xref:System.Windows.Forms.ToolStripControlHost> 또는 <xref:System.Windows.Forms.ToolStripDropDownItem>합니다.

<xref:System.Windows.Forms.ToolStripItem> 컨트롤에 포함 되어야 합니다는 <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.MenuStrip>를 <xref:System.Windows.Forms.StatusStrip>, 또는 <xref:System.Windows.Forms.ContextMenuStrip> 폼에 직접 추가할 수 없습니다. 다양 한 컨테이너 클래스의 적절 한 하위 집합을 포함 하도록 만들어진 <xref:System.Windows.Forms.ToolStripItem> 컨트롤입니다.

다음 표에서는 스톡 <xref:System.Windows.Forms.ToolStripItem> 컨트롤과이 컨트롤이 가장 잘 보이는 컨테이너를 나열 합니다. 모든 항목이 파생 된 컨테이너 <xref:System.Windows.Forms.ToolStrip>에서 호스팅될 수 있지만 이러한 항목은 다음 컨테이너에서 가장 잘 보이도록 설계 되었습니다. <xref:System.Windows.Forms.ToolStrip>

> [!NOTE]
> <xref:System.Windows.Forms.ToolStripDropDown>는 디자이너 도구 상자에 표시 되지 않습니다.

|포함 된 항목|ToolStrip|MenuStrip|ContextMenuStrip|StatusStrip|ToolStripDropDown|
|--------------------|---------------|---------------|----------------------|-----------------|-----------------------|
|<xref:System.Windows.Forms.ToolStripButton>|예|아니오|아니요|아니요|예|
|<xref:System.Windows.Forms.ToolStripComboBox>|예|예|예|아니요|예|
|<xref:System.Windows.Forms.ToolStripSplitButton>|예|아니오|아니요|예|예|
|<xref:System.Windows.Forms.ToolStripLabel>|예|아니오|아니요|예|예|
|<xref:System.Windows.Forms.ToolStripSeparator>|예|예|예|아니요|예|
|<xref:System.Windows.Forms.ToolStripDropDownButton>|예|아니오|아니요|예|예|
|<xref:System.Windows.Forms.ToolStripTextBox>|예|예|예|아니요|예|
|<xref:System.Windows.Forms.ToolStripMenuItem>|아니요|예|예|아니오|아니요|
|<xref:System.Windows.Forms.ToolStripStatusLabel>|아니요|아니요|아니요|예|아니요|
|<xref:System.Windows.Forms.ToolStripProgressBar>|예|아니오|아니요|예|아니요|
|<xref:System.Windows.Forms.ToolStripControlHost>|예|예|아니요|예|예|

### <a name="toolstripbutton"></a>ToolStripButton

<xref:System.Windows.Forms.ToolStripButton>는에 대 한 <xref:System.Windows.Forms.ToolStrip>단추 항목입니다. 다양 한 테두리 스타일을 사용 하 여 표시할 수 있으며,이를 사용 하 여 작동 상태를 표시 하 고 활성화할 수 있습니다. 기본적으로 포커스를 갖도록 정의할 수 있습니다.

### <a name="toolstriplabel"></a>ToolStripLabel

는 <xref:System.Windows.Forms.ToolStripLabel> 컨트롤에 <xref:System.Windows.Forms.ToolStrip> 레이블 기능을 제공 합니다. 합니다 <xref:System.Windows.Forms.ToolStripLabel> 비슷합니다는 <xref:System.Windows.Forms.ToolStripButton> 기본적으로 포커스를 받지 않고 및 푸시 되거나 강조 표시 된으로 렌더링 하지 않습니다.

<xref:System.Windows.Forms.ToolStripLabel> 호스트 항목으로 액세스 키를 지원합니다.

사용 하 여는 <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>, <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A>, 및 <xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A> 속성에는 <xref:System.Windows.Forms.ToolStripLabel> 의 링크 제어를 지원 하려면를 <xref:System.Windows.Forms.ToolStrip>합니다.

### <a name="toolstripstatuslabel"></a>ToolStripStatusLabel

<xref:System.Windows.Forms.ToolStripStatusLabel> 버전이 <xref:System.Windows.Forms.ToolStripLabel> 에서 사용 하기 위해 특별히 설계 된 <xref:System.Windows.Forms.StatusStrip>합니다. 특별 한 기능이 포함 됩니다 <xref:System.Windows.Forms.ToolStripStatusLabel.BorderStyle%2A>, <xref:System.Windows.Forms.ToolStripStatusLabel.BorderSides%2A>, 및 <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A>합니다.

### <a name="toolstripseparator"></a>ToolStripSeparator

는 <xref:System.Windows.Forms.ToolStripSeparator> 방향에 따라 도구 모음이 나 메뉴에 세로 또는 가로 선을 추가 합니다. 메뉴에 있는 항목과 같은 항목의 그룹화 또는 차이를 제공 합니다.

추가할 수는 <xref:System.Windows.Forms.ToolStripSeparator> 드롭 다운 목록에서 선택 하 여 디자인 타임. 그러나 하면 자동으로 만들 수는 <xref:System.Windows.Forms.ToolStripSeparator> 디자이너 템플릿 노드 또는 하이픈 (-)를 입력 하 여는 <xref:System.Windows.Forms.ToolStripItemCollection.Add%2A> 메서드.

### <a name="toolstripcontrolhost"></a>ToolStripControlHost

<xref:System.Windows.Forms.ToolStripControlHost> 에 대 한 추상 기본 클래스인 <xref:System.Windows.Forms.ToolStripComboBox>, <xref:System.Windows.Forms.ToolStripTextBox>, 및 <xref:System.Windows.Forms.ToolStripProgressBar>합니다. <xref:System.Windows.Forms.ToolStripControlHost> 두 가지 방법으로 사용자 지정 컨트롤을 비롯 하 여 다른 컨트롤을 호스팅할 수 있습니다.

- 생성 된 <xref:System.Windows.Forms.ToolStripControlHost> 에서 파생 된 클래스를 사용 하 여 <xref:System.Windows.Forms.Control>입니다. 호스팅된 컨트롤 및 속성에 완전히 액세스 하려면 캐스팅 해야 합니다 <xref:System.Windows.Forms.ToolStripControlHost.Control%2A> 속성을 실제 클래스로 나타냅니다.

- 를 <xref:System.Windows.Forms.ToolStripControlHost>확장 하 고 상속 된 클래스의 매개 변수 없는 생성자에서에서 <xref:System.Windows.Forms.Control>파생 되는 클래스를 전달 하는 기본 클래스 생성자를 호출 합니다. 이 옵션을 사용 하면 일반적인 컨트롤의 메서드 및 속성에 쉽게 액세스할 수를 래핑하는 <xref:System.Windows.Forms.ToolStrip>합니다.

### <a name="toolstripcombobox"></a>ToolStripComboBox

<xref:System.Windows.Forms.ToolStripComboBox> <xref:System.Windows.Forms.ComboBox> 의 호스팅을 위해 최적화를 <xref:System.Windows.Forms.ToolStrip>입니다. 호스팅된 컨트롤의 속성 및 이벤트의 하위 집합에 노출 되는 <xref:System.Windows.Forms.ToolStripComboBox> 수준 이지만 기본 <xref:System.Windows.Forms.ComboBox> 제어를 통해 완벽 하 게 액세스할 수는 <xref:System.Windows.Forms.ToolStripComboBox.ComboBox%2A> 속성입니다.

### <a name="toolstriptextbox"></a>ToolStripTextBox

<xref:System.Windows.Forms.ToolStripTextBox> <xref:System.Windows.Forms.TextBox> 의 호스팅을 위해 최적화를 <xref:System.Windows.Forms.ToolStrip>입니다. 호스팅된 컨트롤의 속성 및 이벤트의 하위 집합에 노출 되는 <xref:System.Windows.Forms.ToolStripTextBox> 수준 이지만 기본 <xref:System.Windows.Forms.TextBox> 제어를 통해 완벽 하 게 액세스할 수는 <xref:System.Windows.Forms.ToolStripTextBox.TextBox%2A> 속성입니다.

### <a name="toolstripprogressbar"></a>ToolStripProgressBar

<xref:System.Windows.Forms.ToolStripProgressBar> <xref:System.Windows.Forms.ProgressBar> 의 호스팅을 위해 최적화를 <xref:System.Windows.Forms.ToolStrip>입니다. 호스팅된 컨트롤의 속성 및 이벤트의 하위 집합에 노출 되는 <xref:System.Windows.Forms.ToolStripProgressBar> 수준 이지만 기본 <xref:System.Windows.Forms.ProgressBar> 제어를 통해 완벽 하 게 액세스할 수는 <xref:System.Windows.Forms.ToolStripProgressBar.ProgressBar%2A> 속성입니다.

### <a name="toolstripdropdownitem"></a>ToolStripDropDownItem

<xref:System.Windows.Forms.ToolStripDropDownItem> 에 대 한 추상 기본 클래스인 <xref:System.Windows.Forms.ToolStripMenuItem>, <xref:System.Windows.Forms.ToolStripDropDownButton>, 및 <xref:System.Windows.Forms.ToolStripSplitButton>, 항목을 직접 또는 드롭 다운 컨테이너에 호스트 추가 항목을 호스팅할 수 있습니다. 설정 하 여이 작업을 수행 합니다 <xref:System.Windows.Forms.ToolStripDropDownItem.DropDown%2A> 속성을를 <xref:System.Windows.Forms.ToolStripDropDown> 설정를 <xref:System.Windows.Forms.ToolStrip.Items%2A> 의 속성은 <xref:System.Windows.Forms.ToolStripDropDown>합니다. 이러한 드롭다운 항목을 통해 직접 액세스는 <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItems%2A> 속성입니다.

### <a name="toolstripmenuitem"></a>ToolStripMenuItem

<xref:System.Windows.Forms.ToolStripMenuItem> <xref:System.Windows.Forms.ToolStripDropDownItem> 작동 하는 <xref:System.Windows.Forms.ToolStripDropDownMenu> 및 <xref:System.Windows.Forms.ContextMenuStrip> 메뉴에 대 한 특별 한 강조 표시, 레이아웃 및 열 정렬을 처리 하기.

### <a name="toolstripdropdownbutton"></a>ToolStripDropDownButton

<xref:System.Windows.Forms.ToolStripDropDownButton> 다음과 같은 <xref:System.Windows.Forms.ToolStripButton>, 하지만 사용자가 클릭 하면 드롭다운 영역을 보여 줍니다. 숨기 거 나 설정 하 여 드롭다운 화살표를 표시 합니다 <xref:System.Windows.Forms.ToolStripDropDownButton.ShowDropDownArrow%2A> 속성입니다. <xref:System.Windows.Forms.ToolStripDropDownButton> 호스트는 <xref:System.Windows.Forms.ToolStripOverflowButton> 오버플로 하는 항목을 표시 하는 <xref:System.Windows.Forms.ToolStrip>합니다.

### <a name="toolstripsplitbutton"></a>ToolStripSplitButton

<xref:System.Windows.Forms.ToolStripSplitButton> 단추 및 드롭다운 단추 기능을 결합합니다.

사용 하 여는 <xref:System.Windows.Forms.ToolStripSplitButton.DefaultItem%2A> 동기화 하는 속성을 <xref:System.Windows.Forms.Control.Click> 단추에 표시 되는 항목을 사용 하 여 선택한 드롭다운 목록 항목의 이벤트입니다.

### <a name="toolstripitem-generic-features"></a>ToolStripItem 일반 기능

<xref:System.Windows.Forms.ToolStripItem>에서는 컨트롤을 상속 하는 다음과 같은 일반 기능과 옵션을 제공 합니다.

- 핵심 이벤트

- 이미지 처리

- 맞춤

- 텍스트 및 이미지 관계

- 표시 스타일

#### <a name="core-events"></a>핵심 이벤트

<xref:System.Windows.Forms.ToolStripItem>컨트롤은 자신의 클릭, 마우스 및 그리기 이벤트를 수신 하 고 일부 키보드 전처리도 수행할 수 있습니다.

#### <a name="image-handling"></a>이미지 처리

합니다 <xref:System.Windows.Forms.ToolStripItem.Image%2A>, <xref:System.Windows.Forms.ToolStripItem.ImageAlign%2A>를 <xref:System.Windows.Forms.ToolStripItem.ImageIndex%2A>, <xref:System.Windows.Forms.ToolStripItem.ImageKey%2A>, 및 <xref:System.Windows.Forms.ToolStripItem.ImageScaling%2A> 다양 한 이미지 처리와 관련 된 속성입니다. 이미지를 사용 하 여 <xref:System.Windows.Forms.ToolStrip> 컨트롤의 실행 시간 – 전용를 설정 하거나 직접 이러한 속성을 설정 하 여 <xref:System.Windows.Forms.ToolStrip.ImageList%2A> 속성입니다.

둘 다에서 속성의 상호 작용에 의해 결정 됩니다 이미지 크기 조정 <xref:System.Windows.Forms.ToolStrip> 및 <xref:System.Windows.Forms.ToolStripItem>다음과 같이 합니다.

- <xref:System.Windows.Forms.ToolStrip.ImageScalingSize%2A> 이미지의 조합으로 결정 된 최종 이미지의 소수 자릿수 <xref:System.Windows.Forms.ToolStripItem.ImageScaling%2A> 설정 및 컨테이너의 <xref:System.Windows.Forms.ToolStrip.AutoSize%2A> 설정 합니다.

  - 경우 <xref:System.Windows.Forms.ToolStrip.AutoSize%2A> 됩니다 `true` (기본값) 및 <xref:System.Windows.Forms.ToolStripItemImageScaling> 됩니다 <xref:System.Windows.Forms.ToolStripItemImageScaling.SizeToFit>, 이미지 크기는 조정 되지 않습니다 및 <xref:System.Windows.Forms.ToolStrip> 크기는 가장 큰 항목 또는 지정 된 최소 크기의 합니다.

  - 경우 <xref:System.Windows.Forms.ToolStrip.AutoSize%2A> 됩니다 `false` 및 <xref:System.Windows.Forms.ToolStripItemImageScaling> 은 <xref:System.Windows.Forms.ToolStripItemImageScaling.None>, 모두 이미지도 <xref:System.Windows.Forms.ToolStrip> 발생 크기 조정 합니다.

#### <a name="alignment"></a>맞춤

<xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 속성의 값은 항목이 표시 되는 <xref:System.Windows.Forms.ToolStrip> 의 끝을 결정 합니다. 속성 <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 은<xref:System.Windows.Forms.ToolStrip> 의 레이아웃 스타일이 스택 오버플로 값 중 하나로 설정 된 경우에만 작동 합니다.

항목은 항목 컬렉션에 <xref:System.Windows.Forms.ToolStrip> 항목이 표시 되는 순서 대로에 배치 됩니다. 항목이 배치 되는 위치를 프로그래밍 방식으로 변경 하려면 <xref:System.Windows.Forms.ToolStripItemCollection.Insert%2A> 메서드를 사용 하 여 컬렉션에서 항목을 이동 합니다. 이 메서드는 항목을 이동 하지만 중복 되지 않습니다.

#### <a name="text-and-image-relationship"></a>텍스트 및 이미지 관계

속성 <xref:System.Windows.Forms.ToolStripItem.TextImageRelation%2A> 은<xref:System.Windows.Forms.ToolStripItem>의 텍스트와 관련 하 여 이미지의 상대적인 배치를 정의 합니다. 이미지, 텍스트 또는 둘 다 없는 항목은 특별 한 경우로 처리 됩니다 있도록는 <xref:System.Windows.Forms.ToolStripItem> 누락 된 요소 또는 요소에 대 한 빈 곳을 표시 하지 않습니다.

#### <a name="display-style"></a>표시 스타일

<xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A>원하는 항목만 표시 하면서 항목의 텍스트 및 이미지 속성 값을 설정할 수 있습니다. 이 각기 다른 컨텍스트에서 동일한 항목을 표시할 때만 표시 스타일을 변경 하려면 일반적으로 사용 됩니다.

## <a name="accessory-classes"></a>액세서리 클래스

다양 한 다른 기능을 제공 하는 클래스는 다음과 같습니다.

- <xref:System.Windows.Forms.ToolStripManager> 지원 <xref:System.Windows.Forms.ToolStrip>-관련 병합, 설정 및 렌더러 옵션 등의 전체 응용 프로그램에 대 한 작업입니다.

- <xref:System.Windows.Forms.ToolStripRenderer>특정 스타일 또는 테마 <xref:System.Windows.Forms.ToolStrip> 를에 쉽게 적용할 수 있습니다.

- <xref:System.Windows.Forms.ToolStripProfessionalRenderer>대체 가능한 색 테이블 (<xref:System.Windows.Forms.ProfessionalColorTable>)을 기반으로 펜 및 브러시를 만듭니다.

- <xref:System.Windows.Forms.ToolStripSystemRenderer> 시스템 색과 평면 비주얼 스타일을 적용 <xref:System.Windows.Forms.ToolStrip> 응용 프로그램입니다.

- <xref:System.Windows.Forms.ToolStripContainer> 비슷합니다 <xref:System.Windows.Forms.SplitContainer>합니다. 도킹 된 쪽 패널 네 개 사용 하 여 (인스턴스의 <xref:System.Windows.Forms.ToolStripPanel>) 및 중앙 패널이 하나 (인스턴스의 <xref:System.Windows.Forms.ToolStripContentPanel>) 일반적인 배열을 만드는 데 있습니다. 측면 패널은 제거할 수 없지만 숨길 수는 있습니다. 중앙 패널을 제거 하거나 숨길 수 없습니다. 하나 이상의 정렬할 수 있습니다 <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.MenuStrip>, 또는 <xref:System.Windows.Forms.StatusStrip> 측면 패널에서 컨트롤 다른 컨트롤에 대 한 중앙 패널을 사용할 수 있습니다. <xref:System.Windows.Forms.ToolStripContentPanel> 또한 일관 된 모양을 위해 폼의 본문으로 렌더러 지원을 받는 방법을 제공 합니다. <xref:System.Windows.Forms.ToolStripContainer>는 MDI (다중 문서 인터페이스)를 지원 하지 않습니다.

- <xref:System.Windows.Forms.ToolStripPanel>컨트롤 이동 및 정렬 <xref:System.Windows.Forms.ToolStrip> 에 사용할 공간을 제공 합니다. 한 패널만 사용할 수 있으며, <xref:System.Windows.Forms.ToolStripPanel> 이 경우 MDI 시나리오에서 잘 작동 합니다.

## <a name="see-also"></a>참고자료

- [ToolStrip 컨트롤 개요](toolstrip-control-overview-windows-forms.md)
- [ToolStrip 기술 요약](toolstrip-technology-summary.md)
- [ToolStrip 컨트롤](toolstrip-control-windows-forms.md)
- [MenuStrip 컨트롤](menustrip-control-windows-forms.md)
- [StatusStrip 컨트롤](statusstrip-control.md)
- [ContextMenuStrip 컨트롤](contextmenustrip-control.md)
- [BindingNavigator 컨트롤](bindingnavigator-control-windows-forms.md)
