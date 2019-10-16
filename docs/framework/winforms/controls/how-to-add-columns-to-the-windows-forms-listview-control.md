---
title: '방법: Windows Forms ListView 컨트롤에 열 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListView control [Windows Forms], adding column headers
- columns [Windows Forms], adding to ListView controls
- list views [Windows Forms], adding columns
ms.assetid: 79174274-12ee-4a5d-80db-6ec02976d010
ms.openlocfilehash: 5c87d43513f2125945145445c61f689cdd9d2aaf
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59345744"
---
# <a name="how-to-add-columns-to-the-windows-forms-listview-control"></a>방법: Windows Forms ListView 컨트롤에 열 추가
세부 정보 뷰에서 <xref:System.Windows.Forms.ListView> 컨트롤 각 목록 항목에 대 한 여러 열을 표시할 수 있습니다. 여러 유형의 각 목록 항목에 대 한 정보를 사용자에 게 표시 하는 열을 사용할 수 있습니다. 예를 들어, 파일 이름, 파일 형식, 크기 및 파일을 마지막으로 수정한 날짜 파일의 목록을 표시할 수 있습니다. 만들어진 후 열을 채우는 방법에 대 한 내용은 참조 하세요. [방법: Windows 사용 하 여 열에 하위 항목 표시 Forms ListView 컨트롤](how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)합니다.  
  
### <a name="to-add-columns-programmatically"></a>프로그래밍 방식으로 열을 추가 하려면  
  
1. 컨트롤의 <xref:System.Windows.Forms.ListView.View%2A> 속성을 <xref:System.Windows.Forms.View.Details>입니다.  
  
2. 사용 된 <xref:System.Windows.Forms.ListView.ColumnHeaderCollection.Add%2A> 목록 보기의 메서드의 <xref:System.Windows.Forms.ListView.Columns%2A> 속성입니다.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#31)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#31)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ListView>
- [ListView 컨트롤](listview-control-windows-forms.md)
- [ListView 컨트롤 개요](listview-control-overview-windows-forms.md)
