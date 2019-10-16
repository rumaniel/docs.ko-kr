---
title: '방법: Windows Forms에 컨트롤 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Windows Forms controls, adding to form
- controls [Windows Forms], adding
ms.assetid: 2af86001-9d62-4154-87fb-66db2c3cd9fd
ms.openlocfilehash: bfe9449ecc862c361719d27dba2f5ed9af563957
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046060"
---
# <a name="how-to-add-controls-to-windows-forms"></a>방법: Windows Forms에 컨트롤 추가

대부분의 폼은 UI (사용자 인터페이스)를 정의 하기 위해 폼의 화면에 컨트롤을 추가 하 여 디자인 되었습니다. *컨트롤* 은 정보를 표시 하거나 사용자 입력을 수락 하는 데 사용 되는 폼의 구성 요소입니다. 컨트롤에 대 한 자세한 내용은 [Windows Forms controls](index.md)을 참조 하세요.

## <a name="to-draw-a-control-on-a-form"></a>폼에 컨트롤을 그리려면

1. 양식을 엽니다. 자세한 내용은 [방법: 디자이너](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w5yd62ts(v=vs.100))에 Windows Forms를 표시 합니다.

2. **도구 상자**에서 폼에 추가 하려는 컨트롤을 클릭 합니다.

3. 폼에서 컨트롤의 왼쪽 위 모퉁이를 배치할 위치를 클릭 하 고 컨트롤의 오른쪽 아래 모퉁이를 배치할 위치를 끕니다.

    지정 된 위치와 크기를 사용 하 여 컨트롤이 폼에 추가 됩니다.

    > [!NOTE]
    > 각 컨트롤에는 기본 크기가 정의 되어 있습니다. 컨트롤을 **도구 상자** 에서 폼으로 끌어서 컨트롤의 기본 크기로 폼에 추가할 수 있습니다.

## <a name="to-drag-a-control-to-a-form"></a>컨트롤을 폼으로 끌려면

1. 양식을 엽니다. 자세한 내용은 [방법: 디자이너](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w5yd62ts(v=vs.100))에 Windows Forms를 표시 합니다.

2. **도구 상자**에서 원하는 컨트롤을 클릭 하 여 폼으로 끕니다.

    컨트롤이 기본 크기의 지정 된 위치에 폼에 추가 됩니다.

    > [!NOTE]
    > **도구 상자** 에서 컨트롤을 두 번 클릭 하 여 기본 크기로 폼의 왼쪽 위 모퉁이에 추가할 수 있습니다.

    런타임에 컨트롤을 폼에 동적으로 추가할 수도 있습니다. 다음 코드 예제 <xref:System.Windows.Forms.TextBox> 에서는 컨트롤을 클릭할 <xref:System.Windows.Forms.Button> 때 폼에 컨트롤이 추가 됩니다.

    > [!NOTE]
    > 다음 절차를 수행 하려면 **단추** 컨트롤이 `Button1`있는 폼이 이미 배치 되어 있어야 합니다.

## <a name="to-add-a-control-to-a-form-programmatically"></a>프로그래밍 방식으로 폼에 컨트롤을 추가 하려면

1. 폼의 클래스 내에서 단추의 `Click` 이벤트를 처리 하는 메서드에서 다음과 비슷한 코드를 삽입 하 여 컨트롤 변수에 대 한 참조를 추가 하 고 컨트롤의 `Location`를 설정 하 고 컨트롤을 추가 합니다.

    ```vb
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
       Dim MyText As New TextBox()
       MyText.Location = New Point(25, 25)
       Me.Controls.Add(MyText)
    End Sub
    ```

    ```csharp
    private void button1_Click(object sender, System.EventArgs e)
    {
       TextBox myText = new TextBox();
       myText.Location = new Point(25,25);
       this.Controls.Add (myText);
    }
    ```

    ```cpp
    private:
      System::Void button1_Click(System::Object ^  sender,
        System::EventArgs ^  e)
      {
        TextBox ^ myText = gcnew TextBox();
        myText->Location = Point(25,25);
        this->Controls->Add(myText);
      }
    ```

    > [!NOTE]
    > 컨트롤의 다른 속성을 초기화 하는 코드를 추가할 수도 있습니다.

    > [!IMPORTANT]
    > 악의적인 `UserControl`을 참조 하 여 네트워크를 통해 로컬 컴퓨터를 보안 위험에 노출 시킬 수 있습니다. 악의적인 사용자가 손상 된 사용자 지정 컨트롤을 만든 다음 실수로 프로젝트에 추가 하는 경우에만이 문제가 발생 합니다.

## <a name="see-also"></a>참고자료

- [Windows Forms 컨트롤](index.md)
- [방법: Windows Forms에서 컨트롤 크기 조정](how-to-resize-controls-on-windows-forms.md)
- [방법: Windows Forms 컨트롤에 표시 되는 텍스트 설정](how-to-set-the-text-displayed-by-a-windows-forms-control.md)
- [Windows Forms에 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)
