---
title: '방법: ListView 컨트롤에 검색 기능 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- lists [Windows Forms], enabling searching
- list views [Windows Forms], enabling searching
- ListView control [Windows Forms], adding search capabilities
- searching [Windows Forms], adding search capabilities to ListView control
ms.assetid: 557782d9-b705-4bab-b496-9938afddac82
ms.openlocfilehash: d5d4dae55fc9f0613ab6535b2fe57e262d0ef141
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62011036"
---
# <a name="how-to-add-search-capabilities-to-a-listview-control"></a>방법: ListView 컨트롤에 검색 기능 추가
에 있는 항목의 큰 목록으로 작업 하는 경우에 종종는 <xref:System.Windows.Forms.ListView> 사용자에 게 검색 기능을 제공 하려는 컨트롤입니다. <xref:System.Windows.Forms.ListView> 두 가지 방법으로이 기능을 제공 하는 컨트롤: 텍스트 일치 및 위치를 검색 합니다.  
  
 합니다 <xref:System.Windows.Forms.ListView.FindItemWithText%2A> 메서드를 사용 하면 텍스트 검색을 수행할 수 있습니다는 <xref:System.Windows.Forms.ListView> 목록 또는 세부 정보 보기에서 검색 문자열 및 선택적 시작 및 끝 인덱스를 지정 합니다. 반면, 합니다 <xref:System.Windows.Forms.ListView.FindNearestItem%2A> 메서드를 사용 하면에서 항목을 찾을 수 있습니다는 <xref:System.Windows.Forms.ListView> 아이콘 또는 타일 보기에서 지정 된 x 좌표와 y 좌표와 검색할 방향을 집합.  
  
### <a name="to-find-an-item-using-text"></a>텍스트를 사용 하 여 항목을 찾으려면  
  
1. 만들기는 <xref:System.Windows.Forms.ListView> 사용 하 여는 <xref:System.Windows.Forms.ListView.View%2A> 속성이로 설정 <xref:System.Windows.Forms.View.Details> 또는 <xref:System.Windows.Forms.View.List>를 입력 합니다 <xref:System.Windows.Forms.ListView> 항목과 합니다.  
  
2. 호출 된 <xref:System.Windows.Forms.ListView.FindItemWithText%2A> 메서드를 찾으려면 원하는 항목의 텍스트를 전달 합니다.  
  
3. 다음 코드 예제를 만드는 방법을 보여 줍니다. <xref:System.Windows.Forms.ListView>, 항목을 사용 하 여 채우기 및 사용자가 입력 한 텍스트를 사용 하 여 목록에서 항목을 찾으려고 합니다.  
  
 [!code-cpp[System.Windows.Forms.ListViewFindItems#1](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/cpp/form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.ListViewFindItems#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.ListViewFindItems#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/VB/form1.vb#1)]  
  
### <a name="to-find-an-item-using-x--and-y-coordinates"></a>X 좌표와 y 좌표를 사용 하 여 항목을 찾으려면  
  
1. 만들기는 <xref:System.Windows.Forms.ListView> 사용 하 여는 <xref:System.Windows.Forms.View> 속성이로 설정 <xref:System.Windows.Forms.View.SmallIcon> 또는 <xref:System.Windows.Forms.View.LargeIcon>를 입력 합니다 <xref:System.Windows.Forms.ListView> 항목과 합니다.  
  
2. 호출 된 <xref:System.Windows.Forms.ListView.FindNearestItem%2A> 메서드를 검색 하려는 방향과 원하는 x 및 y 좌표를 전달 합니다.  
  
3. 다음 코드 예제에서는 기본 아이콘을 만드는 방법을 보여 줍니다 <xref:System.Windows.Forms.ListView>, 항목 및 캡처를 사용 하 여 채우기는 <xref:System.Windows.Forms.Control.MouseDown> 위쪽 방향으로 가장 가까운 항목을 찾으려면 이벤트입니다.  
  
 [!code-cpp[System.Windows.Forms.ListViewFindItems#2](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/cpp/form1.cpp#2)]
 [!code-csharp[System.Windows.Forms.ListViewFindItems#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/CS/form1.cs#2)]
 [!code-vb[System.Windows.Forms.ListViewFindItems#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/VB/form1.vb#2)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ListView>
- <xref:System.Windows.Forms.ListView.FindItemWithText%2A>
- <xref:System.Windows.Forms.ListView.FindNearestItem%2A>
- [ListView 컨트롤](listview-control-windows-forms.md)
- [ListView 컨트롤 개요](listview-control-overview-windows-forms.md)
- [방법: Windows Forms ListView 컨트롤을 사용 하 여 항목 추가 및 제거](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
