---
title: Impersonating the Client
ms.date: 03/30/2017
helpviewer_keywords:
- service behaviors, impersonation sample
- Impersonating the Client Sample [Windows Communication Foundation]
- impersonation, Windows Communication Foundation sample
ms.assetid: 8bd974e1-90db-4152-95a3-1d4b1a7734f8
ms.openlocfilehash: 9e1c38abd1c9cacfd4db953d9fb875437b2f1093
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50199619"
---
# <a name="impersonating-the-client"></a>Impersonating the Client
Impersonation 샘플에서는 서비스가 호출자를 대신하여 시스템 리소스에 액세스할 수 있도록 서비스에서 호출자 응용 프로그램을 가장하는 방법을 보여 줍니다.  
  
 이 샘플은 기반 합니다 [Self-host](../../../../docs/framework/wcf/samples/self-host.md) 샘플입니다. 서비스 및 클라이언트 구성 파일의와 동일 합니다 [Self-host](../../../../docs/framework/wcf/samples/self-host.md) 샘플입니다.  
  
> [!NOTE]
>  이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 다음 샘플 코드와 같이 서비스 코드는 `Add`를 사용하여 서비스의 <xref:System.ServiceModel.OperationBehaviorAttribute> 메서드가 호출자를 가장하도록 수정되었습니다.  
  
```csharp
[OperationBehavior(Impersonation = ImpersonationOption.Required)]  
public double Add(double n1, double n2)  
{  
    double result = n1 + n2;  
    Console.WriteLine("Received Add({0},{1})", n1, n2);  
    Console.WriteLine("Return: {0}", result);  
    DisplayIdentityInformation();  
    return result;  
}  
```  
  
 결과적으로 실행 스레드의 보안 컨텍스트는 `Add` 메서드에 들어가기 전에 호출자를 가장하기 위해 전환되고 메서드 종료 시에 되돌아갑니다.  
  
 다음 샘플 코드에 표시된 `DisplayIdentityInformation` 메서드는 호출자의 ID를 표시하는 유틸리티 함수입니다.  
  
```csharp
static void DisplayIdentityInformation()  
{  
    Console.WriteLine("\t\tThread Identity            :{0}",  
         WindowsIdentity.GetCurrent().Name);  
    Console.WriteLine("\t\tThread Identity level  :{0}",   
         WindowsIdentity.GetCurrent().ImpersonationLevel);  
    Console.WriteLine("\t\thToken                     :{0}",  
         WindowsIdentity.GetCurrent().Token.ToString());  
    return;  
}  
```  
  
 다음 샘플 코드와 같이 서비스의 `Subtract` 메서드는 명령적 호출을 사용하여 호출자를 가장합니다.  
  
```csharp
public double Subtract(double n1, double n2)  
{  
    double result = n1 - n2;  
    Console.WriteLine("Received Subtract({0},{1})", n1, n2);  
    Console.WriteLine("Return: {0}", result);  
    Console.WriteLine("Before impersonating");  
    DisplayIdentityInformation();  
  
    if (ServiceSecurityContext.Current.WindowsIdentity.ImpersonationLevel == TokenImpersonationLevel.Impersonation ||  
        ServiceSecurityContext.Current.WindowsIdentity.ImpersonationLevel == TokenImpersonationLevel.Delegation)  
    {  
        // Impersonate.  
        using (ServiceSecurityContext.Current.WindowsIdentity.Impersonate())  
        {  
            // Make a system call in the caller's context and ACLs   
            // on the system resource are enforced in the caller's context.   
            Console.WriteLine("Impersonating the caller imperatively");  
            DisplayIdentityInformation();  
        }  
    }  
    else  
    {  
        Console.WriteLine("ImpersonationLevel is not high enough to perform this operation.");  
    }  
  
    Console.WriteLine("After reverting");  
    DisplayIdentityInformation();  
    return result;  
}  
```  
  
 이 경우 호출자는 전체 호출에 대해 가장되지 않고 호출의 일부에 대해서만 가장됩니다. 일반적으로 전체 작업에 대해 가장하는 것보다 가장 작은 범위에 대해 가장하는 것이 바람직합니다.  
  
 다른 메서드는 호출자를 가장하지 않습니다.  
  
 클라이언트 코드는 가장 레벨을 <xref:System.Security.Principal.TokenImpersonationLevel.Impersonation>으로 설정하도록 수정되었습니다. 클라이언트는 <xref:System.Security.Principal.TokenImpersonationLevel> 열거형을 사용하여 서비스에 사용되는 가장 레벨을 지정합니다. 이 열거형에서는 <xref:System.Security.Principal.TokenImpersonationLevel.None>, <xref:System.Security.Principal.TokenImpersonationLevel.Anonymous>, <xref:System.Security.Principal.TokenImpersonationLevel.Identification>, <xref:System.Security.Principal.TokenImpersonationLevel.Impersonation> 및 <xref:System.Security.Principal.TokenImpersonationLevel.Delegation> 값이 지원됩니다. Windows ACL을 사용하여 보호되는 로컬 컴퓨터의 시스템 리소스 액세스 시에 액세스 검사를 수행하기 위해 다음 샘플 코드와 같이 가장 레벨은 <xref:System.Security.Principal.TokenImpersonationLevel.Impersonation>으로 설정되어야 합니다.  
  
```csharp
// Create a client with given client endpoint configuration  
CalculatorClient client = new CalculatorClient();  
  
client.ClientCredentials.Windows.AllowedImpersonationLevel = TokenImpersonationLevel.Impersonation;  
```  
  
 샘플을 실행하면 작업 요청 및 응답이 서비스와 클라이언트 콘솔 창 모두에 표시됩니다. 서비스와 클라이언트를 종료하려면 각 콘솔 창에서 Enter 키를 누릅니다.  
  
> [!NOTE]
>  서비스 관리자 계정으로 실행 해야 합니다 또는 실행 되는 계정에 등록할 수 있는 권한이 부여 해야 합니다 `http://localhost:8000/ServiceModelSamples` HTTP 계층을 사용 하 여 URI입니다. 설정 하 여 이러한 권한을 부여할 수 있습니다는 [Namespace 예약](https://go.microsoft.com/fwlink/?LinkId=95012) 사용 하는 [Httpcfg.exe 도구](https://go.microsoft.com/fwlink/?LinkId=95010)합니다.  
  
> [!NOTE]
>  [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]을 실행하는 컴퓨터에서는 Host.exe 응용 프로그램에 가장 권한이 있는 경우에만 가장이 지원됩니다. 기본적으로 관리자만 이 사용 권한을 가집니다. 로 이동 하는 서비스를 실행 하는 계정에이 권한을 추가할 **관리 도구**오픈 **로컬 보안 정책**오픈 **로컬 정책**, 클릭 **사용자 권한 할당**, 선택한 **인증 후 클라이언트 가장** 를 두 번 클릭 하 고 **속성** 사용자 또는 그룹을 추가 합니다.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1.  수행 했는지 확인 합니다 [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)합니다.  
  
2.  C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3.  단일 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면의 지침을 따릅니다 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)합니다.  
  
4.  서비스가 호출자를 가장하는 것을 보기 위해 서비스가 실행 중인 계정이 아닌 다른 계정으로 클라이언트를 실행합니다. 이렇게 하려면 명령 프롬프트에서 다음을 입력합니다.  
  
    ```  
    runas /user:<machine-name>\<user-name> client.exe  
    ```  
  
     그런 다음 암호를 묻는 메시지가 나타납니다. 이전에 지정한 계정에 대한 암호를 입력합니다.  
  
5.  클라이언트를 다른 자격 증명으로 실행하기 전과 후의 ID에 주의합니다.  
  
## <a name="see-also"></a>참고 항목
