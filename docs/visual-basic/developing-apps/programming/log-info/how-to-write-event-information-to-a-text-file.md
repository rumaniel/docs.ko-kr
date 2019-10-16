---
title: '방법: 텍스트 파일에 이벤트 정보 쓰기(Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- event logs [Visual Studio], writing event information
- text files [Visual Basic], writing event information to a text file
- events [Visual Basic], writing event information to a text file
ms.assetid: 9ca7cc03-bf99-4933-9e5e-61ee28e9a6b4
ms.openlocfilehash: 4a34b57eb0a22dcf206456775cdd5817431292e8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956832"
---
# <a name="how-to-write-event-information-to-a-text-file-visual-basic"></a>방법: 텍스트 파일에 이벤트 정보 쓰기(Visual Basic)
`My.Application.Log` 및 `My.Log` 개체를 사용하여 애플리케이션에서 발생하는 이벤트에 대한 정보를 기록할 수 있습니다. 이 예제에서는 `My.Application.Log.WriteEntry` 메서드를 사용하여 추적 정보를 로그 파일에 기록하는 방법을 보여 줍니다.  
  
### <a name="to-add-and-configure-the-file-log-listener"></a>파일 로그 수신기를 추가하고 구성하려면  
  
1. **솔루션 탐색기** 에서 app.config를 마우스 오른쪽 단추로 클릭하고 **열기**를 선택합니다.  
  
     \- 또는 -  
  
     app.config 파일이 없는 경우  
  
    1. **프로젝트** 메뉴에서 **새 항목 추가**를 선택합니다.  
  
    2. **새 항목 추가** 대화 상자에서 **애플리케이션 구성 파일**을 선택합니다.  
  
    3. **추가**를 클릭합니다.  
  
2. 애플리케이션 구성 파일에서 `<listeners>` 섹션을 찾습니다.  
  
     최상위 \<configuration> 섹션 아래에 중첩된 \<system.diagnostics> 섹션 아래에서 이름 특성이 "DefaultSource"인 \<source> 섹션에 \<listeners> 섹션이 있습니다.  
  
3. 다음 요소를 `<listeners>` 섹션에 추가합니다.  
  
    ```xml  
    <add name="FileLogListener" />  
    ```  
  
4. 최상위 `<configuration>` 섹션 아래에 중첩된 `<system.diagnostics>` 섹션에서 `<sharedListeners>` 섹션을 찾습니다.  
  
5. 다음 요소를 `<sharedListeners>` 섹션에 추가합니다.  
  
    ```xml  
    <add name="FileLogListener"   
        type="Microsoft.VisualBasic.Logging.FileLogTraceListener,   
              Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral,   
              PublicKeyToken=b03f5f7f11d50a3a"  
        initializeData="FileLogListenerWriter"  
        location="Custom"  
        customlocation="c:\temp\" />  
    ```  
  
     `customlocation` 특성의 값을 로그 디렉터리로 변경합니다.  
  
    > [!NOTE]
    > 수신기 속성의 값을 설정하려면 속성과 이름이 같고 이름에 있는 모든 문자가 소문자인 특성을 사용 합니다. 예를 들어 `location` 및 `customlocation` 특성은 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.Location%2A> 및 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.CustomLocation%2A> 속성의 값을 설정합니다.  
  
### <a name="to-write-event-information-to-the-file-log"></a>이벤트 정보를 파일 로그에 쓰려면  
  
- `My.Application.Log.WriteEntry` 또는 `My.Application.Log.WriteException` 메서드를 사용하여 파일 로그에 정보를 씁니다. 자세한 내용은 [방법: 로그 메시지 쓰기](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md) 및 [방법: 로그 예외](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)를 참조하세요.  
  
     어셈블리에 대한 파일 로그 수신기를 구성하면 수신기는 `My.Application.Log`가 해당 어셈블리에서 쓰는 모든 메시지를 수신합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [애플리케이션 로그 작업](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)
- [방법: 로그 예외](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)
