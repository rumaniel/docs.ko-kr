---
title: '방법: 디자이너를 사용하여 Windows Forms ListView 컨트롤에서 항목 그룹화'
ms.date: 03/30/2017
helpviewer_keywords:
- ListView control [Windows Forms], grouping items
- grouping
- groups [Windows Forms], in Windows Forms controls
ms.assetid: 8b615000-69d9-4c64-acaf-b54fa09b69e3
ms.openlocfilehash: b63bcd9e5e357db350cc2987e09af84eb58bdcff
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "69039407"
---
# <a name="how-to-group-items-in-a-windows-forms-listview-control-using-the-designer"></a>방법: 디자이너를 사용하여 Windows Forms ListView 컨트롤에서 항목 그룹화

<xref:System.Windows.Forms.ListView> 컨트롤의 그룹화 기능을 사용 하면 관련 항목 집합을 그룹으로 표시할 수 있습니다. 이러한 그룹은 그룹 제목이 포함 된 가로 그룹 헤더로 화면에 구분 됩니다. 그룹을 사용 <xref:System.Windows.Forms.ListView> 하 여 항목을 사전순으로, 날짜별로 또는 다른 논리적 그룹화로 그룹화 하 여 많은 목록을 보다 쉽게 탐색할 수 있습니다. 다음 이미지는 몇 가지 그룹화 된 항목을 보여 줍니다.

![짝수와 짝수 그룹으로 구분 된 숫자입니다.](./media/how-to-group-items-in-a-windows-forms-listview-control-using-the-designer/odd-even-list-view-groups.gif)

다음 절차에는 <xref:System.Windows.Forms.ListView> 컨트롤을 포함 하는 폼을 포함 하는 **Windows 응용 프로그램** 프로젝트가 필요 합니다. 이러한 프로젝트 [를 설정 하는 방법에 대 한 자세한 내용은 방법: Windows Forms 응용 프로그램 프로젝트](/visualstudio/ide/step-1-create-a-windows-forms-application-project) [를 만들고 방법: Windows Forms](how-to-add-controls-to-windows-forms.md)에 컨트롤을 추가 합니다.

그룹화를 사용 하려면 먼저 디자이너에서 또는 프로그래밍 방식으로 <xref:System.Windows.Forms.ListViewGroup> 하나 이상의 개체를 만들어야 합니다. 그룹을 정의한 후에는 해당 그룹에 항목을 할당할 수 있습니다.

> [!NOTE]
> <xref:System.Windows.Forms.ListView>응용 프로그램에서 메서드를 [!INCLUDE[WinXpFamily](../../../../includes/winxpfamily-md.md)] <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=nameWithType> 호출 하는 경우에만 그룹을 사용할 수 있습니다. 이전 버전의 운영 체제 그룹 관련 모든 코드가 미치지 않으며 그룹 표시 되지 않습니다. 자세한 내용은 <xref:System.Windows.Forms.ListView.Groups%2A?displayProperty=nameWithType>을 참조하세요.

## <a name="to-add-or-remove-groups-in-the-designer"></a>디자이너에서 그룹을 추가 하거나 제거 하려면

1. **속성 창에서** <xref:System.Windows.Forms.ListView.Groups%2A> 속성 옆에 있는 **줄임표** 단추![(...)를 클릭 하 여 속성 옆의 Visual Studio](./media/visual-studio-ellipsis-button.png)속성 창에서 줄임표 단추 (...)를 클릭 합니다.

     **ListViewGroup 컬렉션 편집기** 가 나타납니다.

2. 그룹을 추가 하려면 **추가** 단추를 클릭 합니다. 그런 다음 새 그룹의 속성 (예: <xref:System.Windows.Forms.ListViewGroup.Header%2A> 및 <xref:System.Windows.Forms.ListViewGroup.HeaderAlignment%2A> 속성)을 설정할 수 있습니다. 그룹을 제거 하려면 그룹을 선택 하 고 **제거** 단추를 클릭 합니다.

## <a name="to-assign-items-to-groups-in-the-designer"></a>디자이너에서 그룹에 항목을 할당 하려면

1. **속성 창에서** <xref:System.Windows.Forms.ListView.Items%2A> 속성 옆에 있는 **줄임표** 단추![(...)를 클릭 하 여 속성 옆의 Visual Studio](./media/visual-studio-ellipsis-button.png)속성 창에서 줄임표 단추 (...)를 클릭 합니다.

     **ListViewItem 컬렉션 편집기** 가 나타납니다.

2. 새 항목을 추가 하려면 **추가** 단추를 클릭 합니다. 그런 다음 <xref:System.Windows.Forms.ListViewItem.Text%2A> 및 <xref:System.Windows.Forms.ListViewItem.ImageIndex%2A> 속성과 같은 새 항목의 속성을 설정할 수 있습니다.

3. <xref:System.Windows.Forms.ListViewItem.Group%2A> 속성을 선택 하 고 드롭다운 목록에서 그룹을 선택 합니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Windows.Forms.ListView>
- <xref:System.Windows.Forms.ListView.Groups%2A>
- <xref:System.Windows.Forms.ListViewGroup>
- [ListView 컨트롤](listview-control-windows-forms.md)
- [ListView 컨트롤 개요](listview-control-overview-windows-forms.md)
- [방법: Windows Forms ListView 컨트롤을 사용 하 여 항목 추가 및 제거](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
