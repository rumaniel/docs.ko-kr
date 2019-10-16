---
title: '방법: 관리형 HTML 문서 개체 모델에서 요소의 스타일 변경'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- managed HTML DOM [Windows Forms], changing styles on elements
ms.assetid: 154e8d9f-3e2d-4e8b-a6f3-c85a070e9cc1
ms.openlocfilehash: 728bc77db959e25fe31d2ff37288b2359dca852e
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67424588"
---
# <a name="how-to-change-styles-on-an-element-in-the-managed-html-document-object-model"></a>방법: 관리형 HTML 문서 개체 모델에서 요소의 스타일 변경

모양을 제어 하는 문서 및 해당 요소의 html에서 스타일을 사용할 수 있습니다. <xref:System.Windows.Forms.HtmlDocument> 및 <xref:System.Windows.Forms.HtmlElement> 지원 <xref:System.Windows.Forms.HtmlElement.Style%2A> 스타일 문자열의 형식은 사용 하는 속성:

`name1:value1;...;nameN:valueN;`

다음은 `DIV` 을 Arial 고 모든 텍스트를 굵게 글꼴을 설정 하는 스타일 문자열을 사용 하 여:

```html
<DIV style="font-face:arial;font-weight:bold;">
Hello, world!
</DIV>
```

사용 하 여 스타일을 조작 하는 문제는 <xref:System.Windows.Forms.HtmlElement.Style%2A> 속성이 수 있다는 것을 추가 하 고 문자열에서 개별 스타일 설정을 제거 하기가 불편 합니다. 예를 들어, 위에 커서를 가져갈 때마다 기울임꼴에서 이전 텍스트를 렌더링 하는 복잡 한 절차 할 합니다 `DIV`, 기울임꼴 커서를 벗어날 때 해제 하 고는 `DIV`합니다. 시간이이 방식으로 스타일의 큰 숫자를 조작 하는 경우 문제가 될 것입니다.

다음 절차는 HTML 문서와 요소에 대 한 스타일을 쉽게 사용할 수 있는 코드를 포함 합니다. 절차는 Windows forms에서 새 프로젝트 만들기 및 폼에 컨트롤 추가 같은 기본 작업을 수행 하는 방법을 알고 필요 합니다.

### <a name="to-process-style-changes-in-a-windows-forms-application"></a>Windows Forms 응용 프로그램에서 스타일 변경 내용을 처리

1. 새 Windows Forms 프로젝트를 만듭니다.

2. 프로그래밍 언어에 대 한 적절 한 확장명으로 끝나는 새 클래스 파일을 만듭니다.

3. 복사를 `StyleGenerator` 클래스 파일에이 항목의 예제 섹션의 코드를 클래스 및 코드를 저장 합니다.

4. 다음 HTML Test.htm 라는 파일에 저장 합니다.

    ```html
    <HTML>
        <BODY>

            <DIV style="font-face:arial;font-weight:bold;">
                Hello, world!
            </DIV><P>

            <DIV>
                Hello again, world!
            </DIV><P>

        </BODY>
    </HTML>
    ```

5. 추가 된 <xref:System.Windows.Forms.WebBrowser> 라는 컨트롤 `webBrowser1` 프로젝트의 기본 폼에 합니다.

6. 프로젝트의 코드 파일에 다음 코드를 추가 합니다.

    > [!IMPORTANT]
    > 있는지 확인 합니다 `webBrowser1_DocumentCompleted` 이벤트 처리기에 대 한 수신기로 구성 된는 <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> 이벤트입니다. Visual Studio에서 두 번 클릭 합니다 <xref:System.Windows.Forms.WebBrowser> 제어; 텍스트 편집기에서 수신기를 프로그래밍 방식으로 구성 합니다.

     [!code-csharp[ManagedDOMStyles#2](~/samples/snippets/csharp/VS_Snippets_Winforms/ManagedDOMStyles/CS/Form1.cs#2)]
     [!code-vb[ManagedDOMStyles#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/ManagedDOMStyles/VB/Form1.vb#2)]

7. 프로젝트를 실행합니다. 커서를 첫 번째 실행 `DIV` 코드의 결과를 관찰 합니다.

## <a name="example"></a>예제

다음 코드 예제에 대 한 전체 코드를 보여 줍니다.는 `StyleGenerator` 기존 스타일 값을 구문 분석 하는 클래스 지원 추가, 변경 및 스타일을 제거 하 고 요청 된 변경 내용으로 새 스타일 값을 반환 합니다.

[!code-csharp[ManagedDOMStyles#1](~/samples/snippets/csharp/VS_Snippets_Winforms/ManagedDOMStyles/CS/StyleGenerator.cs#1)]
[!code-vb[ManagedDOMStyles#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/ManagedDOMStyles/VB/StyleGenerator.vb#1)]

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.HtmlElement>
