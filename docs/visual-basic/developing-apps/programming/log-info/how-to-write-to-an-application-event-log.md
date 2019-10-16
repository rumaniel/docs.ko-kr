---
title: '방법: 애플리케이션 이벤트 로그에 쓰기(Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- Computer.EventLog element
- WriteEntry method [Visual Basic]
- My.Computer.EventLog element
- event logs, writing to
ms.assetid: cadbc8c1-87af-4746-934e-55b79a4f6e2b
ms.openlocfilehash: 385a85d956a0de727e3c061ec447a3d53ad6c159
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054142"
---
# <a name="how-to-write-to-an-application-event-log-visual-basic"></a>방법: 애플리케이션 이벤트 로그에 쓰기(Visual Basic)

`My.Application.Log` 및 `My.Log` 개체를 사용하여 애플리케이션에서 발생하는 이벤트에 대한 정보를 쓸 수 있습니다. 이 예제에서는 `My.Application.Log` 가 애플리케이션 이벤트 로그에 추적 정보를 쓰도록 이벤트 로그 수신기를 구성하는 방법을 보여 줍니다.

보안 로그에는 쓸 수 없습니다. 시스템 로그에 쓰려면 LocalSystem 또는 Administrator 계정의 멤버여야 합니다.

이벤트 로그를 보려면 **서버 탐색기** 또는 **Windows 이벤트 뷰어**를 사용합니다. 자세한 내용은 [ETW Events in the .NET Framework](../../../../framework/performance/etw-events.md)을 참조하세요.

## <a name="to-add-and-configure-the-event-log-listener"></a>이벤트 로그 수신기를 추가하고 구성하려면

1. **솔루션 탐색기** 에서 app.config를 마우스 오른쪽 단추로 클릭하고 **열기**를 선택합니다.

    \- 또는 -

    app.config 파일이 없는 경우

    1. **프로젝트** 메뉴에서 **새 항목 추가**를 선택합니다.

    2. **새 항목 추가** 대화 상자에서 **애플리케이션 구성 파일**을 선택합니다.

    3. **추가**를 클릭합니다.

2. 애플리케이션 구성 파일에서 `<listeners>` 섹션을 찾습니다.

    최상위 `<listeners>` 섹션 아래의 `<source>` 섹션 아래에서 이름 특성이 "DefaultSource"인 `<system.diagnostics>` 섹션에 `<configuration>` 섹션이 있습니다.

3. 다음 요소를 `<listeners>` 섹션에 추가합니다.

    ```xml
    <add name="EventLog"/>
    ```

4. 최상위 `<sharedListeners>` 섹션의 `<system.diagnostics>` 섹션에서 `<configuration>` 섹션을 찾습니다.

5. 다음 요소를 `<sharedListeners>` 섹션에 추가합니다.

    ```xml
    <add name="EventLog"
        type="System.Diagnostics.EventLogTraceListener, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
         initializeData="APPLICATION_NAME"/>
    ```

    `APPLICATION_NAME` 을 애플리케이션의 이름으로 바꿉니다.

    > [!NOTE]
    > 일반적으로 애플리케이션에서는 이벤트 로그에 오류만 씁니다. 로그 출력 필터링에 대한 자세한 내용은 [연습: My.Application.Log 출력 필터링](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md)을 참조하세요.

## <a name="to-write-event-information-to-the-event-log"></a>이벤트 정보를 이벤트 로그에 쓰려면

`My.Application.Log.WriteEntry` 또는 `My.Application.Log.WriteException` 메서드를 사용하여 이벤트 로그에 정보를 씁니다. 자세한 내용은 [방법: 로그 메시지 쓰기](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md) 및 [방법: 로그 예외](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)를 참조하세요.

어셈블리에 대한 이벤트 로그 수신기를 구성하면 수신기는 `My.Application.Log` 가 해당 어셈블리에서 쓰는 모든 메시지를 수신합니다.

## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [애플리케이션 로그 작업](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)
- [방법: 로그 예외](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)
- [연습: My.Application.Log가 정보를 기록하는 위치 확인](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)
