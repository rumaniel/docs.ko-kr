---
title: '방법: Windows Forms DataGridView 행에 바인딩된 개체 액세스'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- object binding [Windows Forms], accessing bound objects
- data grids [Windows Forms], accessing bound objects
- DataGridView control [Windows Forms], accessing objects bound to rows
ms.assetid: 0e05748f-4403-4eb8-8b2f-b098108181b5
ms.openlocfilehash: 244047f27b0eb109aba599bd26881046eb538163
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65582617"
---
# <a name="how-to-access-objects-bound-to-windows-forms-datagridview-rows"></a>방법: Windows Forms DataGridView 행에 바인딩된 개체 액세스
때로는 비즈니스 개체 컬렉션에 저장된 정보 테이블을 표시하는 것이 유용합니다. <xref:System.Windows.Forms.DataGridView> 컨트롤을 이러한 컬렉션에 바인딩하면 속성이 <xref:System.ComponentModel.BrowsableAttribute>를 통해 검색 불가능으로 표시되지 않은 경우 각 공용 속성이 해당 열에 표시됩니다. 예를 들어 `Customer` 개체 컬렉션에는 **이름** 및 **주소**와 같은 열이 있습니다.  
  
 이러한 개체에 포함된 추가 정보 및 코드에 액세스하려는 경우 행 개체를 통해 접근할 수 있습니다. 다음 코드 예제에서는 사용자가 여러 행을 선택하고 단추를 클릭하여 각 해당 고객에게 송장을 보낼 수 있습니다.  
  
### <a name="to-access-row-bound-objects"></a>행 바인딩된 개체에 액세스하려면  
  
- <xref:System.Windows.Forms.DataGridViewRow.DataBoundItem%2A?displayProperty=nameWithType> 속성을 사용합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewObjectBinding#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/CS/datagridviewobjectbinding.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewObjectBinding#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/VB/datagridviewobjectbinding.vb#10)]  
  
## <a name="example"></a>예제  
 전체 코드 예제는 간단한 `Customer` 구현을 포함하며, 몇 개의 `Customer` 개체가 포함된 <xref:System.Collections.ArrayList>에 <xref:System.Windows.Forms.DataGridView>를 바인딩합니다. <xref:System.Windows.Forms.Form.Load?displayProperty=nameWithType> 이벤트 처리기 외부에서는 고객 컬렉션에 액세스할 수 없기 때문에 <xref:System.Windows.Forms.Button?displayProperty=nameWithType>의 <xref:System.Windows.Forms.Control.Click> 이벤트 처리기는 행을 통해 `Customer` 개체에 액세스해야 합니다.  
  
 [!code-csharp[System.Windows.Forms.DataGridViewObjectBinding#00](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/CS/datagridviewobjectbinding.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewObjectBinding#00](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/VB/datagridviewobjectbinding.vb#00)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System 및 System.Windows.Forms 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewRow>
- <xref:System.Windows.Forms.DataGridViewRow.DataBoundItem%2A?displayProperty=nameWithType>
- [Windows Forms DataGridView 컨트롤에서 데이터 표시](displaying-data-in-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤에 개체 바인딩](how-to-bind-objects-to-windows-forms-datagridview-controls.md)
