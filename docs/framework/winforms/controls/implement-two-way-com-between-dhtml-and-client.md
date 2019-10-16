---
title: '방법: DHTML 코드와 클라이언트 애플리케이션 코드 간의 양방향 통신 구현'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
f1_keywords:
- WebBrowser.ObjectForScripting
- WebBrowser.Document
helpviewer_keywords:
- WebBrowser control [Windows Forms], examples
- communications [Windows Forms], DHTML and client applications
- examples [Windows Forms], WebBrowser control
- WebBrowser control [Windows Forms], communication between DHTML and client application
- DHTML [Windows Forms], embedding in Windows Forms
ms.assetid: 55353a32-b09e-4479-a521-ff3a5ff9a708
ms.openlocfilehash: 26cbc995a749c4c129729be700dee588d1033a05
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69953432"
---
# <a name="how-to-implement-two-way-communication-between-dhtml-code-and-client-application-code"></a>방법: DHTML 코드와 클라이언트 애플리케이션 코드 간의 양방향 통신 구현

<xref:System.Windows.Forms.WebBrowser> 컨트롤을 사용하여 Windows Forms 클라이언트 애플리케이션에 기존 DHTML(동적 HTML) 웹 애플리케이션 코드를 추가할 수 있습니다. DHTML 기반 컨트롤을 만드는 데 상당한 개발 시간을 투자했으며 기존 코드를 다시 작성할 필요 없이 Windows Forms의 풍부한 사용자 인터페이스 기능을 활용하려는 경우에 유용합니다.

<xref:System.Windows.Forms.WebBrowser> 컨트롤을 사용하면 <xref:System.Windows.Forms.WebBrowser.ObjectForScripting%2A> 및 <xref:System.Windows.Forms.WebBrowser.Document%2A> 속성을 통해 클라이언트 애플리케이션 코드와 웹 페이지 스크립팅 코드 간의 양방향 통신을 구현할 수 있습니다. 또한 웹 컨트롤이 애플리케이션 폼의 다른 컨트롤과 매끄럽게 혼합되어 해당 DHTML 구현을 숨기도록 <xref:System.Windows.Forms.WebBrowser> 컨트롤을 구성할 수 있습니다. 컨트롤을 매끄럽게 혼합하려면 배경색 및 시각적 스타일이 폼의 나머지 부분과 일치하도록 표시되는 페이지 형식을 지정하고 <xref:System.Windows.Forms.WebBrowser.AllowWebBrowserDrop%2A>, <xref:System.Windows.Forms.WebBrowser.IsWebBrowserContextMenuEnabled%2A> 및 <xref:System.Windows.Forms.WebBrowser.WebBrowserShortcutsEnabled%2A> 속성을 통해 표준 브라우저 기능을 사용하지 않도록 설정합니다.

## <a name="to-embed-dhtml-in-your-windows-forms-application"></a>Windows Forms 애플리케이션에 DHTML을 포함하려면

1. <xref:System.Windows.Forms.WebBrowser> 컨트롤의 <xref:System.Windows.Forms.WebBrowser.AllowWebBrowserDrop%2A> 속성을 `false`로 설정하여 <xref:System.Windows.Forms.WebBrowser> 컨트롤이 놓여진 파일을 열지 않도록 합니다.

     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#1)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#1)]

2. 컨트롤의 <xref:System.Windows.Forms.WebBrowser.IsWebBrowserContextMenuEnabled%2A> 속성을 `false`로 설정하여 사용자가 마우스 오른쪽 단추로 클릭할 때 <xref:System.Windows.Forms.WebBrowser> 컨트롤이 바로 가기 메뉴를 표시하지 않도록 합니다.

     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#2)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#2)]

3. 컨트롤의 <xref:System.Windows.Forms.WebBrowser.WebBrowserShortcutsEnabled%2A> 속성을 `false`로 설정하여 <xref:System.Windows.Forms.WebBrowser> 컨트롤이 바로 가기 키에 응답하지 않도록 합니다.

     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#3)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#3)]

4. 폼의 생성자나 <xref:System.Windows.Forms.Form.Load> 이벤트 처리기에서 <xref:System.Windows.Forms.WebBrowser.ObjectForScripting%2A> 속성을 설정합니다.

     다음 코드에서는 스크립팅 개체에 대한 폼 클래스 자체를 사용합니다.

    > [!NOTE]
    > COM(구성 요소 개체 모델)에서 스크립팅 개체에 액세스할 수 있어야 합니다. COM에서 폼을 볼 수 있게 하려면 폼 클래스에 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 특성을 추가합니다.

     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#4)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#4)]

5. 스크립트 코드에서 사용할 공용 속성 또는 메서드를 애플리케이션 코드에서 구현합니다.

     예를 들어 스크립팅 개체에 폼 클래스를 사용하는 경우 다음 코드를 폼 클래스에 추가합니다.

     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#5)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#5)]

6. 스크립팅 코드에서 `window.external` 개체를 사용하여 지정된 개체의 공용 속성 및 메서드에 액세스합니다.

     다음 HTML 코드는 단추 클릭에서 스크립팅 개체에 대한 메서드를 호출하는 방법을 보여 줍니다. 컨트롤의 <xref:System.Windows.Forms.WebBrowser.Navigate%2A> 메서드를 사용하여 로드하거나 컨트롤의 <xref:System.Windows.Forms.WebBrowser.DocumentText%2A> 속성에 할당하는 HTML 문서의 BODY 요소에 이 코드를 복사합니다.

    ```html
    <button onclick="window.external.Test('called from script code')">
        call client code from script code
    </button>
    ```

7. 애플리케이션 코드에서 사용할 함수를 스크립트 코드에서 구현합니다.

     다음 HTML SCRIPT 요소는 예제 함수를 제공합니다. 컨트롤의 <xref:System.Windows.Forms.WebBrowser.Navigate%2A> 메서드를 사용하여 로드하거나 컨트롤의 <xref:System.Windows.Forms.WebBrowser.DocumentText%2A> 속성에 할당하는 HTML 문서의 HEAD 요소에 이 코드를 복사합니다.

    ```html
    <script>
    function test(message) {
        alert(message);
    }
    </script>
    ```

8. <xref:System.Windows.Forms.WebBrowser.Document%2A> 속성을 사용하여 클라이언트 애플리케이션 코드에서 스크립트 코드에 액세스합니다.

     예를 들어 단추 <xref:System.Windows.Forms.Control.Click> 이벤트 처리기에 다음 코드를 추가합니다.

     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#8](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#8)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#8](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#8)]

9. DHTML 디버그가 완료되면 컨트롤의 <xref:System.Windows.Forms.WebBrowser.ScriptErrorsSuppressed%2A> 속성을 `true`로 설정하여 <xref:System.Windows.Forms.WebBrowser> 컨트롤이 스크립트 코드 문제에 대한 오류 메시지를 표시하지 않도록 합니다.

     [!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#9](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#9)]
     [!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#9](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#9)]

## <a name="example"></a>예제

다음 전체 코드 예제에서는 이 기능을 이해하는 데 사용할 수 있는 데모 애플리케이션을 제공합니다. HTML 코드는 별도 HTML 파일에서 로드되지 않고 <xref:System.Windows.Forms.WebBrowser.DocumentText%2A> 속성을 통해 <xref:System.Windows.Forms.WebBrowser> 컨트롤에 로드됩니다.

[!code-csharp[System.Windows.Forms.WebBrowser.ObjectForScripting#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/CS/form1.cs#0)]
[!code-vb[System.Windows.Forms.WebBrowser.ObjectForScripting#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.WebBrowser.ObjectForScripting/vb/form1.vb#0)]

## <a name="compiling-the-code"></a>코드 컴파일

이 코드에는 다음이 필요합니다.

- System 및 System.Windows.Forms 어셈블리에 대한 참조

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.WebBrowser>
- <xref:System.Windows.Forms.WebBrowser.Document%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.WebBrowser.ObjectForScripting%2A?displayProperty=nameWithType>
- [WebBrowser 컨트롤](webbrowser-control-windows-forms.md)
