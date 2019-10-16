---
title: '방법: 애플리케이션 코드에 추적 문 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tracing [.NET Framework], conditional writes based on switches
- trace statements
- WriteLineIf method
- tracing [.NET Framework], adding trace statements
- Assert method, tracing code
- trace switches, conditional writes based on switches
- WriteIf method
ms.assetid: f3a93fa7-1717-467d-aaff-393e5c9828b4
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4517da87603dcdd398d536cd9bf9e441430be375
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052734"
---
# <a name="how-to-add-trace-statements-to-application-code"></a>방법: 애플리케이션 코드에 추적 문 추가
추적에 가장 자주 사용 되는 메서드는 출력을 수신기에 쓰기 위한 메서드입니다. **Write**, **WriteIf**, **WriteLine**, **WriteLineIf**, **Assert**및 **Fail**이 있습니다. 이러한 메서드는 두 가지 범주로 나눌 수 있습니다. **WriteIf**, **WriteLineIf**및 **Assert** 는 부울 조건을 테스트 하 고 조건의 값을 기준으로 작성 하거나 쓰지 않고 모든 내보내기 출력을 무조건 **작성**, **WriteLine**및 **실패** 합니다. **WriteIf** 및 **WriteLineIf** 메서드는 조건이 `true`인 경우 출력을 내보내며 **Assert** 메서드는 조건이 `false`인 경우 출력을 내보냅니다.  
  
 추적 및 디버깅 전략을 디자인할 때 원하는 출력 모양을 고려해야 합니다. 관련 없는 정보로 채워진 여러 **Write** 문은 읽기 어려운 로그를 생성합니다. 다른 한편으로는 **WriteLine**을 사용하여 별도의 줄에 관련된 문을 넣으면 함께 속한 정보를 구분하기 어렵게 될 수도 있습니다. 일반적으로 여러 소스의 정보를 결합하여 단일 정보 메시지를 생성하려는 경우 여러 **Write** 문을 사용하고, 완전한 단일 메시지를 생성하려는 경우 **WriteLine** 문을 사용합니다.  
  
### <a name="to-write-a-complete-line"></a>완전한 줄을 작성하려면  
  
1. <xref:System.Diagnostics.Trace.WriteLine%2A> 또는 <xref:System.Diagnostics.Trace.WriteLineIf%2A> 메서드를 호출합니다.  
  
     이 메서드가 반환하는 메시지의 끝에 캐리지 리턴을 추가합니다. 그러면 **Write**, **WriteIf**, **WriteLine** 또는 **WriteLineIf**에서 반환한 다음 메시지가 다음 줄에서 시작됩니다.  
  
    ```vb  
    Dim errorFlag As Boolean = False  
    Trace.WriteLine("Error in AppendData procedure.")  
    Trace.WriteLineIf(errorFlag, "Error in AppendData procedure.")  
    ```  
  
    ```csharp  
    bool errorFlag = false;  
    System.Diagnostics.Trace.WriteLine ("Error in AppendData procedure.");  
    System.Diagnostics.Trace.WriteLineIf(errorFlag,   
       "Error in AppendData procedure.");  
    ```  
  
### <a name="to-write-a-partial-line"></a>부분 줄을 작성하려면  
  
1. <xref:System.Diagnostics.Trace.Write%2A> 또는 <xref:System.Diagnostics.Trace.WriteIf%2A> 메서드를 호출합니다.  
  
     **Write**, **WriteIf**, **WriteLine** 또는 **WriteLineIf**에서 출력하는 다음 메시지는 **Write** 또는 **WriteIf** 문에서 출력하는 메시지와 동일한 줄에서 시작됩니다.  
  
    ```vb  
    Dim errorFlag As Boolean = False  
    Trace.WriteIf(errorFlag, "Error in AppendData procedure.")  
    Debug.WriteIf(errorFlag, "Transaction abandoned.")  
    Trace.Write("Invalid value for data request")  
    ```  
  
    ```csharp  
    bool errorFlag = false;  
    System.Diagnostics.Trace.WriteIf(errorFlag,   
       "Error in AppendData procedure.");  
    System.Diagnostics.Debug.WriteIf(errorFlag, "Transaction abandoned.");  
    Trace.Write("Invalid value for data request");  
    ```  
  
### <a name="to-verify-that-certain-conditions-exist-either-before-or-after-you-execute-a-method"></a>메서드를 실행하기 전후에 특정 조건이 있는지 확인하려면  
  
1. <xref:System.Diagnostics.Trace.Assert%2A> 메서드를 호출합니다.  
  
    ```vb  
    Dim i As Integer = 4  
    Trace.Assert(i = 5, "i is not equal to 5.")  
    ```  
  
    ```csharp  
    int i = 4;  
    System.Diagnostics.Trace.Assert(i == 5, "i is not equal to 5.");  
    ```  
  
    > [!NOTE]
    > 추적과 디버깅 둘 다에 **Assert**를 사용할 수 있습니다. 이 예제에서는 **수신기** 컬렉션의 수신기로 호출 스택을 출력합니다. 자세한 내용은 [관리 코드의 어설션](/visualstudio/debugger/assertions-in-managed-code) 및 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType>를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Diagnostics.Debug.WriteIf%2A?displayProperty=nameWithType>
- <xref:System.Diagnostics.Debug.WriteLineIf%2A?displayProperty=nameWithType>
- <xref:System.Diagnostics.Trace.WriteIf%2A?displayProperty=nameWithType>
- <xref:System.Diagnostics.Trace.WriteLineIf%2A?displayProperty=nameWithType>
- [응용 프로그램 추적 및 조율](tracing-and-instrumenting-applications.md)
- [방법: 추적 스위치 만들기, 초기화 및 구성](how-to-create-initialize-and-configure-trace-switches.md)
- [추적 스위치](trace-switches.md)
- [추적 수신기](trace-listeners.md)
