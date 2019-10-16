---
title: 추적 스위치
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tracing [.NET Framework], trace switches
- trace switches, about trace switches
- tracing [.NET Framework], level of detail
- switches, trace
- trace switches
- trace switches, creating custom
ms.assetid: 8ab913aa-f400-4406-9436-f45bc6e54fbe
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b796d79fc6acf7d54aac7c69d376e587144d14d1
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052253"
---
# <a name="trace-switches"></a>추적 스위치
추적 스위치를 사용하여 추적 출력을 활성화, 비활성화 및 필터링할 수 있습니다. 코드에 존재하며 .config 파일을 통해 외부에서 구성할 수 있는 개체입니다. .NET Framework에서 제공되는 세 가지 유형의 추적 스위치( <xref:System.Diagnostics.BooleanSwitch> 클래스, <xref:System.Diagnostics.TraceSwitch> 클래스 및 <xref:System.Diagnostics.SourceSwitch> 클래스)가 있습니다. <xref:System.Diagnostics.BooleanSwitch> 클래스는 다양한 trace 문을 사용하거나 사용하지 않도록 설정하는 토글 스위치 역할을 합니다. <xref:System.Diagnostics.TraceSwitch> 및 <xref:System.Diagnostics.SourceSwitch> 클래스를 통해 특정 추적 수준에 대한 추적 스위치를 사용하도록 설정하여 해당 수준 및 그 아래의 모든 수준에 대해 지정된 <xref:System.Diagnostics.Trace> 또는 <xref:System.Diagnostics.TraceSource> 메시지를 표시할 수 있습니다. 스위치를 사용하지 않도록 설정하면 추적 메시지가 나타나지 않습니다. 이러한 모든 클래스는 사용자 개발 스위치와 마찬가지로 추상(**MustInherit**) 클래스 **Switch**에서 파생됩니다.  
  
 추적 스위치는 정보를 필터링하는 데 유용할 수 있습니다. 예를 들어 데이터 액세스 모듈에서는 모든 추적 메시지가 표시되고 애플리케이션의 나머지 부분에서는 오류 메시지만 표시되도록 할 수 있습니다. 이 경우 데이터 액세스 모듈에 대해 하나의 추적 스위치를 사용하고 애플리케이션의 나머지 부분에 대해 하나의 스위치를 사용합니다. .config 파일을 사용하여 스위치를 적절한 설정으로 구성하면 수신하는 추적 메시지 유형을 제어할 수 있습니다. 자세한 내용은 [방법: 추적 스위치](how-to-create-initialize-and-configure-trace-switches.md)만들기, 초기화 및 구성  
  
 일반적으로 배포된 애플리케이션은 애플리케이션 실행 시 화면에 나타나거나 로그 파일에 채워지는 여러 관련 없는 추적 메시지를 사용자가 관찰할 필요가 없도록 스위치를 사용할 수 없는 상태로 실행됩니다. 애플리케이션 실행 중에 문제가 발생할 경우 애플리케이션을 중지하고 스위치를 사용하도록 설정한 다음 애플리케이션을 다시 시작할 수 있습니다. 그러면 추적 메시지가 표시됩니다.  
  
 스위치를 사용하려면 먼저 **BooleanSwitch** 클래스, **TraceSwitch** 클래스 또는 개발자 정의 스위치 클래스에서 스위치 개체를 만들어야 합니다. 개발자 정의 스위치를 만드는 방법에 대한 자세한 내용은 .NET Framework 참조에서 <xref:System.Diagnostics.Switch> 클래스를 참조하세요. 스위치 개체를 사용할 시기를 지정하는 구성 값을 설정합니다. 그런 후에 다양한 **추적** (또는 **디버그**) 추적 메서드에서 스위치 개체의 설정을 테스트합니다.  
  
## <a name="trace-levels"></a>추적 수준  
 **TraceSwitch**를 사용하는 경우 추가로 고려해야 할 사항이 있습니다. **TraceSwitch** 개체에는 스위치가 특정 수준 이상으로 설정되었는지 여부를 나타내는 **부울** 값을 반환하는 다음 4가지 속성이 있습니다.  
  
- <xref:System.Diagnostics.TraceSwitch.TraceError%2A?displayProperty=nameWithType>  
  
- <xref:System.Diagnostics.TraceSwitch.TraceWarning%2A?displayProperty=nameWithType>  
  
- <xref:System.Diagnostics.TraceSwitch.TraceInfo%2A?displayProperty=nameWithType>  
  
- <xref:System.Diagnostics.TraceSwitch.TraceVerbose%2A?displayProperty=nameWithType>  
  
 수준을 통해 수신하는 추적 정보의 양을 문제 해결에 필요한 정보로만 제한할 수 있습니다. 추적 스위치를 적절한 추적 수준으로 설정하고 구성하여 추적 출력에 표시할 세부 정보 수준을 지정합니다. 오류 메시지, 경고 메시지, 정보 메시지, 자세한 추적 메시지를 수신하거나 메시지를 수신하지 않을 수 있습니다.  
  
 각 수준에 연결할 메시지 종류는 전적으로 사용자가 결정합니다. 일반적으로 추적 메시지의 내용은 각 수준에 연결하는 항목에 따라 달라지지만 수준 간의 차이를 결정합니다. 예를 들어 수준 3(**Info**)에서는 문제에 대한 자세한 설명을 제공하지만 수준 1(**Error**)에서는 오류 참조 번호만 제공할 수 있습니다. 애플리케이션에 가장 적합한 체계는 전적으로 사용자가 결정합니다.  
  
 이러한 속성은 **TraceLevel** 열거형의 값 1-4에 해당합니다. 다음 표에서는 **TraceLevel** 열거형의 수준 및 해당 값을 보여 줍니다.  
  
|열거형 값|정수 값|표시(또는 지정된 출력 대상에 기록)되는 메시지 유형|  
|----------------------|-------------------|---------------------------------------------------------------------------|  
|끄기|0|없음|  
|Error|1|오류 메시지만|  
|경고|2|경고 메시지와 오류 메시지|  
|Info|3|정보 메시지, 경고 메시지 및 오류 메시지|  
|자세히|4|자세한 메시지, 정보 메시지, 경고 메시지 및 오류 메시지|  
  
 **TraceSwitch** 속성은 스위치에 대한 최대 추적 수준을 나타냅니다. 즉, 지정된 수준 및 모든 하위 수준에 대한 추적 정보가 기록됩니다. 예를 들어 **TraceInfo** 가 **true**이면 **TraceError** 및 **TraceWarning** 도 **true** 이지만 **TraceVerbose** 는 **false**가 될 수도 있습니다.  
  
 이러한 속성은 읽기 전용입니다. **TraceLevel** 속성이 설정될 때 **TraceSwitch** 개체가 자동으로 설정합니다. 예를 들어:  
  
```vb  
Dim myTraceSwitch As New TraceSwitch("SwitchOne", "The first switch")  
myTraceSwitch.Level = TraceLevel.Info  
' This message box displays true, because setting the level to  
' TraceLevel.Info sets all lower levels to true as well.  
MessageBox.Show(myTraceSwitch.TraceWarning.ToString())  
' This messagebox displays false.  
MessageBox.Show(myTraceSwitch.TraceVerbose.ToString())  
```  
  
```csharp  
System.Diagnostics.TraceSwitch myTraceSwitch =   
   new System.Diagnostics.TraceSwitch("SwitchOne", "The first switch");  
myTraceSwitch.Level = System.Diagnostics.TraceLevel.Info;  
// This message box displays true, because setting the level to   
// TraceLevel.Info sets all lower levels to true as well.  
MessageBox.Show(myTraceSwitch.TraceWarning.ToString());  
// This message box displays false.  
MessageBox.Show(myTraceSwitch.TraceVerbose.ToString());  
```  
  
## <a name="developer-defined-switches"></a>개발자 정의 스위치  
 **BooleanSwitch** 및 **TraceSwitch**를 제공하는 것 외에도 **Switch** 클래스에서 상속하고 기본 클래스 메서드를 사용자 지정 메서드로 재정의하여 고유한 스위치를 정의할 수 있습니다. 개발자 정의 스위치를 만드는 방법에 대한 자세한 내용은 .NET Framework 참조에서 <xref:System.Diagnostics.Switch> 클래스를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [추적 수신기](trace-listeners.md)
- [방법: 응용 프로그램 코드에 Trace 문 추가](how-to-add-trace-statements-to-application-code.md)
- [응용 프로그램 추적 및 조율](tracing-and-instrumenting-applications.md)
