---
title: 개체(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- objects [Visual Basic]
ms.assetid: 651c73e4-dca8-402b-9c6b-e3902b3a3f4b
ms.openlocfilehash: 8852a3daa3cd3891d5053cc1fffe19fa310125de
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65880716"
---
# <a name="objects-visual-basic"></a>개체(Visual Basic)
이 항목에서는 Visual Basic 런타임 개체를 설명하고 멤버 프로시저, 속성 및 이벤트 테이블을 포함하는 기타 항목의 링크를 제공합니다.  
  
## <a name="visual-basic-run-time-objects"></a>Visual Basic 런타임 개체  
  
|||  
|---|---|  
|<xref:Microsoft.VisualBasic.Collection>|항목의 관련 그룹을 단일 개체로 표시하는 편리한 방법을 제공합니다.|  
|<xref:Microsoft.VisualBasic.Information.Err%2A>|런타임 오류에 대한 정보를 포함합니다.|  
|`My.Application` 개체는 다음 클래스로 구성됩니다.<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>는 모든 프로젝트에서 사용 가능한 멤버를 제공합니다.<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>는 Windows Forms 응용 프로그램에서 사용 가능한 멤버를 제공합니다.<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase>는 콘솔 응용 프로그램에서 사용 가능한 멤버를 제공합니다.|현재 애플리케이션 또는 DLL과 연결된 데이터만 제공합니다. 시스템 수준 정보는 `My.Application`을 사용하여 변경할 수 없습니다.<br /><br /> 일부 멤버는 Windows Forms 또는 콘솔 애플리케이션에만 사용할 수 있습니다.|  
|`My.Application.Info` (<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Info%2A>)|버전 번호, 설명, 로드된 어셈블리와 같은 애플리케이션에 대한 정보를 가져오기 위한 속성을 제공합니다.|  
|`My.Application.Log` (<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Log%2A>)|애플리케이션의 로그 수신기에 이벤트 및 예외 정보를 쓸 수 있는 속성 및 메서드를 제공합니다.|  
|`My.Computer` (<xref:Microsoft.VisualBasic.Devices.Computer>)|오디오, 시계, 키보드, 파일 시스템과 같은 컴퓨터 구성 요소를 조작하기 위한 속성을 제공합니다.|  
|`My.Computer.Audio` (<xref:Microsoft.VisualBasic.Devices.Audio>)|소리를 재생하기 위한 메서드를 제공합니다.|  
|`My.Computer.Clipboard` (<xref:Microsoft.VisualBasic.Devices.Computer.Clipboard%2A>)|클립보드를 조작하기 위한 메서드를 제공합니다.|  
|`My.Computer.Clock` (<xref:Microsoft.VisualBasic.Devices.Clock>)|시스템 시계에서 현재 현지 시간 및 협정 세계시(그리니치 표준시와 같음)에 액세스하기 위한 속성을 제공합니다.|  
|`My.Computer.FileSystem` (<xref:Microsoft.VisualBasic.FileIO.FileSystem>)|드라이브, 파일 및 디렉터리를 사용하기 위한 속성 및 메서드를 제공합니다.|  
|`My.Computer.FileSystem.SpecialDirectories` (<xref:Microsoft.VisualBasic.FileIO.SpecialDirectories>)|일반적으로 참조되는 디렉터리에 액세스하기 위한 속성을 제공합니다.|  
|`My.Computer.Info` (<xref:Microsoft.VisualBasic.Devices.ComputerInfo>)|컴퓨터의 메모리, 로드된 어셈블리, 이름 및 운영 체제에 대한 정보를 가져오기 위한 속성을 제공합니다.|  
|`My.Computer.Keyboard` (<xref:Microsoft.VisualBasic.Devices.Keyboard>)|현재 누른 키 등 키보드의 현재 상태에 액세스하기 위한 속성을 제공하고, 활성 창에 키 입력을 보내기 위한 메서드를 제공합니다.|  
|`My.Computer.Mouse` (<xref:Microsoft.VisualBasic.Devices.Mouse>)|로컬 컴퓨터에 설치된 마우스의 형식 및 구성 정보를 가져오기 위한 속성을 제공합니다.|  
|`My.Computer.Network` (<xref:Microsoft.VisualBasic.Devices.Network>)|컴퓨터가 연결된 네트워크와 상호 작용하기 위한 속성, 이벤트 및 메서드를 제공합니다.|  
|`My.Computer.Ports` (<xref:Microsoft.VisualBasic.Devices.Ports>)|컴퓨터의 직렬 포트에 액세스하기 위한 속성 및 메서드를 제공합니다.|  
|`My.Computer.Registry` (<xref:Microsoft.VisualBasic.MyServices.RegistryProxy>)|레지스트리를 조작하기 위한 속성 및 메서드를 제공합니다.|  
|[My.Forms 개체](../../../visual-basic/language-reference/objects/my-forms-object.md)|현재 프로젝트에서 각 Windows Form의 인스턴스에 액세스하기 위한 속성을 제공합니다.|  
|`My.Log` (<xref:Microsoft.VisualBasic.Logging.AspLog>)|웹 애플리케이션에 대한 이벤트 및 예외 정보를 애플리케이션의 로그 수신기에 쓰기 위한 속성 및 메서드를 제공합니다.|  
|[My.Request 개체](../../../visual-basic/language-reference/objects/my-request-object.md)|요청된 페이지에 대한 <xref:System.Web.HttpRequest> 개체를 가져옵니다. `My.Request` 개체에는 현재 HTTP 요청에 대한 정보가 포함됩니다.<br /><br /> `My.Request` 개체는 ASP.NET 애플리케이션에만 사용할 수 있습니다.|  
|[My.Resources 개체](../../../visual-basic/language-reference/objects/my-resources-object.md)|애플리케이션 리소스에 액세스하기 위한 속성 및 클래스를 제공합니다.|  
|[My.Response 개체](../../../visual-basic/language-reference/objects/my-response-object.md)|<xref:System.Web.HttpResponse>와 연결된 <xref:System.Web.UI.Page> 개체를 가져옵니다. 이 개체를 사용하여 HTTP 응답 데이터를 클라이언트에 보낼 수 있고 이 개체는 해당 응답에 대한 정보를 포함합니다.<br /><br /> `My.Response` 개체는 ASP.NET 애플리케이션에만 사용할 수 있습니다.|  
|[My.Settings 개체](../../../visual-basic/language-reference/objects/my-settings-object.md)|애플리케이션 설정에 액세스하기 위한 속성 및 메서드를 제공합니다.|  
|`My.User` (<xref:Microsoft.VisualBasic.ApplicationServices.User>)|현재 사용자에 대한 정보에 액세스할 수 있습니다.|  
|[My.WebServices 개체](../../../visual-basic/language-reference/objects/my-webservices-object.md)|현재 프로젝트에서 참조하는 각 웹 서비스의 단일 인스턴스를 만들고 액세스하기 위한 속성을 제공합니다.|  
|<xref:Microsoft.VisualBasic.FileIO.TextFieldParser>|구조화된 텍스트 파일을 구문 분석하기 위한 메서드와 속성을 제공합니다.|  
  
## <a name="see-also"></a>참고자료

- [Visual Basic 언어 참조](../../../visual-basic/language-reference/index.md)
- [Visual Basic](../../../visual-basic/index.md)
