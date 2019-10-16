---
title: '방법: Visual Basic에서 직렬 포트에 연결된 모뎀 전화 접속'
ms.date: 07/20/2015
helpviewer_keywords:
- modems [Visual Basic], dialing
- serial ports [Visual Basic], dialing
- My.Computer.Ports object
ms.assetid: 3834db40-f431-45f1-b671-dc91787164b6
ms.openlocfilehash: db482af7750012d8805d4f834063a2c82224cf67
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59337034"
---
# <a name="how-to-dial-modems-attached-to-serial-ports-in-visual-basic"></a>방법: Visual Basic에서 직렬 포트에 연결된 모뎀 전화 접속
이 항목에서는 Visual Basic에서 `My.Computer.Ports`를 사용하여 모뎀으로 전화를 거는 방법을 설명합니다.  
  
 일반적으로 모뎀은 컴퓨터의 직렬 포트 중 하나에 연결되어 있습니다. 애플리케이션이 모뎀과 통신하려면 적절한 직렬 포트로 명령을 보내야 합니다.  
  
### <a name="to-dial-a-modem"></a>모뎀으로 전화를 걸려면  
  
1. 모뎀이 연결된 직렬 포트를 확인합니다. 이 예제에서는 모뎀이 COM1에 있다고 가정합니다.  
  
2. `My.Computer.Ports.OpenSerialPort` 메서드를 사용하여 포트에 대한 참조를 가져옵니다. 자세한 내용은 <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A>을 참조하세요.  
  
     `Using` 블록을 사용하면 예외를 생성하는 경우 애플리케이션이 직렬 포트를 닫을 수 있습니다. 직렬 포트를 조작하는 모든 코드는 이 블록 안이나 `Try...Catch...Finally` 블록 안에 표시되어야 합니다.  
  
     [!code-vb[VbVbalrMyComputer#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#28)]  
  
3. `DtrEnable` 속성을 설정하여 컴퓨터가 모뎀에서 들어오는 전송을 받을 준비가 되었음을 나타냅니다.  
  
     [!code-vb[VbVbalrMyComputer#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#29)]  
  
4. <xref:System.IO.Ports.SerialPort.Write%2A> 메서드를 사용하여 직렬 포트를 통해 전화 걸기 명령과 전화 번호를 모뎀으로 보냅니다.  
  
     [!code-vb[VbVbalrMyComputer#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#30)]  
  
## <a name="example"></a>예제  
 [!code-vb[VbVbalrMyComputer#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#27)]  
  
 이 코드 예제는 IntelliSense 코드 조각으로 사용할 수도 있습니다. 코드 조각 선택에서는 **연결 및 네트워킹**에 있습니다. 자세한 내용은 [코드 조각](/visualstudio/ide/code-snippets)을 참조하세요.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에서는 <xref:System?displayProperty=nameWithType> 네임스페이스에 대한 참조가 필요합니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 이 예제에서는 모뎀이 COM1에 연결되어 있다고 가정합니다. 코드에서 사용자가 사용 가능한 포트 목록에서 원하는 직렬 포트를 선택할 수 있도록 하는 것이 좋습니다. 자세한 내용은 [방법: 사용 가능한 직렬 포트 표시](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md)를 참조하세요.  
  
 이 예제에서는 `Using` 블록을 사용하여 예외가 throw되는 경우에도 애플리케이션이 포트를 닫도록 합니다. 자세한 내용은 [using 문](../../../../visual-basic/language-reference/statements/using-statement.md)을 참조하세요.  
  
 이 예제에서 애플리케이션은 모뎀으로 전화를 건 후 직렬 포트의 연결을 끊습니다. 현실적으로 모뎀과 데이터를 주고받으려 합니다. 자세한 내용은 [방법: 직렬 포트에서 문자열 받기](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-receive-strings-from-serial-ports.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.Devices.Ports>
- <xref:System.IO.Ports.SerialPort?displayProperty=nameWithType>
- [방법: 직렬 포트로 문자열 보내기](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-send-strings-to-serial-ports.md)
- [방법: 직렬 포트에서 문자열 받기](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-receive-strings-from-serial-ports.md)
- [방법: 사용 가능한 직렬 포트 표시](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md)
