---
title: '방법: 비동기적으로 웹 서비스 호출(Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- asynchronous calls [Visual Basic]
- Web services [Visual Basic], accessing
ms.assetid: ff8046f4-f1f2-4d8b-90b7-95e3f7415418
ms.openlocfilehash: bf109780f26ce2fa4d5dbaa63832e765970b5cb4
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48842699"
---
# <a name="how-to-call-a-web-service-asynchronously-visual-basic"></a>방법: 비동기적으로 웹 서비스 호출(Visual Basic)
이 예제에서는 비동기 메서드 호출의 결과를 검색할 수 있도록 웹 서비스의 비동기 처리기 이벤트에 처리기를 연결합니다. 여기에는 `http://www.xmethods.net`에 DemoTemperatureService 웹 서비스가 사용되었습니다.  
  
 Visual Studio IDE(통합 개발 환경)에서 프로젝트의 웹 서비스를 참조하면, `My.WebServices` 개체에 해당 웹 서비스가 추가되며 IDE에서 지정된 웹 서비스에 액세스하기 위해 클라이언트 프록시 클래스를 생성합니다.  
  
 프록시 클래스를 통해 웹 서비스 메서드를 동기식으로 호출할 수 있습니다. 이 경우 응용 프로그램은 함수가 완료될 때까지 기다립니다. 또한 프록시는 추가 멤버를 만들어 메서드를 비동기식으로 호출합니다. 각 웹 서비스 함수(*NameOfWebServiceFunction*)에 대해 프록시는 *NameOfWebServiceFunction*`Async` 서브루틴, *NameOfWebServiceFunction*`Completed` 이벤트 및 *NameOfWebServiceFunction*`CompletedEventArgs` 클래스를 만듭니다. 이 예제에서는 비동기 멤버를 사용하여 DemoTemperatureService 웹 서비스의 `getTemp` 함수에 액세스하는 방법을 보여줍니다.  
  
> [!NOTE]
>  ASP.NET은 `My.WebServices` 개체를 지원하지 않으므로 웹 응용 프로그램에서는 이 코드가 작동하지 않습니다.  
  
### <a name="to-call-a-web-service-asynchronously"></a>웹 서비스를 비동기식으로 호출하려면  
  
1.  `http://www.xmethods.net`에서 DemoTemperatureService 웹 서비스를 참조합니다. 해당 주소는 다음과 같습니다.  
  
    ```  
    http://www.xmethods.net/sd/2001/DemoTemperatureService.wsdl  
    ```  
  
2.  `getTempCompleted` 이벤트에 대한 이벤트 처리기를 추가합니다.  
  
    ```  
    Private Sub getTempCompletedHandler(ByVal sender As Object,   
        ByVal e As net.xmethods.www.getTempCompletedEventArgs)  
  
        MsgBox("Temperature: " & e.Result)  
    End Sub  
    ```  
  
    > [!NOTE]
    >  `Handles` 문을 사용하여 이벤트 처리기를 `My.WebServices` 개체의 이벤트와 연결할 수는 없습니다.  
  
3.  이벤트 처리기가 `getTempCompleted` 이벤트에 추가되었는지를 추적할 필드를 추가합니다.  
  
    ```  
    Private handlerAttached As Boolean = False  
    ```  
  
4.  필요한 경우 이벤트 처리기를 `getTempCompleted` 이벤트에 추가하고 `getTempAsynch` 메서드를 호출하는 메서드를 추가합니다.  
  
    ```  
    Sub CallGetTempAsync(ByVal zipCode As Integer)  
        If Not handlerAttached Then  
            AddHandler My.WebServices.  
                TemperatureService.getTempCompleted,   
                AddressOf Me.TS_getTempCompleted  
            handlerAttached = True  
        End If  
        My.WebServices.TemperatureService.getTempAsync(zipCode)  
    End Sub  
    ```  
  
     `getTemp` 웹 메서드를 비동기식으로 호출하려면 `CallGetTempAsync` 메서드를 호출합니다. 웹 메서드가 완료되면 해당 반환 값이 `getTempCompletedHandler` 이벤트 처리기로 전달됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [응용 프로그램 웹 서비스 액세스](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md)  
 [My.WebServices 개체](../../../visual-basic/language-reference/objects/my-webservices-object.md)
