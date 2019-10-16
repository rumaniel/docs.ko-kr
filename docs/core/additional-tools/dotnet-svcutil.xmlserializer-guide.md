---
title: .NET Core에서 dotnet-svcutil.xmlserializer 사용
description: '`dotnet-svcutil.xmlserializer` NuGet 패키지를 사용하여 .NET Core 프로젝트용 serialization 어셈블리를 미리 생성하는 방법을 알아봅니다.'
author: huanwu
ms.date: 11/27/2018
ms.openlocfilehash: f1eebeb70206ce883a8e4e4bbd5216ae0ba5507c
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117277"
---
# <a name="using-dotnet-svcutilxmlserializer-on-net-core"></a>.NET Core에서 dotnet-svcutil.xmlserializer 사용

`dotnet-svcutil.xmlserializer` NuGet 패키지는 .NET Core 프로젝트용 serialization 어셈블리를 미리 생성할 수 있습니다. WCF 서비스 계약에서 사용되고 XmlSerializer를 통해 직렬화할 수 있는 클라이언트 애플리케이션의 형식에 대해 C# serialization 코드를 미리 생성합니다. 이렇게 하면 해당 형식의 개체를 직렬화 또는 deserialize할 때 XML serialization의 시작 성능이 향상됩니다.

## <a name="prerequisites"></a>전제 조건

* [.NET Core 2.1 SDK](https://dotnet.microsoft.com/download) 이상
* 선호하는 코드 편집기

`dotnet --info` 명령을 사용하여 이미 설치한 .NET Core SDK 및 런타임 버전을 확인할 수 있습니다.

## <a name="getting-started"></a>시작

.NET Core 콘솔 애플리케이션에서 `dotnet-svcutil.xmlserializer`를 사용하려면

1. .NET Framework에서 기본 템플릿 ‘WCF 서비스 애플리케이션’을 사용하여 ‘MyWCFService’라는 WCF 서비스를 만듭니다. 다음과 같이 서비스 메서드에 `[XmlSerializerFormat]` 특성을 추가합니다.

   ```csharp
    [ServiceContract]
    public interface IService1
    {
        [XmlSerializerFormat]
        [OperationContract(Action = "http://tempuri.org/IService1/GetData", ReplyAction = "http://tempuri.org/IService1/GetDataResponse")]
        string GetData(int value);
    }
    ```

2. .NET Core 2.1 이상 버전을 대상으로 하는 WCF 클라이언트 애플리케이션으로 .NET Core 콘솔 애플리케이션을 만듭니다. 예를 들어, 다음 명령으로 'MyWCFClient'라는 앱을 만듭니다.

    ```dotnetcli
    dotnet new console --name MyWCFClient
    ```

    프로젝트가 .NET Core 2.1 이상을 대상으로 하고 있는지 확인하려면 프로젝트 파일에서 `TargetFramework` XML 요소를 검사합니다.

    ```xml
    <TargetFramework>netcoreapp2.1</TargetFramework>
    ```

3. 다음 명령을 실행하여 `System.ServiceModel.Http`에 패키지 참조를 추가합니다.

    ```dotnetcli
    dotnet add package System.ServiceModel.Http
    ```

4. WCF 클라이언트 코드를 추가합니다.

    ```csharp
    using System.ServiceModel;

        class Program
        {
            static void Main(string[] args)
            {
                var myBinding = new BasicHttpBinding();
                var myEndpoint = new EndpointAddress("http://localhost:2561/Service1.svc"); //Fill your service url here
                var myChannelFactory = new ChannelFactory<IService1>(myBinding, myEndpoint);
                IService1 client = myChannelFactory.CreateChannel();
                string s = client.GetData(1);
                ((ICommunicationObject)client).Close();
            }
        }

    [ServiceContract]
    public interface IService1
    {
        [XmlSerializerFormat]
        [OperationContract(Action = "http://tempuri.org/IService1/GetData", ReplyAction = "http://tempuri.org/IService1/GetDataResponse")]
        string GetData(int value);
    }
    ```

5. 다음 명령을 실행하여 `dotnet-svcutil.xmlserializer` 패키지에 참조를 추가합니다.
  
    ```dotnetcli
    dotnet add package dotnet-svcutil.xmlserializer
    ```

    명령을 실행하면 다음과 비슷한 항목이 프로젝트 파일에 추가됩니다.
  
    ```xml
    <ItemGroup>
      <DotNetCliToolReference Include="dotnet-svcutil.xmlserializer" Version="1.0.0" />
    </ItemGroup>
    ```

6. `dotnet build`를 실행하여 애플리케이션을 빌드합니다. 모든 항목이 성공하면 *MyWCFClient.XmlSerializers.dll*이라는 어셈블리가 출력 폴더에 생성됩니다. 도구가 어셈블리 생성에 실패할 경우 빌드 출력에 경고가 표시됩니다.

7. 예를 들어 브라우저에서 `http://localhost:2561/Service1.svc`를 실행하여 WCF 서비스를 시작합니다. 그런 다음, 클라이언트 애플리케이션을 시작하면 미리 생성된 직렬 변환기가 런타임 시 자동으로 로드되어 사용됩니다.
