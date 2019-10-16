---
title: '방법: 디자이너를 사용하여 Windows Forms DataGridView 컨트롤에서 열 다시 정렬 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], column order
- Windows Forms, columns
- columns [Windows Forms], reordering
- data [Windows Forms], displaying
ms.assetid: d82bd69c-6799-4439-a32c-91139c5901d1
ms.openlocfilehash: 3864ce70f058259b597df904311bd4a48218b151
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040342"
---
# <a name="how-to-enable-column-reordering-in-the-windows-forms-datagridview-control-using-the-designer"></a>방법: 디자이너를 사용하여 Windows Forms DataGridView 컨트롤에서 열 다시 정렬 사용
Windows Forms <xref:System.Windows.Forms.DataGridView> 컨트롤에 표시 되는 데이터를 볼 때 사용자는 특정 열의 값을 비교 하려는 경우가 있습니다. 이는 열이 컨트롤에서 광범위 하 게 분리 된 경우에 불편할 수 있습니다. 특히 사용자가 관심 있는 모든 열을 표시 하기 위해 앞뒤로 가로 방향으로 스크롤해야 하는 경우에는 불편할 수 있습니다. 사용자가 열을 다시 정렬할 수 있도록 하 여 열 값을 보다 쉽게 비교 하는 태스크를 수행할 수 있습니다. 열 다시 정렬을 사용 하도록 설정 하면 사용자가 열 머리글을 마우스로 끌어 열을 새 위치로 이동할 수 있습니다.

 다음 절차에는 <xref:System.Windows.Forms.DataGridView> 컨트롤을 포함 하는 폼을 포함 하는 **Windows 응용 프로그램** 프로젝트가 필요 합니다. 이러한 프로젝트 [를 설정 하는 방법에 대 한 자세한 내용은 방법: Windows Forms 응용 프로그램 프로젝트](/visualstudio/ide/step-1-create-a-windows-forms-application-project) [를 만들고 방법: Windows Forms](how-to-add-controls-to-windows-forms.md)에 컨트롤을 추가 합니다.

## <a name="to-enable-column-reordering"></a>열 다시 정렬을 사용 하도록 설정 하려면

- <xref:System.Windows.Forms.DataGridView> 컨트롤의 오른쪽 위 모퉁이에 있는 스마트 태그 문자 모양 (![스마트 태그 문자 모양](./media/vs-winformsmttagglyph.gif "VS_WinFormSmtTagGlyph"))을 클릭 한 다음 열 다시 **정렬 사용**을 선택 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.AllowUserToOrderColumns%2A?displayProperty=nameWithType>
- [방법: 디자이너를 사용 하 여 Windows Forms DataGridView 컨트롤의 열 고정](freeze-columns-in-the-datagrid-using-the-designer.md)
- [방법: Windows Forms 애플리케이션 프로젝트 만들기](/visualstudio/ide/step-1-create-a-windows-forms-application-project)
- [방법: Windows Forms에 컨트롤 추가](how-to-add-controls-to-windows-forms.md)
