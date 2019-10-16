---
title: '방법: 관리형 HTML 문서 개체 모델 액세스'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- HTML DOM [Windows Forms], accessing
- managed HTML DOM [Windows Forms], accessing
ms.assetid: 40fa5cd5-1ed8-42f6-a93f-9ac01608bbeb
ms.openlocfilehash: 2a195dc6583d5a0a72bd08b66f8933f4002e879a
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487269"
---
# <a name="how-to-access-the-managed-html-document-object-model"></a>방법: 관리형 HTML 문서 개체 모델 액세스
다음과 같은 두 가지 유형의 애플리케이션에서 관리되는 HTML DOM(문서 개체 모델)에 액세스할 수 있습니다.  
  
- 관리되는 <xref:System.Windows.Forms.WebBrowser> 컨트롤을 호스팅하는 Windows Forms 애플리케이션(.exe). 이러한 두 가지 기술은 서로를 보완하며 <xref:System.Windows.Forms.WebBrowser> 컨트롤을 통해 사용자에게 페이지를 표시하고 HTML DOM을 통해 문서의 논리 구조를 나타냅니다.  
  
- Internet Explorer 내에서 호스팅되는 <xref:System.Windows.Forms.UserControl>. <xref:System.Windows.Forms.UserControl>이 호스팅되는 페이지를 나타내는 HTML DOM에 액세스하여 문서 구조를 변경하거나 모달 대화 상자를 여는 등 여러 작업을 수행할 수 있습니다.  
  
### <a name="to-access-dom-from-a-windows-forms-application"></a>Windows Forms 애플리케이션에서 DOM에 액세스하려면  
  
1. Windows Forms 애플리케이션 내에서 <xref:System.Windows.Forms.WebBrowser> 컨트롤을 호스팅하고 <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> 이벤트를 모니터링합니다. 컨트롤 호스팅 및 이벤트 모니터링에 대한 자세한 내용은 [이벤트](../../../standard/events/index.md)를 참조하세요.  
  
2. <xref:System.Windows.Forms.HtmlDocument> 컨트롤의 <xref:System.Windows.Forms.WebBrowser.Document%2A> 속성에 액세스하여 현재 페이지에 대해 <xref:System.Windows.Forms.WebBrowser>를 검색합니다.  

### <a name="to-access-dom-from-a-usercontrol-hosted-in-internet-explorer"></a>Internet Explorer에서 호스팅되는 UserControl에서 DOM에 액세스하려면  
  
1. <xref:System.Windows.Forms.UserControl> 클래스의 고유한 사용자 지정 파생 클래스를 만듭니다. 자세한 내용은 [방법: 합성 컨트롤 제작](how-to-author-composite-controls.md)합니다.  
  
2. <xref:System.Windows.Forms.UserControl>의 로드 이벤트 처리기 내에 다음 코드를 삽입합니다.  
  
 [!code-csharp[AccessHTMLDOMControl#1](~/samples/snippets/csharp/VS_Snippets_Winforms/AccessHTMLDOMControl/cs/UserControl1.cs#1)]
 [!code-vb[AccessHTMLDOMControl#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/AccessHTMLDOMControl/vb/UserControl1.vb#1)]  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
  
1. <xref:System.Windows.Forms.WebBrowser> 컨트롤을 통해 DOM을 사용할 때는 항상 <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> 이벤트가 발생할 때까지 기다린 후에 <xref:System.Windows.Forms.WebBrowser.Document%2A> 컨트롤의 <xref:System.Windows.Forms.WebBrowser> 속성 액세스를 시도해야 합니다. 전체 문서가 로드되고 나면 <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> 이벤트가 발생합니다. 그 전에 DOM을 사용하면 애플리케이션에서 런타임 예외가 발생할 위험이 있습니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
  
1. 관리되는 HTML DOM에 액세스하려면 애플리케이션 또는 <xref:System.Windows.Forms.UserControl>을 완전히 신뢰해야 합니다. ClickOnce를 사용 하 여 Windows Forms 응용 프로그램을 배포 하는 경우 권한 상승 또는 신뢰할 수 있는 응용 프로그램 배포를 사용 하 여 완전 신뢰를 요청할 수 있습니다. 참조 [ClickOnce 응용 프로그램 보안](/visualstudio/deployment/securing-clickonce-applications) 세부 정보에 대 한 합니다.  
  
## <a name="see-also"></a>참고자료

- [관리되는 HTML 문서 개체 모델 사용](using-the-managed-html-document-object-model.md)
