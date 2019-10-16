---
title: '방법: Windows Forms 컨트롤에서 표시하는 텍스트 설정'
ms.date: 08/20/2019
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Windows Forms, captions
- Button control [Windows Forms], button text
- StdFont object and CommandButton caption
- captions [Windows Forms], Windows Forms controls
- Text property [Windows Forms], Windows Forms control
- Button control [Windows Forms], text display
- labels [Windows Forms], adding to CommandButton control
- buttons [Windows Forms], text
- captions [Windows Forms], setting
- text
- examples [Windows Forms], controls
- text [Windows Forms], Windows Forms controls
- controls [Windows Forms], captions
- forms [Windows Forms], captions
ms.assetid: 36b95bff-8780-479d-b86a-f1a0673653aa
ms.openlocfilehash: 887aa5ec9b97770903cd87459d6df5adc3f7ddf0
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666150"
---
# <a name="how-to-set-the-text-displayed-by-a-windows-forms-control"></a>방법: Windows Forms 컨트롤에 표시 되는 텍스트 설정

Windows Forms 컨트롤은 일반적으로 컨트롤의 기본 함수와 관련 된 일부 텍스트를 표시 합니다. 예를 들어, <xref:System.Windows.Forms.Button> 컨트롤은 일반적으로 단추를 클릭 하는 경우 수행할 동작을 나타내는 캡션을 표시 합니다. 모든 컨트롤에 대해 <xref:System.Windows.Forms.Control.Text%2A> 속성을 사용하여 텍스트를 설정하거나 반환할 수 있습니다. <xref:System.Windows.Forms.Control.Font%2A> 속성을 사용하여 글꼴을 변경할 수 있습니다.

[디자이너](#designer)를 사용 하 여 텍스트를 설정할 수도 있습니다.

## <a name="programmatic"></a>기능의

1. <xref:System.Windows.Forms.Control.Text%2A> 속성을 문자열로 설정합니다.

   밑줄이 그어진 액세스 키를 만들기 위해에는 선택 키가 될 문자 앞에 앰퍼샌드 (&)가 포함 됩니다.

2. <xref:System.Windows.Forms.Control.Font%2A> 속성을 <xref:System.Drawing.Font> 형식의 개체로 설정합니다.

    ```vb
    Button1.Text = "Click here to save changes"
    Button1.Font = New Font("Arial", 10, FontStyle.Bold, GraphicsUnit.Point)
    ```

    ```csharp
    button1.Text = "Click here to save changes";
    button1.Font = new Font("Arial", 10, FontStyle.Bold, GraphicsUnit.Point);
    ```

    ```cpp
    button1->Text = "Click here to save changes";
    button1->Font = new System::Drawing::Font("Arial", 10, FontStyle::Bold, GraphicsUnit::Point);
    ```

    > [!NOTE]
    > 이스케이프 문자를 사용하여 일반적으로 다르게 해석하는 메뉴 항목과 같은 사용자 인터페이스 요소에 특수 문자를 표시할 수 있습니다. 예를 들어 다음 코드 줄은 메뉴 항목의 텍스트를 "& 이제 완전히 다른 항목을 읽도록" 설정 합니다.

    ```vb
    MPMenuItem.Text = "&& Now For Something Completely Different"
    ```

    ```csharp
    mpMenuItem.Text = "&& Now For Something Completely Different";
    ```

    ```cpp
    mpMenuItem->Text = "&& Now For Something Completely Different";
    ```

## <a name="designer"></a>Designer

1. Visual Studio의 **속성** 창에서 컨트롤의 **Text** 속성을 적절 한 문자열로 설정 합니다.

   밑줄이 있는 바로 가기 키를 만들려면 바로 가기 키가 될 문자 앞에 앰퍼샌드 (&)를 포함 합니다.

2. **속성** 창의 **Font** 속성 옆에 있는 줄임표 단추 (![Visual Studio](./media/visual-studio-ellipsis-button.png)속성 창)에서 줄임표 단추 (...)를 선택 합니다.

   표준 글꼴 대화 상자에서 글꼴, 글꼴 스타일, 크기, 효과 (취소선 또는 밑줄 등) 및 원하는 스크립트를 선택 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Control.Text%2A?displayProperty=nameWithType>
- [방법: Windows Forms 컨트롤에 대 한 선택 키 만들기](how-to-create-access-keys-for-windows-forms-controls.md)
- [방법: Windows Forms 단추 클릭에 응답](how-to-respond-to-windows-forms-button-clicks.md)
