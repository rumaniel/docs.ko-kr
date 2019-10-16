---
title: '연습: Windows Forms DataGridView 컨트롤에서 가상 모드 구현'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- data [Windows Forms], managing large data sets
- DataGridView control [Windows Forms], virtual mode
- virtual mode [Windows Forms], walkthroughs
- DataGridView control [Windows Forms], large data sets
- walkthroughs [Windows Forms], DataGridView control
ms.assetid: 74eb5276-5ab8-4ce0-8005-dae751d85f7c
ms.openlocfilehash: 9e7fb3a42b56c40f713d73e3734142f4aab335f4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64649990"
---
# <a name="walkthrough-implementing-virtual-mode-in-the-windows-forms-datagridview-control"></a>연습: Windows Forms DataGridView 컨트롤에서 가상 모드 구현
매우 많은 양의의 표 형식 데이터를 표시 하려는 경우는 <xref:System.Windows.Forms.DataGridView> 컨트롤을 설정할 수 있습니다 합니다 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 속성을 `true` 명시적으로 해당 데이터 저장소를 사용 하 여 컨트롤의 상호 작용을 관리 합니다. 이렇게 하면이 상황에서 컨트롤의 성능을 미세 조정할 수 있습니다.  
  
 <xref:System.Windows.Forms.DataGridView> 컨트롤 사용자 지정 데이터 저장소와 상호 작용을 처리할 수 있는 몇 가지 이벤트를 제공 합니다. 이 연습에서는 이러한 이벤트 처리기를 구현 하는 과정을 안내 합니다. 이 항목의 코드 예제에서는 이해를 돕기 위해 매우 간단한 데이터 소스를 사용합니다. 프로덕션 설정에서 일반적으로 로드 하려는 캐시에 표시 하 고 처리 해야 하는 행만 <xref:System.Windows.Forms.DataGridView> 캐시 업데이트와 상호 작용 하는 이벤트입니다. 자세한 내용은 참조 하세요. [Windows Forms DataGridView 컨트롤에서 Just-In-Time 데이터 로드 사용 하 여 가상 모드 구현](implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)  
  
 이 항목의 코드를 단일 목록으로 복사하려면 [방법: Windows에서 가상 모드 구현 Forms DataGridView 컨트롤](how-to-implement-virtual-mode-in-the-windows-forms-datagridview-control.md)합니다.  
  
## <a name="creating-the-form"></a>폼 만들기  
  
#### <a name="to-implement-virtual-mode"></a>가상 모드 구현  
  
1. 파생 되는 클래스를 만듭니다 <xref:System.Windows.Forms.Form> 개와 <xref:System.Windows.Forms.DataGridView> 제어 합니다.  
  
     다음 코드는 몇 가지 기본 초기화를 포함합니다. 이후 단계에서 사용할 몇 가지 변수 선언, 제공을 `Main` 메서드를 클래스 생성자에서 간단한 폼 레이아웃을 제공 합니다.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#001](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#001)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#001](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#001)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#001](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#001)]  
    [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#002](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#002)]
    [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#002](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#002)]
    [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#002](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#002)]  
  
2. 폼의 처리기를 구현 <xref:System.Windows.Forms.Form.Load> 초기화 하는 이벤트를 <xref:System.Windows.Forms.DataGridView> 제어 하 고 샘플 값을 사용 하 여 데이터 저장소를 채웁니다.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#110](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#110)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#110](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#110)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#110](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#110)]  
  
3. 에 대 한 처리기를 구현 합니다 <xref:System.Windows.Forms.DataGridView.CellValueNeeded> 데이터 저장소에서 요청된 된 셀 값을 검색 하는 이벤트 또는 `Customer` 편집에서 현재 개체입니다.  
  
     이 이벤트가 발생할 때마다는 <xref:System.Windows.Forms.DataGridView> 셀 그리기를 제어 해야 합니다.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#120](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#120)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#120](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#120)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#120](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#120)]  
  
4. 에 대 한 처리기를 구현 합니다 <xref:System.Windows.Forms.DataGridView.CellValuePushed> 에서 편집된 셀 값을 저장 하는 이벤트를 `Customer` 편집된 된 행을 나타내는 개체입니다. 이 이벤트는 사용자 커밋 셀 값이 변경 될 때마다 발생 합니다.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#130](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#130)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#130](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#130)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#130](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#130)]  
  
5. 에 대 한 처리기를 구현 합니다 <xref:System.Windows.Forms.DataGridView.NewRowNeeded> 새로 만든 이벤트 `Customer` 새로 만든된 행을 나타내는 개체입니다.  
  
     이 이벤트는 사용자가 새 레코드에 대 한 행을 입력할 때마다 발생 합니다.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#140](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#140)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#140](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#140)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#140](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#140)]  
  
6. 에 대 한 처리기를 구현 합니다 <xref:System.Windows.Forms.DataGridView.RowValidated> 데이터 저장소로 새롭거나 수정 된 행을 저장 하는 이벤트입니다.  
  
     이 이벤트는 사용자는 현재 행이 변경 될 때마다 발생 합니다.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#150](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#150)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#150](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#150)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#150](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#150)]  
  
7. 에 대 한 처리기를 구현 합니다 <xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded> 나타내는 이벤트 여부를 <xref:System.Windows.Forms.DataGridView.CancelRowEdit> 사용자 행의 편집 모드에 두 번 또는 한 번 편집 모드 외부 ESC 키를 눌러 신호를 보낼 때 이벤트가 발생 하는 합니다.  
  
     기본적으로 <xref:System.Windows.Forms.DataGridView.CancelRowEdit> 경우가 아니면 수정 된 현재 행에서 셀 있을 때 행의 버전을 변경 시 발생 합니다 <xref:System.Windows.Forms.QuestionEventArgs.Response%2A?displayProperty=nameWithType> 속성이로 설정 되어 `true` 에 <xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded> 이벤트 처리기. 이 이벤트는 커밋 범위 런타임 시 결정 되는 경우에 유용 합니다.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#160](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#160)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#160](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#160)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#160](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#160)]  
  
8. 에 대 한 처리기를 구현 합니다 <xref:System.Windows.Forms.DataGridView.CancelRowEdit> 의 값을 삭제 하는 이벤트를 `Customer` 현재 행을 나타내는 개체입니다.  
  
     이 이벤트는 사용자 행의 편집 모드에 두 번 또는 한 번 편집 모드 외부 ESC 키를 눌러 신호를 보낼 때 발생 합니다. 경우 또는 현재 행에서 셀을 수정한 경우이 이벤트가 발생 하지 않습니다 값을 <xref:System.Windows.Forms.QuestionEventArgs.Response%2A?displayProperty=nameWithType> 속성 설정한 `false` 에 <xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded> 이벤트 처리기입니다.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#170](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#170)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#170](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#170)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#170](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#170)]  
  
9. 처리기를 구현 합니다 <xref:System.Windows.Forms.DataGridView.UserDeletingRow> 기존를 삭제 하는 이벤트 `Customer` 데이터 저장소에서 개체는 저장 되지 않은 삭제 또는 `Customer` 새로 생성된 된 행을 나타내는 개체입니다.  
  
     이 이벤트는 사용자 행 머리글을 클릭 하 고 DELETE 키를 눌러 행을 삭제 될 때마다 발생 합니다.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#180](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#180)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#180](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#180)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#180](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#180)]  
  
10. 간단한 구현 `Customers` 이 코드 예제에서 사용 하는 데이터 항목을 나타내는 클래스입니다.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#200](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#200)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#200](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#200)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#200](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#200)]  
  
## <a name="testing-the-application"></a>애플리케이션 테스트  
 이제 예상 대로 작동 되도록 폼을 테스트할 수 있습니다.  
  
#### <a name="to-test-the-form"></a>폼을 테스트 하려면  
  
- 애플리케이션을 컴파일하고 실행합니다.  
  
     표시 됩니다는 <xref:System.Windows.Forms.DataGridView> 컨트롤 세 고객 레코드를 사용 하 여 채워집니다. 여러 행에 있는 셀의 값을 수정할 수 있으며 편집 모드에 두 번 및 한 번 전체 행을 원래 값으로 되돌리려면 편집 모드 외부 ESC 키를 누릅니다. 수정, 추가 또는 컨트롤에서 행을 삭제 하는 경우 `Customer` 데이터 저장소의 개체는 수정, 추가 또는 삭제 합니다.  
  
## <a name="next-steps"></a>다음 단계  
 이 응용 프로그램의 가상 모드 구현 하려면 처리 해야 하는 이벤트에 대 한 기본적인 이해를 제공 합니다 <xref:System.Windows.Forms.DataGridView> 제어 합니다. 다양 한 방법으로에서이 기본 응용 프로그램을 향상 시킬 수 있습니다.  
  
- 외부 데이터베이스에서 값을 캐시 하는 데이터 저장소를 구현 합니다. 캐시를 검색 하 고 클라이언트 컴퓨터에서 적은 양의 메모리를 사용 하는 동안 표시 하기 위해 필요한 것만 포함 되도록 필요에 따라 값을 삭제 해야 합니다.  
  
- 요구 사항에 따라 데이터 저장소의 성능을 미세 조정 합니다. 예를 들어, 다음 더 큰 캐시 크기를 사용 하 고 데이터베이스 쿼리의 수를 최소화 하 여 클라이언트 컴퓨터 메모리 제한 보다는 느린 네트워크 연결에 대 한 보정 하는 것이 좋습니다.  
  
 외부 데이터베이스에서 값을 캐시 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: Forms DataGridView 컨트롤의 Windows에서-Just-in-time 데이터 로드를 사용 하 여 가상 모드 구현](virtual-mode-with-just-in-time-data-loading-in-the-datagrid.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>
- <xref:System.Windows.Forms.DataGridView.CellValueNeeded>
- <xref:System.Windows.Forms.DataGridView.CellValuePushed>
- <xref:System.Windows.Forms.DataGridView.NewRowNeeded>
- <xref:System.Windows.Forms.DataGridView.RowValidated>
- <xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded>
- <xref:System.Windows.Forms.DataGridView.CancelRowEdit>
- <xref:System.Windows.Forms.DataGridView.UserDeletingRow>
- [Windows Forms DataGridView 컨트롤의 성능 조정](performance-tuning-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 크기를 조정하는 최선의 방법](best-practices-for-scaling-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤에서 Just-In-Time 데이터 로드를 사용하여 가상 모드 구현](implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)
- [방법: Windows Forms DataGridView 컨트롤에서 가상 모드 구현](how-to-implement-virtual-mode-in-the-windows-forms-datagridview-control.md)
