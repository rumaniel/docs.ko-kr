---
title: '방법: 디자이너를 사용하여 Windows Forms DataGridView 컨트롤에서 열 추가 및 제거'
ms.date: 03/30/2017
f1_keywords:
- vs.DataGridViewAddColumnDialog
helpviewer_keywords:
- DataGridView control [Windows Forms], adding columns
- DataGridView control [Windows Forms], removing columns
ms.assetid: 9e709f35-0a8c-4e7e-b4c4-bacb7a834077
ms.openlocfilehash: 7a3029192ab0da4a954dfd7d3d258a00b154924e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69957107"
---
# <a name="how-to-add-and-remove-columns-in-the-windows-forms-datagridview-control-using-the-designer"></a>방법: 디자이너를 사용하여 Windows Forms DataGridView 컨트롤에서 열 추가 및 제거
Windows Forms <xref:System.Windows.Forms.DataGridView> 컨트롤은 데이터를 표시 하기 위해 열을 포함 해야 합니다. 컨트롤을 수동으로 채울 계획인 경우 열을 직접 추가 해야 합니다. 또는 데이터 소스에 컨트롤을 바인딩할 수 있습니다. 그러면 열이 자동으로 생성 되 고 채워집니다. 데이터 원본에 표시 하려는 열 보다 많은 열이 포함 된 경우 원하지 않는 열을 제거할 수 있습니다.

 다음 절차에는 <xref:System.Windows.Forms.DataGridView> 컨트롤을 포함 하는 폼을 포함 하는 **Windows 응용 프로그램** 프로젝트가 필요 합니다. 이러한 프로젝트 [를 설정 하는 방법에 대 한 자세한 내용은 방법: Windows Forms 응용 프로그램 프로젝트](/visualstudio/ide/step-1-create-a-windows-forms-application-project) [를 만들고 방법: Windows Forms](how-to-add-controls-to-windows-forms.md)에 컨트롤을 추가 합니다.

## <a name="to-add-a-column-using-the-designer"></a>디자이너를 사용 하 여 열을 추가 하려면

1. <xref:System.Windows.Forms.DataGridView> 컨트롤의 오른쪽 위 모퉁이에 있는 스마트 태그 문자 모양 (![스마트 태그 문자 모양](./media/vs-winformsmttagglyph.gif "VS_WinFormSmtTagGlyph"))을 클릭 한 다음 **열 추가**를 선택 합니다.

2. **열 추가** 대화 상자에서 데이터 **바인딩 열** 옵션을 선택 하 고 데이터 원본에서 열을 선택 하거나 **바인딩되지 않은 열** 옵션을 선택 하 고 제공 된 필드를 사용 하 여 열을 정의 합니다.

3. **추가** 단추를 클릭 하 여 열을 추가 하면 기존 열이 컨트롤 표시 영역을 아직 채우지 않은 경우 디자이너에 표시 됩니다.

    > [!NOTE]
    > 컨트롤의 스마트 태그를 사용 하 여 액세스할 수 있는 **열 편집** 대화 상자에서 열 속성을 수정할 수 있습니다.

## <a name="to-remove-a-column-using-the-designer"></a>디자이너를 사용 하 여 열을 제거 하려면

1. 컨트롤의 스마트 태그에서 **열 편집** 을 선택 합니다.

2. **선택한 열** 목록에서 열을 선택 합니다.

3. **제거** 단추를 클릭 하 여 열을 삭제 하면 디자이너에서 해당 열이 사라집니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- [방법: Windows Forms 애플리케이션 프로젝트 만들기](/visualstudio/ide/step-1-create-a-windows-forms-application-project)
- [방법: Windows Forms에 컨트롤 추가](how-to-add-controls-to-windows-forms.md)
