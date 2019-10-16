---
title: '방법: TableLayoutPanel 컨트롤에서 열 및 행 편집'
ms.date: 03/30/2017
f1_keywords:
- net.ComponentModel.StyleCollectionEditor
helpviewer_keywords:
- columns [Windows Forms], editing
- TableLayoutPanel control [Windows Forms], editing
- rows [Windows Forms], editing
ms.assetid: c367ed43-40dc-49eb-9e0f-ba70e83dfec0
ms.openlocfilehash: 99ff3286592da0a097835b8f35d687475ca54fb0
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040289"
---
# <a name="how-to-edit-columns-and-rows-in-a-tablelayoutpanel-control"></a>방법: TableLayoutPanel 컨트롤에서 열 및 행 편집

<xref:System.Windows.Forms.TableLayoutPanel> **열 및 행 스타일** 대화 상자 라는 컨트롤의 컬렉션 편집기를 사용 하 여 컨트롤의 행과 열을 편집할 수 있습니다.

> [!NOTE]
> 컨트롤이 여러 행 또는 열에 걸쳐 있도록 하려면 컨트롤에서 `RowSpan` 및 `ColumnSpan` 속성을 설정 합니다. 자세한 내용은 [연습: TableLayoutPanel](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)를 사용 하 여 Windows Forms에 컨트롤 정렬
>
> 셀 내에 컨트롤을 맞추려면이 고, 컨트롤이 셀 내에서 스트레치 되도록 하려면 컨트롤의 <xref:System.Windows.Forms.Control.Anchor%2A> 속성을 사용 합니다. 자세한 내용은 [연습: TableLayoutPanel](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)를 사용 하 여 Windows Forms에 컨트롤 정렬

## <a name="to-edit-rows-and-columns"></a>행 및 열을 편집 하려면

1. <xref:System.Windows.Forms.TableLayoutPanel> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

2. ![](./media/vs-winformsmttagglyph.gif "") 컨트롤의 스마트 태그 문자 모양 (스마트 태그 문자 모양 VS_WinFormSmtTagGlyph)을 클릭 하 고 행 및 열 편집을 선택 하 여 열 및 행 스타일 대화 상자를 엽니다. <xref:System.Windows.Forms.TableLayoutPanel> <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤을 마우스 오른쪽 단추로 클릭 하 고 바로 가기 메뉴에서 **행 및 열 편집** 을 선택할 수도 있습니다.

3. 열을 추가 하거나 제거 하려면 **멤버 유형** 드롭다운 목록 상자에서 **열** 을 선택 합니다.

4. 행을 추가 하거나 제거 하려면 **멤버 유형** 드롭다운 목록 상자에서 **행** 을 선택 합니다.

5. **멤버** 목록의 끝에 행 또는 열을 추가 하려면 **추가** 단추를 클릭 합니다.

6. **삽입** 단추를 클릭 하 여 목록에서 현재 선택한 항목 앞에 행 또는 열을 추가 합니다.

7. 행 또는 열을 추가 하는 경우 새 행 또는 열의 **크기 유형을** 선택 합니다. 자세한 내용은 <xref:System.Windows.Forms.SizeType>을 참조하세요.

8. 행 또는 열을 제거 하려면 **제거** 단추를 클릭 하 여 **멤버** 목록에서 현재 선택한 항목을 삭제 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.SizeType>
- [TableLayoutPanel 컨트롤](tablelayoutpanel-control-windows-forms.md)
