---
title: 형식화 되지 않은 요청-회신
ms.date: 03/30/2017
ms.assetid: 0bf0f9d9-7caf-4d3d-8c9e-2d468cca16a5
ms.openlocfilehash: 132ae05236b23ff5bb0cce67d66d26d308cce305
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038679"
---
# <a name="untyped-requestreply"></a>형식없는 요청/회신
이 샘플에서는 Message 클래스를 사용하는 작업 계약을 정의하는 방법을 보여 줍니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 이 샘플은 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)을 기반으로 합니다. 서비스 계약에서는 메시지 형식을 인수로 받는 작업을 하나 정의하고 메시지를 반환합니다. 작업에서는 필요한 데이터를 모두 수집하여 메시지 본문으로부터 합계를 계산한 다음 컴퓨팅된 합계를 반환 메시지의 본문으로 보냅니다.  
  
```csharp
[OperationContract(Action = CalculatorService.RequestAction, ReplyAction = CalculatorService.ReplyAction)]  
Message ComputeSum(Message request);  
```  
  
 서비스에서 작업은 입력 메시지로 전달된 정수의 배열을 검색한 다음 합계를 계산합니다. 샘플에서는 응답 메시지를 보내기 위해 적절한 메시지 버전 및 동작으로 새 메시지를 만들고 계산된 합계를 본문으로 추가합니다. 다음 샘플 코드에서는 이를 보여 줍니다.  
  
```csharp
public Message ComputeSum(Message request)  
{  
    //The body of the message contains a list of numbers which will be   
    //read as a int[] using GetBody<T>  
    int result = 0;  
  
    int[] inputs = request.GetBody<int[]>();  
    foreach (int i in inputs)  
    {  
        result += i;  
    }  
  
    Message response = Message.CreateMessage(request.Version,   
                                      ReplyAction, result);  
    return response;  
}  
```  
  
 클라이언트는 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 에서 생성 된 코드를 사용 하 여 원격 서비스에 대 한 프록시를 만듭니다. 요청 메시지를 보내려면 클라이언트에 내부 채널에 따라 결정되는 메시지 버전이 필요합니다. 따라서 여기서는 만들어지는 프록시 채널의 범위에 맞게 <xref:System.ServiceModel.OperationContextScope> 속성에 올바른 메시지 버전이 채워진 <xref:System.ServiceModel.OperationContext>를 만드는 새 `OutgoingMessageHeaders.MessageVersion`를 만듭니다. 클라이언트에서는 요청 메시지에 본문으로 입력 배열을 전달한 다음 프록시에서 `ComputeSum`을 호출합니다. 그런 다음 클라이언트에서는 회신 메시지에 있는 `GetBody<T>` 메서드에 액세스하여 전달한 입력의 합계를 검색합니다. 다음 샘플 코드에서는 이를 보여 줍니다.  
  
```csharp
using (new OperationContextScope(client.InnerChannel))  
{  
    // Call the Sum service operation.  
    int[] values = { 1, 2, 3, 4, 5 };  
    Message request = Message.CreateMessage(  
        OperationContext.Current.OutgoingMessageHeaders.MessageVersion,   
        RequestAction, values);  
    Message reply = client.ComputeSum(request);  
    int response = reply.GetBody<int>();  
  
    Console.WriteLine("Sum of numbers passed (1,2,3,4,5) = {0}",   
                                                       response);  
}  
```  
  
 이 샘플은 웹 호스팅 샘플이기 때문에 클라이언트 실행 파일만 실행해야 합니다. 다음은 클라이언트의 샘플 출력입니다.  
  
```console  
Prompt>Client.exe  
Sum of numbers passed (1,2,3,4,5) = 15  
  
Press <ENTER> to terminate client.  
```  
  
 이 샘플은 웹 호스팅 샘플이기 때문에 샘플의 빌드 및 실행 방법을 보려면 3단계에 있는 링크를 참조하십시오.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Message\Untyped`  
