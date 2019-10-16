---
title: '방법: 프로그래밍 방식으로 WCF 서비스 및 클라이언트에 검색 기능 추가'
ms.date: 03/30/2017
ms.assetid: 4f7ae7ab-6fc8-4769-9730-c14d43f7b9b1
ms.openlocfilehash: a139eb4a15486be329bc6853ee6b3a3be06b0619
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291564"
---
# <a name="how-to-programmatically-add-discoverability-to-a-wcf-service-and-client"></a>방법: 프로그래밍 방식으로 WCF 서비스 및 클라이언트에 검색 기능 추가
이 항목에서는 WCF (Windows Communication Foundation) 서비스를 검색할 수 있도록 하는 방법에 대해 설명 합니다. [자체 호스트](https://go.microsoft.com/fwlink/?LinkId=145523) 샘플을 기반으로 합니다.  
  
### <a name="to-configure-the-existing-self-host-service-sample-for-discovery"></a>기존 자체 호스팅 서비스 샘플을 검색용으로 구성하려면  
  
1. Visual Studio 2012에서 자체 호스트 솔루션을 엽니다. 샘플은 TechnologySamples\Basic\Service\Hosting\SelfHost 디렉터리에 있습니다.  
  
2. 서비스 프로젝트에 `System.ServiceModel.Discovery.dll`에 대한 참조를 추가합니다. "System" 이라는 오류 메시지가 표시 될 수 있습니다. ServiceModel 또는 해당 종속성 중 하나에는 프로젝트에 지정 된 것 보다 최신 버전의 .NET Framework 필요 합니다. " 이 메시지가 표시 되 면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다. **프로젝트 속성** 창에서 **대상 프레임 워크가** [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] 인지 확인 합니다.  
  
3. Service.cs 파일을 열고 다음 `using` 문을 추가합니다.  
  
    ```csharp  
    using System.ServiceModel.Discovery;  
    ```  
  
4. `Main()` 메서드의 `using` 문 안에서 서비스 호스트에 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> 인스턴스를 추가합니다.  
  
    ```csharp  
    public static void Main()  
    {  
        // Create a ServiceHost for the CalculatorService type.  
        using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService)))  
        {  
            // Add a ServiceDiscoveryBehavior  
            serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());                  
  
            // ...  
        }  
    }  
    ```  
  
     <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>는 자신이 적용되는 서비스가 검색 가능하게 되도록 지정합니다.  
  
5. <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>를 추가하는 코드 바로 뒤에 있는 서비스 호스트에 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>를 추가합니다.  
  
    ```csharp  
    // Add ServiceDiscoveryBehavior  
    serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());  
  
    // Add a UdpDiscoveryEndpoint  
    serviceHost.AddServiceEndpoint(new UdpDiscoveryEndpoint());  
    ```  
  
     이 코드는 검색 메시지를 표준 UDP 검색 엔드포인트에 보내도록 지정합니다.  
  
### <a name="to-create-a-client-application-that-uses-discovery-to-call-the-service"></a>검색을 사용하는 클라이언트 애플리케이션을 만들어 서비스를 호출하려면  
  
1. `DiscoveryClientApp`라는 솔루션에 새 콘솔 애플리케이션을 추가합니다.  
  
2. `System.ServiceModel.dll` 및 `System.ServiceModel.Discovery.dll`에 대한 참조를 추가합니다.  
  
3. GeneratedClient.cs 및 App.config 파일을 기본 클라이언트 프로젝트에서 새 DiscoveryClientApp 프로젝트로 복사합니다. 이렇게 하려면 **솔루션 탐색기**파일을 마우스 오른쪽 단추로 클릭 하 고 **복사**를 선택한 다음 **discoveryclientapp.exe** 프로젝트를 선택 하 고 마우스 오른쪽 단추를 클릭 한 다음 **붙여넣기**를 선택 합니다.  
  
4. Program.cs를 엽니다.  
  
5. 다음 `using` 문을 추가합니다.  
  
    ```csharp  
    using System.ServiceModel;  
    using System.ServiceModel.Discovery;  
    using Microsoft.ServiceModel.Samples;  
    ```  
  
6. `FindCalculatorServiceAddress()`라는 정적 메서드를 `Program` 클래스에 추가합니다.  
  
    ```csharp  
    static EndpointAddress FindCalculatorServiceAddress()  
    {  
    }  
    ```  
  
     이 메서드는 검색을 사용하여 `CalculatorService` 서비스를 찾습니다.  
  
7. `FindCalculatorServiceAddress` 메서드 안에서 생성자에 <xref:System.ServiceModel.Discovery.DiscoveryClient>를 전달하여 새 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> 인스턴스를 만듭니다.  
  
    ```csharp  
    static EndpointAddress FindCalculatorServiceAddress()  
    {  
        // Create DiscoveryClient  
        DiscoveryClient discoveryClient = new DiscoveryClient(new UdpDiscoveryEndpoint());  
    }  
    ```  
  
     이는 <xref:System.ServiceModel.Discovery.DiscoveryClient> 클래스가 표준 UDP 검색 끝점을 사용 하 여 검색 메시지를 보내고 받는 것을 WCF에 지시 합니다.  
  
8. 다음 줄에서 <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> 메서드를 호출하고 검색하려는 서비스 계약이 포함된 <xref:System.ServiceModel.Discovery.FindCriteria> 인스턴스를 지정합니다. 이 경우 `ICalculator`를 지정합니다.  
  
    ```csharp  
    // Find ICalculatorService endpoints              
    FindResponse findResponse = discoveryClient.Find(new FindCriteria(typeof(ICalculator)));  
    ```  
  
9. <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A>를 호출한 후 일치하는 서비스가 하나 이상 있는지 확인하고 첫 번째 일치하는 서비스의 <xref:System.ServiceModel.EndpointAddress>를 반환합니다. 그렇지 않으면 `null`을 반환합니다.  
  
    ```csharp  
    if (findResponse.Endpoints.Count > 0)  
    {  
        return findResponse.Endpoints[0].Address;  
    }  
    else  
    {  
        return null;  
    }  
    ```  
  
10. `InvokeCalculatorService`라는 정적 메서드를 `Program` 클래스에 추가합니다.  
  
    ```csharp  
    static void InvokeCalculatorService(EndpointAddress endpointAddress)  
    {  
    }  
    ```  
  
     이 메서드는 `FindCalculatorServiceAddress`에서 반환되는 엔드포인트 주소를 사용하여 계산기 서비스를 호출합니다.  
  
11. `InvokeCalculatorService` 메서드 안에서 `CalculatorServiceClient` 클래스의 인스턴스를 만듭니다. 이 클래스는 [자체 호스트](https://go.microsoft.com/fwlink/?LinkId=145523) 샘플에 의해 정의 됩니다. 이 클래스는 Svcutil.exe를 사용하여 생성되었습니다.  
  
    ```csharp  
    // Create a client  
    CalculatorClient client = new CalculatorClient();  
    ```  
  
12. 다음 줄에서 클라이언트의 엔드포인트 주소를 `FindCalculatorServiceAddress()`에서 반환되는 엔드포인트 주소로 설정합니다.  
  
    ```csharp  
    // Connect to the discovered service endpoint  
    client.Endpoint.Address = endpointAddress;  
    ```  
  
13. 이전 단계의 코드 바로 뒤에서 계산기 서비스에 의해 노출되는 메서드를 호출합니다.  
  
    ```csharp  
    Console.WriteLine("Invoking CalculatorService at {0}", endpointAddress);  
  
    double value1 = 100.00D;  
    double value2 = 15.99D;  
  
    // Call the Add service operation.  
    double result = client.Add(value1, value2);  
    Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
    // Call the Subtract service operation.  
    result = client.Subtract(value1, value2);  
    Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);  
  
    // Call the Multiply service operation.  
    result = client.Multiply(value1, value2);  
    Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);  
  
    // Call the Divide service operation.  
    result = client.Divide(value1, value2);  
    Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
    Console.WriteLine();  
  
    //Closing the client gracefully closes the connection and cleans up resources  
    client.Close();  
    ```  
  
14. `Main()` 클래스의 `Program` 메서드에 `FindCalculatorServiceAddress`를 호출하는 코드를 추가합니다.  
  
    ```csharp  
    public static void Main()  
    {  
        EndpointAddress endpointAddress = FindCalculatorServiceAddress();  
    }  
    ```  
  
15. 다음 줄에서 `InvokeCalculatorService()`를 호출하고 `FindCalculatorServiceAddress()`에서 반환되는 엔드포인트 주소를 전달합니다.  
  
    ```csharp  
    if (endpointAddress != null)  
    {  
        InvokeCalculatorService(endpointAddress);  
    }  
  
    Console.WriteLine("Press <ENTER> to exit.");  
    Console.ReadLine();  
    ```  
  
### <a name="to-test-the-application"></a>애플리케이션을 테스트하려면  
  
1. 권한이 높은 명령 프롬프트를 열고 Service.exe를 실행합니다.  
  
2. 명령 프롬프트를 열고 Discoveryclientapp.exe를 실행합니다.  
  
3. service.exe의 출력이 다음과 같이 표시됩니다.  
  
    ```output  
    Received Add(100,15.99)  
    Return: 115.99  
    Received Subtract(100,15.99)  
    Return: 84.01  
    Received Multiply(100,15.99)  
    Return: 1599  
    Received Divide(100,15.99)  
    Return: 6.25390869293308  
    ```  
  
4. Discoveryclientapp.exe의 출력이 다음과 같이 표시됩니다.  
  
    ```output  
    Invoking CalculatorService at http://localhost:8000/ServiceModelSamples/service  
    Add(100,15.99) = 115.99  
    Subtract(100,15.99) = 84.01  
    Multiply(100,15.99) = 1599  
    Divide(100,15.99) = 6.25390869293308  
  
    Press <ENTER> to exit.  
    ```  
  
## <a name="example"></a>예제  
 다음은 이 샘플의 코드 목록입니다. 이 코드는 [자체 호스트](https://go.microsoft.com/fwlink/?LinkId=145523) 샘플을 기반으로 하기 때문에 변경 된 파일만 나열 됩니다. 자체 호스트 샘플에 대 한 자세한 내용은 [설치 지침](https://go.microsoft.com/fwlink/?LinkId=145522)을 참조 하세요.  
  
```csharp  
// Service.cs  
using System;  
using System.Configuration;  
using System.ServiceModel;  
using System.ServiceModel.Discovery;  
  
namespace Microsoft.ServiceModel.Samples  
{  
    // See SelfHost sample for service contract and implementation  
    // ...  
  
        // Host the service within this EXE console application.  
        public static void Main()  
        {  
            // Create a ServiceHost for the CalculatorService type.  
            using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService)))  
            {  
                // Add the ServiceDiscoveryBehavior to make the service discoverable  
                serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());  
                serviceHost.AddServiceEndpoint(new UdpDiscoveryEndpoint());  
  
                // Open the ServiceHost to create listeners and start listening for messages.  
                serviceHost.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
            }  
        }  
    }  
}  
```  
  
```csharp  
// Program.cs  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.ServiceModel;  
using System.ServiceModel.Discovery;  
using Microsoft.ServiceModel.Samples;  
using System.Text;  
  
namespace DiscoveryClientApp  
{  
    class Program  
    {  
        static EndpointAddress FindCalculatorServiceAddress()  
        {  
            // Create DiscoveryClient  
            DiscoveryClient discoveryClient = new DiscoveryClient(new UdpDiscoveryEndpoint());  
  
            // Find ICalculatorService endpoints              
            FindResponse findResponse = discoveryClient.Find(new FindCriteria(typeof(ICalculator)));  
  
            if (findResponse.Endpoints.Count > 0)  
            {  
                return findResponse.Endpoints[0].Address;  
            }  
            else  
            {  
                return null;  
            }  
        }  
  
        static void InvokeCalculatorService(EndpointAddress endpointAddress)  
        {  
            // Create a client  
            CalculatorClient client = new CalculatorClient();  
  
            // Connect to the discovered service endpoint  
            client.Endpoint.Address = endpointAddress;  
  
            Console.WriteLine("Invoking CalculatorService at {0}", endpointAddress);  
  
            double value1 = 100.00D;  
            double value2 = 15.99D;  
  
            // Call the Add service operation.  
            double result = client.Add(value1, value2);  
            Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
            // Call the Subtract service operation.  
            result = client.Subtract(value1, value2);  
            Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);  
  
            // Call the Multiply service operation.  
            result = client.Multiply(value1, value2);  
            Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);  
  
            // Call the Divide service operation.  
            result = client.Divide(value1, value2);  
            Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
            Console.WriteLine();  
  
            //Closing the client gracefully closes the connection and cleans up resources  
            client.Close();  
        }  
        static void Main(string[] args)  
        {  
            EndpointAddress endpointAddress = FindCalculatorServiceAddress();  
  
            if (endpointAddress != null)  
            {  
                InvokeCalculatorService(endpointAddress);  
            }  
  
            Console.WriteLine("Press <ENTER> to exit.");  
            Console.ReadLine();  
  
        }  
    }  
}  
```  

## <a name="see-also"></a>참조

- [WCF 검색 개요](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md)
- [WCF 검색 개체 모델](../../../../docs/framework/wcf/feature-details/wcf-discovery-object-model.md)
