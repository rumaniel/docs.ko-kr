---
title: '방법: 추적 스위치 만들기, 초기화 및 구성'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- trace switches, configuring
- tracing [.NET Framework], trace switches
- switches, trace
- tracing [.NET Framework], enabling or disabling
- Web.config configuration file, trace switches
ms.assetid: 5a0e41bf-f99c-4692-8799-f89617f5bcf9
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 13f89af41520fa023d8841d6dc6d7766e2abe6da
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052708"
---
# <a name="how-to-create-initialize-and-configure-trace-switches"></a>방법: 추적 스위치 만들기, 초기화 및 구성
추적 스위치를 사용하여 추적 출력을 활성화, 비활성화 및 필터링할 수 있습니다.  
  
<a name="create"></a>   
## <a name="creating-and-initializing-a-trace-switch"></a>추적 스위치 만들기 및 초기화  
 추적 스위치를 사용하려면 먼저 만들어서 코드에 배치해야 합니다. 스위치 개체를 만드는 데 사용할 수 있는 미리 정의된 두 개의 클래스로는 <xref:System.Diagnostics.BooleanSwitch?displayProperty=nameWithType> 클래스와 <xref:System.Diagnostics.TraceSwitch?displayProperty=nameWithType> 클래스가 있습니다. 추적 메시지의 표시 여부에만 관심이 있으면 <xref:System.Diagnostics.BooleanSwitch>를 사용하고 추적 수준을 구분하려면 <xref:System.Diagnostics.TraceSwitch>를 사용할 수 있습니다. <xref:System.Diagnostics.TraceSwitch>가 사용되면 개인적인 디버거 메시지를 정의한 다음 다양한 추적 수준과 연결할 수 있습니다. 추적 또는 디버깅에 두 가지 스위치 형식을 모두 사용할 수 있습니다. 기본적으로 <xref:System.Diagnostics.BooleanSwitch>는 비활성화되고 <xref:System.Diagnostics.TraceSwitch>는 <xref:System.Diagnostics.TraceLevel.Off?displayProperty=nameWithType> 수준으로 설정됩니다. 추적 스위치를 만들고 이 스위치를 사용할 수 있는 코드의 모든 부분에 배치할 수 있습니다.  
  
 코드에 추적 수준과 기타 구성 옵션을 설정할 수도 있지만 구성 파일을 사용하여 스위치의 상태를 관리하는 것이 좋습니다. 이것은 구성 시스템에서 스위치 구성을 관리하면 좀 더 융통성 있게 사용할 수 있기 때문입니다. 즉, 응용 프로그램을 다시 컴파일하지 않고도 다양한 스위치를 설정하거나 해제하고 수준을 변경할 수 있습니다.  
  
#### <a name="to-create-and-initialize-a-trace-switch"></a>추적 스위치를 만들고 초기화하려면  
  
1. 스위치를 <xref:System.Diagnostics.BooleanSwitch?displayProperty=nameWithType> 형식 또는 <xref:System.Diagnostics.TraceSwitch?displayProperty=nameWithType> 형식으로 정의하고 스위치의 이름과 설명을 설정합니다.  
  
2. 추적 스위치를 구성합니다. 자세한 내용은 [추적 스위치 구성](#configure)을 참조하세요.  
  
     다음 코드에서는 각 형식당 하나씩, 두 개의 스위치를 만듭니다.  
  
    ```vb  
    Dim dataSwitch As New BooleanSwitch("Data", "DataAccess module")  
    Dim generalSwitch As New TraceSwitch("General", "Entire application")  
    ```  
  
    ```csharp  
    System.Diagnostics.BooleanSwitch dataSwitch =   
       new System.Diagnostics.BooleanSwitch("Data", "DataAccess module");  
    System.Diagnostics.TraceSwitch generalSwitch =   
       new System.Diagnostics.TraceSwitch("General",   
       "Entire application");  
    ```  
  
<a name="configure"></a>   
## <a name="configuring-trace-switches"></a>추적 스위치 구성  
 응용 프로그램이 배포된 후 응용 프로그램에서 추적 스위치를 구성하여 추적 출력을 사용하거나 사용하지 않도록 설정할 수도 있습니다. 스위치 구성은 스위치가 초기화된 후 외부 소스에서 해당 값을 변경하는 것을 의미합니다. 구성 파일을 사용하여 스위치 개체의 값을 변경할 수 있습니다. 추적 스위치를 구성하여 설정 및 해제하거나 해당 수준을 설정하고 수신기로 전달되는 메시지의 양과 형식을 결정합니다.  
  
 스위치는 .config 파일을 사용하여 구성됩니다. 웹 애플리케이션의 경우 프로젝트와 연결된 Web.config 파일입니다. Windows 응용 프로그램에서 이 파일의 이름은 (응용 프로그램 이름).exe.config입니다. 배포된 응용 프로그램에서 이 파일은 실행 파일과 동일한 폴더에 있어야 합니다.  
  
 응용 프로그램은 스위치 인스턴스를 만드는 코드를 처음 실행할 때 명명된 스위치에 대한 추적 수준 정보를 구성 파일에서 확인합니다. 추적 시스템은 특정 스위치에 대해 한 번만, 즉 응용 프로그램이 스위치를 처음 만들 때만 구성 파일을 검사합니다.  
  
 배포된 응용 프로그램에서 응용 프로그램이 실행되지 않을 때 스위치 개체를 재구성하여 추적 코드를 사용하도록 설정합니다. 일반적으로 이 작업을 위해 스위치 개체를 설정 및 해제하거나 추적 수준을 변경한 다음 응용 프로그램을 다시 시작해야 합니다.  
  
 스위치 인스턴스를 만들 때 *displayName* 인수와 *description* 인수의 두 인수를 지정하여 초기화도 수행합니다. 생성자의 *displayName* 인수는 <xref:System.Diagnostics.Switch> 클래스 인스턴스의 <xref:System.Diagnostics.Switch.DisplayName%2A?displayProperty=nameWithType> 속성을 설정합니다. *displayName*은 .config 파일에서 스위치를 구성하는 데 사용되는 이름이고, *description* 인수는 스위치 및 스위치가 제어하는 메시지에 대한 간략한 설명을 반환해야 합니다.  
  
 구성할 스위치의 이름을 지정하는 것은 물론 스위치의 값도 지정해야 합니다. 이 값은 정수입니다. <xref:System.Diagnostics.BooleanSwitch>에서 값 0은 **끄기**에 해당하고 0이 아닌 값은 **켜기**에 해당합니다. <xref:System.Diagnostics.TraceSwitch>에서 0, 1, 2, 3, 4는 각각 **끄기**, **오류**, **경고**, **정보** 및 **동사**에 해당합니다. 4보다 큰 숫자는 **동사**로 처리되고 0보다 작은 숫자는 **끄기**로 처리됩니다.  
  
> [!NOTE]
> .NET Framework 버전 2.0에서는 텍스트를 사용하여 스위치의 값을 지정할 수 있습니다. 예를 들어 <xref:System.Diagnostics.BooleanSwitch>에 대한 `true` 또는 <xref:System.Diagnostics.TraceSwitch>에 대한 열거형 값을 나타내는 텍스트(예: `Error`)가 있습니다. `<add name="myTraceSwitch" value="Error" />` 줄은 `<add name="myTraceSwitch" value="1" />`과 같습니다.  
  
 최종 사용자가 응용 프로그램의 추적 스위치를 구성할 수 있으려면 응용 프로그램에서 스위치에 대한 자세한 설명서를 제공해야 합니다. 어떤 스위치가 어떤 기능을 제어하는지 및 설정/해제하는 방법을 세부적으로 설정해야 합니다. 또한 주석에 적절한 도움말이 있는 .config 파일을 최종 사용자에게 제공해야 합니다.  
  
#### <a name="to-configure-trace-switches"></a>추적 스위치를 구성 하려면  
  
1. 추적 스위치를 사용하려면 [추적 스위치 만들기 및 초기화](#create) 섹션의 설명대로 추적 스위치를 만들고 코드에 배치해야 합니다.  
  
2. 프로젝트에 구성 파일(app.config 또는 Web.config)이 없는 경우 **프로젝트** 메뉴에서 **새 항목 추가**를 선택합니다.  
  
    - **Visual Basic:** **새 항목 추가** 대화 상자에서 **응용 프로그램 구성 파일**을 선택 합니다.  
  
         응용 프로그램 구성 파일이 만들어져 열립니다. 이 파일은 루트 요소가 `<configuration>.`인 XML 문서입니다.  
  
    - **Visual C#:** **새 항목 추가** 대화 상자에서 **XML 파일**을 선택 합니다. 이 파일 이름을 **app.config**로 지정합니다. XML 편집기에서 XML 선언 뒤에 다음 XML을 추가합니다.  
  
        ```xml  
        <configuration>  
        </configuration>  
        ```  
  
         프로젝트를 컴파일하면 app.config 파일이 프로젝트 출력 폴더에 복사되고 이름이 *applicationname*.exe.config로 바뀝니다.  
  
3. `<configuration>` 태그 뒤, `</configuration>` 태그 앞에 적절한 XML을 추가하여 스위치를 구성합니다. 다음 예제에서는 **DisplayName** 속성이 `DataMessageSwitch`인 **BooleanSwitch** 및 **DisplayName** 속성이 `TraceLevelSwitch`인 **TraceSwitch**를 보여 줍니다.  
  
    ```xml  
    <system.diagnostics>  
       <switches>  
          <add name="DataMessagesSwitch" value="0" />  
          <add name="TraceLevelSwitch" value="0" />  
       </switches>  
    </system.diagnostics>  
    ```  
  
     이 구성에서는 두 스위치가 모두 해제되어 있습니다.  
  
4. 이전 예제에 표시된 `DataMessagesSwitch`와 같은 **BooleanSwitch**를 설정해야 하는 경우 **Value**를 0이 아닌 임의의 정수로 변경합니다.  
  
5. 이전 예제에 표시된 `TraceLevelSwitch`와 같은 **TraceSwitch**를 설정해야 하는 경우 **Value**를 적절한 수준 설정(1-4)으로 변경합니다.  
  
6. 최종 사용자가 스위치를 적절하게 구성하기 위해 변경할 값을 명확하게 이해할 수 있도록 .config 파일에 주석을 추가합니다.  
  
     다음 예제에서는 주석을 포함하는 최종 코드의 모양을 보여 줍니다.  
  
    ```xml  
    <system.diagnostics>  
       <switches>  
          <!-- This switch controls data messages. In order to receive data   
             trace messages, change value="0" to value="1" -->  
          <add name="DataMessagesSwitch" value="0" />  
          <!-- This switch controls general messages. In order to   
             receive general trace messages change the value to the   
             appropriate level. "1" gives error messages, "2" gives errors   
             and warnings, "3" gives more detailed error information, and   
             "4" gives verbose trace information -->  
          <add name="TraceLevelSwitch" value="0" />  
       </switches>  
    </system.diagnostics>  
    ```  
  
## <a name="see-also"></a>참고자료

- [응용 프로그램 추적 및 조율](tracing-and-instrumenting-applications.md)
- [방법: 응용 프로그램 코드에 Trace 문 추가](how-to-add-trace-statements-to-application-code.md)
- [추적 스위치](trace-switches.md)
- [추적 및 디버그 설정 스키마](../configure-apps/file-schema/trace-debug/index.md)
