---
title: '방법: 디자이너를 사용하여 Windows Forms DataGridView 컨트롤에서 열 숨기기'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, columns
- columns [Windows Forms], hiding
- DataGridView control [Windows Forms], column hiding
- data [Windows Forms], displaying
ms.assetid: a81c38e6-2527-426a-bcb1-be691403be04
ms.openlocfilehash: 35aa1cdeef919d4267cb27da79f183c4c52aefa2
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916389"
---
# <a name="how-to-hide-columns-in-the-windows-forms-datagridview-control-using-the-designer"></a>방법: 디자이너를 사용하여 Windows Forms DataGridView 컨트롤에서 열 숨기기
Windows Forms <xref:System.Windows.Forms.DataGridView> 컨트롤에서 사용할 수 있는 열 중 일부만 표시하려는 경우도 있습니다. 예를 들어 관리 자격 증명이 있는 사용자에 게 직원 급여 열을 표시 하 고 다른 사용자는 숨길 수 있습니다. 또는 많은 열을 포함 하는 데이터 소스에 컨트롤을 바인딩할 수 있습니다. 이러한 열 중 일부만 표시 하려는 경우가 있습니다. 이 경우 일반적으로 표시 되지 않는 열은 숨기는 대신 제거 합니다. 자세한 내용은 [방법: 디자이너](add-and-remove-columns-in-the-datagrid-using-the-designer.md)를 사용 하 여 Windows Forms DataGridView 컨트롤에서 열을 추가 및 제거 합니다.

 다음 절차에는 <xref:System.Windows.Forms.DataGridView> 컨트롤을 포함 하는 폼을 포함 하는 **Windows 응용 프로그램** 프로젝트가 필요 합니다. 이러한 프로젝트 [를 설정 하는 방법에 대 한 자세한 내용은 방법: Windows Forms 응용 프로그램 프로젝트](/visualstudio/ide/step-1-create-a-windows-forms-application-project) [를 만들고 방법: Windows Forms](how-to-add-controls-to-windows-forms.md)에 컨트롤을 추가 합니다.

## <a name="to-hide-a-column-using-the-designer"></a>디자이너를 사용 하 여 열을 숨기려면

1. <xref:System.Windows.Forms.DataGridView> 컨트롤의 오른쪽 위 모퉁이에 있는 스마트 태그 문자 모양 (![스마트 태그 문자 모양](./media/vs-winformsmttagglyph.gif "VS_WinFormSmtTagGlyph"))을 클릭 한 다음 **열 편집**을 선택 합니다.

2. **선택한 열** 목록에서 열을 선택 합니다.

3. **열 속성** 표에서 <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A> 속성을로 `false`설정 합니다.

    > [!NOTE]
    > 열 **추가** 대화 상자에서 **표시** 확인란의 선택을 취소 하 여 열을 추가할 때 열을 숨길 수도 있습니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A?displayProperty=nameWithType>
- [방법: 디자이너를 사용 하 여 Windows Forms DataGridView 컨트롤에서 열 추가 및 제거](add-and-remove-columns-in-the-datagrid-using-the-designer.md)
- [방법: Windows Forms 애플리케이션 프로젝트 만들기](/visualstudio/ide/step-1-create-a-windows-forms-application-project)
- [방법: Windows Forms에 컨트롤 추가](how-to-add-controls-to-windows-forms.md)
