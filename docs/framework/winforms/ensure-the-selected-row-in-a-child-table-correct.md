---
title: '방법: 자식 테이블에서 선택된 행이 올바른 위치에 유지되도록 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- master-details view
- row position [Windows Forms]
- parent/child view [Windows Forms]
- resetting child position
- data binding [.NET Framework], row selection
- caching [.NET Framework], child position
- child position
- master/details view [Windows Forms]
- child tables row selection
- current child position
ms.assetid: c5fa2562-43a4-46fa-a604-52d8526a87bd
ms.openlocfilehash: 1047958a5600d8e6ee0ba461305e09395151ab14
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592276"
---
# <a name="how-to-ensure-the-selected-row-in-a-child-table-remains-at-the-correct-position"></a>방법: 자식 테이블에서 선택된 행이 올바른 위치에 유지되도록 설정
Windows Forms에서 데이터 바인딩을 사용할 때 부모/자식 또는 마스터/세부 정보 뷰에 데이터를 표시하는 경우가 많습니다. 이는 동일한 소스의 데이터가 두 컨트롤에 표시되는 데이터 바인딩 시나리오를 가리킵니다. 한 컨트롤에서 선택 항목을 변경하면 두 번째 컨트롤에 표시되는 데이터가 변경됩니다. 예를 들어 첫 번째 컨트롤에는 고객 목록이 포함되고 두 번째 컨트롤에는 첫 번째 컨트롤에서 선택한 고객과 관련된 주문 목록이 포함될 수 있습니다.  
  
 .NET Framework 버전 2.0부터 부모/자식 뷰에 데이터를 표시하는 경우 자식 테이블에서 현재 선택된 행이 테이블의 첫 번째 행으로 다시 설정되지 않도록 추가 단계를 수행해야 할 수도 있습니다. 이 작업을 수행하려면 자식 테이블 위치를 캐시하고 부모 테이블이 변경된 후 다시 설정해야 합니다. 일반적으로 자식 다시 설정은 부모 테이블의 행에 있는 필드가 처음 변경될 때 발생합니다.  
  
### <a name="to-cache-the-current-child-position"></a>현재 자식 위치를 캐시하려면  
  
1. 정수 변수를 선언하여 자식 목록 위치를 저장하고, 부울 변수를 선언하여 자식 위치를 캐시할지 여부를 저장합니다.  
  
     [!code-csharp[System.Windows.Forms.CurrencyManagerReset#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.CurrencyManagerReset#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#4)]  
  
2. 바인딩의 <xref:System.Windows.Forms.CurrencyManager>에 대한 <xref:System.Windows.Forms.CurrencyManager.ListChanged> 이벤트를 처리하고 <xref:System.ComponentModel.ListChangedType.Reset>의 <xref:System.ComponentModel.ListChangedType>을 확인합니다.  
  
3. <xref:System.Windows.Forms.CurrencyManager>의 현재 위치를 확인합니다. 목록의 첫 번째 항목(일반적으로 0)보다 크면 변수에 저장합니다.  
  
     [!code-csharp[System.Windows.Forms.CurrencyManagerReset#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.CurrencyManagerReset#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#2)]  
  
4. 부모 통화 관리자에 대한 부모 목록의 <xref:System.Windows.Forms.BindingManagerBase.CurrentChanged> 이벤트를 처리합니다. 처리기에서 캐싱 시나리오가 아님을 나타내는 부울 값을 설정합니다. <xref:System.Windows.Forms.BindingManagerBase.CurrentChanged>가 발생하는 경우 부모에 대한 변경 내용은 항목 값 변경이 아니라 목록 위치 변경입니다.  
  
     [!code-csharp[System.Windows.Forms.CurrencyManagerReset#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.CurrencyManagerReset#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#5)]  
  
### <a name="to-reset-the-child-position"></a>자식 위치를 다시 설정하려면  
  
1. 자식 바인딩의 <xref:System.Windows.Forms.CurrencyManager>에 대한 <xref:System.Windows.Forms.BindingManagerBase.PositionChanged> 이벤트를 처리합니다.  
  
2. 자식 테이블 위치를 이전 절차에서 저장된 캐시된 위치로 다시 설정합니다.  
  
     [!code-csharp[System.Windows.Forms.CurrencyManagerReset#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.CurrencyManagerReset#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#3)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Forms.CurrencyManager>에서 자식 테이블의 현재 위치를 저장하고 부모 테이블에서 편집이 완료된 후 위치를 다시 설정하는 방법을 보여 줍니다. 이 예제에는 <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용하여 <xref:System.Data.DataSet>의 두 테이블에 바인딩된 두 개의 <xref:System.Windows.Forms.DataGridView> 컨트롤이 포함되어 있습니다. 두 테이블 간에 관계가 설정되고 <xref:System.Data.DataSet>에 관계가 추가됩니다. 자식 테이블의 위치는 데모용으로 초기에 세 번째 행으로 설정되어 있습니다.  
  
 [!code-csharp[System.Windows.Forms.CurrencyManagerReset#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.CurrencyManagerReset#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#1)]  
  
 코드 예제를 테스트하려면 다음 단계를 수행합니다.  
  
1. 예제를 실행합니다.  
  
2. **Cache and reset position** 확인란이 선택되었는지 확인합니다.  
  
3. **Clear parent field** 단추를 클릭하여 부모 테이블의 필드를 변경합니다. 자식 테이블에서 선택한 행은 변경되지 않습니다.  
  
4. 예제를 닫고 다시 실행합니다. 다시 설정 동작이 부모 행을 처음 변경할 때만 발생하기 때문에 이 작업을 수행해야 합니다.  
  
5. **Cache and reset position** 확인란을 선택 취소합니다.  
  
6. **Clear parent field** 단추를 클릭합니다. 자식 테이블에서 선택한 행이 첫 번째 행으로 변경됩니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System, System.Data, System.Drawing, System.Windows.Forms and System.XML 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- [방법: 여러 컨트롤을 확인 동일한 데이터 소스에 바인딩된 동기화 된 상태로 유지](multiple-controls-bound-to-data-source-synchronized.md)
- [BindingSource 구성 요소](./controls/bindingsource-component.md)
- [데이터 바인딩 및 Windows Forms](data-binding-and-windows-forms.md)
