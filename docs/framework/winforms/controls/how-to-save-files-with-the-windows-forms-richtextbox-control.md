---
title: '방법: Windows Forms RichTextBox 컨트롤을 사용하여 파일 저장'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- saving files
- RTF files [Windows Forms], saving in RichTextBox control
- examples [Windows Forms], text boxes
- saving files [Windows Forms], RichTextBox control
- files [Windows Forms], saving with RichTextBox control
- RichTextBox control [Windows Forms], saving files
- .rtf files [Windows Forms], saving in RichTextBox control
- text files [Windows Forms], saving from RichTextBox control
ms.assetid: 4a58ec19-84d1-4383-9110-298c06adcfca
ms.openlocfilehash: c5d88e4942d96ee12e8b9f40156090c874386668
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046260"
---
# <a name="how-to-save-files-with-the-windows-forms-richtextbox-control"></a>방법: Windows Forms RichTextBox 컨트롤을 사용하여 파일 저장

Windows Forms <xref:System.Windows.Forms.RichTextBox> 컨트롤은 다음과 같은 여러 형식 중 하나로 표시 되는 정보를 쓸 수 있습니다.

- 일반 텍스트

- 유니코드 일반 텍스트

- RTF (서식 있는 텍스트)

- OLE 개체 대신 공백을 사용 하는 RTF

- OLE 개체의 텍스트 표현을 포함 하는 일반 텍스트

파일을 저장 하려면 <xref:System.Windows.Forms.RichTextBox.SaveFile%2A> 메서드를 호출 합니다. **SaveFile** 메서드를 사용 하 여 데이터를 스트림에 저장할 수도 있습니다. 자세한 내용은 <xref:System.Windows.Forms.RichTextBox.SaveFile%28System.IO.Stream%2CSystem.Windows.Forms.RichTextBoxStreamType%29>을 참조하세요.

### <a name="to-save-the-contents-of-the-control-to-a-file"></a>컨트롤의 내용을 파일에 저장 하려면

1. 저장할 파일의 경로를 결정 합니다.

    실제 응용 프로그램에서이 작업을 수행 하려면 일반적으로 <xref:System.Windows.Forms.SaveFileDialog> 구성 요소를 사용 합니다. 개요는 [Savefiledialog 구성 요소 개요](savefiledialog-component-overview-windows-forms.md)를 참조 하세요.

2. 저장할 파일 <xref:System.Windows.Forms.RichTextBox.SaveFile%2A> 및 선택적으로 <xref:System.Windows.Forms.RichTextBox> 파일 형식을 지정 하 여 컨트롤의 메서드를 호출 합니다. 파일 이름을 유일한 인수로 사용 하 여 메서드를 호출 하는 경우 파일은 RTF로 저장 됩니다. 다른 파일 형식을 지정하려면 <xref:System.Windows.Forms.RichTextBoxStreamType> 열거형의 값을 두 번째 인수로 사용하여 메서드를 호출합니다.

    아래 예제에서 서식 있는 텍스트 파일의 위치에 대해 설정 된 경로는 **내 문서** 폴더입니다. 이 위치는 Windows 운영 체제를 실행 하는 대부분의 컴퓨터에이 폴더가 포함 된다고 가정할 수 있으므로 사용 됩니다. 이 위치를 선택 하면 최소한의 시스템 액세스 수준을 가진 사용자도 응용 프로그램을 안전 하 게 실행할 수 있습니다. 아래 예제에서는 <xref:System.Windows.Forms.RichTextBox> 컨트롤이 이미 추가 된 폼을 가정 합니다.

    ```vb
    Public Sub SaveFile()
       ' You should replace the bold file name in the
       ' sample below with a file name of your own choosing.
       RichTextBox1.SaveFile(System.Environment.GetFolderPath _
       (System.Environment.SpecialFolder.Personal) _
       & "\Testdoc.rtf", _
          RichTextBoxStreamType.RichNoOleObjs)
    End Sub
    ```

    ```csharp
    public void SaveFile()
    {
       // You should replace the bold file name in the
       // sample below with a file name of your own choosing.
       // Note the escape character used (@) when specifying the path.
       richTextBox1.SaveFile(System.Environment.GetFolderPath
       (System.Environment.SpecialFolder.Personal)
       + @"\Testdoc.rtf",
          RichTextBoxStreamType.RichNoOleObjs);
    }
    ```

    ```cpp
    public:
       void SaveFile()
       {
          // You should replace the bold file name in the
          // sample below with a file name of your own choosing.
          richTextBox1->SaveFile(String::Concat
             (System::Environment::GetFolderPath
             (System::Environment::SpecialFolder::Personal),
             "\\Testdoc.rtf"), RichTextBoxStreamType::RichNoOleObjs);
       }
    ```

    > [!IMPORTANT]
    > 이 예제에서는 파일이 아직 없는 경우 새 파일을 만듭니다. 응용 프로그램에서 파일을 만들어야 하는 경우 해당 응용 프로그램에 폴더에 대 한 만들기 권한이 있어야 합니다. 권한은 액세스 제어 목록을 사용하여 설정됩니다. 파일이 이미 있는 경우 응용 프로그램은 낮은 권한인 쓰기 액세스만 있으면 됩니다. 가능 하면 배포 중에 파일을 만드는 것이 더 안전 하며, 폴더에 대 한 액세스를 만드는 대신 단일 파일에 대 한 읽기 권한만 부여 합니다. 또한 루트 폴더나 Program Files 폴더보다 사용자 폴더에 데이터를 쓰는 것이 더 안전합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.RichTextBox.SaveFile%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.RichTextBox>
- [RichTextBox 컨트롤](richtextbox-control-windows-forms.md)
- [Windows Forms에 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)
