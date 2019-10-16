---
title: '방법: Windows Forms 애플리케이션에 웹 브라우저 기능 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- WebBrowser control [Windows Forms], adding Web browser capabilities to your application
- WebBrowser control [Windows Forms], examples
- Web browsers [.NET Framework], adding to Windows Forms
- examples [Windows Forms], WebBrowser control
- Windows Forms, adding Web browser functionality
ms.assetid: 3871f072-b57a-435b-9976-e5da28df04a7
ms.openlocfilehash: 60b544c630fc5c7c876293b27a5c5e159e57a797
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65588883"
---
# <a name="how-to-add-web-browser-capabilities-to-a-windows-forms-application"></a>방법: Windows Forms 애플리케이션에 웹 브라우저 기능 추가
<xref:System.Windows.Forms.WebBrowser> 컨트롤을 통해 애플리케이션에 웹 브라우저 기능을 추가할 수 있습니다. 컨트롤은 기본적으로 웹 브라우저처럼 작동합니다. <xref:System.Windows.Forms.WebBrowser.Url%2A> 속성을 설정하여 초기 URL을 로드한 후 하이퍼링크를 클릭하거나 바로 가기 키를 통해 탐색 기록을 앞뒤로 이동하여 탐색할 수 있습니다. 기본적으로 오른쪽 클릭 바로 가기 메뉴를 통해 추가 브라우저 기능에 액세스할 수 있습니다. 컨트롤에 끌어서 놓아 새 문서를 열 수도 있습니다. <xref:System.Windows.Forms.WebBrowser> 컨트롤에는 Internet Explorer에 있는 것과 비슷한 사용자 인터페이스 기능을 구현하는 데 사용할 수 있는 여러 속성, 메서드 및 이벤트도 있습니다.  
  
 다음 코드 예제에서는 주소 표시줄, 일반적인 브라우저 단추, **파일** 메뉴, 상태 표시줄 및 현재 페이지 제목을 표시하는 제목 표시줄을 구현합니다.  
  
## <a name="example"></a>예제  
 [!code-cpp[System.Windows.Forms.WebBrowser#0](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser/CPP/form1.cpp#0)]
 [!code-csharp[System.Windows.Forms.WebBrowser#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser/CS/form1.cs#0)]
 [!code-vb[System.Windows.Forms.WebBrowser#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser/VB/form1.vb#0)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- `System`, `System.Drawing` 및 `System.Windows.Forms` 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.WebBrowser>
- [WebBrowser 컨트롤](webbrowser-control-windows-forms.md)
