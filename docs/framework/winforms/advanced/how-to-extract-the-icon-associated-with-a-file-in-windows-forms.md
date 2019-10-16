---
title: '방법: Windows Forms에서 파일과 연결된 아이콘 추출'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- displaying a file name and its file type icon in a ListView control [Windows Forms]
- file name extension icons [Windows Forms], displaying in a ListView
- extracting icons associated with a file type [Windows Forms]
ms.assetid: 88e2ad8b-c34f-415a-84f2-dad756b5c928
ms.openlocfilehash: c3173a3fa756a3294154217f5cf0a13dbc8721f3
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645407"
---
# <a name="how-to-extract-the-icon-associated-with-a-file-in-windows-forms"></a>방법: Windows Forms에서 파일과 연결된 아이콘 추출
여러 파일에는 시각적 연결된 된 파일 형식으로 제공 하는 아이콘이 포함 되어 있습니다. 예를 들어 Microsoft Word 문서를 Word 문서로 하 게 식별 하는 아이콘을 포함 합니다. 목록 컨트롤 또는 테이블 컨트롤에서 파일을 표시 하는 경우에 각 파일 이름 옆에 있는 파일 형식을 나타내는 아이콘을 표시 하는 것이 좋습니다. 사용 하 여이 작업을 쉽게 수행할 수 있습니다는 <xref:System.Drawing.Icon.ExtractAssociatedIcon%2A> 메서드.  
  
## <a name="example"></a>예제  
 다음 코드 예제에는 파일과 연결 된 아이콘 추출 파일 이름 및 연결 된 아이콘을 표시 하는 방법을 보여 줍니다.는 <xref:System.Windows.Forms.ListView> 제어 합니다.  
  
 [!code-csharp[System.Drawing.Icon.ExtractAssociatedIconEx#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Icon.ExtractAssociatedIconEx/CS/Form1.cs#1)]
 [!code-vb[System.Drawing.Icon.ExtractAssociatedIconEx#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Icon.ExtractAssociatedIconEx/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 예제를 컴파일하려면:  
  
- Windows 폼 호출에 위의 코드를 붙여넣고 합니다 `ExtractAssociatedIconExample` 폼의 생성자에서 메서드 또는 <xref:System.Windows.Forms.Form.Load> 이벤트 처리 메서드.  
  
     폼을 가져옵니다는 있는지 확인 해야 합니다 <xref:System.IO> 네임 스페이스입니다.  
  
## <a name="see-also"></a>참고자료

- [이미지, 비트맵 및 메타파일](images-bitmaps-and-metafiles.md)
- [ListView 컨트롤](../controls/listview-control-windows-forms.md)
