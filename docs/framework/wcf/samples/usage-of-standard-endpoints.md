---
title: 표준 엔드포인트 사용
ms.date: 03/30/2017
ms.assetid: ecd6a62f-9619-4778-a497-6f888087a9ea
ms.openlocfilehash: a2af1ae793166d1ed3742782b911ded30d0b9d35
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662377"
---
# <a name="usage-of-standard-endpoints"></a>표준 엔드포인트 사용

이 샘플에서는 서비스 구성 파일에서 표준 엔드포인트를 사용하는 방법을 보여 줍니다. 표준 엔드포인트를 사용하면 사용자는 주소, 바인딩 및 계약 조합을 설명하는 단일 속성과 엔드포인트에 관련된 추가 속성을 사용하여 엔드포인트 정의를 단순화할 수 있습니다. 이 샘플에서는 사용자 지정 표준 엔드포인트를 정의 및 구현하는 방법과 엔드포인트의 특정 속성을 정의하는 방법을 보여 줍니다.

## <a name="sample-details"></a>샘플 세부 정보

서비스 엔드포인트는 주소, 바인딩 및 계약의 세 매개 변수를 제공하여 지정할 수 있습니다. 제공할 수 있는 다른 매개 변수로는 동작 구성, 헤더 및 수신 대기 URI 등이 있습니다. 일부 경우에는 주소, 바인딩 및 계약의 일부 또는 모두에 변경할 수 없는 값이 있을 수 있습니다. 이러한 이유로 표준 엔드포인트를 사용할 수 있습니다. 이러한 엔드포인트의 몇 가지 예로는 메타데이터 교환 엔드포인트와 검색 엔드포인트가 있습니다. 표준 엔드포인트를 사용하면 고정 특성의 정보를 제공하거나 고유한 표준 엔드포인트를 만들 필요 없이 서비스 엔드포인트의 구성을 그대로 사용하여 유용성을 향상시킬 수도 있습니다. 예를 들어 적절한 기본값 집합을 제공하여 구성 파일의 복잡성을 줄임으로써 유용성을 향상시킬 수 있습니다.

이 샘플은 두 개의 표준 엔드포인트를 정의하는 서비스 및 이 서비스와 통신하는 클라이언트의 두 프로젝트로 구성되어 있습니다. 구성 파일에서 서비스에 대한 표준 엔드포인트가 정의되는 방법은 다음 예제와 같습니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <extensions>
      <endpointExtensions>
        <add name="customEndpoint" type="Microsoft.Samples.StandardEndpoints.CustomEndpointCollectionElement, service" />
      </endpointExtensions>
    </extensions>
    <services>
      <service name="Microsoft.Samples.StandardEndpoints.CalculatorService">
        <endpoint address="http://localhost:8000/Samples/Service.svc/customEndpoint" contract="Microsoft.Samples.StandardEndpoints.ICalculator" kind="customEndpoint" />
        <endpoint kind="mexEndpoint" />
      </service>
    </services>
    <behaviors>
      <serviceBehaviors>
        <behavior>
          <serviceMetadata httpGetEnabled="True"/>
        </behavior>
      </serviceBehaviors>
    </behaviors>
    <standardEndpoints>
      <customEndpoint>
        <standardEndpoint property="True" />
      </customEndpoint>
    </standardEndpoints>
  </system.serviceModel>
</configuration>
```

서비스에 대해 정의되는 첫 번째 엔드포인트는 `customEndpoint` 종류로, `<standardEndpoints>` 섹션에서 해당 정의를 볼 수 있으며 `property` 속성 값은 `true`로 지정됩니다. 이 엔드포인트는 새 속성으로 사용자 지정된 엔드포인트입니다. 두 번째 엔드포인트는 주소, 바인딩 및 계약의 값이 고정된 메타데이터 엔드포인트에 해당합니다.

표준 엔드포인트 요소를 정의하려면 `StandardEndpointElement`에서 파생된 클래스를 만들어야 합니다. 이 샘플에서는 `CustomEndpointElement`가 다음 예제와 같이 정의되었습니다.

```csharp
public class CustomEndpointElement : StandardEndpointElement
{
    public bool Property
    {
        get { return (bool)base["property"]; }
        set { base["property"] = value; }
    }

    protected override ConfigurationPropertyCollection Properties
    {
        get
        {
            ConfigurationPropertyCollection properties = base.Properties;
            properties.Add(new ConfigurationProperty("property", typeof(bool), false, ConfigurationPropertyOptions.None));
            return properties;
        }
    }

    protected override Type EndpointType
    {
        get { return typeof(CustomEndpoint); }
    }

    protected override ServiceEndpoint CreateServiceEndpoint(ContractDescription contract)
    {
        return new CustomEndpoint();
    }

    protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ServiceEndpointElement serviceEndpointElement)
    {
        CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;
        customEndpoint.Property = this.Property;
    }

    protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ChannelEndpointElement channelEndpointElement)
    {
        CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;
        customEndpoint.Property = this.Property;
    }

    protected override void OnInitializeAndValidate(ServiceEndpointElement serviceEndpointElement)
    {
    }

    protected override void OnInitializeAndValidate(ChannelEndpointElement channelEndpointElement)
    {
    }
}
```

`CreateServiceEndpoint` 함수에서는 `CustomEndpoint` 개체가 만들어집니다. 해당 정의 다음 예제에 표시 됩니다.

```csharp
public class CustomEndpoint : ServiceEndpoint
{
    public CustomEndpoint()
        : this(string.Empty)
    {
    }

    public CustomEndpoint(string address)
        : this(address, ContractDescription.GetContract(typeof(ICalculator)))
    {
    }

    public CustomEndpoint(string address, ContractDescription contract)
        : base(contract)
    {
        this.Binding = new BasicHttpBinding();
        this.IsSystemEndpoint = false;
    }

    public bool Property
    {
        get;
        set;
    }
}
```

 서비스와 클라이언트 간의 통신을 수행하기 위해 서비스에 대한 서비스 참조가 클라이언트에 만들어집니다. 샘플이 빌드되어 실행되면 서비스가 실행되고 클라이언트가 서비스와 통신합니다. 서비스 참조는 서비스에 변경 사항이 있을 때마다 업데이트해야 합니다.

#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면

1. StandardEndpoints.sln 파일을 열고 Visual Studio 2012를 사용 합니다.

2. 여러 개의 프로젝트가 시작되도록 설정합니다.

    1. **솔루션 탐색기**Standard Endpoints 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택한 **속성**합니다.

    2. **공용 속성**를 선택 **시작 프로젝트**를 클릭 하 고 **여러 개의 시작 프로젝트**합니다.

    3. 서비스 프로젝트를 사용 하 여 목록의 처음으로 이동 합니다.는 **동작** 로 설정 **시작**합니다.

    4. 사용 하 여 클라이언트 프로젝트를 Service 프로젝트 다음에 이동 합니다 **동작** 로 설정 **시작**합니다.

         이렇게 하면 Client 프로젝트가 Service 프로젝트 다음에 실행됩니다.

3. F5 키를 눌러 솔루션을 실행합니다.

> [!NOTE]
> 이 단계 작동 하지 않으면는 사용자 환경에 올바르게 설정 되었는지, 다음 단계를 사용 하 여 있는지 확인 한 후:
>
> 1. 수행 했는지 확인 합니다 [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](one-time-setup-procedure-for-the-wcf-samples.md)합니다.
> 2. 지침에 따라 솔루션을 빌드하려면 [Building Windows Communication Foundation Samples](building-the-samples.md)합니다.
> 3. 단일 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면의 지침을 따릅니다 [Windows Communication Foundation 샘플 실행](running-the-samples.md)합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없으면 이동할 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\StandardEndpoints`
