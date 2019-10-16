---
title: '방법: 디자이너를 사용하여 Windows Forms ListView 컨트롤에 열 추가'
ms.date: 03/30/2017
helpviewer_keywords:
- ListView control [Windows Forms], adding column headers
- columns [Windows Forms], adding to ListView controls
ms.assetid: 5b1a8b4d-587e-479a-95c1-f9b90884f13a
ms.openlocfilehash: 10963fcb6d87ed74f73ecf4f1831a56eae5a392d
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69658453"
---
# <a name="how-to-add-columns-to-the-windows-forms-listview-control-using-the-designer"></a>방법: 디자이너를 사용하여 Windows Forms ListView 컨트롤에 열 추가

Windows Forms <xref:System.Windows.Forms.ListView> 컨트롤은 **자세히** 보기에서 각 목록 항목에 대해 여러 열을 표시할 수 있습니다. 열을 사용 하 여 각 목록 항목에 대 한 여러 유형의 정보를 표시할 수 있습니다. 예를 들어 파일 목록에 파일 이름, 파일 형식, 크기 및 파일을 마지막으로 수정한 날짜를 표시할 수 있습니다. 열을 만든 [후 해당 열을 채우는 방법에 대 한 자세한 내용은 방법: Windows Forms ListView 컨트롤](how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)을 사용 하 여 열에 하위 항목을 표시 합니다.

다음 절차에는 <xref:System.Windows.Forms.ListView> 컨트롤을 포함 하는 폼을 포함 하는 **Windows 응용 프로그램** 프로젝트가 필요 합니다. 이러한 프로젝트 [를 설정 하는 방법에 대 한 자세한 내용은 방법: Windows Forms 응용 프로그램 프로젝트](/visualstudio/ide/step-1-create-a-windows-forms-application-project) [를 만들고 방법: Windows Forms](how-to-add-controls-to-windows-forms.md)에 컨트롤을 추가 합니다.

### <a name="to-add-columns-in-the-designer"></a>디자이너에서 열을 추가 하려면

1. **속성** 창에서 컨트롤의 <xref:System.Windows.Forms.ListView.View%2A> 속성을로 <xref:System.Windows.Forms.View.Details>설정 합니다.

2. 속성 창 에서 ![ <xref:System.Windows.Forms.ListView.Columns%2A> 속성 옆에 있는 줄임표 단추 (Visual Studio](./media/visual-studio-ellipsis-button.png)속성 창의 줄임표 단추 (...)를 클릭 합니다.

     **ColumnHeader 컬렉션 편집기** 가 나타납니다.

3. **추가** 단추를 사용 하 여 새 열을 추가 합니다. 그런 다음 열 머리글을 선택 하 고 해당 텍스트 (열의 캡션), 텍스트 맞춤 및 너비를 설정할 수 있습니다.

## <a name="see-also"></a>참고자료

- [ListView 컨트롤 개요](listview-control-overview-windows-forms.md)
- [방법: Windows Forms ListView 컨트롤을 사용 하 여 항목 추가 및 제거](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
- [방법: Windows Forms ListView 컨트롤을 사용 하 여 열에 하위 항목 표시](how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)
- [방법: Windows Forms ListView 컨트롤의 아이콘 표시](how-to-display-icons-for-the-windows-forms-listview-control.md)
- [방법: TreeView 또는 ListView 컨트롤에 사용자 지정 정보 추가 (Windows Forms)](add-custom-information-to-a-treeview-or-listview-control-wf.md)
