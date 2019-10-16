---
title: DataGridView 컨트롤 시나리오(Windows Forms)
ms.date: 03/30/2017
helpviewer_keywords:
- data [Windows Forms], displaying in tabular format
- data grids [Windows Forms], about data grids
- DataGridView control [Windows Forms], scenarios
ms.assetid: 09a5fd05-3447-47ec-a4ec-6082a2b7f0dd
ms.openlocfilehash: 7350b0da19650b99bcfd456f93e994492a56d7e3
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64648090"
---
# <a name="datagridview-control-scenarios-windows-forms"></a>DataGridView 컨트롤 시나리오(Windows Forms)
사용 하 여는 <xref:System.Windows.Forms.DataGridView> 컨트롤, 다양 한 데이터 원본에서에서 테이블 형식 데이터를 표시할 수 있습니다. 간단한 용도로 수동으로 채울 수 있습니다는 <xref:System.Windows.Forms.DataGridView> 제어를 통해 직접 데이터를 조작 합니다. 그러나 일반적으로 외부 데이터 원본에 데이터를 저장할을 통해 컨트롤을 바인딩하는 <xref:System.Windows.Forms.BindingSource> 구성 요소입니다.  
  
 이 항목에서는 관련 된 일반적인 시나리오 중 일부를 설명 합니다 <xref:System.Windows.Forms.DataGridView> 제어 합니다.  
  
## <a name="scenario-1-displaying-small-amounts-of-data"></a>시나리오 1: 적은 양의 데이터를 표시합니다.  
 에 표시할 외부 데이터 원본에 데이터를 저장할 필요가 없습니다를 <xref:System.Windows.Forms.DataGridView> 제어 합니다. 적은 양의 데이터를 사용 하 여 작업 하는 경우 컨트롤을 통해 데이터를 조작 하을 직접 컨트롤을 채울 수 있습니다. 이 이라고 *바인딩되지 않은 모드*합니다. 자세한 내용은 [방법: 바인딩되지 않은 Windows Forms DataGridView 컨트롤 만들기](how-to-create-an-unbound-windows-forms-datagridview-control.md)합니다.  
  
### <a name="scenario-key-points"></a>시나리오의 주요 요소  
  
- 바인딩되지 않은 모드로 채웁니다 컨트롤을 수동으로.  
  
- 바인딩되지 않은 모드는 읽기 전용 데이터의 양이 적은 경우에 특히 적합 합니다.  
  
- 바인딩되지 않은 모드는 스프레드시트 모양의 또는 부분적으로 채워진 테이블도 적합 합니다.  
  
## <a name="scenario-2-viewing-and-updating-data-stored-in-an-external-data-source"></a>시나리오 2: 외부 데이터 원본에 저장 된 데이터 보기 및 업데이트  
 사용할 수는 <xref:System.Windows.Forms.DataGridView> 데이터베이스 테이블 또는 비즈니스 개체의 컬렉션 같은 데이터 원본에 유지 하는 데이터에 액세스할 수 있는 사용자를 통해 사용자 인터페이스 (UI)으로 제어 합니다. 자세한 내용은 [방법: 바인딩 데이터는 Windows Forms DataGridView 컨트롤](how-to-bind-data-to-the-windows-forms-datagridview-control.md)합니다.  
  
### <a name="scenario-key-points"></a>시나리오의 주요 요소  
  
- 바인딩된 모드를 사용 하 여 데이터 원본에 연결, 데이터 원본 속성 또는 데이터베이스 열을 기반으로 하는 열을 자동으로 생성 및 컨트롤을 채울 수 있습니다.  
  
- 바인딩된 모드는 많은 사용자 데이터와 상호 작용에 대 한 적합 합니다. 표시 되는 데이터 형식을 지정할 수 및 사용자 지정 데이터를 데이터 소스에서 필요한 형식으로 구문 분석할 수 있습니다. 잘못 된 셀을 수정할 수 있습니다 하 고 사용자가 경고를 보낼 수 있도록 데이터베이스 제약 조건 오류 및 오류를 형식 지정 데이터 항목을 검색할 수 있습니다.  
  
- 열 정렬과 같은 추가 기능을 고정 및 다시에 사용자가 해당 워크플로에 대 한 가장 편리한 방식으로 데이터를 볼 수 있게 합니다.  
  
- 클립보드 지원을 통해 사용자가 다른 응용 프로그램으로 응용 프로그램에서 데이터를 복사할 수 있습니다.  
  
## <a name="scenario-3-advanced-data"></a>시나리오 3: 고급 데이터  
 표준 데이터 바인딩 모델을 해결 되지 않는 경우 컨트롤 및 데이터 간의 상호 작용을 구현 하 여 관리할 수 있습니다 *가상 모드*합니다. 구현 정보로 셀에 대 한 제어 요청 정보를 수 있는 하나 이상의 이벤트 처리기를 구현 하는 가상 모드 이면 필요 합니다.  
  
 예를 들어, 많은 양의 데이터를 사용 하 여 작업 하는 경우 최적의 효율성을 위해 가상 모드 구현 하는 것이 좋습니다. 가상 모드의 다른 데이터 원본에서 검색 하는 열과 함께 표시 하는 바인딩되지 않은 열 값을 유지 관리도 유용 합니다.  
  
 가상 모드에 대 한 자세한 내용은 참조 하세요. [연습: Forms DataGridView 컨트롤의 Windows에서 가상 모드 구현](implementing-virtual-mode-wf-datagridview-control.md)합니다.  
  
### <a name="scenario-key-points"></a>시나리오의 주요 요소  
  
- 가상 모드는 성능을 미세 조정 해야 할 때 매우 많은 양의 데이터를 표시 하기 위한 적합 합니다.  
  
## <a name="scenario-4-automatically-resizing-rows-and-columns"></a>시나리오 4: 행 및 열을 자동으로 크기 조정  
 정기적으로 업데이트 되는 데이터를 표시 하면 행 및 열 모든 콘텐츠 표시 되는지 확인을 자동으로 조정할 수 있습니다. <xref:System.Windows.Forms.DataGridView> 크기 조정 자동으로 콘텐츠가 변경 될 때마다 또는 컨트롤 사용 또는 사용 하지 않도록 설정 수동 크기 조정, 특정 시간에 프로그래밍 방식으로 크기를 조정할 수 있는 몇 가지 옵션을 제공 합니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤의 크기 조정 옵션](sizing-options-in-the-windows-forms-datagridview-control.md)합니다.  
  
### <a name="scenario-key-points"></a>시나리오의 주요 요소  
  
- 수동 크기 조정을 통해 사용자가 셀 높이 너비를 조정할 수 있습니다.  
  
- 자동 크기 조정 셀 내용이 잘리지 않도록 셀 크기를 유지할 수 있습니다.  
  
- 프로그래밍 방식의 크기를 사용 하면 지속적인 자동 크기 조정의 성능 저하를 방지 하려면 특정 시간에 크기를 조정할 수 있습니다.  
  
## <a name="scenario-5-simple-customization"></a>시나리오 5: 간단한 사용자 지정  
 <xref:System.Windows.Forms.DataGridView> 컨트롤의 기본 모양과 동작을 변경할 수 있는 여러 가지 방법으로 제공 합니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)합니다.  
  
### <a name="scenario-key-points"></a>시나리오의 주요 요소  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle> 개체에 색, 글꼴, 서식 및 여러 수준 및 컨트롤의 개별 요소에 대 한 위치 정보를 제공할 수 있습니다.  
  
- 셀 스타일 계층화 하 고 코드를 재사용할 수 있도록 하는 여러 요소를 공유할 수 있습니다.  
  
## <a name="scenario-6-advanced-customization"></a>시나리오 6: 고급 사용자 지정  
 <xref:System.Windows.Forms.DataGridView> 컨트롤의 모양과 동작을 사용자 지정할 수 있습니다 하는 여러 방법을 제공 합니다.  
  
### <a name="scenario-key-points"></a>시나리오의 주요 요소  
  
- 셀 그리기 코드를 제공할 수 있습니다. 자세한 내용은 [방법: Windows Forms DataGridView 컨트롤에서 셀 모양 사용자 지정](customize-the-appearance-of-cells-in-the-datagrid.md)합니다.  
  
- 고유한 행 그리기를 제공할 수 있습니다. 유용, 예를 들어 여러 열에 걸쳐 있는 콘텐츠를 사용 하 여 행을 만들려고 합니다. 자세한 내용은 [방법: Windows Forms DataGridView 컨트롤에서 행 모양 사용자 지정](customize-the-appearance-of-rows-in-the-datagrid.md)합니다.  
  
- 셀 모양에 맞게 사용자 고유의 셀 및 열 클래스를 구현할 수 있습니다. 자세한 내용은 [방법: 셀과 사용자 지정 열에는 Windows Forms DataGridView 컨트롤은 동작과 모양을 확장 하 여](customize-cells-and-columns-in-the-datagrid-by-extending-behavior.md)입니다.  
  
- 기본 제공 열 형식으로 제공 되지 않는 호스트 컨트롤에 고유한 셀 및 열 클래스를 구현할 수 있습니다. 자세한 내용은 [방법: DataGridView 셀에서 Windows Forms 컨트롤 호스팅](how-to-host-controls-in-windows-forms-datagridview-cells.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- [DataGridView 컨트롤 개요](datagridview-control-overview-windows-forms.md)
