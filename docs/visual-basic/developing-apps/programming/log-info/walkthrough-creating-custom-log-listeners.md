---
title: 사용자 지정 로그 수신기 만들기(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- custom log listeners
- My.Application.Log object, custom log listeners
ms.assetid: 0e019115-4b25-4820-afb1-af8c6e391698
ms.openlocfilehash: a4bd64d4c8232f9b6448baf98ee73ee497ccd5ca
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972101"
---
# <a name="walkthrough-creating-custom-log-listeners-visual-basic"></a>연습: 사용자 지정 로그 수신기 만들기(Visual Basic)
이 연습에서는 사용자 지정 로그 수신기를 만들고 `My.Application.Log` 개체의 출력을 수신 대기하도록 구성하는 방법을 보여 줍니다.  
  
## <a name="getting-started"></a>시작  
 로그 수신기는 <xref:System.Diagnostics.TraceListener> 클래스에서 상속해야 합니다.  
  
#### <a name="to-create-the-listener"></a>수신기를 만들려면  
  
- <xref:System.Diagnostics.TraceListener>에서 상속하는 이름이 `SimpleListener`인 클래스를 애플리케이션에서 만듭니다.  
  
     [!code-vb[VbVbalrMyApplicationLog#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#16)]  
  
     기본 클래스에 필요한 <xref:System.Diagnostics.TraceListener.Write%2A> 및 <xref:System.Diagnostics.TraceListener.WriteLine%2A> 메서드는 `MsgBox`를 호출하여 해당 입력을 표시합니다.  
  
     <xref:System.Diagnostics.TraceListener.Write%2A> 및 <xref:System.Diagnostics.TraceListener.WriteLine%2A> 메서드의 특정이 기본 클래스 메서드와 일치하도록 이 두 메서드에 <xref:System.Security.Permissions.HostProtectionAttribute> 특성이 적용됩니다. <xref:System.Security.Permissions.HostProtectionAttribute> 특성을 사용하면 코드를 실행하는 호스트에서는 코드가 호스트 보호 동기화를 노출하는지를 확인할 수 있습니다.  
  
    > [!NOTE]
    > <xref:System.Security.Permissions.HostProtectionAttribute> 특성은 공용 언어 런타임을 호스트하고 SQL Server와 같은 호스트 보호를 구현하는 관리되지 않는 애플리케이션에서만 적용됩니다.  
  
 `My.Application.Log`가 로그 수신기를 사용하도록 하려면 로그 수신기를 포함하는 어셈블리에 강력한 이름을 지정해야 합니다.  
  
 다음 절차에서는 강력한 이름의 로그 수신기 어셈블리를 만들기 위한 몇 가지 간단한 단계를 제공합니다. 자세한 내용은 [강력한 이름의 어셈블리 만들기 및 사용](../../../../standard/assembly/create-use-strong-named.md)을 참조하세요.  
  
#### <a name="to-strongly-name-the-log-listener-assembly"></a>로그 수신기 어셈블리에 강력한 이름을 지정하려면  
  
1. **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 선택합니다.   
  
2. **시그니처** 탭을 클릭합니다.  
  
3. **어셈블리 시그니처** 상자를 선택합니다.  
  
4. **강력한 이름 키 파일 선택** 드롭다운 목록에서 **\<새로 만들기>** 를 선택합니다.  
  
     **강력한 이름 키 만들기** 대화 상자가 열립니다.  
  
5. **키 파일 이름** 상자에 키 파일의 이름을 입력합니다.  
  
6. **암호 입력** 및 **암호 확인** 상자에 암호를 입력합니다.  
  
7. **확인**을 클릭합니다.  
  
8. 애플리케이션을 다시 빌드합니다.  
  
## <a name="adding-the-listener"></a>수신기 추가  
 이제 어셈블리에 강력한 이름을 지정했으므로 `My.Application.Log`에서 로그 수신기를 사용하도록 수신기의 강력한 이름을 결정해야 합니다.  
  
 강력한 이름의 형식은 다음과 같은 구문을 갖습니다.  
  
 \<type name>, \<assembly name>, \<version number>, \<culture>, \<strong name>  
  
#### <a name="to-determine-the-strong-name-of-the-listener"></a>수신기의 강력한 이름을 결정하려면  
  
- 다음 코드에서는 `SimpleListener`에 대해 강력한 형식의 이름을 결정하는 방법을 보여 줍니다.  
  
     [!code-vb[VbVbalrMyApplicationLog#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#17)]  
  
     강력한 형식의 이름은 프로젝트에 따라 다릅니다.  
  
 강력한 이름을 사용하면 수신기를 `My.Application.Log` 로그 수신기 컬렉션에 추가할 수 있습니다.  
  
#### <a name="to-add-the-listener-to-myapplicationlog"></a>My.Application.Log에 수신기를 추가하려면  
  
1. **솔루션 탐색기**에서 app.config를 마우스 오른쪽 단추로 클릭하고 **열기**를 선택합니다.  
  
     또는  
  
     app.config 파일이 있는 경우:  
  
    1. **프로젝트** 메뉴에서 **새 항목 추가**를 선택합니다.  
  
    2. **새 항목 추가** 대화 상자에서 **애플리케이션 구성 파일**을 선택합니다.  
  
    3. **추가**를 클릭합니다.  
  
2. `<listeners>` 특성이 "DefaultSource"인 `<source>` 섹션에서 `name` 섹션에 있는 `<sources>` 섹션을 찾습니다. `<sources>` 섹션은 최상위 `<system.diagnostics>` 섹션의 `<configuration>` 섹션에 있습니다.  
  
3. 이 요소를 `<listeners>` 섹션에 추가합니다.  
  
    ```xml  
    <add name="SimpleLog" />  
    ```  
  
4. 최상위 `<sharedListeners>` 섹션의 `<system.diagnostics>` 섹션에서 `<configuration>` 섹션을 찾습니다.  
  
5. 다음 요소를 `<sharedListeners>` 섹션에 추가합니다.  
  
    ```xml  
    <add name="SimpleLog" type="SimpleLogStrongName" />  
    ```  
  
     수신기의 강력한 이름이 되도록 `SimpleLogStrongName`의 값을 변경합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- [애플리케이션 로그 작업](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)
- [방법: 로그 예외](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)
- [방법: 로그 메시지 쓰기](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)
- [연습: My.Application.Log가 정보를 기록하는 위치 변경](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)
