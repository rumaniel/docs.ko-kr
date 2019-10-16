---
title: '방법: Windows Forms ListView 컨트롤에서 항목 선택'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- lists [Windows Forms], selecting items
- ListView control [Windows Forms], selecting items
- selection [Windows Forms], in list views
- list views [Windows Forms], selecting items
ms.assetid: ddea918e-1ddf-47f4-bd09-1e9b4c9d0c39
ms.openlocfilehash: 41a30ba6c242d0587e98b458e41ca213e8885bca
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64638199"
---
# <a name="how-to-select-an-item-in-the-windows-forms-listview-control"></a>방법: Windows Forms ListView 컨트롤에서 항목 선택
이 예제에서는 프로그래밍 방식으로 Windows Forms에서 항목을 선택 하는 방법에 설명 <xref:System.Windows.Forms.ListView> 제어 합니다. 프로그래밍 방식으로 항목을 선택 하면 자동으로 바뀌지 않습니다에 포커스를 <xref:System.Windows.Forms.ListView> 제어 합니다. 따라서 일반적으로 하려는 항목을 선택할 때 강조 하는 항목을 설정 합니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[System.Windows.Forms.ListView.Misc#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListView.Misc/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.ListView.Misc#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListView.Misc/VB/form1.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- A <xref:System.Windows.Forms.ListView> 제어 라는 `listView1` 하나 이상의 항목이 포함 된 합니다.  
  
- <xref:System?displayProperty=nameWithType> 및 <xref:System.Windows.Forms?displayProperty=nameWithType> 네임스페이스에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ListView>
- <xref:System.Windows.Forms.ListViewItem.Selected%2A?displayProperty=nameWithType>
