---
title: '연습: 디자이너를 사용하여 ListView 및 TreeView 컨트롤에서 탐색기 스타일 인터페이스 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Explorer-style applications [Windows Forms], walkthroughs
- TreeView control [Windows Forms], ListView controls used with
- ListView control [Windows Forms], TreeView controls used with
- Explorer-style applications
- TreeView control [Windows Forms], using for explorer-style interface
- ListView control [Windows Forms], explorer style interface
- ListView control [Windows Forms], explorer-style interface
ms.assetid: 9e5e7721-19e2-4890-b273-a43589fe99ff
ms.openlocfilehash: d80f8e3bc729689b274af520bc37fda8417b0407
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "69658576"
---
# <a name="walkthrough-creating-an-explorer-style-interface-with-the-listview-and-treeview-controls-using-the-designer"></a>연습: 디자이너를 사용하여 ListView 및 TreeView 컨트롤에서 탐색기 스타일 인터페이스 만들기

Visual Studio의 이점 중 하나는 짧은 시간 내에 전문적인 Windows Forms 응용 프로그램을 만드는 기능입니다. 일반적인 시나리오는 및 <xref:System.Windows.Forms.ListView> <xref:System.Windows.Forms.TreeView> 컨트롤을 사용 하 여 windows 운영 체제의 windows 탐색기 기능과 유사한 UI (사용자 인터페이스)를 만드는 것입니다. Windows 탐색기는 사용자의 컴퓨터에 있는 파일 및 폴더의 계층 구조를 표시 합니다.

### <a name="to-create-the-form-containing-a-listview-and-treeview-control"></a>ListView 및 TreeView 컨트롤이 포함 된 폼을 만들려면

1. **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다.

2. **새 프로젝트** 대화 상자에서 다음을 수행 합니다.

    1. 범주에서 **Visual Basic** 또는 **시각적 개체 C#** 중 하나를 선택 합니다.

    2. 템플릿 목록에서 **Windows Forms 응용 프로그램**을 선택 합니다.

3. **확인**을 클릭합니다. 새 Windows Forms 프로젝트가 생성 됩니다.

4. 폼에 <xref:System.Windows.Forms.SplitContainer> 컨트롤을 추가 하 고 해당 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 속성을로 <xref:System.Windows.Forms.DockStyle.Fill>설정 합니다.

5. <xref:System.Windows.Forms.ImageList> 이라는`imageList1` 를 폼에 추가 하 고 속성 창를 사용 하 여 폴더 이미지와 문서 이미지 등 두 개의 이미지를 순서 대로 추가 합니다.

6. 이라는 컨트롤 <xref:System.Windows.Forms.TreeView> 을 폼 `treeview1` 에 추가 하 고 <xref:System.Windows.Forms.SplitContainer> 컨트롤의 왼쪽에 위치를 지정 합니다. 속성 창에서 다음을 `treeView1` 수행 합니다.

    1. <xref:System.Windows.Forms.Control.Dock%2A> 속성을 <xref:System.Windows.Forms.DockStyle.Fill>으로 설정합니다.

    2. <xref:System.Windows.Forms.TreeView.ImageList%2A> 속성을 `imagelist1.`로 설정합니다.

7. <xref:System.Windows.Forms.SplitContainer> 이라는 <xref:System.Windows.Forms.ListView> 컨트롤을폼에추가하고컨트롤의오른쪽에배치합니다.`listView1` 속성 창에서 다음을 `listview1` 수행 합니다.

    1. <xref:System.Windows.Forms.Control.Dock%2A> 속성을 <xref:System.Windows.Forms.DockStyle.Fill>으로 설정합니다.

    2. <xref:System.Windows.Forms.ListView.View%2A> 속성을 <xref:System.Windows.Forms.View.Details>으로 설정합니다.

    3. 속성에서![](./media/visual-studio-ellipsis-button.png)줄임표 (Visual Studio 속성 창의 줄임표 단추 (...)를 클릭 하 여 ColumnHeader 컬렉션 편집기를**엽니다.** <xref:System.Windows.Forms.ListView.Columns%2A> 세 개의 열을 추가 하 <xref:System.Windows.Forms.ColumnHeader.Text%2A> 고 속성 `Name`을 `Type`각각, `Last Modified`및로 설정 합니다. **확인** 을 클릭하여 대화 상자를 닫습니다.

    4. <xref:System.Windows.Forms.ListView.SmallImageList%2A> 속성을 `imageList1.`로 설정합니다.

8. 노드 및 하위 노드로를 <xref:System.Windows.Forms.TreeView> 채우는 코드를 구현 합니다. 이 코드를 `Form1` 클래스에 추가 합니다.

     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#1)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#1)]

9. 이전 코드는 System.IO 네임 스페이스를 사용 하므로 폼의 맨 위에 적절 한 using 또는 import 문을 추가 합니다.

     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#4)]

10. 폼의 생성자 또는 <xref:System.Windows.Forms.Form.Load> 이벤트 처리 메서드의 이전 단계에서 설정 메서드를 호출 합니다. 이 코드를 폼 생성자에 추가 합니다.

     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#2)]

11. `treeview1` `listview1` 에 대 <xref:System.Windows.Forms.TreeView.NodeMouseClick> 한 이벤트를 처리 하 고 노드를 클릭할 때 노드 내용으로 채울 코드를 구현 합니다. 이 코드를 `Form1` 클래스에 추가 합니다.

     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#3)]

     를 사용 하 C#는 경우 이벤트 처리 방법과 연결 된 <xref:System.Windows.Forms.TreeView.NodeMouseClick> 이벤트가 있는지 확인 합니다. 이 코드를 폼 생성자에 추가 합니다.

     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#5)]

## <a name="testing-the-application"></a>애플리케이션 테스트

이제 폼을 테스트 하 여 예상 대로 동작 하는지 확인할 수 있습니다.

#### <a name="to-test-the-form"></a>폼을 테스트 하려면

- F5 키를 눌러 애플리케이션을 실행합니다.

     왼쪽에 프로젝트 디렉터리를 표시 하는 <xref:System.Windows.Forms.TreeView> 컨트롤을 포함 하는 분할 폼 <xref:System.Windows.Forms.ListView> 과 오른쪽에 세 개의 열이 있는 컨트롤이 표시 됩니다. 디렉터리 노드를 선택 <xref:System.Windows.Forms.TreeView> 하 여를 트래버스할 수 <xref:System.Windows.Forms.ListView> 있으며,은 선택한 디렉터리의 콘텐츠로 채워집니다.

## <a name="next-steps"></a>다음 단계

이 응용 프로그램은를 사용 <xref:System.Windows.Forms.TreeView> 하 고 <xref:System.Windows.Forms.ListView> 제어할 수 있는 방법의 예를 제공 합니다. 이러한 컨트롤에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [방법: TreeView 또는 ListView 컨트롤에 사용자 지정 정보 추가 (Windows Forms)](add-custom-information-to-a-treeview-or-listview-control-wf.md)

- [방법: ListView 컨트롤에 검색 기능 추가](how-to-add-search-capabilities-to-a-listview-control.md)

- [방법: TreeView 노드에 바로 가기 메뉴 연결](how-to-attach-a-shortcut-menu-to-a-treeview-node.md)

## <a name="see-also"></a>참고 항목

- <xref:System.Windows.Forms.ListView>
- <xref:System.Windows.Forms.TreeView>
- [ListView 컨트롤](listview-control-windows-forms.md)
- [방법: Windows Forms TreeView 컨트롤을 사용 하 여 노드 추가 및 제거](how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)
- [방법: Windows Forms ListView 컨트롤을 사용 하 여 항목 추가 및 제거](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
- [방법: Windows Forms ListView 컨트롤에 열 추가](how-to-add-columns-to-the-windows-forms-listview-control.md)
