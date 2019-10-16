---
title: '방법: Visual Basic에서 사용할 수 있는 직렬 포트 표시'
ms.date: 07/20/2015
helpviewer_keywords:
- serial ports, availability
- My.Computer.Ports.SerialPortNames property
- My.Computer.Ports object
- ports, serial port availability
ms.assetid: eaf2ee5a-8103-4e10-a205-ed1d4db120ba
ms.openlocfilehash: e8e0f6d63f7135c3bbe24ee6426cd714f2eb275f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956917"
---
# <a name="how-to-show-available-serial-ports-in-visual-basic"></a>방법: Visual Basic에서 사용할 수 있는 직렬 포트 표시
이 항목에서는 Visual Basic에서 `My.Computer.Ports`를 사용하여 컴퓨터에서 사용 가능한 직렬 포트를 보여 주는 방법을 설명합니다.  
  
 사용자가 사용할 포트를 선택할 수 있도록 직렬 포트의 이름이 <xref:System.Windows.Forms.ListBox>에 배치됩니다.  
  
## <a name="example"></a>예  
 이 예제에서는 `My.Computer.Ports.SerialPortNames` 속성이 반환하는 모든 문자열을 반복합니다. 이러한 문자열은 컴퓨터에서 사용할 수 있는 직렬 포트의 이름입니다.  
  
 일반적으로 사용자는 사용 가능한 포트 목록에서 애플리케이션이 사용해야 하는 직렬 포트를 선택합니다. 이 예제에서 직렬 포트 이름은 <xref:System.Windows.Forms.ListBox> 컨트롤에 저장됩니다. 자세한 내용은 [ListBox 컨트롤](../../../../framework/winforms/controls/listbox-control-windows-forms.md)을 참조하세요.  
  
 [!code-vb[VbVbalrMyComputer#45](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#45)]  
  
 이 코드 예제는 IntelliSense 코드 조각으로 사용할 수도 있습니다. 코드 조각 선택에서는 **연결 및 네트워킹**에 있습니다. 자세한 내용은 [코드 조각](/visualstudio/ide/code-snippets)을 참조하세요.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System.Windows.Forms.dll에 대한 프로젝트 참조  
  
- <xref:System.Windows.Forms> 네임스페이스의 멤버에 대한 액세스 권한. 코드에서 멤버 이름을 정규화하지 않는 경우 `Imports` 문을 추가합니다. 자세한 내용은 [Imports 문(.NET 네임스페이스 및 형식)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)을 참조하세요.  
  
- `ListBox1`이라는 <xref:System.Windows.Forms.ListBox> 컨트롤이 폼에 있어야 함  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 사용 가능한 직렬 포트 이름을 표시하기 위해 <xref:System.Windows.Forms.ListBox> 컨트롤을 사용할 필요는 없습니다. 대신 <xref:System.Windows.Forms.ComboBox> 또는 기타 컨트롤을 사용할 수 있습니다. 애플리케이션에 사용자 응답이 필요하지 않은 경우 <xref:System.Windows.Forms.TextBox> 컨트롤을 사용하여 정보를 표시할 수 있습니다.  
  
> [!NOTE]
> Windows 98에서 실행하는 경우 `My.Computer.Ports.SerialPortNames`에서 반환되는 포트 이름이 부정확할 수 있습니다. 애플리케이션 오류를 방지하려면 포트 이름을 사용하여 포트를 열 때 `Try...Catch...Finally` 문 또는 `Using` 문과 같은 예외 처리를 사용합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.Devices.Ports>
- [방법: 직렬 포트에 연결된 모뎀 전화 접속](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-dial-modems-attached-to-serial-ports.md)
- [방법: 직렬 포트로 문자열 보내기](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-send-strings-to-serial-ports.md)
- [방법: 직렬 포트에서 문자열 받기](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-receive-strings-from-serial-ports.md)
