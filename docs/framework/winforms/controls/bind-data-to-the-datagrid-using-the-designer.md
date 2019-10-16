---
title: '방법: 디자이너를 사용하여 Windows Forms DataGridView 컨트롤에 데이터 바인딩'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms controls, binding to a data source
- data sources [Windows Forms], binding to Windows Forms controls
- DataGridView control [Windows Forms], data binding
ms.assetid: f4f46009-cec2-441b-8668-6b5af057558b
ms.openlocfilehash: 609878416be26786ce865168c996c78e18b1897f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917886"
---
# <a name="how-to-bind-data-to-the-windows-forms-datagridview-control-using-the-designer"></a>방법: 디자이너를 사용하여 Windows Forms DataGridView 컨트롤에 데이터 바인딩
디자이너를 사용 하 여 데이터베이스, 비즈니스 <xref:System.Windows.Forms.DataGridView> 개체 또는 웹 서비스를 비롯 한 다양 한 종류의 데이터 소스에 컨트롤을 연결할 수 있습니다. 디자이너를 사용 하 여 컨트롤을 데이터 소스에 바인딩하면 컨트롤이 데이터 소스를 나타내는 <xref:System.Windows.Forms.BindingSource> 구성 요소에 자동으로 바인딩됩니다. 또한 열은 데이터 소스에서 제공하는 스키마 정보와 일치하는 컨트롤에 자동으로 생성됩니다.

 열을 생성한 후에 사용자 요구에 맞게 수정할 수 있습니다. 예를 들어 표시하지 않아도 되는 열을 제거하거나 숨길 수 있습니다. 열을 다시 정렬하거나 열 형식을 수정할 수도 있습니다. 열을 수정하는 방법에 대한 자세한 내용은 [참고 항목] 섹션에 나열된 항목을 참조하세요.

 여러 <xref:System.Windows.Forms.DataGridView> 컨트롤을 관련 테이블에 바인딩하여 마스터/세부 관계를 만들 수도 있습니다. 이 구성에서 하나의 컨트롤은 부모 테이블을 표시하고 다른 컨트롤은 부모 테이블에 있는 현재 행에 관련된 자식 테이블의 해당 행만을 표시합니다. 자세한 내용은 [방법: Windows Forms 응용 프로그램](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/57tx3hhe(v=vs.120))에 관련 데이터를 표시 합니다.

 다음 절차를 수행 하려면 <xref:System.Windows.Forms.DataGridView> 컨트롤이 포함 된 양식이 있는 **Windows 응용 프로그램** 프로젝트 또는 마스터/세부 관계에 대 한 두 개의 컨트롤이 필요 합니다. 이러한 프로젝트 [를 시작 하는 방법에 대 한 자세한 내용은 방법: Windows Forms 응용 프로그램 프로젝트](/visualstudio/ide/step-1-create-a-windows-forms-application-project) [를 만들고 방법: Windows Forms](how-to-add-controls-to-windows-forms.md)에 컨트롤을 추가 합니다.

## <a name="to-bind-the-control-to-a-data-source"></a>데이터 소스에 컨트롤을 바인딩하려면

1. <xref:System.Windows.Forms.DataGridView> 컨트롤의 오른쪽 위 모퉁이에 있는 스마트 태그 문자 모양 (![스마트 태그 문자 모양](./media/vs-winformsmttagglyph.gif "VS_WinFormSmtTagGlyph"))을 클릭 합니다.

2. **데이터 소스 선택** 옵션에서 드롭다운 화살표를 클릭합니다.

3. 프로젝트에 데이터 소스가 아직 없는 경우 **프로젝트 데이터 소스 추가**를 클릭하고 마법사에 의해 표시된 단계를 따릅니다.

     자세한 내용은 [데이터 소스 구성 마법사](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/w4dd7z6t(v=vs.120))를 참조하세요. 새 데이터 소스은 **데이터 소스 선택** 드롭다운 창에 표시됩니다. 새 데이터 소스에 단일 데이터베이스 테이블과 같은 하나의 구성원만이 포함되는 경우 컨트롤은 해당 구성원에 자동으로 바인딩됩니다. 그렇지 않으면 다음 단계를 계속합니다.

4. **기타 데이터 소스** 및 **프로젝트 데이터 소스** 노드가 아직 확장되지 않은 경우 확장한 다음 컨트롤을 바인딩할 데이터 소스를 선택합니다.

5. 여러 테이블이 포함 된를 <xref:System.Data.DataSet?displayProperty=nameWithType> 만든 경우와 같이 데이터 원본에 둘 이상의 멤버가 포함 된 경우 데이터 원본을 확장 한 다음 바인딩할 특정 멤버를 선택 합니다.

6. 마스터/세부 관계를 만들려면 두 번째 <xref:System.Windows.Forms.DataGridView> 컨트롤에 대 한 **데이터 소스 선택** 드롭다운 창에서 부모 테이블에 대해 만든를 <xref:System.Windows.Forms.BindingSource> 확장 한 다음 표시 된 목록에서 관련 자식 테이블을 선택 합니다.

    > [!NOTE]
    > 프로젝트에 데이터 소스가 이미 있으면 **데이터 소스** 창을 사용하여 데이터 양식을 만들 수도 있습니다. 자세한 내용은 [데이터 소스 창](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/6ckyxa83(v=vs.120))을 참조하세요.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.BindingSource>
- <xref:System.Windows.Forms.DataGridView.DataMember%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.DataSource%2A?displayProperty=nameWithType>
- [방법: 데이터베이스의 데이터에 연결](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/fxk9yw1t(v=vs.120))
- [방법: 디자이너를 사용 하 여 Windows Forms DataGridView 컨트롤에서 열 추가 및 제거](add-and-remove-columns-in-the-datagrid-using-the-designer.md)
- [방법: 디자이너를 사용 하 여 Windows Forms DataGridView 컨트롤에서 열 순서 변경](change-the-order-of-columns-in-the-datagrid-using-the-designer.md)
- [방법: 디자이너를 사용 하 여 Windows Forms DataGridView 열의 형식 변경](change-the-type-of-a-wf-datagridview-column-using-the-designer.md)
- [방법: 디자이너를 사용 하 여 Windows Forms DataGridView 컨트롤의 열 고정](freeze-columns-in-the-datagrid-using-the-designer.md)
- [방법: 디자이너를 사용 하 여 Windows Forms DataGridView 컨트롤에서 열 숨기기](hide-columns-in-the-datagrid-using-the-designer.md)
- [방법: 디자이너를 사용 하 여 Windows Forms DataGridView 컨트롤에서 열을 읽기 전용으로 설정](make-columns-read-only-in-the-datagrid-using-the-designer.md)
- [방법: Windows Forms 애플리케이션 프로젝트 만들기](/visualstudio/ide/step-1-create-a-windows-forms-application-project)
- [방법: Windows Forms에 컨트롤 추가](how-to-add-controls-to-windows-forms.md)
- [데이터 소스 창](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/6ckyxa83(v=vs.120))
- [방법: Windows Forms 응용 프로그램에 관련 데이터 표시](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/57tx3hhe(v=vs.120))
