---
title: Windows Forms DataGridView 컨트롤의 데이터 정렬
ms.date: 02/13/2018
helpviewer_keywords:
- data [Windows Forms], sorting in grids
- data grids [Windows Forms], sorting data
- DataGridView control [Windows Forms], sorting data
ms.assetid: c1d4f24c-d961-4181-809d-5a5caa6122e4
ms.openlocfilehash: 606ffc7bd6136b775adaaaa79cf5042cf1e2dd70
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62012154"
---
# <a name="sorting-data-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤의 데이터 정렬

기본적으로 사용자의 데이터를 정렬할 수는 <xref:System.Windows.Forms.DataGridView> 컨트롤의 텍스트 상자 열 머리글을 클릭 하 여 (또는.NET Framework 4.7.2 이상에서 텍스트 상자 셀 포커스가 F3 키를 눌러). 수정할 수는 <xref:System.Windows.Forms.DataGridViewColumn.SortMode> 이렇게 하려면 적합 한 경우 다른 열 유형에 정렬할 수 있도록 특정 열 속성입니다. 정렬할 수 있습니다도 데이터를 프로그래밍 방식으로 모든 열 또는 여러 열을 기준으로.

## <a name="in-this-section"></a>단원 내용

[Windows Forms DataGridView 컨트롤의 열 정렬 모드](column-sort-modes-in-the-windows-forms-datagridview-control.md)  
컨트롤의 데이터 정렬에 대 한 옵션을 설명 합니다.

[방법: Windows Forms DataGridView 컨트롤의 열 정렬 모드 설정](set-the-sort-modes-for-columns-wf-datagridview-control.md)  
기본적으로 정렬 가능 하지 않은 열을 정렬할 수 있도록 하는 방법에 설명 합니다.

[방법: Windows Forms DataGridView 컨트롤에서 정렬 사용자 지정](how-to-customize-sorting-in-the-windows-forms-datagridview-control.md)  
프로그래밍 방식으로 데이터를 정렬 하는 방법 및 사용 하 여 정렬 사용자 지정 하는 방법에 설명 합니다 <xref:System.Windows.Forms.DataGridView.SortCompare?displayProperty=nameWithType> 이벤트 또는 구현 하 여는 <xref:System.Collections.IComparer> 인터페이스입니다.

## <a name="reference"></a>참조

<xref:System.Windows.Forms.DataGridView>  
<xref:System.Windows.Forms.DataGridView> 컨트롤에 대한 참조 설명서를 제공합니다.  

<xref:System.Windows.Forms.DataGridView.Sort%2A?displayProperty=nameWithType>  
에 대 한 참조 설명서를 제공 합니다 <xref:System.Windows.Forms.DataGridView.Sort%2A> 메서드.

<xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A?displayProperty=nameWithType>  
에 대 한 참조 설명서를 제공 합니다 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 속성입니다.

<xref:System.Windows.Forms.DataGridViewColumnSortMode>  
에 대 한 참조 설명서를 제공 합니다 <xref:System.Windows.Forms.DataGridViewColumnSortMode> 열거형입니다.

## <a name="see-also"></a>참고자료

- [DataGridView 컨트롤](datagridview-control-windows-forms.md)
- [Windows Forms DataGridView 컨트롤의 열 형식](column-types-in-the-windows-forms-datagridview-control.md)
