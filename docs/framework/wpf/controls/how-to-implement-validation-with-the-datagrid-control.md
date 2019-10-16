---
title: '방법: DataGrid 컨트롤을 사용하여 유효성 검사 구현'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGrid [WPF], validation
- validation [WPF], DataGrid
ms.assetid: ec6078a8-1e42-4648-b414-f4348e81bda1
ms.openlocfilehash: 8ae651b3085b39673a51cf8d5f65e9bfb9da87d7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962036"
---
# <a name="how-to-implement-validation-with-the-datagrid-control"></a>방법: DataGrid 컨트롤을 사용하여 유효성 검사 구현
<xref:System.Windows.Controls.DataGrid> 컨트롤을 사용 하면 셀 및 행 수준에서 유효성 검사를 수행할 수 있습니다. 셀 수준 유효성 검사를 사용 하 여 사용자는 값을 업데이트 하는 경우 바인딩된 데이터 개체의 개별 속성을 확인 합니다. 행 수준 유효성 검사를 사용 하 여 행에 변경 내용을 커밋할 때 전체 데이터 개체에 유효성 검사 합니다. 유효성 검사 오류에 대 한 사용자 지정 시각적 피드백을 제공 하거나 <xref:System.Windows.Controls.DataGrid> 컨트롤이 제공 하는 기본 시각적 피드백을 사용할 수도 있습니다.  
  
 다음 절차에서는 <xref:System.Windows.Controls.DataGrid> 바인딩에 유효성 검사 규칙을 적용 하 고 시각적 피드백을 사용자 지정 하는 방법을 설명 합니다.  
  
### <a name="to-validate-individual-cell-values"></a>개별 셀 값의 유효성을 검사 하려면  
  
- 열에 사용 되는 바인딩에 대해 하나 이상의 유효성 검사 규칙을 지정 합니다. 이는 [데이터 바인딩 개요](../data/data-binding-overview.md)에 설명 된 대로 간단한 컨트롤에서 데이터의 유효성을 검사 하는 것과 유사 합니다.  
  
     다음 예제에서는 비즈니스 개체 <xref:System.Windows.Controls.DataGrid> 의 다른 속성에 바인딩된 4 개의 열이 있는 컨트롤을 보여 줍니다. 열 중 세 개는 <xref:System.Windows.Controls.ExceptionValidationRule> <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> 속성을로 `true`설정 하 여를 지정 합니다.  
  
     [!code-xaml[DataGrid_Validation#BasicXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/window1.xaml#basicxaml)]  
  
     사용자가 잘못 된 값 (예: 강좌 ID 열에 정수가 아닌 값)을 입력 하면 셀 주위에 빨간색 테두리가 나타납니다. 다음 절차에 설명 된 대로이 기본 유효성 검사 피드백을 변경할 수 있습니다.  
  
### <a name="to-customize-cell-validation-feedback"></a>셀 유효성 검사 피드백을 사용자 지정 하려면  
  
- <xref:System.Windows.Controls.DataGridBoundColumn.EditingElementStyle%2A> 열의 속성을 열 편집 컨트롤에 적절 한 스타일로 설정 합니다. 편집 컨트롤은 런타임에 만들어지므로 간단한 컨트롤과 같이 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A?displayProperty=nameWithType> 연결 된 속성을 사용할 수 없습니다.  
  
     다음 예에서는 세 개의 열에서 유효성 검사 규칙을 사용 하 여 공유 하는 오류 스타일을 추가 하 여 이전 예제를 업데이트 합니다. 사용자가 잘못 된 값을 입력 하는 경우 스타일은 셀 배경색을 변경 하 고 도구 설명을 추가 합니다. 트리거를 사용 하 여 유효성 검사 오류가 있는지 여부를 확인 합니다. 이는 현재 셀에 대 한 전용 오류 템플릿이 없기 때문에 필요 합니다.  
  
     [!code-xaml[DataGrid_Validation#CellValidationXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#cellvalidationxaml)]  
  
     열에서 사용 하는을 대체 하 여 <xref:System.Windows.Controls.DataGridColumn.CellStyle%2A> 보다 광범위 한 사용자 지정을 구현할 수 있습니다.  
  
### <a name="to-validate-multiple-values-in-a-single-row"></a>단일 행에서 여러 값의 유효성을 검사 하려면  
  
1. 바인딩된 데이터 <xref:System.Windows.Controls.ValidationRule> 개체의 여러 속성을 확인 하는 서브 클래스를 구현 합니다. 메서드 구현에서 `value` 매개 변수 값 <xref:System.Windows.Data.BindingGroup> 을 인스턴스로 캐스팅 합니다. <xref:System.Windows.Controls.ValidationRule.Validate%2A> 그런 다음 속성을 <xref:System.Windows.Data.BindingGroup.Items%2A> 통해 데이터 개체에 액세스할 수 있습니다.  
  
     다음 예제에서는 `StartDate` `Course` 개체에 대 한 속성 값이 해당 `EndDate` 속성 값 보다 이전 인지 여부를 확인 하는이 프로세스를 보여 줍니다.  
  
     [!code-csharp[DataGrid_Validation#CourseValidationRule](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#coursevalidationrule)]
     [!code-vb[DataGrid_Validation#CourseValidationRule](~/samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#coursevalidationrule)]  
  
2. <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A?displayProperty=nameWithType> 컬렉션에 유효성 검사 규칙을 추가 합니다. 속성 <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A> 은 컨트롤에서 사용 하는 <xref:System.Windows.Data.BindingGroup.ValidationRules%2A> 모든 바인딩을 그룹화 <xref:System.Windows.Data.BindingGroup> 하는 인스턴스의 속성에 대 한 직접 액세스를 제공 합니다.  
  
     다음 예제에서는 <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A> XAML의 속성입니다. 합니다 <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> 속성이 <xref:System.Windows.Controls.ValidationStep.UpdatedValue> 바인딩된 데이터 개체를 업데이트 한 후에 유효성 검사가 수행 되도록 합니다.  
  
     [!code-xaml[DataGrid_Validation#RowValidationRulesXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationrulesxaml)]  
  
     사용자 종료 날짜는 시작 날짜 보다 이전 인지를 지정 하는 경우 빨간색 느낌표 (!) 행 머리글에 나타납니다. 다음 절차에 설명 된 대로이 기본 유효성 검사 피드백을 변경할 수 있습니다.  
  
### <a name="to-customize-row-validation-feedback"></a>행 유효성 검사 피드백을 사용자 지정 하려면  
  
- <xref:System.Windows.Controls.DataGrid.RowValidationErrorTemplate%2A?displayProperty=nameWithType> 속성을 설정합니다. 이 속성을 사용 하면 개별 <xref:System.Windows.Controls.DataGrid> 컨트롤에 대 한 행 유효성 검사 피드백을 사용자 지정할 수 있습니다. 또한 <xref:System.Windows.Controls.DataGridRow.ValidationErrorTemplate%2A?displayProperty=nameWithType> 속성을 설정 하기 위해 암시적 행 스타일을 사용 하 여 여러 컨트롤에 영향을 줄 수 있습니다.  
  
     다음 예제에서는 기본 행 유효성 검사 의견을 더 잘 보이도록 표시기를 바꿉니다. 사용자가 잘못 된 값을 입력 하는 경우 행 머리글에 흰색 느낌표가 있는 빨간색 원이 나타납니다. 이는 행 및 셀 유효성 검사 오류 모두에 대해 발생 합니다. 관련된 된 오류 메시지는 도구 설명에 표시 됩니다.  
  
     [!code-xaml[DataGrid_Validation#RowValidationFeedbackXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationfeedbackxaml)]  
  
## <a name="example"></a>예제  
 다음 예에서는 셀 및 행 유효성 검사에 대 한 전체 데모를 제공 합니다. 클래스 `Course` 는 트랜잭션을 지원 하기 위해를 구현 <xref:System.ComponentModel.IEditableObject> 하는 샘플 데이터 개체를 제공 합니다. 컨트롤 <xref:System.Windows.Controls.DataGrid> 은와 <xref:System.ComponentModel.IEditableObject> 상호 작용 하 여 사용자가 ESC 키를 눌러 변경 내용을 되돌릴 수 있도록 합니다.  
  
> [!NOTE]
> Visual Basic를 사용 하는 경우 mainwindow.xaml의 첫 번째 줄에서을로 `x:Class="DataGridValidation.MainWindow"` `x:Class="MainWindow"`바꿉니다.  
  
 유효성 검사를 테스트 하려면 다음을 시도 합니다.  
  
- 과정 ID 열에 정수가 아닌 값을 입력 합니다.  
  
- 종료 날짜 열에 시작 날짜 보다 이전인 날짜를 입력 합니다.  
  
- 강좌 ID, 시작 날짜 또는 종료 날짜에서 값을 삭제 합니다.  
  
- 잘못 된 셀 값을 실행 취소 하려면 커서를 다시 셀에 놓고 ESC 키를 누릅니다.  
  
- 현재 셀이 편집 모드에 있을 때 전체 행의 변경 내용을 실행 취소 하려면 ESC 키를 두 번 누릅니다.  
  
- 유효성 검사 오류가 발생 하면 행 머리글의 표시기 위로 마우스 포인터를 이동 하 여 관련 오류 메시지를 확인 합니다.  
  
 [!code-csharp[DataGrid_Validation#FullCode](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#fullcode)]
 [!code-vb[DataGrid_Validation#FullCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#fullcode)]  
  
 [!code-xaml[DataGrid_Validation#FullXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#fullxaml)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.DataGrid>
- [DataGrid](datagrid.md)
- [데이터 바인딩](../data/data-binding-wpf.md)
- [바인딩 유효성 검사 구현](../data/how-to-implement-binding-validation.md)
- [사용자 지정 개체의 유효성 검사 논리 구현](../data/how-to-implement-validation-logic-on-custom-objects.md)
