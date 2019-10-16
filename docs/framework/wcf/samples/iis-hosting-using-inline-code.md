---
title: 인라인 코드를 사용한 IIS 호스팅
ms.date: 03/30/2017
helpviewer_keywords:
- Web hosted service
- IIS Hosting Using Inline Code Sample [Windows Communication Foundation]
ms.assetid: 56fe3687-a34b-4661-8e30-b33770f413fa
ms.openlocfilehash: 7713c8ca690570ee80721329a7857e6111c93e2f
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70893207"
---
# <a name="iis-hosting-using-inline-code"></a>인라인 코드를 사용한 IIS 호스팅

이 샘플에서는 IIS(인터넷 정보 서비스)에서 호스팅하는 서비스를 구현하는 방법을 보여 줍니다. 여기서 서비스 코드는 .svc 파일에 인라인으로 포함되어 있으며 필요할 때 컴파일됩니다. 또한 서비스 코드를 애플리케이션의 \App_Code 디렉터리에 있는 소스 코드 파일에서 직접 구현하거나 \bin에 배포된 어셈블리로 컴파일할 수 있습니다. 이 샘플에서는 이러한 기술은 보여 주지 않습니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebHost\InlineCode`

이 샘플에서는 요청-회신 통신 패턴을 정의하는 계약을 구현하는 일반적인 서비스를 보여 줍니다. 이 서비스는 IIS에서 호스팅되며 서비스 코드는 모두 Service.svc 파일에 포함되어 있습니다. 서비스는 호스트에서 활성화되며 서비스로 전송된 첫 번째 메시지에 의해 필요할 때 컴파일됩니다. 미리 컴파일할 필요는 없습니다. 서비스는 다음 코드에 정의된 대로 `ICalculator` 계약을 구현합니다.

```csharp
// Define a service contract.
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
    public interface ICalculator
{
    [OperationContract]
    double Add(double n1, double n2);
    [OperationContract]
    double Subtract(double n1, double n2);
    [OperationContract]
    double Multiply(double n1, double n2);
    [OperationContract]
    double Divide(double n1, double n2);
}
```

이 서비스 구현에서는 해당 결과를 계산하여 반환합니다.

`<%@ServiceHost language=c# Debug="true" Service="Microsoft.ServiceModel.Samples.CalculatorService" %>`

```csharp
// Service class that implements the service contract.
public class CalculatorService : ICalculator
{
    public double Add(double n1, double n2)
    {
        return n1 + n2;
    }
    public double Subtract(double n1, double n2)
    {
        return n1 - n2;
    }
    public double Multiply(double n1, double n2)
    {
        return n1 * n2;
    }
    public double Divide(double n1, double n2)
    {
        return n1 / n2;
    }
}
```

샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714

Press <ENTER> to terminate client.
```

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.

3. 솔루션이 빌드된 후에는 setup.exe를 실행 하 여 IIS 7.0에서 ServiceModelSamples 응용 프로그램을 설정 합니다. 이제 ServiceModelSamples 디렉터리가 IIS 7.0 응용 프로그램으로 표시 됩니다.

4. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요. 이 서비스 [를 호출할 수 있는 클라이언트 응용 프로그램을 만드는 방법에 대 한 예제는 방법: 클라이언트](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md)를 만듭니다.

## <a name="see-also"></a>참고자료

- [AppFabric 호스팅 및 지 속성 샘플](https://go.microsoft.com/fwlink/?LinkId=193961)
