---
title: '연습: Windows Forms에서 맞춤선을 사용하여 컨트롤 정렬'
ms.date: 03/30/2017
helpviewer_keywords:
- controls [Windows Forms], arranging with snaplines
- snaplines [Windows Forms], arranging Windows Forms controls
- SnapLine class [Windows Forms], walkthroughs
- Windows Forms controls, arranging
ms.assetid: d5c9edc7-cf30-4a97-8ebe-201d569340f8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 83f0365ffb7335cb67c729c5a113e550c119191a
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987000"
---
# <a name="walkthrough-arrange-controls-on-windows-forms-using-snaplines"></a>연습: 맞춤선을 사용 하 여 Windows Forms에 대 한 컨트롤 정렬

폼의 정확한 컨트롤 배치는 많은 애플리케이션에서 우선 순위가 높습니다. Windows Forms 디자이너는이를 위해 다양 한 레이아웃 도구를 제공 합니다. 가장 중요 <xref:System.Windows.Forms.Design.Behavior.SnapLine> 한 기능 중 하나는 기능입니다.

맞춤선은 컨트롤을 다른 컨트롤과 비교할 수 있는 정확한 위치를 표시 합니다. 또한 [Windows 사용자 인터페이스 지침](/windows/win32/uxguide/guidelines)에 지정 된 대로 컨트롤 간의 여백에 권장 되는 거리가 표시 됩니다.

맞춤선을 사용 하면 선명 하 고 전문적인 모양 및 동작 (모양 및 느낌)을 위해 컨트롤을 쉽게 맞출 수 있습니다.

## <a name="create-the-project"></a>프로젝트를 만듭니다.

1. Visual Studio에서 "SnaplineExample" 이라는 Windows 기반 응용 프로그램 프로젝트를 만듭니다.

2. 폼 디자이너에서 폼을 선택 합니다.

## <a name="space-and-align-controls"></a>공간 및 맞춤 컨트롤

맞춤선은 폼에서 컨트롤을 정확 하 고 직관적인 방식으로 정렬 하는 방법을 제공 합니다. 이러한 컨트롤은 다른 컨트롤이 나 컨트롤 집합과 일치 하는 위치 근처에서 선택 된 컨트롤을 이동할 때 나타납니다. 선택 항목은 다른 컨트롤을 지나서 이동할 때 제안 된 위치에 "스냅" 됩니다.

### <a name="to-arrange-controls-using-snaplines"></a>맞춤선을 사용 하 여 컨트롤을 정렬 하려면

1. <xref:System.Windows.Forms.Button> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

2. 컨트롤을 <xref:System.Windows.Forms.Button> 폼의 오른쪽 아래 모퉁이로 이동 합니다. 컨트롤에 <xref:System.Windows.Forms.Button> 표시 되는 맞춤선은 폼의 아래쪽 및 오른쪽 테두리에 가까워집니다. 이러한 맞춤선은 컨트롤과 폼의 테두리 사이에 권장 되는 거리를 표시 합니다.

3. 폼의 <xref:System.Windows.Forms.Button> 테두리 주위에 컨트롤을 이동 하 고 맞춤선이 나타나는 위치를 확인 합니다. 완료 되 면 <xref:System.Windows.Forms.Button> 컨트롤을 폼의 가운데 근처로 이동 합니다.

4. <xref:System.Windows.Forms.Button> **도구 상자** 에서 다른 컨트롤을 폼으로 끌어 놓습니다.

5. 첫 번째 컨트롤 <xref:System.Windows.Forms.Button> 의 수준이 거의 될 때까지 두 번째 컨트롤을 이동 합니다. 두 단추의 텍스트 기준선에 표시 되는 맞춤선을 확인 하 고 이동 하는 컨트롤이 다른 컨트롤과 정확히 같은 수준의 위치로 스냅 되는지 확인 합니다.

6. 첫 번째 컨트롤 <xref:System.Windows.Forms.Button> 바로 위에 배치 될 때까지 두 번째 컨트롤을 이동 합니다. 두 단추의 왼쪽 및 오른쪽 가장자리를 따라 표시 되는 맞춤선을 확인 하 고 이동 하는 컨트롤이 다른 컨트롤에 정확히 맞춰진 위치에 맞춰집니다.

7. <xref:System.Windows.Forms.Button> 컨트롤 중 하나를 선택 하 고 거의 닿을 때까지 다른 컨트롤에 가깝게 이동 합니다. 두 요소 사이에 표시 되는 맞춤선을 확인 합니다. 이 거리는 컨트롤의 테두리 사이에 권장 되는 거리입니다. 또한 이동 하는 컨트롤이이 위치에 맞춰집니다.

8. <xref:System.Windows.Forms.Panel> **도구 상자** 에서 두 컨트롤을 폼으로 끌어 옵니다.

9. 첫 번째와 거의 <xref:System.Windows.Forms.Panel> 같은 수준에 도달할 때까지 컨트롤 중 하나를 이동 합니다. 두 컨트롤의 위쪽 및 아래쪽 가장자리에 표시 되는 맞춤선을 확인 하 고 이동 하는 컨트롤이 다른 컨트롤과 정확히 같은 수준의 위치로 맞춰집니다.

## <a name="align-to-form-and-container-margins"></a>폼 및 컨테이너 여백에 맞춤

맞춤선을 통해 컨트롤을 일관 된 방식으로 폼과 컨테이너 여백에 맞출 수 있습니다.

1. <xref:System.Windows.Forms.Button> 컨트롤 중 하나를 선택 하 고 맞춤선이 나타날 때까지 폼의 오른쪽 테두리에 가깝게 이동 합니다. 오른쪽 테두리의 맞춤선 거리는 컨트롤의 <xref:System.Windows.Forms.Control.Margin%2A> 속성 및 폼의 <xref:System.Windows.Forms.Control.Padding%2A> 속성 값의 합입니다.

   > [!NOTE]
   > 폼의 <xref:System.Windows.Forms.Control.Padding%2A> 속성이 0, 0, 0, 0으로 설정 된 경우 Windows Forms 디자이너는 폼에 9, 9, 9 <xref:System.Windows.Forms.Control.Padding%2A> , 9의 그림자 값을 제공 합니다. 이 동작을 재정의 하려면 0, 0, 0, 0이 아닌 값을 할당 합니다.

2. <xref:System.Windows.Forms.Button> **속성** 창에서 <xref:System.Windows.Forms.Control.Margin%2A> 항목을<xref:System.Windows.Forms.Control.Margin%2A> 확장 하 고 속성을0으로설정하여컨트롤의속성값을변경합니다.<xref:System.Windows.Forms.Padding.All%2A> 자세한 [내용은 연습: 안쪽 여백, 여백 및 AutoSize 속성](windows-forms-controls-padding-autosize.md)을 사용 하 여 Windows Forms 컨트롤 레이아웃

3. 맞춤선이 <xref:System.Windows.Forms.Button> 나타날 때까지 컨트롤을 폼의 오른쪽 테두리에 가깝게 이동 합니다. 이제이 거리가 폼의 <xref:System.Windows.Forms.Control.Padding%2A> 속성 값으로 제공 됩니다.

4. <xref:System.Windows.Forms.GroupBox> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

5. <xref:System.Windows.Forms.GroupBox> **속성** 창에서 <xref:System.Windows.Forms.Control.Padding%2A> 항목을<xref:System.Windows.Forms.Control.Padding%2A> 확장 하 고 속성을10으로설정하여컨트롤의속성값을변경합니다.<xref:System.Windows.Forms.Padding.All%2A>

6. **도구 상자** <xref:System.Windows.Forms.Button> 에서컨트롤로컨트롤을끌어옵니다.<xref:System.Windows.Forms.GroupBox>

7. 맞춤선이 나타날 때까지 컨트롤을 <xref:System.Windows.Forms.GroupBox> 컨트롤의 오른쪽 테두리에 가깝게 이동 합니다. <xref:System.Windows.Forms.Button> <xref:System.Windows.Forms.Button> 컨트롤<xref:System.Windows.Forms.GroupBox> 내에서 컨트롤을 이동 하 고 맞춤선이 나타나는 위치를 확인 합니다.

## <a name="align-to-grouped-controls"></a>그룹화 된 컨트롤에 맞춤

맞춤선을 사용 하 여 컨트롤 내의 컨트롤 뿐만 아니라 그룹화 된 <xref:System.Windows.Forms.GroupBox> 컨트롤을 맞출 수 있습니다.

1. 폼에서 컨트롤을 두 개 선택 합니다. 선택 영역을 이동 하 고 선택 영역과 다른 컨트롤 사이에 나타나는 맞춤선을 확인 합니다.

2. <xref:System.Windows.Forms.GroupBox> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

3. **도구 상자** <xref:System.Windows.Forms.Button> 에서컨트롤로컨트롤을끌어옵니다.<xref:System.Windows.Forms.GroupBox>

4. <xref:System.Windows.Forms.Button> 컨트롤 중 하나를 선택 하 여 <xref:System.Windows.Forms.GroupBox> 컨트롤 주위로 이동 합니다. <xref:System.Windows.Forms.GroupBox> 컨트롤의 가장자리에 표시 되는 맞춤선을 확인 합니다. 컨트롤에 포함 <xref:System.Windows.Forms.Button> <xref:System.Windows.Forms.GroupBox> 된 컨트롤의 가장자리에 나타나는 맞춤선도 확인 합니다. 컨테이너 컨트롤의 자식인 컨트롤은 맞춤선도 지원 합니다.

## <a name="use-snaplines-to-place-a-control-by-outlining-its-size"></a>맞춤선을 사용 하 여 컨트롤 크기를 표시 합니다.

1. **도구 상자**에서 <xref:System.Windows.Forms.Button> 컨트롤 아이콘을 클릭합니다. 폼으로 끌어다 놓지 마세요.

2. 폼의 디자인 화면 위로 마우스 포인터를 이동 합니다. 포인터가 <xref:System.Windows.Forms.Button> 컨트롤 아이콘이 연결된 십자형으로 바뀝니다. 또한 <xref:System.Windows.Forms.Button> 컨트롤의 맞춤 위치를 제안 하기 위해 표시 되는 맞춤선에 주목 하십시오.

3. 마우스 단추를 길게 클릭합니다.

4. 마우스 포인터를 폼 주위로 끌어 옵니다. 컨트롤의 위치와 크기를 나타내는 윤곽선이 그려집니다.

5. 폼의 다른 컨트롤에 맞춰질 때까지 포인터를 끕니다. 맞춤을 나타내는 맞춤선이 표시 됩니다.

6. 마우스 단추를 놓습니다. 컨트롤이 윤곽선에 표시 되는 위치와 크기에 생성 됩니다.

## <a name="use-snaplines-when-dragging-a-control-from-the-toolbox"></a>도구 상자에서 컨트롤을 끌 때 맞춤선 사용

1. <xref:System.Windows.Forms.Button> **도구 상자** 에서 컨트롤을 폼으로 끌어 온 다음 마우스 단추를 놓지 마십시오.

2. 폼의 디자인 화면 위로 마우스 포인터를 이동 합니다. 포인터가 새 <xref:System.Windows.Forms.Button> 컨트롤을 만들 위치를 나타내도록 변경 됩니다.

3. 마우스 포인터를 폼 주위로 끌어 옵니다. <xref:System.Windows.Forms.Button> 컨트롤의 맞춤 위치를 제안 하기 위해 표시 되는 맞춤선을 확인 합니다. 다른 컨트롤과 정렬 된 위치를 찾습니다.

4. 마우스 단추를 놓습니다. 컨트롤이 맞춤선이 나타내는 위치에 만들어집니다.

## <a name="resize-a-control-using-snaplines"></a>맞춤선을 사용 하 여 컨트롤 크기 조정

1. <xref:System.Windows.Forms.Button> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

2. 모퉁이 크기 <xref:System.Windows.Forms.Button> 조정 핸들 중 하나를 가져오고 끌어서 컨트롤의 크기를 조정 합니다. 자세한 내용은 [방법: Windows Forms](how-to-resize-controls-on-windows-forms.md)에서 컨트롤의 크기를 조정 합니다.

3. <xref:System.Windows.Forms.Button> 컨트롤의 테두리 중 하나가 다른 컨트롤에 맞춰질 때까지 크기 조정 핸들을 끕니다. 맞춤선이 표시 됩니다. 또한 크기 조정 핸들은 맞춤선이 나타내는 위치로 맞춰집니다.

4. 여러 방향 <xref:System.Windows.Forms.Button> 으로 컨트롤의 크기를 조정 하 고 크기 조정 핸들을 다른 컨트롤에 맞춥니다. 맞춤을 나타내기 위해 여러 방향에 맞춤선이 표시 되는 방식을 확인 합니다.

## <a name="align-a-label-to-a-controls-text"></a>컨트롤의 텍스트에 레이블 맞춤

1. <xref:System.Windows.Forms.TextBox> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다. 컨트롤을 <xref:System.Windows.Forms.TextBox> 폼에 놓으면 스마트 태그 문자 모양을 클릭 하 고 **텍스트를 textBox1으로 설정** 옵션을 선택 합니다. 자세한 [내용은 연습: Windows Forms 컨트롤](performing-common-tasks-using-smart-tags-on-wf-controls.md)에서 스마트 태그를 사용 하 여 일반적인 작업 수행

2. <xref:System.Windows.Forms.Label> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

3. <xref:System.Windows.Forms.Label> 컨트롤의 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성 값을 `true`로 변경합니다. 컨트롤의 테두리는 표시 텍스트에 맞게 조정 됩니다.

4. 컨트롤을 컨트롤의 왼쪽 <xref:System.Windows.Forms.TextBox> 으로 이동 하 여 컨트롤의 <xref:System.Windows.Forms.TextBox> 아래쪽 가장자리에 맞춥니다. <xref:System.Windows.Forms.Label> 두 컨트롤의 아래쪽 가장자리를 따라 나타나는 맞춤선을 확인 합니다.

5. <xref:System.Windows.Forms.Label> <xref:System.Windows.Forms.Label> 텍스트 와<xref:System.Windows.Forms.TextBox> 텍스트가 맞춰질 때까지 컨트롤을 조금 위로 이동 합니다. 두 컨트롤의 텍스트 필드가 정렬 되는 경우를 나타내는, 표시 되는 다른 스타일의 맞춤선에 유의 하십시오.

## <a name="use-snaplines-with-keyboard-navigation"></a>키보드 탐색에서 맞춤선 사용

1. <xref:System.Windows.Forms.Button> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다. 폼의 왼쪽 위 모퉁이에 놓습니다.

2. **Ctrl**+**아래쪽 화살표**를 누릅니다. 컨트롤은 폼을 사용 가능한 첫 번째 가로 맞춤 위치로 아래로 이동 합니다.

3. 컨트롤이 폼의 아래쪽에 도달할 때까지 **ctrl**+**아래쪽 화살표** 를 누릅니다. 폼을 아래로 이동할 때 위치를 확인 합니다.

4. **Ctrl**+**오른쪽 화살표**를 누릅니다. 컨트롤이 폼에서 사용 가능한 첫 번째 세로 맞춤 위치로 이동 합니다.

5. 컨트롤이 폼의 양쪽에 도달할 때까지 **ctrl**+**오른쪽 화살표** 를 누릅니다. 폼에서 이동할 때 위치를 확인 합니다.

6. 화살표 키의 조합을 사용 하 여 컨트롤을 폼 주위로 이동 합니다. 컨트롤이 있는 위치와 해당 컨트롤이 함께 나타나는 맞춤선을 확인 합니다.

7. <xref:System.Windows.Forms.Button> **Shift**+**화살표 키** 를 눌러 컨트롤의 크기를 한 픽셀씩 늘립니다.

8. <xref:System.Windows.Forms.Button> **Ctrl**+Shift화살표+**키** 를 눌러 맞춤선 단위로 컨트롤의 크기를 조정 합니다.

## <a name="selectively-disable-snaplines"></a>맞춤선을 선택적으로 사용 하지 않도록 설정

1. <xref:System.Windows.Forms.TableLayoutPanel> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

2. <xref:System.Windows.Forms.Button> 도구 상자 **에서**컨트롤 아이콘을 두 번 클릭합니다. 새 단추 컨트롤이 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤의 첫 번째 셀에 나타납니다.

3. **도구 상자** 에서 두 <xref:System.Windows.Forms.Button> 번 클릭 하 여 컨트롤 아이콘을 두 번 클릭 합니다. 이렇게 하면 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤에 빈 셀이 하나 남아 있습니다.

4. <xref:System.Windows.Forms.Button> **도구 상자** 에서 컨트롤의 <xref:System.Windows.Forms.TableLayoutPanel> 빈 셀로 컨트롤을 끌어 옵니다. 맞춤선이 나타나지 않습니다.

5. 컨트롤을 컨트롤 외부로 <xref:System.Windows.Forms.TableLayoutPanel> 끌고 컨트롤 주위로 <xref:System.Windows.Forms.TableLayoutPanel> 이동 합니다. <xref:System.Windows.Forms.Button> 맞춤선이 다시 표시 됩니다.

## <a name="disable-snaplines"></a>맞춤선 사용 안 함

컨트롤을 폼 주위로 이동 하는 동안 **alt** 키를 누릅니다.

맞춤선이 나타나지 않으며 컨트롤이 잠재적 맞춤 위치에 맞추지 않습니다.

### <a name="to-disable-snaplines-in-the-design-environment"></a>디자인 환경에서 맞춤선을 사용 하지 않도록 설정 하려면

1. **도구** 메뉴에서 **옵션** 대화 상자를 엽니다. **Windows Forms 디자이너**를 선택 합니다.

2. **일반** 노드를 선택 합니다. **레이아웃 모드** 섹션에서 선택 영역을 **맞춤선** 에서 **SnapToGrid**로 변경 합니다.

3. **확인** 을 선택 하 여 설정을 적용 합니다.

4. 폼에서 컨트롤을 선택 하 고 다른 컨트롤 주위로 이동 합니다. 맞춤선은 표시 되지 않습니다.

## <a name="next-steps"></a>다음 단계

맞춤선은 폼에서 컨트롤을 정렬 하는 직관적인 방법을 제공 합니다. 다음과 같은 사항을 더 살펴보는 것이 좋습니다.

- <xref:System.Windows.Forms.GroupBox> 다른<xref:System.Windows.Forms.GroupBox> 컨트롤 내에 컨트롤을 중첩 해 보세요. 자식 <xref:System.Windows.Forms.GroupBox> <xref:System.Windows.Forms.Button> 컨트롤내에컨트롤을추가하고부모컨트롤내에다른컨트롤을추가합니다.<xref:System.Windows.Forms.GroupBox> 컨트롤을 <xref:System.Windows.Forms.Button> 이동 하 여 맞춤선이 컨테이너 경계를 교차 하는 방식을 확인 합니다.

- <xref:System.Windows.Forms.TextBox> 컨트롤의 열과 컨트롤의 <xref:System.Windows.Forms.Label> 해당 열을 만듭니다. <xref:System.Windows.Forms.Label> `true`컨트롤의 속성값을로설정합니다.<xref:System.Windows.Forms.Control.AutoSize%2A> 표시 된 텍스트를 <xref:System.Windows.Forms.Label> <xref:System.Windows.Forms.TextBox> 컨트롤의 텍스트와 맞추도록 맞춤선을 사용 하 여 컨트롤을 이동 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Design.Behavior.SnapLine>
- [연습: FlowLayoutPanel를 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)
- [연습: TableLayoutPanel를 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)
- [연습: 안쪽 여백, 여백 및 AutoSize 속성을 사용 하 여 Windows Forms 컨트롤 레이아웃](windows-forms-controls-padding-autosize.md)
