---
title: 데이터를 클립보드에 저장하고 클립보드에서 읽기(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Clipboard, storing data to (My.Computer.Clipboard)
- Clipboard, reading from (My.Computer.Clipboard)
- Clipboard
- My.Computer.Clipboard object, tasks
- data [Visual Basic], Clipboard
- reading data, from Clipboard
ms.assetid: f690119a-4378-4f7d-b20e-d9377ef49496
ms.openlocfilehash: d7693f6b5dc74e17686cd7d2667f32adbde9df80
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916513"
---
# <a name="storing-data-to-and-reading-from-the-clipboard-visual-basic"></a>데이터를 클립보드에 저장하고 클립보드에서 읽기(Visual Basic)
클립보드를 사용하여 텍스트 및 이미지와 같은 데이터를 저장할 수 있습니다. 클립보드는 모든 활성 프로세스에서 공유되기 때문에 프로세스 간에 데이터를 전송하는 데 사용할 수 있습니다. `My.Computer.Clipboard` 개체를 사용하면 클립보드에 쉽게 액세스하고 읽고 쓸 수 있습니다.  
  
## <a name="reading-from-the-clipboard"></a>클립보드에서 읽기  
 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.GetText%2A> 메서드를 사용하여 클립보드에 텍스트를 읽습니다. 다음 코드는 텍스트를 읽고 메시지 상자에 표시합니다. 예제가 제대로 실행되려면 클립보드에 텍스트가 저장되어 있어야 합니다.  
  
 [!code-vb[VbVbcnMyClipboard#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyClipboard/VB/Class1.vb#4)]  
  
 이 코드 예제는 IntelliSense 코드 조각으로 사용할 수도 있습니다. 코드 조각 선택에서 **Windows Forms 애플리케이션 &gt; 클립보드**에 있습니다. 자세한 내용은 [코드 조각](/visualstudio/ide/code-snippets)을 참조하세요.  
  
 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.GetImage%2A> 메서드를 사용하여 클립보드에서 이미지를 검색합니다. 이 예제에서는 이미지를 검색하고 `PictureBox1`에 할당하기 전에 클립보드에 이미지가 있는지 확인합니다.  
  
 [!code-vb[VbResourceTasks#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#16)]  
  
 이 코드 예제는 IntelliSense 코드 조각으로 사용할 수도 있습니다. 코드 조각 선택에서 **Windows Forms 애플리케이션 &gt; 클립보드**에 있습니다. 자세한 내용은 [코드 조각](/visualstudio/ide/code-snippets)을 참조하세요.  
  
 클립보드에 배치된 항목은 애플리케이션이 종료된 후에도 유지됩니다.  
  
## <a name="determining-the-type-of-file-stored-in-the-clipboard"></a>클립보드에 저장된 파일 형식 확인  
 클립보드의 데이터는 텍스트, 오디오 파일 또는 이미지와 같은 다양한 형태일 수 있습니다. 클립보드에 있는 파일의 종류를 확인하려는 경우 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsAudio%2A>, <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsFileDropList%2A>, <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsImage%2A>, <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsText%2A> 등의 메서드를 사용할 수 있습니다. 사용자 지정 형식을 확인하려는 경우에는 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.ContainsData%2A> 메서드를 사용할 수 있습니다.  
  
 `ContainsImage` 함수를 사용하여 클립보드에 포함된 데이터가 이미지인지 여부를 확인할 수 있습니다. 다음 코드는 데이터가 이미지인지 여부를 확인하고 그에 따라 보고합니다.  
  
 [!code-vb[VbResourceTasks#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#13)]  
  
## <a name="clearing-the-clipboard"></a>클립보드 지우기  
 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.Clear%2A> 메서드는 클립보드를 지웁니다. 클립보드가 다른 프로세스에서 공유되기 때문에 클립보드를 지우면 해당 프로세스에 영향을 줄 수 있습니다.  
  
 다음 코드에서는 `Clear` 메서드를 사용하는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbcnMyClipboard#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyClipboard/VB/Class1.vb#3)]  
  
## <a name="writing-to-the-clipboard"></a>클립보드에 쓰기  
 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.SetText%2A> 메서드를 사용하여 클립보드에 텍스트를 씁니다. 다음 코드는 클립보드에 "This is a test string" 문자열을 씁니다.  
  
 [!code-vb[VbVbcnMyClipboard#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyClipboard/VB/Class1.vb#1)]  
  
 `SetText` 메서드는 <xref:System.Windows.Forms.TextDataFormat> 형식을 포함하는 형식 매개 변수를 수락할 수 있습니다. 다음 코드는 클립보드에 "This is a test string" 문자열을 RTF 텍스트로 씁니다.  
  
 [!code-vb[VbVbcnMyClipboard#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyClipboard/VB/Class1.vb#2)]  
  
 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.SetData%2A> 메서드를 사용하여 클립보드에 데이터를 씁니다. 이 예제에서는 `DataObject` `dataChunk`를 사용자 지정 형식 `specialFormat`으로 클립보드에 씁니다.  
  
 [!code-vb[VbVbcnMyClipboard#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyClipboard/VB/Class1.vb#7)]  
  
 <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.SetAudio%2A> 메서드를 사용하여 클립보드에 오디오 데이터를 씁니다. 이 예제에서는 바이트 배열 `musicReader`를 만들고, `cool.wav` 파일을 배열로 읽어온 다음 클립보드에 씁니다.  
  
 [!code-vb[VbResourceTasks#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#5)]  
  
> [!IMPORTANT]
> 다른 사용자가 클립보드에 액세스할 수 있기 때문에 클립보드를 사용하여 암호 또는 기밀 데이터와 같은 중요한 정보를 저장하지 마세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy>
- <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.GetAudioStream%2A>
- <xref:Microsoft.VisualBasic.MyServices.ClipboardProxy.SetDataObject%2A>
- [방법: XML 파일에서 개체 데이터 읽기](../../../programming-guide/concepts/serialization/how-to-read-object-data-from-an-xml-file.md)
- [방법: XML 파일에 개체 데이터 쓰기](../../../programming-guide/concepts/serialization/how-to-write-object-data-to-an-xml-file.md)
