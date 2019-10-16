---
title: '방법: Windows Forms LinkLabel 컨트롤을 사용하여 개체 또는 웹 페이지에 연결'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], LinkLabel control
- Windows Forms, linking to objects
- Web page link control
- linking [Windows Forms], to other forms
- Windows Forms, linking to Web pages
- links [Windows Forms], to other forms
- LinkLabel control [Windows Forms], linking to object or Web page
- LinkLabel control [Windows Forms], examples
ms.assetid: 6c91c975-3cb7-4504-82f0-fc6255f8fb85
ms.openlocfilehash: cd9c53527429dfc3e7156c4023b52509452b96cd
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046247"
---
# <a name="how-to-link-to-an-object-or-web-page-with-the-windows-forms-linklabel-control"></a>방법: Windows Forms LinkLabel 컨트롤을 사용하여 개체 또는 웹 페이지에 연결

Windows Forms <xref:System.Windows.Forms.LinkLabel> 컨트롤을 사용 하면 폼에 웹 스타일 링크를 만들 수 있습니다. 링크를 클릭 하면 링크를 방문한 것을 나타내도록 색을 변경할 수 있습니다. 색 변경에 대 한 자세한 내용은 [방법: Windows Forms LinkLabel 컨트롤](how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)의 모양을 변경 합니다.

## <a name="linking-to-another-form"></a>다른 폼에 연결

#### <a name="to-link-to-another-form-with-a-linklabel-control"></a>LinkLabel 컨트롤을 사용 하 여 다른 폼에 연결 하려면

1. <xref:System.Windows.Forms.LinkLabel.Text%2A> 속성을 적절 한 캡션으로 설정 합니다.

2. <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 속성을 설정 하 여 링크로 나타낼 캡션 부분을 결정 합니다. 표시 되는 방법은 링크 레이블의 모양 관련 속성에 따라 달라 집니다. 값은 두 개의 숫자, <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 시작 문자 위치 및 문자 수를 포함 하는 개체로 표현 됩니다. <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 속성 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 은 다음과 같은 방법으로 속성 창 또는 코드에서 설정할 수 있습니다.

    ```vb
    ' In this code example, the link area has been set to begin
    ' at the first character and extend for eight characters.
    ' You may need to modify this based on the text entered in Step 1.
    LinkLabel1.LinkArea = New LinkArea(0, 8)
    ```

    ```csharp
    // In this code example, the link area has been set to begin
    // at the first character and extend for eight characters.
    // You may need to modify this based on the text entered in Step 1.
    linkLabel1.LinkArea = new LinkArea(0,8);
    ```

    ```cpp
    // In this code example, the link area has been set to begin
    // at the first character and extend for eight characters.
    // You may need to modify this based on the text entered in Step 1.
    linkLabel1->LinkArea = LinkArea(0,8);
    ```

3. 이벤트 처리기에서 <xref:System.Windows.Forms.Form.Show%2A> 메서드를 호출 하 여 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> 프로젝트에서 다른 폼을 열고 속성을로 `true`설정 합니다. <xref:System.Windows.Forms.LinkLabel.LinkClicked>

    > [!NOTE]
    > <xref:System.Windows.Forms.LinkLabelLinkClickedEventArgs> 클래스의 인스턴스는 클릭 한 <xref:System.Windows.Forms.LinkLabel> 컨트롤에 대 한 참조를 전달 하므로 `sender` 개체를 캐스팅할 필요가 없습니다.

    ```vb
    Protected Sub LinkLabel1_LinkClicked(ByVal Sender As System.Object, _
       ByVal e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) _
       Handles LinkLabel1.LinkClicked
       ' Show another form.
       Dim f2 As New Form()
       f2.Show
       LinkLabel1.LinkVisited = True
    End Sub
    ```

    ```csharp
    protected void linkLabel1_LinkClicked(object sender, System. Windows.Forms.LinkLabelLinkClickedEventArgs e)
    {
       // Show another form.
       Form f2 = new Form();
       f2.Show();
       linkLabel1.LinkVisited = true;
    }
    ```

    ```cpp
    private:
       void linkLabel1_LinkClicked(System::Object ^  sender,
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)
       {
          // Show another form.
          Form ^ f2 = new Form();
          f2->Show();
          linkLabel1->LinkVisited = true;
       }
    ```

## <a name="linking-to-a-web-page"></a>웹 페이지에 연결

컨트롤 <xref:System.Windows.Forms.LinkLabel> 은 기본 브라우저를 사용 하 여 웹 페이지를 표시 하는 데에도 사용할 수 있습니다.

#### <a name="to-start-internet-explorer-and-link-to-a-web-page-with-a-linklabel-control"></a>Internet Explorer를 시작 하 고 LinkLabel 컨트롤을 사용 하 여 웹 페이지에 연결 하려면

1. <xref:System.Windows.Forms.LinkLabel.Text%2A> 속성을 적절 한 캡션으로 설정 합니다.

2. <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 속성을 설정 하 여 링크로 나타낼 캡션 부분을 결정 합니다.

3. 이벤트 처리기에서 예외 처리 블록 중간 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> 에 <xref:System.Diagnostics.Process.Start%2A> 속성을로 `true` 설정 하 고 메서드를 사용 하 여 URL로 기본 브라우저를 시작 하는 두 번째 프로시저를 호출 합니다. <xref:System.Windows.Forms.LinkLabel.LinkClicked> <xref:System.Diagnostics.Process.Start%2A> 메서드를 사용 하려면 <xref:System.Diagnostics?displayProperty=nameWithType> 네임 스페이스에 대 한 참조를 추가 해야 합니다.

    > [!IMPORTANT]
    > 아래 코드를 공유 드라이브 등의 부분 신뢰 환경에서 실행 하는 경우 `VisitLink` 메서드가 호출 될 때 JIT 컴파일러가 실패 합니다. `System.Diagnostics.Process.Start` 문은 링크 요청이 실패 하는 원인이 됩니다. 다음 코드는 `VisitLink` 메서드를 호출할 때 예외를 catch 하 여 JIT 컴파일러에 오류가 발생 하는 경우 오류를 정상적으로 처리 하는지 확인 합니다.

    ```vb
    Private Sub LinkLabel1_LinkClicked(ByVal sender As System.Object, _
       ByVal e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) _
       Handles LinkLabel1.LinkClicked
       Try
          VisitLink()
       Catch ex As Exception
          ' The error message
          MessageBox.Show("Unable to open link that was clicked.")
       End Try
    End Sub

    Sub VisitLink()
       ' Change the color of the link text by setting LinkVisited
       ' to True.
       LinkLabel1.LinkVisited = True
       ' Call the Process.Start method to open the default browser
       ' with a URL:
       System.Diagnostics.Process.Start("http://www.microsoft.com")
    End Sub
    ```

    ```csharp
    private void linkLabel1_LinkClicked(object sender, System.Windows.Forms.LinkLabelLinkClickedEventArgs e)
    {
       try
       {
          VisitLink();
       }
       catch (Exception ex )
       {
          MessageBox.Show("Unable to open link that was clicked.");
       }
    }

    private void VisitLink()
    {
       // Change the color of the link text by setting LinkVisited
       // to true.
       linkLabel1.LinkVisited = true;
       //Call the Process.Start method to open the default browser
       //with a URL:
       System.Diagnostics.Process.Start("http://www.microsoft.com");
    }
    ```

    ```cpp
    private:
       void linkLabel1_LinkClicked(System::Object ^  sender,
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)
       {
          try
          {
             VisitLink();
          }
          catch (Exception ^ ex)
          {
             MessageBox::Show("Unable to open link that was clicked.");
          }
       }
    private:
       void VisitLink()
       {
          // Change the color of the link text by setting LinkVisited
          // to true.
          linkLabel1->LinkVisited = true;
          // Call the Process.Start method to open the default browser
          // with a URL:
          System::Diagnostics::Process::Start("http://www.microsoft.com");
       }
    ```

## <a name="see-also"></a>참고자료

- <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType>
- [LinkLabel 컨트롤 개요](linklabel-control-overview-windows-forms.md)
- [방법: Windows Forms LinkLabel 컨트롤의 모양 변경](how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)
- [LinkLabel 컨트롤](linklabel-control-windows-forms.md)
