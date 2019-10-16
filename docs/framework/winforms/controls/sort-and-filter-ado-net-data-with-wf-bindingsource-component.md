---
title: '방법: Windows Forms BindingSource 구성 요소를 사용하여 ADO.NET 데이터 정렬 및 필터링'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sorting data
- data sorting [Windows Forms], ADO.NET
- data [Windows Forms], filtering
- BindingSource component [Windows Forms], sorting and filtering data
- filtering [Windows Forms], ADO.NET
- data [Windows Forms], sorting
- ADO.NET [Windows Forms]
ms.assetid: 6c206daf-d706-4602-9dbe-435343052063
ms.openlocfilehash: ae331ca9e3fd2aed654659e11434454874eff8fa
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960424"
---
# <a name="how-to-sort-and-filter-adonet-data-with-the-windows-forms-bindingsource-component"></a>방법: Windows Forms BindingSource 구성 요소를 사용하여 ADO.NET 데이터 정렬 및 필터링
<xref:System.Windows.Forms.BindingSource.Sort%2A> <xref:System.Windows.Forms.BindingSource> 및<xref:System.Windows.Forms.BindingSource.Filter%2A> 속성을 통해 제어의 정렬 및 필터링 기능을 노출할 수 있습니다. 기본 데이터 원본이 <xref:System.ComponentModel.IBindingList>인 경우 간단한 정렬을 적용할 수 있으며, 데이터 원본이 <xref:System.ComponentModel.IBindingListView>인 경우 필터링 및 고급 정렬을 적용할 수 있습니다. 속성 <xref:System.Windows.Forms.BindingSource.Sort%2A> 에는 표준 ADO.NET 구문이 필요 합니다. 데이터 원본 `ASC` 에 있는 데이터 열의 이름을 나타내는 문자열 이거나 `DESC` , 오름차순 이나 내림차순으로 정렬 해야 하는지 여부를 나타내는 문자열입니다. 쉼표 구분 기호를 사용 하 여 각 열을 구분 하 여 고급 정렬 또는 다중 열 정렬을 설정할 수 있습니다. 속성 <xref:System.Windows.Forms.BindingSource.Filter%2A> 은 문자열 식을 사용 합니다.  
  
> [!NOTE]
> 암호와 같은 중요한 정보를 연결 문자열 내에 저장하면 애플리케이션 보안 문제가 발생할 수 있습니다. 데이터베이스 액세스를 제어할 경우에는 통합 보안이라고도 하는 Windows 인증을 사용하는 방법이 더 안전합니다. 자세한 내용은 [연결 정보 보호](../../data/adonet/protecting-connection-information.md)를 참조하세요.  
  
### <a name="to-filter-data-with-the-bindingsource"></a>BindingSource를 사용 하 여 데이터를 필터링 하려면  
  
- <xref:System.Windows.Forms.BindingSource.Filter%2A> 속성을 원하는 식으로 설정 합니다.  
  
     다음 코드 예제에서 식은 열 이름 뒤에 열에 대해 원하는 값을 입력 합니다.  
  
 [!code-csharp[System.Windows.Forms.DataConnectorFilterAndSort#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/CS/form1.cs#11)]
 [!code-vb[System.Windows.Forms.DataConnectorFilterAndSort#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/VB/form1.vb#11)]  
  
### <a name="to-sort-data-with-the-bindingsource"></a>BindingSource를 사용 하 여 데이터를 정렬 하려면  
  
1. 속성을 뒤에 표시 되는 열 이름으로 설정 `DESC` 하거나오름차순이나내림차순으로설정합니다.`ASC` <xref:System.Windows.Forms.BindingSource.Sort%2A>  
  
2. 여러 열을 쉼표로 구분 합니다.  
  
 [!code-csharp[System.Windows.Forms.DataConnectorFilterAndSort#12](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/CS/form1.cs#12)]
 [!code-vb[System.Windows.Forms.DataConnectorFilterAndSort#12](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/VB/form1.vb#12)]  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 Northwind 샘플 데이터베이스 <xref:System.Windows.Forms.DataGridView> 의 Customers 테이블에서 컨트롤로 데이터를 로드 하 고 표시 된 데이터를 필터링 및 정렬 합니다.  
  
 [!code-csharp[System.Windows.Forms.DataConnectorFilterAndSort#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.DataConnectorFilterAndSort#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/VB/form1.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제를 실행 <xref:System.Windows.Forms.BindingSource> 하려면 라는 `BindingSource1` 와 <xref:System.Windows.Forms.DataGridView> `dataGridView1`라는를 포함 하는 폼에 코드를 붙여넣습니다. 폼에 <xref:System.Windows.Forms.Form.Load> 대 한 이벤트를 처리 하 `InitializeSortedFilteredBindingSource` 고 load 이벤트 처리기 메서드에서를 호출 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.BindingSource.Sort%2A>
- <xref:System.Windows.Forms.BindingSource.Filter%2A>
- [방법: 예제 데이터베이스 설치](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/8b6y4c7s(v=vs.120))
- [BindingSource 구성 요소](bindingsource-component.md)
