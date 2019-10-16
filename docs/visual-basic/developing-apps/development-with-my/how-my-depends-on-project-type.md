---
title: My가 프로젝트 형식에 의존하는 방식(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- _MYTYPE
ms.assetid: c188b38e-bd9d-4121-9983-41ea6a94d28e
ms.openlocfilehash: 72b9799d1f5ba7efa37d5f8f2a633e6806a58607
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64755721"
---
# <a name="how-my-depends-on-project-type-visual-basic"></a>My가 프로젝트 형식에 의존하는 방식(Visual Basic)
`My` 특정 프로젝트 형식에 필요한 개체만 표시 합니다. 예를 들어를 `My.Forms` 개체가 Windows Forms 응용 프로그램에서 사용할 수 있지만 콘솔 응용 프로그램에서 사용할 수 없습니다. 이 항목에서는 설명 하는 `My` 개체는 다른 프로젝트 형식에서 사용할 수 있습니다.  
  
## <a name="my-in-windows-applications-and-web-sites"></a>내에서 Windows 응용 프로그램 및 웹 사이트  
 `My` 현재 프로젝트 형식에 유용한 개체에만 노출 합니다. 적용할 수 없는 개체를 표시 하지 않습니다. 예를 들어, 다음 이미지는 `My` Windows Forms 프로젝트의 개체 모델입니다.  
  
 ![보여 주는 다이어그램은 Windows Forms 응용 프로그램에서 내 개체 모델입니다.](./media/how-my-depends-on-project-type/my-object-model-windows-forms.png)  
  
 웹 사이트 프로젝트에서 `My` 웹 개발자에 게 관련 된 개체를 노출 (같은 합니다 `My.Request` 및 `My.Response` 개체) 관련 되지 않은 개체를 억제 하는 동안 (같은 `My.Forms` 개체). 다음 이미지는 `My` 웹 사이트 프로젝트의 개체 모델:  
  
 ![보여 주는 다이어그램은 웹 응용 프로그램에서 내 개체 모델입니다.](./media/how-my-depends-on-project-type/my-object-model-web.png)  
  
## <a name="project-details"></a>프로젝트 세부 정보  
 다음 표에 나와 있는 `My` 8 프로젝트 형식에 대 한 개체 기본적으로 사용할 수 있습니다. Windows 응용 프로그램, 클래스 라이브러리, 콘솔 응용 프로그램, Windows 컨트롤 라이브러리, 웹 컨트롤 라이브러리, Windows 서비스, 비어 있거나, 및 웹 사이트입니다.  
  
 다음 세 가지 버전의를 `My.Application` 개체, 두 가지 버전의 합니다 `My.Computer` 개체 및 두 가지 버전의 `My.User` 개체 표 다음에 나오는 각주에서 이러한 버전에 대 한 세부 정보를 제공 합니다.  
  
|My 개체|Windows 애플리케이션|클래스 라이브러리|콘솔 애플리케이션|Windows 컨트롤 라이브러리|웹 컨트롤 라이브러리|Windows 서비스|Empty|웹 사이트|  
|---|---|---|---|---|---|---|---|---|  
|`My.Application`|**예** <sup>1</sup>|**예** <sup>2</sup>|**예** <sup>3</sup>|**예** <sup>2</sup>|아니요|**예** <sup>3</sup>|아니요|아니요|  
|`My.Computer`|**예** <sup>4</sup>|**예** <sup>4</sup>|**예** <sup>4</sup>|**예** <sup>4</sup>|**예** <sup>5</sup>|**예** <sup>4</sup>|아니요|**예** <sup>5</sup>|  
|`My.Forms`|**예**|아니요|아니요|**예**|아니요|아니요|아니요|아니요|  
|`My.Log`|아니요|아니요|아니요|아니요|아니요|아니요|아니요|**예**|  
|`My.Request`|아니요|아니요|아니요|아니요|아니요|아니요|아니요|**예**|  
|`My.Resources`|**예**|**예**|**예**|**예**|**예**|**예**|아니요|아니요|  
|`My.Response`|아니요|아니요|아니요|아니요|아니요|아니요|아니요|**예**|  
|`My.Settings`|**예**|**예**|**예**|**예**|**예**|**예**|아니요|아니요|  
|`My.User`|**예** <sup>6</sup>|**예** <sup>6</sup>|**예** <sup>6</sup>|**예** <sup>6</sup>|**예** <sup>7</sup>|**예** <sup>6</sup>|아니요|**예** <sup>7</sup>|  
|`My.WebServices`|**예**|**예**|**예**|**예**|**예**|**예**|아니요|아니요|  
  
 <sup>1</sup> Windows Forms 버전의 `My.Application`합니다. 콘솔 버전에서 파생 됩니다 (참고 3 참조). 응용 프로그램의 windows와 상호 작용에 대 한 지원을 추가 하 고 Visual Basic 응용 프로그램 모델을 제공 합니다.  
  
 <sup>2</sup> library의 `My.Application`합니다. 응용 프로그램에 필요한 기본 기능을 제공 합니다: 응용 프로그램 로그에 작성 하 고 응용 프로그램 정보에 액세스 하기 위한 멤버를 제공 합니다.  
  
 <sup>3</sup> 콘솔 버전이 `My.Application`합니다. 라이브러리 버전에서 파생 됩니다 (참고 2 참조), 응용 프로그램의 명령줄 인수 및 ClickOnce 배포 정보에 액세스 하기 위한 추가 멤버를 추가 합니다.  
  
 <sup>4</sup> 버전의 Windows `My.Computer`합니다. 서버 버전에서 파생 됩니다 (참고 5 참조), 키보드, 화면에서 마우스와 같은 클라이언트 컴퓨터에서 유용한 개체에 대 한 액세스를 제공 합니다.  
  
 <sup>5</sup> 의 서버 버전 `My.Computer`합니다. 이름, 액세스 하 고 시계를 같은 컴퓨터에 대 한 기본 정보를 제공 합니다.  
  
 <sup>6</sup> 버전의 Windows `My.User`합니다. 이 개체는 스레드의 현재 id와 연결 합니다.  
  
 <sup>7</sup> 웹 버전의 `My.User`합니다. 이 개체는 현재 HTTP 요청을 응용 프로그램의 사용자 id와 연결 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>
- <xref:Microsoft.VisualBasic.Devices.Computer>
- <xref:Microsoft.VisualBasic.Logging.Log>
- <xref:Microsoft.VisualBasic.ApplicationServices.User>
- [My에 사용할 수 있는 개체 사용자 지정](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)
- [조건부 컴파일](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
- [/define (Visual Basic)](../../../visual-basic/reference/command-line-compiler/define.md)
- [My.Forms 개체](../../../visual-basic/language-reference/objects/my-forms-object.md)
- [My.Request 개체](../../../visual-basic/language-reference/objects/my-request-object.md)
- [My.Response 개체](../../../visual-basic/language-reference/objects/my-response-object.md)
- [My.WebServices 개체](../../../visual-basic/language-reference/objects/my-webservices-object.md)
