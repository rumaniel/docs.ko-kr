---
title: Windows Forms DataGridView 컨트롤의 성능 조정
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], performance tuning
- performance [Windows Forms], DataGridView control
- performance tuning [Windows Forms], data grids
ms.assetid: 6ccbff28-a0ff-41e4-b601-61b31b61851d
ms.openlocfilehash: 79f74db4ebd095156207a6218f59c0e9ae423085
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62012648"
---
# <a name="performance-tuning-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤의 성능 조정
많은 양의 데이터를 작업할 때의 `DataGridView` 신중 하 게 사용 하지 않는 한 컨트롤 많은 양의 메모리를에서 사용할 수 있습니다. 제한 된 메모리를 사용 하 여 클라이언트에 메모리가 많이 하는 기능은 사용 하지 않음으로써이 오버 헤드의 일부를 방지할 수 있습니다. 데이터 유지 관리의 일부 또는 전부를 관리할 수도 있습니다 및 검색 시나리오에 대 한 메모리 사용량을 사용자 지정 하기 위해 가상 모드를 사용 하 여 직접 작업 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [Windows Forms DataGridView 컨트롤의 크기를 조정하는 최선의 방법](best-practices-for-scaling-the-windows-forms-datagridview-control.md)  
 사용 하는 방법에 설명 합니다 `DataGridView` 많은 양의 데이터를 사용 하 여 작업 하는 경우 불필요 한 메모리 사용량 및 성능 저하를 방지 하는 방식으로 컨트롤입니다.  
  
 [Windows Forms DataGridView 컨트롤의 가상 모드](virtual-mode-in-the-windows-forms-datagridview-control.md)  
 가상 모드를 사용 하 여 보완 하거나 표준 데이터 바인딩 메커니즘을 대체 하는 방법에 설명 합니다.  
  
 [연습: Windows Forms DataGridView 컨트롤에서 가상 모드 구현](implementing-virtual-mode-wf-datagridview-control.md)  
 여러 가상 모드 이벤트에 대 한 처리기를 구현 하는 방법에 설명 합니다. 또한 행 수준 rollback 및 commit 사용자 편집에 대 한 구현 하는 방법을 보여 줍니다.  
  
 [Windows Forms DataGridView 컨트롤에서 Just-In-Time 데이터 로드를 사용하여 가상 모드 구현](implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)  
 사용 가능한 클라이언트 메모리에 저장할 수 있는 보다 표시할 데이터가 많은 경우에 유용 하는 요청 시 데이터를 로드 하는 방법을 설명 합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Windows.Forms.DataGridView>  
 <xref:System.Windows.Forms.DataGridView> 컨트롤에 대한 참조 설명서를 제공합니다.  
  
 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>  
 에 대 한 참조 설명서를 제공 합니다 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 속성입니다.  
  
## <a name="see-also"></a>참고자료

- [DataGridView 컨트롤](datagridview-control-windows-forms.md)
- [Windows Forms DataGridView 컨트롤의 데이터 디스플레이 모드](data-display-modes-in-the-windows-forms-datagridview-control.md)
