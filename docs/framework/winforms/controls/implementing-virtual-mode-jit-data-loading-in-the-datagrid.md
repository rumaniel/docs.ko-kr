---
title: Windows Forms DataGridView 컨트롤에서 Just-In-Time 데이터 로드를 사용하여 가상 모드 구현
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- examples [Windows Forms], just-in-time data loading
- data [Windows Forms], managing large data sets
- DataGridView control [Windows Forms], virtual mode
- just-in-time data loading
- DataGridView control [Windows Forms], large data sets
- virtual mode [Windows Forms], just-in-time data loading
ms.assetid: c2a052b9-423c-4ff7-91dc-d8c7c79345f6
ms.openlocfilehash: fa40f1657a433f5f4ade3de25648ca04c37dfa67
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962597"
---
# <a name="implementing-virtual-mode-with-just-in-time-data-loading-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤에서 Just-In-Time 데이터 로드를 사용하여 가상 모드 구현
<xref:System.Windows.Forms.DataGridView> 컨트롤에서 가상 모드를 구현 하는 한 가지 이유는 필요한 경우에만 데이터를 검색 하는 것입니다. 이를 *just-in-time 데이터 로드*라고 합니다.  
  
 예를 들어 원격 데이터베이스에서 매우 큰 테이블로 작업 하는 경우 사용자가 새 행을 뷰로 스크롤하면 추가 데이터를 표시 하 고 검색 하는 데 필요한 데이터만 검색 하 여 시작 지연을 방지할 수 있습니다. 응용 프로그램을 실행 하는 클라이언트 컴퓨터에 데이터를 저장 하는 데 사용할 수 있는 제한 된 양의 메모리가 있는 경우 데이터베이스에서 새 값을 검색할 때 사용 하지 않는 데이터를 삭제할 수도 있습니다.  
  
 다음 섹션에서는 just-in-time 캐시에서 컨트롤을 <xref:System.Windows.Forms.DataGridView> 사용 하는 방법을 설명 합니다.  
  
 이 항목의 코드를 단일 목록으로 복사하려면 [방법: Windows Forms DataGridView 컨트롤](virtual-mode-with-just-in-time-data-loading-in-the-datagrid.md)에서 just-in-time 데이터 로드를 사용 하 여 가상 모드를 구현 합니다.  
  
## <a name="the-form"></a>양식  
 다음 코드 예제에서는 이벤트 처리기를 <xref:System.Windows.Forms.DataGridView> <xref:System.Windows.Forms.DataGridView.CellValueNeeded> 통해 `Cache` 개체와 상호 작용 하는 읽기 전용 컨트롤이 포함 된 폼을 정의 합니다. 개체 `Cache` 는 로컬로 저장 된 값을 관리 하 고 `DataRetriever` 개체를 사용 하 여 sample Northwind 데이터베이스의 Orders 테이블에서 값을 검색 합니다. 클래스에 필요한 `IDataPageRetriever` `DataRetriever` 인터페이스를구현하는개체도컨트롤행과열을초기화하는데사용됩니다.<xref:System.Windows.Forms.DataGridView> `Cache`  
  
 `IDataPageRetriever`, 및형식`Cache` 에 대해서는이 항목의 뒷부분에서 설명 합니다. `DataRetriever`  
  
> [!NOTE]
> 암호와 같은 중요한 정보를 연결 문자열 내에 저장하면 애플리케이션 보안 문제가 발생할 수 있습니다. 데이터베이스 액세스를 제어할 경우에는 통합 보안이라고도 하는 Windows 인증을 사용하는 방법이 더 안전합니다. 자세한 내용은 [연결 정보 보호](../../data/adonet/protecting-connection-information.md)를 참조하세요.  
  
 [!code-csharp[System.Windows.Forms.DataGridView.Virtual_lazyloading#100](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/CS/lazyloading.cs#100)]
 [!code-vb[System.Windows.Forms.DataGridView.Virtual_lazyloading#100](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/VB/lazyloading.vb#100)]  
  
## <a name="the-idatapageretriever-interface"></a>IDataPageRetriever 인터페이스  
 다음 코드 예제에서는 `IDataPageRetriever` `DataRetriever` 클래스에 의해 구현 되는 인터페이스를 정의 합니다. 이 인터페이스 `SupplyPageOfData` 에 선언 된 유일한 메서드는 초기 행 인덱스 및 단일 데이터 페이지의 행 수를 필요로 하는 메서드입니다. 이러한 값은 구현자에서 데이터 원본에 있는 데이터의 하위 집합을 검색 하는 데 사용 됩니다.  
  
 개체 `Cache` 는 생성 중에이 인터페이스의 구현을 사용 하 여 두 초기 데이터 페이지를 로드 합니다. 캐시 되지 않은 값이 필요할 때마다 캐시는 이러한 페이지 중 하나를 삭제 하 고의 값 `IDataPageRetriever`을 포함 하는 새 페이지를 요청 합니다.  
  
 [!code-csharp[System.Windows.Forms.DataGridView.Virtual_lazyloading#201](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/CS/lazyloading.cs#201)]
 [!code-vb[System.Windows.Forms.DataGridView.Virtual_lazyloading#201](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/VB/lazyloading.vb#201)]  
  
## <a name="the-dataretriever-class"></a>DataRetriever 클래스  
 다음 코드 예제에서는 `DataRetriever` `IDataPageRetriever` 인터페이스를 구현 하 여 서버에서 데이터 페이지를 검색 하는 클래스를 정의 합니다. `Columns` <xref:System.Windows.Forms.DataGridView> 또한 클래스는 및`RowCount` 속성을 제공 합니다 .이 속성은 컨트롤에서 필요한 열을 만들고 <xref:System.Windows.Forms.DataGridView.Rows%2A> 컬렉션에 적절 한 수의 빈 행을 추가 하는 데 사용 합니다. `DataRetriever` 컨트롤이 테이블의 모든 데이터를 포함 하는 것 처럼 동작 하 게 하려면 빈 행을 추가 해야 합니다. 즉, 스크롤 막대의 스크롤 상자에 적절 한 크기가 포함 되 고 사용자가 테이블의 모든 행에 액세스할 수 있습니다. 행은 뷰로 스크롤할 때만 <xref:System.Windows.Forms.DataGridView.CellValueNeeded> 이벤트 처리기에 의해 채워집니다.  
  
 [!code-csharp[System.Windows.Forms.DataGridView.Virtual_lazyloading#200](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/CS/lazyloading.cs#200)]
 [!code-vb[System.Windows.Forms.DataGridView.Virtual_lazyloading#200](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/VB/lazyloading.vb#200)]  
  
## <a name="the-cache-class"></a>Cache 클래스  
 다음 코드 예제에서는 `Cache` `IDataPageRetriever` 구현을 통해 채워진 두 페이지의 데이터를 관리 하는 클래스를 정의 합니다. 클래스 `Cache` 는 단일 캐시 페이지 `DataPage` 에 값을 저장 하 <xref:System.Data.DataTable> 고 페이지의 위쪽 및 아래쪽 경계를 나타내는 행 인덱스를 계산 하는을 포함 하는 내부 구조를 정의 합니다.  
  
 클래스 `Cache` 는 생성 시 두 개의 데이터 페이지를 로드 합니다. 이벤트가 값을 요청할 때마다 개체는 `Cache` 해당 값을 두 페이지 중 하나에서 사용할 수 있는지 여부를 확인 하 고, 그럴 경우 반환 합니다. <xref:System.Windows.Forms.DataGridView.CellValueNeeded> 값을 로컬로 사용할 수 없는 경우 개체는 `Cache` 현재 표시 된 행에서 가장 멀리 있는 두 페이지를 확인 하 고이 페이지를 요청 된 값을 포함 하는 새 항목으로 대체 합니다. 그러면이 페이지를 반환 합니다.  
  
 데이터 페이지의 행 수가 화면에 화면에 표시 될 수 있는 행 수와 동일 하다 고 가정할 경우이 모델을 사용 하면 사용자가 테이블을 페이징 하 여 가장 최근에 본 페이지로 효율적으로 돌아갈 수 있습니다.  
  
 [!code-csharp[System.Windows.Forms.DataGridView.Virtual_lazyloading#300](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/CS/lazyloading.cs#300)]
 [!code-vb[System.Windows.Forms.DataGridView.Virtual_lazyloading#300](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/VB/lazyloading.vb#300)]  
  
## <a name="additional-considerations"></a>추가 고려 사항  
 위의 코드 예제는 just-in-time 데이터 로드의 데모로 제공 됩니다. 효율성을 극대화 하기 위해 고유한 요구 사항에 맞게 코드를 수정 해야 합니다. 최소한 캐시에 있는 데이터 페이지당 행 수에 대 한 적절 한 값을 선택 해야 합니다. 이 값은 `Cache` 생성자에 전달 됩니다. 페이지당 행 수는 <xref:System.Windows.Forms.DataGridView> 컨트롤에 동시에 표시 될 수 있는 행 수보다 작아야 합니다.  
  
 최상의 결과를 위해서는 시스템 및 사용자의 요구 사항을 확인 하기 위해 성능 테스트 및 유용성 테스트를 수행 해야 합니다. 고려해 야 할 몇 가지 요소에는 응용 프로그램을 실행 하는 클라이언트 컴퓨터의 메모리 양, 사용 되는 네트워크 연결의 사용 가능한 대역폭, 사용 되는 서버 대기 시간 등이 포함 됩니다. 대역폭 및 대기 시간은 최대 사용량에 따라 결정 되어야 합니다.  
  
 응용 프로그램의 스크롤 성능을 향상 시키기 위해 로컬에 저장 된 데이터의 양을 늘릴 수 있습니다. 그러나 시작 시간을 개선 하기 위해 처음에 너무 많은 데이터를 로드 하는 것을 방지 해야 합니다. 클래스를 `Cache` 수정 하 여 저장할 수 있는 데이터 페이지 수를 늘릴 수 있습니다. 더 많은 데이터 페이지를 사용 하면 스크롤 효율성을 향상 시킬 수 있지만 사용 가능한 대역폭과 서버 대기 시간에 따라 데이터 페이지의 이상적인 행 수를 결정 해야 합니다. 페이지가 작을수록 서버는 더 자주 액세스 되지만 요청 된 데이터를 반환 하는 데 시간이 더 적게 소요 됩니다. 대기 시간이 대역폭 보다 더 많은 문제인 경우 더 큰 데이터 페이지를 사용 하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>
- [Windows Forms DataGridView 컨트롤의 성능 조정](performance-tuning-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 크기를 조정하는 최선의 방법](best-practices-for-scaling-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 가상 모드](virtual-mode-in-the-windows-forms-datagridview-control.md)
- [연습: Windows Forms DataGridView 컨트롤에서 가상 모드 구현](implementing-virtual-mode-wf-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤에서 Just-in-time 데이터 로드를 사용 하 여 가상 모드 구현](virtual-mode-with-just-in-time-data-loading-in-the-datagrid.md)
