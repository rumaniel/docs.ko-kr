---
title: Windows Forms DataGridView 컨트롤의 기본 기능
ms.date: 03/30/2017
helpviewer_keywords:
- data grids [Windows Forms], default functionality in DataGridView control
- DataGridView control [Windows Forms], default functionality
ms.assetid: 4405f697-cad1-4839-9bcd-8ddb09d9f00e
ms.openlocfilehash: b84d5a279bfe7cd99262ca904daeceabc9d0355d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64648065"
---
# <a name="default-functionality-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤의 기본 기능
Windows Forms <xref:System.Windows.Forms.DataGridView> 컨트롤은 상당한 양의 기본 기능을 사용 하 여 사용자를 제공 합니다.  
  
## <a name="default-functionality"></a>기본 기능  
 기본적으로 <xref:System.Windows.Forms.DataGridView> 제어 합니다.  
  
- 열 머리글 및 테이블을 세로로 스크롤할 때 계속 표시 되는 행 머리글을 자동으로 표시 합니다.  
  
- 현재 행에 대 한 선택 표시기를 포함 하는 행 머리글을 있습니다.  
  
- 선택 영역 직사각형을 첫 번째 셀에 있습니다.  
  
- 열 구분선을 두 번 클릭할 때 자동으로 조정 하는 열이 있습니다.  
  
- 자동으로 Windows XP 및 Windows Server 2003 제품군에서 비주얼 스타일을 지 원하는 경우는 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> 메서드는 응용 프로그램에서 `Main` 메서드.  
  
 내용을 또한는 <xref:System.Windows.Forms.DataGridView> 기본적으로 컨트롤을 편집할 수 있습니다.  
  
- 사용자가 두 번 클릭 또는 셀에서 f2 키를 누를 경우 컨트롤 자동으로 셀을 편집 모드로 전환 하 고 사용자가 셀의 내용을 업데이트 합니다.  
  
- 눈금의 끝에 사용자를 스크롤하면 하는 경우 사용자는 새 레코드를 추가 하는 것에 대 한 행이 나타납니다. 사용자가이 행에 새 행에 추가 됩니다는 <xref:System.Windows.Forms.DataGridView> 기본값을 사용 하 여 제어 합니다. 사용자가 esc 키를 누를 때 새 행이 사라집니다.  
  
- 사용자가 행 머리글을 클릭 하면 전체 행이 선택 됩니다.  
  
 바인딩하는 경우는 <xref:System.Windows.Forms.DataGridView> 컨트롤을 설정 하 여 데이터 소스는 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 속성, 컨트롤:  
  
- 자동 데이터 원본의 열 이름으로 열 머리글 텍스트를 사용합니다.  
  
- 데이터 원본 내용으로 채워집니다. <xref:System.Windows.Forms.DataGridView> 열은 데이터 원본의 각 열에 대해 자동으로 만들어집니다.  
  
- 테이블에 표시 되는 각 행에 대 한 행을 만듭니다.  
  
- 열 머리글을 마우스 오른쪽 단추로 클릭할 때 기본 데이터를 기준으로 행을 자동으로 정렬 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- [DataGridView 컨트롤](datagridview-control-windows-forms.md)
