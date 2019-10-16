---
title: '방법: Windows Forms RichTextBox 컨트롤을 사용하여 웹 스타일 링크 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- text boxes [Windows Forms], displaying Web links
- examples [Windows Forms], text boxes
- RichTextBox control [Windows Forms], linking to Web pages
ms.assetid: 95089a37-a202-4f7a-94ee-6ee312908851
ms.openlocfilehash: ce71981f7b233d3e168689c766128646eed3e981
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046182"
---
# <a name="how-to-display-web-style-links-with-the-windows-forms-richtextbox-control"></a>방법: Windows Forms RichTextBox 컨트롤을 사용하여 웹 스타일 링크 표시

Windows Forms <xref:System.Windows.Forms.RichTextBox> 컨트롤은 웹 링크를 색과 밑줄로 표시할 수 있습니다. 링크를 클릭 하면 링크 텍스트에 지정 된 웹 사이트를 표시 하는 브라우저 창을 여는 코드를 작성할 수 있습니다.

### <a name="to-link-to-a-web-page-with-the-richtextbox-control"></a>RichTextBox 컨트롤을 사용 하 여 웹 페이지에 연결 하려면

1. 속성을 올바른 URL (예: "http://www.microsoft.com/")이 포함 된 문자열로 설정 합니다. <xref:System.Windows.Forms.RichTextBox.Text%2A>

2. <xref:System.Windows.Forms.RichTextBox.DetectUrls%2A> 속성이 (기본값)로 `true` 설정 되어 있는지 확인 합니다.

3. <xref:System.Diagnostics.Process> 개체의 새 전역 인스턴스를 만듭니다.

4. 브라우저에서 원하는 텍스트를 전송 <xref:System.Windows.Forms.RichTextBox.LinkClicked> 하는 이벤트에 대 한 이벤트 처리기를 작성 합니다.

    아래 예제에서 이벤트는 <xref:System.Windows.Forms.RichTextBox.LinkClicked> <xref:System.Windows.Forms.RichTextBox> 컨트롤의 <xref:System.Windows.Forms.RichTextBox.Text%2A> 속성에 지정 된 URL에 대 한 Internet Explorer의 인스턴스를 엽니다. 이 예에서는 폼에 <xref:System.Windows.Forms.RichTextBox> 컨트롤을 사용 한다고 가정 합니다.

    > [!IMPORTANT]
    > 권한이 부족 하 <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType> 여 부분 신뢰 컨텍스트에서 코드를 <xref:System.Security.SecurityException> 실행 하는 경우에는이 메서드를 호출할 때 예외가 발생 합니다. 자세한 내용은 [코드 액세스 보안 기본 사항](../../misc/code-access-security-basics.md)을 참조하세요.

    ```vb
    Public p As New System.Diagnostics.Process
    Private Sub RichTextBox1_LinkClicked _
       (ByVal sender As Object, ByVal e As _
       System.Windows.Forms.LinkClickedEventArgs) _
       Handles RichTextBox1.LinkClicked
          ' Call Process.Start method to open a browser
          ' with link text as URL.
          p = System.Diagnostics.Process.Start("IExplore.exe", e.LinkText)
    End Sub
    ```

    ```csharp
    public System.Diagnostics.Process p = new System.Diagnostics.Process();

    private void richTextBox1_LinkClicked(object sender,
    System.Windows.Forms.LinkClickedEventArgs e)
    {
       // Call Process.Start method to open a browser
       // with link text as URL.
       p = System.Diagnostics.Process.Start("IExplore.exe", e.LinkText);
    }
    ```

    ```cpp
    public:
       System::Diagnostics::Process ^ p;

    private:
       void richTextBox1_LinkClicked(System::Object ^  sender,
          System::Windows::Forms::LinkClickedEventArgs ^  e)
       {
          // Call Process.Start method to open a browser
          // with link text as URL.
          p = System::Diagnostics::Process::Start("IExplore.exe",
             e->LinkText);
       }
    ```

    (시각적 C++개체) 폼의 생성자에 `p`다음 문을 포함 하 여 수행할 수 있는 프로세스를 초기화 해야 합니다.

    ```cpp
    p = gcnew System::Diagnostics::Process();
    ```

    (시각적 C#개체, C++시각적 개체) 폼의 생성자에 다음 코드를 추가 하 여 이벤트 처리기를 등록 합니다.

    ```csharp
    this.richTextBox1.LinkClicked += new
       System.Windows.Forms.LinkClickedEventHandler
       (this.richTextBox1_LinkClicked);
    ```

    ```cpp
    this->richTextBox1->LinkClicked += gcnew
       System::Windows::Forms::LinkClickedEventHandler
       (this, &Form1::richTextBox1_LinkClicked);
    ```

    작업을 마친 후 만든 프로세스를 즉시 중지 하는 것이 중요 합니다. 위의 코드를 참조 하 여 프로세스를 중지 하는 코드는 다음과 같이 표시 될 수 있습니다.

    ```vb
    Public Sub StopWebProcess()
       p.Kill()
    End Sub
    ```

    ```csharp
    public void StopWebProcess()
    {
       p.Kill();
    }
    ```

    ```cpp
    public: void StopWebProcess()
    {
       p->Kill();
    }
    ```

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.RichTextBox.DetectUrls%2A>
- <xref:System.Windows.Forms.RichTextBox.LinkClicked>
- <xref:System.Windows.Forms.RichTextBox>
- [RichTextBox 컨트롤](richtextbox-control-windows-forms.md)
- [Windows Forms에 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)
