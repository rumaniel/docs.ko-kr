---
title: 동기 및 비동기 작업
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- service contracts [WCF], synchronous operations
- service contracts [WCF], asynchronous operations
ms.assetid: db8a51cb-67e6-411b-9035-e5821ed350c9
ms.openlocfilehash: 14bf9c89fd7142746b93cc45af6c2152e8700571
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988539"
---
# <a name="synchronous-and-asynchronous-operations"></a>동기 및 비동기 작업
이 항목에서는 비동기 서비스 작업의 구현 및 호출에 대해 설명합니다.  
  
 대부분의 응용 프로그램은 메서드를 비동기적으로 호출합니다. 이렇게 하면 메서드 호출이 실행되는 동안 응용 프로그램이 유용한 작업을 계속할 수 있기 때문입니다. WCF(Windows Communication Foundation) 서비스와 클라이언트는 두 개의 다른 애플리케이션 수준에서 비동기 작업 호출에 참여할 수 있으므로 WCF 애플리케이션에서 보다 유연하게 대화형 작업과 균형을 맞춰 처리량을 최대화할 수 있습니다.  
  
## <a name="types-of-asynchronous-operations"></a>비동기 작업 형식  
 WCF의 모든 서비스 계약은 매개 변수 형식 및 반환 값과 관계없이 WCF 특성을 사용하여 클라이언트와 서비스 간의 특정 메시지 교환 패턴을 지정합니다. WCF에서는 인바운드 및 아웃바운드 메시지를 자동으로 적절한 서비스 작업이나 실행 중인 클라이언트 코드로 라우팅합니다.  
  
 클라이언트는 특정 작업의 메시지 교환 패턴을 지정하는 서비스 계약만 소유하며 기본 메시지 교환 패턴이 확인되는 한 클라이언트가 선택한 프로그래밍 모델을 개발자에게 제공할 수 있습니다. 또한 지정된 메시지 패턴이 확인되는 한 서비스도 임의의 방식으로 작업을 구현할 수 있습니다.  
  
 서비스나 클라이언트 구현에서 서비스 계약이 독립되면 WCF 애플리케이션에서 다음과 같은 비동기 실행을 구현할 수 있습니다.  
  
- 클라이언트는 동기 메시지 교환을 사용하여 요청/응답 작업을 비동기적으로 호출할 수 있습니다.  
  
- 서비스는 동기 메시지 교환을 사용하여 요청/응답 작업을 비동기적으로 구현할 수 있습니다.  
  
- 클라이언트나 서비스의 구현에 관계없이 메시지 교환은 단방향일 수 있습니다.  
  
### <a name="suggested-asynchronous-scenarios"></a>제안된 비동기 시나리오  
 작업 서비스 구현에서 I/O 작업을 수행하는 경우와 같이 블로킹 호출을 만드는 경우 서비스 작업 구현에서 비동기 접근 방법을 사용하는 것이 좋습니다. 비동기 작업 구현 중인 경우에는 비동기 작업 및 메서드를 호출하여 비동기 호출 경로를 최대한 확장해 보세요. 예를 들면 `BeginOperationTwo()` 내에서 `BeginOperationOne()`를 호출합니다.  
  
- 다음과 같은 경우에는 클라이언트 또는 호출 응용 프로그램에서 비동기 접근 방법을 사용하세요.  
  
- 중간 계층 응용 프로그램에서 작업을 호출하는 경우. 이러한 시나리오에 대한 자세한 내용은 [중간 계층 클라이언트 애플리케이션](../../../docs/framework/wcf/feature-details/middle-tier-client-applications.md)을 참조하세요.  
  
- ASP.NET 페이지 내에서 작업을 호출하는 경우에는 비동기 페이지를 사용하세요.  
  
- Windows Forms 또는 WPF(Windows Presentation Foundation) 등의 단일 스레드 애플리케이션에서 작업을 호출하는 경우. 이벤트 기반의 비동기 호출 모델을 사용하는 경우에는 결과 이벤트가 UI 스레드에서 발생하기 때문에 사용자가 직접 여러 스레드를 처리할 필요 없이 응용 프로그램에 응답이 추가됩니다.  
  
- 일반적으로 동기 호출과 비동기 호출 중에서 선택해야 하는 경우에는 비동기 호출을 선택하세요.  
  
### <a name="implementing-an-asynchronous-service-operation"></a>비동기 서비스 작업 구현  
 다음 세 가지 방법 중 하나를 사용하여 비동기 작업을 구현할 수 있습니다.  
  
1. 작업 기반 비동기 패턴  
  
2. 이벤트 기반 비동기 패턴  
  
3. IAsyncResult 비동기 패턴  
  
#### <a name="task-based-asynchronous-pattern"></a>작업 기반 비동기 패턴  
 작업 기반 비동기 패턴은 가장 쉽고 단순하기 때문에 비동기 작업을 구현하는 데 가장 선호하는 방법입니다. 이 방법을 사용하려면 서비스 작업을 구현하고 반환 형식으로 Task\<T>를 지정하면 됩니다. 여기서, T는 논리 연산에서 반환하는 형식입니다. 예를 들어:  
  
```csharp  
public class SampleService:ISampleService   
{   
   // ...  
   public async Task<string> SampleMethodTaskAsync(string msg)   
   {   
      return Task<string>.Factory.StartNew(() =>   
      {   
         return msg;   
      });   
   }  
   // ...  
}  
```  
  
 논리 연산에서는 문자열을 반환하므로 SampleMethodTaskAsync 작업은 Task\<string>을 반환합니다. 작업 기반 비동기 패턴에 대한 자세한 내용은 [작업 기반 비동기 패턴](https://go.microsoft.com/fwlink/?LinkId=232504)을 참조하세요.  
  
> [!WARNING]
> 작업 기반 비동기 패턴을 사용할 경우 작업 완료를 대기하는 동안 예외가 발생하면 T:System.AggregateException이 throw될 수 있습니다. 클라이언트 또는 서비스에서 이 예외가 발생할 수 있습니다.  
  
#### <a name="event-based-asynchronous-pattern"></a>이벤트 기반 비동기 패턴  
 이벤트 기반 비동기 패턴을 지원하는 서비스에는 MethodNameAsync라는 작업이 하나 이상 있습니다. 이러한 메서드는 현재 스레드에서 동일한 작업을 수행하는 동기 버전을 미러링할 수 있습니다. 또한 이 클래스에는 MethodNameCompleted 이벤트가 있을 수 있고 MethodNameAsyncCancel 메서드가 있거나 단순히 CancelAsync 메서드가 있을 수 있습니다. 작업을 호출하려는 클라이언트는 작업이 완료될 때 호출할 이벤트 처리기를 정의합니다.  
  
 다음 코드 조각에서는 이벤트 기반 비동기 패턴을 사용하여 비동기 작업을 선언하는 방법을 보여 줍니다.  
  
```csharp  
public class AsyncExample  
{  
    // Synchronous methods.  
    public int Method1(string param);  
    public void Method2(double param);  
  
    // Asynchronous methods.  
    public void Method1Async(string param);  
    public void Method1Async(string param, object userState);  
    public event Method1CompletedEventHandler Method1Completed;  
  
    public void Method2Async(double param);  
    public void Method2Async(double param, object userState);  
    public event Method2CompletedEventHandler Method2Completed;  
  
    public void CancelAsync(object userState);  
  
    public bool IsBusy { get; }  
  
    // Class implementation not shown.  
}  
```  
  
 이벤트 기반 비동기 패턴에 대한 자세한 내용은 [이벤트 기반 비동기 패턴](https://go.microsoft.com/fwlink/?LinkId=232515)을 참조하세요.  
  
#### <a name="iasyncresult-asynchronous-pattern"></a>IAsyncResult 비동기 패턴  
 비동기 방식으로 .NET Framework 비동기 프로그래밍 패턴을 사용 하 여 서비스 작업을 구현 하 고 `<Begin>` <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> 속성을 `true`로 설정 하 여 메서드를 표시할 수 있습니다. 이 경우 비동기 작업은 동기 작업과 동일한 형식으로 메타 데이터에 노출 됩니다. 요청 메시지 및 상관 관계가 지정 된 응답 메시지를 사용 하 여 단일 작업으로 노출 됩니다. 그런 다음 클라이언트 프로그래밍 모델에서는 둘 중 하나를 선택할 수 있습니다. 즉, 서비스가 호출될 때 요청-응답 메시지 교환이 발생하는 한 이 패턴을 동기 작업이나 비동기 작업으로 나타낼 수 있습니다.  
  
 일반적으로 시스템의 비동기 특성을 사용하는 경우 스레드에 대한 종속성을 사용하지 않아야 합니다.  작업 디스패치 처리의 다양한 단계에 데이터를 전달하는 가장 안정적인 방법은 확장을 사용하는 것입니다.  
  
 예는 [방법: 비동기 서비스 작업](../../../docs/framework/wcf/how-to-implement-an-asynchronous-service-operation.md)을 구현 합니다.  
  
 클라이언트 응용 프로그램에서 호출되는 방식에 관계없이 비동기적으로 실행되는 계약 작업 `X`를 정의하려면 다음을 수행합니다.  
  
- 패턴 `BeginOperation` 및 `EndOperation`을 사용하여 두 개의 메서드를 정의합니다.  
  
- `BeginOperation` 메서드는 작업에 대한 `in` 및 `ref` 매개 변수를 포함하고 <xref:System.IAsyncResult> 형식을 반환합니다.  
  
- `EndOperation` 메서드는 <xref:System.IAsyncResult> 및 `out` 매개 변수뿐 아니라 `ref` 매개 변수를 포함하고 작업 반환 형식을 반환합니다.  
  
 다음 메서드를 예로 들 수 있습니다.  
  
```csharp  
int DoWork(string data, ref string inout, out string outonly)  
```  
  
```vb  
Function DoWork(ByVal data As String, ByRef inout As String, _out outonly As out) As Integer  
```  
  
 비동기 작업을 만들려는 경우 두 가지 메서드는 다음과 같습니다.  
  
```csharp  
[OperationContract(AsyncPattern=true)]
IAsyncResult BeginDoWork(string data,
                         ref string inout,
                         AsyncCallback callback,
                         object state);
int EndDoWork(ref string inout, out string outonly, IAsyncResult result);  
```  
  
```vb  
<OperationContract(AsyncPattern := True)>
Function BeginDoWork(ByVal data As String, _
                     ByRef inout As String, _
                     ByVal callback As AsyncCallback, _
                     ByVal state As Object) As IAsyncResult
Function EndDoWork(ByRef inout As String, ByRef outonly As String, ByVal result As IAsyncResult) As Integer  
```  
  
> [!NOTE]
> <xref:System.ServiceModel.OperationContractAttribute> 특성은 `BeginDoWork` 메서드에만 적용됩니다. 결과 계약에는 `DoWork`라는 하나의 WSDL 작업이 포함됩니다.  
  
### <a name="client-side-asynchronous-invocations"></a>클라이언트측 비동기 호출  
 WCF 클라이언트 애플리케이션은 위에서 설명한 세 가지 비동기 호출 모델 중 하나를 사용할 수 있습니다.  
  
 작업 기반 모델을 사용하는 경우 다음 코드 조각과 같이 await 키워드를 사용하여 작업을 호출합니다.  
  
```  
await simpleServiceClient.SampleMethodTaskAsync("hello, world");  
```  
  
 이벤트 기반 비동기 패턴을 사용할 경우 응답 알림을 받기 위해 이벤트 처리기를 추가하기만 하면 되고 결과 이벤트가 사용자 인터페이스 스레드에서 자동으로 발생합니다. 이 방법을 사용하려면 다음 예제와 같이 [ServiceModel Metadata 유틸리티 도구(Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)에서 **/async**와 **/tcv:Version35** 명령 옵션을 모두 지정합니다.  
  
```  
svcutil http://localhost:8000/servicemodelsamples/service/mex /async /tcv:Version35  
```  
  
 그러면 Svcutil.exe는 호출 애플리케이션이 응답을 받고 적절한 작업을 수행하기 위한 이벤트 처리기를 구현하고 할당할 수 있는 이벤트 인프라를 사용하여 WCF 클라이언트 클래스를 생성합니다. 전체 예제는 [방법: 서비스 작업을 비동기적](../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)으로 호출 합니다.  
  
 그러나 이벤트 기반 비동기 모델은 [!INCLUDE[netfx35_long](../../../includes/netfx35-long-md.md)]에서만 사용할 수 있으며, <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType>를 사용하여 WCF 클라이언트 채널이 만들어진 경우에는 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]에서도 지원되지 않습니다. WCF 클라이언트 채널 개체가 있는 경우 <xref:System.IAsyncResult?displayProperty=nameWithType> 개체를 사용하여 작업을 비동기적으로 호출해야 합니다. 이 방법을 사용하려면 다음 예제와 같이 [ServiceModel Metadata 유틸리티 도구(Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)에서 **/async** 명령 옵션을 지정합니다.  
  
```  
svcutil http://localhost:8000/servicemodelsamples/service/mex /async   
```  
  
 그러면 각 작업이 `<Begin>` 속성이 <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A>로 설정된 `true` 메서드와 해당 `<End>` 메서드로 모델링되는 서비스 계약이 생성됩니다. 을 <xref:System.ServiceModel.ChannelFactory%601>사용 하는 전체 예제를 보려면 [방법: 채널 팩터리](../../../docs/framework/wcf/feature-details/how-to-call-operations-asynchronously-using-a-channel-factory.md)를 사용 하 여 작업을 비동기적으로 호출 합니다.  
  
 두 경우 모두 응용 프로그램은 서비스가 동기적으로 구현되더라도 동일한 패턴을 사용하여 로컬 동기 메서드를 비동기적으로 호출하는 것과 같은 방식으로 작업을 비동기적으로 호출할 수 있습니다. 작업이 구현되는 방식은 클라이언트에게 중요하지 않습니다. 응답 메시지가 도착하면 메시지 내용이 클라이언트의 비동기 <`End`> 메서드에 디스패치되고 클라이언트는 정보를 검색합니다.  
  
### <a name="one-way-message-exchange-patterns"></a>단방향 메시지 교환 패턴  
 클라이언트 또는 서비스에서 단독으로 어느 방향으로나 단방향 작업(<xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A?displayProperty=nameWithType>가 `true`인 작업에는 관련 응답이 없음)을 보낼 수 있는 비동기 메시지 교환 패턴을 만들 수도 있습니다. 이 메시지 교환 패턴에서는 단방향 메시지에 이중 메시지 교환 패턴을 사용합니다. 이 경우 서비스 계약은 어느 쪽에서든 필요에 따라 적절하게 비동기 호출 또는 구현으로 구현할 수 있는 단방향 메시지 교환을 지정합니다. 일반적으로 계약이 단방향 메시지 교환이면 메시지가 전송된 후 응용 프로그램이 응답을 기다리지 않고 계속해서 다른 작업을 수행할 수 있으므로 구현이 대체로 비동기적일 수 있습니다.  
  
### <a name="event-based-asynchronous-clients-and-message-contracts"></a>이벤트 기반 비동기 클라이언트 및 메시지 계약  
 이벤트 기반 비동기 모델에 대한 디자인 지침에 따르면 둘 이상의 값이 반환될 경우 그 중 하나는 `Result` 속성으로 반환되고 나머지 값은 <xref:System.EventArgs> 개체의 속성으로 반환됩니다. 따라서 클라이언트가 이벤트 기반 비동기 명령 옵션을 사용하여 메타데이터를 가져오고 작업이 둘 이상의 값을 반환할 경우 기본 <xref:System.EventArgs> 개체는 그 중 하나를 `Result` 속성으로 반환하고, 나머지 값은 <xref:System.EventArgs> 개체의 속성이 됩니다.  
  
 메시지 개체를 `Result` 속성으로 받고 반환된 값을 해당 개체의 속성으로 포함하려면 **/messageContract** 명령 옵션을 사용합니다. 이렇게 하면 응답 메시지를 `Result` 개체의 <xref:System.EventArgs> 속성으로 반환하는 서명이 생성됩니다. 모든 내부 반환 값은 응답 메시지 개체의 속성이 됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A>
- <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A>
