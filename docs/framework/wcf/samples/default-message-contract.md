---
title: 기본 메시지 계약
ms.date: 03/30/2017
helpviewer_keywords:
- Message Contract
ms.assetid: 5a200b78-1a46-4104-b7fb-da6dbab33893
ms.openlocfilehash: 2115ac88c52efca09d32a870fc52905f80f6f746
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045047"
---
# <a name="default-message-contract"></a>기본 메시지 계약
Default Message Contract 샘플에서는 사용자 지정 사용자 정의 메시지를 서비스 작업에 전달하고 전달받는 서비스를 보여 줍니다. 이 샘플은 형식화 된 서비스로 계산기 인터페이스를 구현 하는 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md) 을 기반으로 합니다. [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)부분에서 사용 되는 더하기, 빼기, 곱하기 및 나누기에 대 한 개별 서비스 작업 대신이 샘플은 피연산자와 연산자를 모두 포함 하는 사용자 지정 메시지를 전달 하 고 결과를 반환 합니다. 산술 계산.  
  
 클라이언트는 콘솔 프로그램(.exe)이고 서비스 라이브러리(.dll)는 IIS(인터넷 정보 서비스)에서 호스팅됩니다. 콘솔 창에는 클라이언트 동작이 표시됩니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 서비스에서는 `MyMessage` 형식의 사용자 지정 메시지를 수락하고 반환하는 단일 서비스 작업이 정의됩니다. 이 샘플에서는 요청 및 응답 메시지의 형식이 동일하지만 필요한 경우 서로 다른 메시지 계약이 될 수 있습니다.  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculator  
{  
    [OperationContract(Action="http://test/MyMessage_action",  
                  ReplyAction="http://test/MyMessage_action")]  
    MyMessage Calculate(MyMessage request);  
}  
```  
  
 사용자 지정 메시지 `MyMessage`는 <xref:System.ServiceModel.MessageContractAttribute>, <xref:System.ServiceModel.MessageHeaderAttribute> 및 <xref:System.ServiceModel.MessageBodyMemberAttribute> 특성과 함께 주석 처리된 클래스에서 정의됩니다. 이 샘플에서는 세 번째 생성자만 사용됩니다. 메시지 계약을 사용하면 SOAP 메시지를 완전히 제어할 수 있습니다. 이 샘플에서는 <xref:System.ServiceModel.MessageHeaderAttribute> 특성을 사용하여 SOAP 헤더에 `Operation`을 배치합니다. 피연산자 `N1`, `N2` 및 `Result`에는 <xref:System.ServiceModel.MessageBodyMemberAttribute> 특성이 적용되어 있으므로 이러한 피연산자는 SOAP 본문 내에 표시됩니다.  
  
```csharp
[MessageContract]  
public class MyMessage  
{  
    private string operation;  
    private double n1;  
    private double n2;  
    private double result;  
  
    //Constructor - create an empty message.  
  
    public MyMessage() {}  
  
    //Constructor - create a message and populate its members.  
  
    public MyMessage(double n1, double n2, string operation,   
                     double result)  
    {  
        this.n1 = n1;  
        this.n2 = n2;  
        this.operation = operation;  
        this.result = result;  
    }  
  
    //Constructor - create a message from another message.  
  
    public MyMessage(MyMessage message)  
    {  
        this.n1 = message.n1;  
        this.n2 = message.n2;  
        this.operation = message.operation;  
        this.result = message.result;  
    }  
  
    [MessageHeader]  
    public string Operation  
    {  
        get { return operation; }  
        set { operation = value; }  
    }  
  
    [MessageBodyMember]  
    public double N1  
    {  
        get { return n1; }  
        set { n1 = value; }  
    }  
  
    [MessageBodyMember]  
    public double N2  
    {  
        get { return n2; }  
        set { n2 = value; }  
    }  
  
    [MessageBodyMember]  
    public double Result  
    {  
        get { return result; }  
        set { result = value; }  
    }  
}  
```  
  
 구현 클래스에는 `Calculate` 서비스 작업의 코드가 포함됩니다. 다음 샘플 코드에서와 같이 `CalculateService` 클래스는 요청 메시지로부터 피연산자와 연산자를 받고 요청된 계산의 결과가 포함된 응답 메시지를 만듭니다.  
  
```csharp
// Service class which implements the service contract.  
public class CalculatorService : ICalculator  
{  
    // Perform a calculation.  
  
    public MyMessage Calculate(MyMessage request)  
    {  
        MyMessage response = new MyMessage(request);  
        switch (request.Operation)  
        {  
            case "+":  
                response.Result = request.N1 + request.N2;  
                break;  
            case "-":  
                response.Result = request.N1 - request.N2;  
                break;  
            case "*":  
                response.Result = request.N1 * request.N2;  
                break;  
            case "/":  
                response.Result = request.N1 / request.N2;  
                break;  
            default:  
                response.Result = 0.0D;  
                break;  
        }  
        return response;  
    }  
}  
```  
  
 클라이언트에 대해 생성 된 클라이언트 코드는 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 도구를 사용 하 여 만들었습니다. 필요한 경우 이 도구는 생성된 클라이언트 코드에 자동으로 메시지 계약 형식을 만듭니다. `/messageContract` 명령 옵션을 지정하여 메시지 계약을 강제로 생성할 수 있습니다.  
  
```console  
svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" /o:client\generatedClient.cs http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 다음 샘플 코드에서는 `MyMessage` 메시지를 사용하는 클라이언트를 보여 줍니다.  
  
```csharp
// Create a client with given client endpoint configuration  
CalculatorClient client = new CalculatorClient();  
  
// Perform addition using a typed message.  
  
MyMessage request = new MyMessage() 
                    {  
                        N1 = 100D,  
                        N2 = 15.99D,  
                        Operation = "+"  
                    };
MyMessage response = ((ICalculator)client).Calculate(request);  
Console.WriteLine("Add({0},{1}) = {2}", request.N1, request.N2, response.Result);  
```  
  
 샘플을 실행하면 계산이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```console  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
 여기서 클라이언트와 서비스 작업 간에 사용자 지정 사용자 정의 메시지가 전달되었습니다. 메시지 계약은 피연산자와 결과가 메시지 본문에 있고 연산자는 메시지 헤더에 있는 것으로 정의했습니다. 메시지 로깅을 구성하여 이 메시지 구조를 살펴볼 수 있습니다.  
  
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
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Message\Default`  
