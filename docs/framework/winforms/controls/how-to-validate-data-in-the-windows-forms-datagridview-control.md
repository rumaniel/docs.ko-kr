---
title: '방법: Windows Forms DataGridView 컨트롤에서 데이터 유효성 검사'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data [Windows Forms], validation
- DataGridView control [Windows Forms], data validation
- data grids [Windows Forms], validating data
- data validation [Windows Forms], Windows Forms
ms.assetid: d10aef35-701e-4a3c-a684-2a2ed1aeaca6
ms.openlocfilehash: 12fd668e22703271f8c629baf56487dd084cfd8b
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591040"
---
# <a name="how-to-validate-data-in-the-windows-forms-datagridview-control"></a>방법: Windows Forms DataGridView 컨트롤에서 데이터 유효성 검사
다음 코드 예제에서는 사용자가 <xref:System.Windows.Forms.DataGridView> 컨트롤에 입력한 데이터의 유효성을 검사하는 방법을 보여 줍니다. 이 예제에서 <xref:System.Windows.Forms.DataGridView>는 Northwind 샘플 데이터베이스, `Customers` 테이블의 행으로 채워집니다. 사용자가 `CompanyName` 열에서 셀을 편집하면 셀이 비어 있지 않은지 검사함으로써 해당 값의 유효성이 테스트됩니다. <xref:System.Windows.Forms.DataGridView.CellValidating> 이벤트의 이벤트 처리기가 값이 빈 문자열인 것으로 확인하면 <xref:System.Windows.Forms.DataGridView>는 비어 있지 않은 문자열이 입력될 때까지 사용자가 셀을 종료하지 못하도록 합니다.  
  
 에 대 한 전체 설명은이 코드 예제를 참조 하세요. [연습: Forms DataGridView 컨트롤을 Windows의 데이터 유효성 검사](walkthrough-validating-data-in-the-windows-forms-datagridview-control.md)합니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#00](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewDataValidation#00](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#00)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System, System.Data, System.Windows.Forms 및 System.XML 어셈블리에 대한 참조  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 암호와 같은 중요한 정보를 연결 문자열 내에 저장하면 애플리케이션 보안 문제가 발생할 수 있습니다. 데이터베이스 액세스를 제어할 경우에는 통합 보안이라고도 하는 Windows 인증을 사용하는 방법이 더 안전합니다. 자세한 내용은 [연결 정보 보호](../../data/adonet/protecting-connection-information.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.BindingSource>
- [연습: Windows Forms DataGridView 컨트롤의 데이터 유효성 검사](walkthrough-validating-data-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 데이터 입력](data-entry-in-the-windows-forms-datagridview-control.md)
- [연습: Windows Forms DataGridView 컨트롤에서 데이터 입력 중에 발생 하는 오류 처리](handling-errors-that-occur-during-data-entry-in-the-datagrid.md)
- [연결 정보 보호](../../data/adonet/protecting-connection-information.md)
