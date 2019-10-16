---
title: '방법: 이미지가 있는 단추 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Button controls [WPF], creating
ms.assetid: 607a193c-4098-4dd8-8dc0-51256cec2020
ms.openlocfilehash: 5be928ac75ad727feabcde07ac0c6dc76ed130e6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910951"
---
# <a name="how-to-create-a-button-that-has-an-image"></a>방법: 이미지가 있는 단추 만들기
이 예제에서 이미지를 포함 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.Button>합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 개의 <xref:System.Windows.Controls.Button> 컨트롤입니다. 하나의 <xref:System.Windows.Controls.Button> 텍스트가 이미지를 포함 합니다. 예제의 프로젝트 폴더의 하위 데이터 라는 폴더에 이미지가입니다. 클릭할 때 합니다 <xref:System.Windows.Controls.Button> 이미지, 백그라운드 및 다른 텍스트 있는 <xref:System.Windows.Controls.Button> 변경 합니다.  
  
 이 예제에서는 <xref:System.Windows.Controls.Button> 태그를 사용 하 여 제어 하지만 코드를 사용 하 여 작성 된 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트 처리기입니다.  
  
 [!code-xaml[BtnColor#4](~/samples/snippets/csharp/VS_Snippets_Wpf/BtnColor/CSharp/Pane1.xaml#4)]  
  
 [!code-csharp[BtnColor#6](~/samples/snippets/csharp/VS_Snippets_Wpf/BtnColor/CSharp/Pane1.xaml.cs#6)]
 [!code-vb[BtnColor#6](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BtnColor/VisualBasic/Pane1.xaml.vb#6)]  
  
## <a name="see-also"></a>참고자료

- [컨트롤](index.md)
- [컨트롤 라이브러리](control-library.md)
