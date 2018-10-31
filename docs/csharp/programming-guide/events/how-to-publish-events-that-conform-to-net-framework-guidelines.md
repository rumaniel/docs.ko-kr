---
title: '방법: .NET Framework 지침을 따르는 이벤트 게시(C# 프로그래밍 가이드)'
ms.date: 07/20/2015
helpviewer_keywords:
- events [C#], implementation guidelines
ms.assetid: 9310ae16-8627-44a2-b08c-05e5976202b1
ms.openlocfilehash: 9a17aaec20b03325abadfcc168f7ac4653f300df
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48030606"
---
# <a name="how-to-publish-events-that-conform-to-net-framework-guidelines-c-programming-guide"></a>방법: .NET Framework 지침을 따르는 이벤트 게시(C# 프로그래밍 가이드)
다음 절차에서는 표준 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 패턴을 따르는 이벤트를 클래스와 구조체에 추가하는 방법을 보여 줍니다. [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 클래스 라이브러리의 모든 이벤트는 다음과 같이 정의된 <xref:System.EventHandler> 대리자를 기반으로 합니다.  
  
```csharp  
public delegate void EventHandler(object sender, EventArgs e);  
```  
  
> [!NOTE]
>  [!INCLUDE[dnprdnlong](~/includes/dnprdnlong-md.md)]에서는 이 대리자의 제네릭 버전인 <xref:System.EventHandler%601>가 도입되었습니다. 다음 예제에서는 두 버전을 사용하는 방법을 모두 보여 줍니다.  
  
 정의하는 클래스의 이벤트는 값을 반환하는 대리자를 포함하여 유효한 모든 대리자 형식을 기반으로 할 수 있지만 다음 예제와 같이 <xref:System.EventHandler>를 사용하여 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 패턴에 따라 이벤트를 만드는 것이 좋습니다.  
  
### <a name="to-publish-events-based-on-the-eventhandler-pattern"></a>EventHandler 패턴에 따라 이벤트를 게시하려면  
  
1.  이벤트와 함께 사용자 지정 데이터를 보낼 필요가 없는 경우 이 단계를 건너뛰고 3a 단계로 이동합니다. 게시자 및 구독자 클래스 둘 다에 표시되는 범위에서 사용자 지정 데이터에 대한 클래스를 선언합니다. 그런 다음 사용자 지정 이벤트 데이터를 저장하는 데 필요한 멤버를 추가합니다. 이 예제에서는 간단한 문자열이 반환됩니다.  
  
    ```csharp  
    public class CustomEventArgs : EventArgs  
    {  
        public CustomEventArgs(string s)  
        {  
            msg = s;  
        }  
        private string msg;  
        public string Message  
        {  
            get { return msg; }  
        }   
    }  
    ```  
  
2.  <xref:System.EventHandler%601>의 제네릭 버전을 사용하는 경우 이 단계를 건너뜁니다. 게시 클래스에서 대리자를 선언합니다. *EventHandler*로 끝나는 이름을 지정합니다. 두 번째 매개 변수는 사용자 지정 EventArgs 형식을 지정합니다.  
  
    ```csharp  
    public delegate void CustomEventHandler(object sender, CustomEventArgs a);  
    ```  
  
3.  다음 단계 중 하나를 사용하여 게시 클래스에서 이벤트를 선언합니다.  
  
    1.  사용자 지정 EventArgs 클래스가 없는 경우 이벤트 유형은 제네릭이 아닌 EventHandler 대리자가 됩니다. C# 프로젝트를 만들 때 포함된 <xref:System> 네임스페이스에서 이미 선언되었기 때문에 대리자를 선언할 필요는 없습니다. 게시자 클래스에 다음 코드를 추가합니다.  
  
        ```csharp  
        public event EventHandler RaiseCustomEvent;  
        ```  
  
    2.  제네릭이 아닌 버전의 <xref:System.EventHandler>를 사용 중이고 <xref:System.EventArgs>에서 파생된 사용자 지정 클래스가 있는 경우 게시 클래스 내에서 이벤트를 선언하고 2단계의 대리자를 형식으로 사용합니다.  
  
        ```csharp  
        public event CustomEventHandler RaiseCustomEvent;  
        ```  
  
    3.  제네릭 버전을 사용하는 경우에는 사용자 지정 대리자가 필요하지 않습니다. 대신, 게시 클래스에서 이벤트 유형을 `EventHandler<CustomEventArgs>`로 지정하고 고유한 클래스 이름을 꺾쇠 괄호로 묶어 대체합니다.  
  
        ```csharp  
        public event EventHandler<CustomEventArgs> RaiseCustomEvent;  
        ```  
  
## <a name="example"></a>예  
 다음 예제에서는 사용자 지정 EventArgs 클래스와 <xref:System.EventHandler%601>를 이벤트 유형으로 사용하여 이전 단계를 보여 줍니다.  
  
 [!code-csharp[csProgGuideEvents#2](../../../csharp/programming-guide/events/codesnippet/CSharp/how-to-publish-events-that-conform-to-net-framework-guidelines_1.cs)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Delegate>  
- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [이벤트](../../../csharp/programming-guide/events/index.md)  
- [대리자](../../../csharp/programming-guide/delegates/index.md)
