---
title: 닫기 및 중단을 사용하여 WCF 클라이언트 리소스 해제
description: Dispose는 실패 하 고 네트워크 실패 시 예외를 throw 수 있습니다. 원치 않는 동작이 될 수 있습니다. 대신, 닫기 사용 하 고 리소스를 해제 하려면 클라이언트 네트워크 실패 했을 때 중단 합니다.
ms.date: 11/12/2018
ms.assetid: aff82a8d-933d-4bdc-b0c2-c2f7527204fb
ms.openlocfilehash: 58f828d9cd85806f5f04c349a7de18828ab5f6f2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62007580"
---
# <a name="close-and-abort-release-resources-safely-when-network-connections-have-dropped"></a>닫기 및 네트워크 연결을 삭제 한 경우에 안전 하 게 중단 릴리스 리소스

이 샘플에서는 합니다 `Close` 고 `Abort` 형식화 된 클라이언트를 사용 하는 경우에 리소스를 정리 하는 방법입니다. `using` 문을 네트워크 연결이 안정적이 지 않습니다 때 예외를 발생 합니다. 이 샘플은 기반 합니다 [Getting Started](../../../../docs/framework/wcf/samples/getting-started-sample.md) 계산기 서비스를 구현 하는 합니다. 이 샘플에서 클라이언트는 콘솔 애플리케이션(.exe)이고 서비스는 IIS(인터넷 정보 서비스)를 통해 호스트됩니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

이 샘플에서는 형식화된 클라이언트와 함께 C# "using" 문을 사용할 경우 발생하는 일반적인 두 가지 문제와 예외 발생 후 올바르게 정리되는 코드를 보여 줍니다.

C# "using" 문을 사용하면 결과적으로 `Dispose`()가 호출됩니다. 이는 네트워크 오류 발생 시에 예외를 throw할 수 있는 `Close`()와 동일합니다. "using" 블록의 닫는 중괄호에서 `Dispose`() 호출이 암시적으로 발생하므로 이 예외 원인은 코드를 작성하는 사용자와 읽는 사용자 모두가 알아차리지 못합니다. 이로 인해 애플리케이션 오류가 발생할 가능성이 있습니다.

`DemonstrateProblemUsingCanThrow` 메서드에서 나타나는 첫 번째 문제는 닫는 중괄호로 인해 예외가 throw되고 닫는 중괄호 뒤의 코드가 실행되지 않는다는 것입니다.

```csharp
using (CalculatorClient client = new CalculatorClient())
{
    ...
} // <-- this line might throw
Console.WriteLine("Hope this code wasn't important, because it might not happen.");
```

using 블록 안의 어떠한 항목도 예외를 throw하지 않거나 using 블록 안의 모든 예외가 catch될 경우에도 닫는 중괄호에서 암시적 `Console.WriteLine`() 호출이 예외를 throw할 수 있으므로 `Dispose`이 발생하지 않을 수 있습니다.

`DemonstrateProblemUsingCanThrowAndMask` 메서드에서 나타나는 두 번째 문제는 예외를 throw하는 닫는 중괄호와 관련된 또 다른 문제입니다.

```csharp
using (CalculatorClient client = new CalculatorClient())
{
    ...
    throw new ApplicationException("Hope this exception was not important, because "+
                                   "it might be masked by the Close exception.");
} // <-- this line might throw an exception.
```

`Dispose`()가 "finally" 블록 안에서 발생하므로 `ApplicationException`()가 실패할 경우 `Dispose`은 using 블록 외부에서 표시되지 않습니다. 외부 코드가 `ApplicationException`이 발생하는 시점을 알아야 할 경우 "using" 구문은 이 예외를 마스킹하여 문제를 일으킬 수 있습니다.

마지막으로 이 샘플에서는 `DemonstrateCleanupWithExceptions`에 예외가 발생할 경우 올바르게 정리하는 방법을 보여 줍니다. 이를 위해 오류를 보고하고 `Abort`를 호출하는 try/catch 블록이 사용됩니다. 참조 된 [예상 예외](../../../../docs/framework/wcf/samples/expected-exceptions.md) 클라이언트 호출에서 예외를 catch 하는 방법에 대 한 자세한 세부 정보에 대 한 샘플.

```csharp
try
{
    ...
    client.Close();
}
catch (CommunicationException e)
{
    ...
    client.Abort();
}
catch (TimeoutException e)
{
    ...
    client.Abort();
}
catch (Exception e)
{
    ...
    client.Abort();
    throw;
}
```

> [!NOTE]
> using 문 및 ServiceHost: 대부분의 자체 호스팅 응용 프로그램 서비스를 호스트 약간 넘는 않는 및 이러한 응용 프로그램을 사용 하 여 안전 하 게 사용할 수 있도록 거의 ServiceHost.Close에서 예외를 throw ServiceHost로 문입니다. 그러나 ServiceHost.Close에서 `CommunicationException`을 throw할 수 있으므로 ServiceHost를 닫은 후 애플리케이션이 계속될 경우 using 문을 사용하지 않아야 하고 위에 제공된 패턴을 따라야 합니다.

샘플을 실행하면 작업 응답 및 예외가 클라이언트 콘솔 창에 표시됩니다.

클라이언트 프로세스는 각각 `Divide` 호출을 시도하는 세 개의 시나리오를 실행합니다. 첫 번째 시나리오는 `Dispose`()의 예외로 인해 코드를 건너뛰는 것을 보여 줍니다. 두 번째 시나리오는 `Dispose`()의 예외로 인해 중요한 예외가 마스킹되는 것을 보여 줍니다. 세 번째 시나리오는 올바른 정리를 보여 줍니다.

클라이언트 프로세스로부터의 예상 출력은 다음과 같습니다.

```
=
= Demonstrating problem:  closing brace of using statement can throw.
=
Got System.ServiceModel.CommunicationException from Divide.
Got System.ServiceModel.Security.MessageSecurityException
=
= Demonstrating problem:  closing brace of using statement can mask other Exceptions.
=
Got System.ServiceModel.CommunicationException from Divide.
Got System.ServiceModel.Security.MessageSecurityException
=
= Demonstrating cleanup with Exceptions.
=
Calling client.Add(0.0, 0.0);
        client.Add(0.0, 0.0); returned 0
Calling client.Divide(0.0, 0.0);
Got System.ServiceModel.CommunicationException from Divide.

Press <ENTER> to terminate client.
```

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. 수행 했는지 확인 합니다 [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)합니다.

2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.

3. 단일 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면의 지침을 따릅니다 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Client\UsingUsing`
