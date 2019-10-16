---
title: My.Application, My.Computer 및 My.User를 사용한 작업 수행(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- My.Application object [Visual Basic], developing applications
- rapid application development (RAD), My.Application
- rapid application development (RAD), My.Computer
- rapid application development (RAD), My.User
- My.Computer object [Visual Basic], developing applications
- My.User object [Visual Basic], developing applications
ms.assetid: c8af61bd-4dd3-4a0f-9af5-795b594b240b
ms.openlocfilehash: 0372fbf63f6d12e266674f92225183911aa4ca30
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62014130"
---
# <a name="performing-tasks-with-myapplication-mycomputer-and-myuser-visual-basic"></a>My.Application, My.Computer 및 My.User를 사용한 작업 수행(Visual Basic)
세 개의 핵심 `My` 액세스 정보 및 일반적으로 사용 되는 기능을 제공 하는 개체가 `My.Application` (<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>), `My.Computer` (<xref:Microsoft.VisualBasic.Devices.Computer>), 및 `My.User` (<xref:Microsoft.VisualBasic.ApplicationServices.User>). 현재 응용 프로그램, 응용 프로그램에 설치 된 컴퓨터 또는 응용 프로그램의 현재 사용자에 관련 된 정보를 각각 액세스 하려면 이러한 개체를 사용할 수 있습니다.  
  
## <a name="myapplication-mycomputer-and-myuser"></a>My.Application, My.Computer 및 My.User  
 다음 예제에서는 정보 수 있는 방법을 보여 줍니다. 사용 하 여 검색할 `My`합니다.  
  
 [!code-vb[VbVbcnMy#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#1)]  
  
 [!code-vb[VbVbcnMy#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#2)]  
  
 정보를 검색 하는 것 외에도 이러한 세 가지 개체를 통해 노출 되는 멤버를 허용 하는 개체와 관련 된 메서드를 실행할 수 있습니다도 합니다. 예를 들어, 다양 한 파일을 조작 하거나 레지스트리를 통해 업데이트 하는 방법에 액세스할 수 있습니다 `My.Computer`합니다.  
  
 파일 I/O가 훨씬 쉽고 빠릅니다 `My`, 다양 한 파일, 디렉터리 및 드라이브를 조작 하기 위한 속성과 메서드를 포함 하는 합니다. <xref:Microsoft.VisualBasic.FileIO.TextFieldParser> 개체를 구분 하는 대규모 구조화 된 파일 또는 고정 너비 필드에서 읽을 수 있습니다. 이 예제에서는 합니다 `TextFieldParser` `reader` 에서 읽기를 사용 하 여 `C:\TestFolder1\test1.txt`입니다.  
  
 [!code-vb[VbVbalrTextFieldParser#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTextFieldParser/VB/Class1.vb#23)]  
  
 `My.Application` 응용 프로그램에 대 한 문화권을 변경할 수 있습니다. 다음 예제에서는이 메서드를 호출할 수 있습니다 하는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbcnMy#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#3)]  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>
- <xref:Microsoft.VisualBasic.Devices.Computer>
- <xref:Microsoft.VisualBasic.ApplicationServices.User>
- [My가 프로젝트 형식에 의존하는 방식](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)
