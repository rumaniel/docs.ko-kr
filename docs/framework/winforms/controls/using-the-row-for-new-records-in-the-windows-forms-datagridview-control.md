---
title: Windows Forms DataGridView 컨트롤에서 새 레코드에 대한 행 사용
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], adding rows for new records
- rows [Windows Forms], new records
- DataGridView control [Windows Forms], data entry
ms.assetid: 6110f1ea-9794-442c-a98a-f104a1feeaf4
ms.openlocfilehash: b28a8a8fc2d75f80a14447008c850de63e4e04b3
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65882431"
---
# <a name="using-the-row-for-new-records-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤에서 새 레코드에 대한 행 사용
사용 하는 경우는 <xref:System.Windows.Forms.DataGridView> 응용 프로그램에서 데이터 편집을 위해 종종 하려는 사용자에 게 데이터 저장소에 새 데이터 행을 추가 하는 기능을 제공 합니다. <xref:System.Windows.Forms.DataGridView> 컨트롤은 항상 마지막 행으로 표시 된 새 레코드에 대 한 행을 제공 하 여이 기능을 지원 합니다. 행 헤더에 별표 (*) 기호로 표시 됩니다. 다음 섹션에서는 설명 하는 몇 가지 새 레코드에 대 한 행을 사용 하 여 프로그램 사용 하도록 설정 하는 것이 좋습니다.  
  
## <a name="displaying-the-row-for-new-records"></a>새 레코드에 대 한 행을 표시합니다.  
 사용 된 <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> 속성을 새 레코드에 대 한 행을 표시할지 여부를 나타냅니다. 이 속성의 기본값은 `true`입니다.  
  
 새 레코드의 행을 표시할 데이터 바인딩된 경우를 하는 경우는 <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> 컨트롤의 속성 및 <xref:System.ComponentModel.IBindingList.AllowNew%2A?displayProperty=nameWithType> 데이터 원본 속성은 모두 `true`합니다. 중 하나에 해당 하는 경우 `false` 다음 행에 표시 되지 것입니다.  
  
## <a name="populating-the-row-for-new-records-with-default-data"></a>기본 데이터를 사용 하 여 새 레코드에 대 한 행을 채우는  
 사용자가 현재 행으로 새 레코드에 대 한 행을 선택 합니다 <xref:System.Windows.Forms.DataGridView> 를 발생 시킵니다는 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded> 이벤트입니다.  
  
 이 이벤트는 새에 대 한 액세스를 제공 <xref:System.Windows.Forms.DataGridViewRow> 기본 데이터를 사용 하 여 새 행을 채울 수 있습니다. 자세한 내용은 [방법: Windows Forms DataGridView 컨트롤에서 새 행에 기본값을 지정 합니다.](specify-default-values-for-new-rows-in-the-datagrid.md)  
  
## <a name="the-rows-collection"></a>행 컬렉션  
 새 레코드에 대 한 행에 포함 된 <xref:System.Windows.Forms.DataGridView> 컨트롤의 <xref:System.Windows.Forms.DataGridView.Rows%2A> 컬렉션 두 가지 측면에서 다르게 하지만 동작:  
  
- 새 레코드에 대 한 행을 제거할 수 없습니다는 <xref:System.Windows.Forms.DataGridView.Rows%2A> 컬렉션 프로그래밍 방식으로 합니다. <xref:System.InvalidOperationException> 이 시도 하는 경우 throw 됩니다. 또한 사용자 새 레코드에 대 한 행을 삭제할 수 없습니다. 합니다 <xref:System.Windows.Forms.DataGridViewRowCollection.Clear%2A?displayProperty=nameWithType> 메서드를이 행을 제거 하지 않습니다는 <xref:System.Windows.Forms.DataGridView.Rows%2A> 컬렉션입니다.  
  
- 새 레코드의 행을 한 후 행을 추가할 수 있습니다. <xref:System.InvalidOperationException> 이 시도 하는 경우 발생 합니다. 결과적으로, 새 레코드에 대 한 행은 항상 마지막 행에는 <xref:System.Windows.Forms.DataGridView> 제어 합니다. 메서드에 <xref:System.Windows.Forms.DataGridViewRowCollection> 행을 추가 하는-<xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A>를 <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopy%2A>, 및 <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopies%2A>-모든 메서드를 호출 삽입 내부적으로 새 레코드에 대 한 행이 있는 경우.  
  
## <a name="visual-customization-of-the-row-for-new-records"></a>새 레코드에 대 한 행의 시각적 사용자 지정  
 새 레코드에 대 한 행 만들어질 때 지정 된 행에 기반을 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A> 속성입니다. 이 행에 대해 지정 되지 않은 모든 셀 스타일은 다른 속성에서 상속 됩니다. 셀 스타일 상속에 대 한 자세한 내용은 참조 하세요. [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)합니다.  
  
 각 셀에서 새 레코드를 검색에 대 한 행의 셀에서 표시 되는 초기 값 <xref:System.Windows.Forms.DataGridViewCell.DefaultNewRowValue%2A> 속성입니다. 셀 형식에 대 한 <xref:System.Windows.Forms.DataGridViewImageCell>,이 속성에는 자리 표시자 이미지를 반환 합니다. 그렇지 않은 경우 `null`을 반환합니다. 사용자 지정 값을 반환 하도록이 속성을 재정의할 수 있습니다. 하지만 이러한 초기 값으로 바꿀 수 있습니다는 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded> 새 레코드에 대 한 행으로 포커스가 이벤트 처리기입니다.  
  
 화살표 또는 별표는이 행의이 헤더에 대 한 표준 아이콘 공개적으로 노출 되지 않습니다. 사용자 지정 만들기 해야 아이콘을 사용자 지정 하려는 경우 <xref:System.Windows.Forms.DataGridViewRowHeaderCell> 클래스입니다.  
  
 표준 아이콘을 사용 하 여는 <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> 의 속성을 <xref:System.Windows.Forms.DataGridViewCellStyle> 행 머리글 셀을 사용 합니다. 완전히 표시할 수 있는 공간이 없는 경우에 표준 아이콘 렌더링 되지 않습니다.  
  
 행 머리글 셀에 설정 하는 문자열 값 및 텍스트와 아이콘에 대 한 충분 한 공간이 없는 경우 아이콘을 먼저 삭제 됩니다.  
  
## <a name="sorting"></a>정렬  
 바인딩되지 않은 모드에서 새 레코드는 항상 추가할의 끝에는 <xref:System.Windows.Forms.DataGridView> 사용자의 콘텐츠를 정렬 하는 경우에는 <xref:System.Windows.Forms.DataGridView>합니다. 사용자를 올바른 위치에 행을 정렬 하기 위해 정렬을 다시 적용 해야 합니다. 이 동작은 비슷합니다는 <xref:System.Windows.Forms.ListView> 제어 합니다.  
  
 데이터 정렬을 적용 될 때 삽입 동작 경계와 가상 모드 데이터 모델의 구현에 종속 됩니다. ADO.NET에 대 한 행을 즉시 올바른 위치에 정렬 됩니다.  
  
## <a name="other-notes-on-the-row-for-new-records"></a>새 레코드에 대 한 행의 기타 참고 사항  
 설정할 수 없습니다는 <xref:System.Windows.Forms.DataGridViewRow.Visible%2A> 속성을이 행의 `false`합니다. <xref:System.InvalidOperationException> 이 시도 하는 경우 발생 합니다.  
  
 새 레코드의 행을 선택 하지 않은 상태에서 항상 만들어집니다.  
  
## <a name="virtual-mode"></a>가상 모드  
 가상 모드 구현 하는 경우에 행의 추가 롤백할 시점 및 데이터 모델에 새 레코드에 대 한 행을 필요로 하는 시기를 추적 해야 합니다. 이 기능은 구현에 따라 달라 집니다 데이터 모델 및 해당 트랜잭션 의미 체계를 구현 예를 들어, 셀 또는 행 수준에서 커밋 범위 인지 합니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤에서 가상 모드](virtual-mode-in-the-windows-forms-datagridview-control.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded?displayProperty=nameWithType>
- [Windows Forms DataGridView 컨트롤의 데이터 입력](data-entry-in-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤에서 새 행에 기본값을 지정 합니다.](specify-default-values-for-new-rows-in-the-datagrid.md)
