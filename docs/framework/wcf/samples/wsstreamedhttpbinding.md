---
title: WSStreamedHttpBinding
ms.date: 03/30/2017
ms.assetid: 97ce4d3d-ca6f-45fa-b33b-2429bb84e65b
ms.openlocfilehash: aa2acc7228f802f69e8692ed747af0382345c1d6
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70016069"
---
# <a name="wsstreamedhttpbinding"></a>WSStreamedHttpBinding

이 샘플에서는 HTTP 전송이 사용될 때 스트리밍 시나리오를 지원하도록 디자인된 바인딩을 만드는 방법을 보여 줍니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Binding\WSStreamedHttpBinding`

 새 표준 바인딩을 만들고 구성하기 위한 단계는 다음과 같습니다.

1. 새 표준 바인딩 만들기

    BasicHttpBinding과 같은 Windows Communication Foundation (WCF)의 표준 바인딩과 netTcpBinding는 특정 요구 사항에 맞게 기본 전송 및 채널 스택을 구성 합니다. 이 샘플에서 `WSStreamedHttpBinding`은 스트리밍을 지원하도록 채널 스택을 구성합니다. 기본적으로 WS-Security 및 신뢰할 수 있는 메시징은 스트리밍에서 지원되지 않으므로 이러한 기능은 둘 다 채널 스택에 추가되지 않습니다. 새 바인딩은 `WSStreamedHttpBinding`에서 파생되는 <xref:System.ServiceModel.Channels.Binding> 클래스에서 구현됩니다. `WSStreamedHttpBinding`은 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>, <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>, <xref:System.ServiceModel.Channels.TransactionFlowBindingElement> 및 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> 바인딩 요소를 포함합니다. 다음 샘플 코드와 같이 결과 바인딩 스택을 구성하기 위해 클래스에서 `CreateBindingElements()` 메서드를 제공합니다.

    ```csharp
    public override BindingElementCollection CreateBindingElements()
    {
        // return collection of BindingElements
        BindingElementCollection bindingElements = new BindingElementCollection();

        // the order of binding elements within the collection is important: layered channels are applied in the order included, followed by
        // the message encoder, and finally the transport at the end
        if (flowTransactions)
        {
            bindingElements.Add(transactionFlow);
        }
        bindingElements.Add(textEncoding);

        // add transport (http or https)
        bindingElements.Add(transport);
        return bindingElements.Clone();
    }
    ```

2. 구성 지원 추가

    구성을 통해 전송을 노출하기 위해 샘플에서는 두 개의 추가 클래스인 `WSStreamedHttpBindingConfigurationElement` 및 `WSStreamedHttpBindingSection`을 구현합니다. 클래스 `WSStreamedHttpBindingSection` 는WCF`WSStreamedHttpBinding` 구성 시스템에를 노출 하는입니다.<xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602> 대량의 구현은 `WSStreamedHttpBindingConfigurationElement`에서 파생되는 <xref:System.ServiceModel.Configuration.StandardBindingElement>에 위임됩니다. `WSStreamedHttpBindingConfigurationElement` 클래스에는 `WSStreamedHttpBinding`의 속성에 해당하는 속성과 각 구성 요소를 바인딩에 매핑하기 위한 함수가 있습니다.

    서비스의 구성 파일에 다음 섹션을 추가하여 구성 시스템에 처리기를 등록합니다.

    ```xml
    <configuration>
      <system.serviceModel>
        <extensions>
          <bindingExtensions>
            <add name="wsStreamedHttpBinding" type="Microsoft.ServiceModel.Samples.WSStreamedHttpBindingCollectionElement, WSStreamedHttpBinding, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null" />
          </bindingExtensions>
        </extensions>
      </system.serviceModel>
    </configuration>
    ```

    그런 다음 serviceModel 구성 섹션에서 처리기를 참조할 수 있습니다.

    ```xml
    <configuration>
      <system.serviceModel>
        <client>
          <endpoint
                    address="https://localhost/servicemodelsamples/service.svc"
                    bindingConfiguration="Binding"
                    binding="wsStreamedHttpBinding"
                    contract="Microsoft.ServiceModel.Samples.IStreamedEchoService"/>
        </client>
      </system.serviceModel>
    </configuration>
    ```

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. 다음 명령을 사용 하 여 ASP.NET 4.0을 설치 합니다.

    ```
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable
    ```

2. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)에 나열 된 단계를 수행 했는지 확인 합니다.

3. [인터넷 정보 서비스 (IIS) 서버 인증서 설치 지침](../../../../docs/framework/wcf/samples/iis-server-certificate-installation-instructions.md)을 수행 했는지 확인 합니다.

4. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요.

5. 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.

6. 클라이언트 창이 표시되면 "Sample.txt"를 입력합니다. 디렉터리에서 "Copy of Sample.txt"를 볼 수 있습니다.

## <a name="the-wsstreamedhttpbinding-sample-service"></a>WSStreamedHttpBinding 샘플 서비스

`WSStreamedHttpBinding`을 사용하는 샘플 서비스는 서비스 하위 디렉터리에 있습니다. `OperationContract` 구현에서는 `MemoryStream`을 반환하기 전에 `MemoryStream`을 사용하여 들어오는 스트림에서 모든 데이터를 검색합니다. 샘플 서비스는 IIS(인터넷 정보 서비스)에 의해 호스팅됩니다.

```csharp
[ServiceContract]
public interface IStreamedEchoService
{
    [OperationContract]
    Stream Echo(Stream data);
}

public class StreamedEchoService : IStreamedEchoService
{
    public Stream Echo(Stream data)
    {
        MemoryStream dataStorage = new MemoryStream();
        byte[] byteArray = new byte[8192];
        int bytesRead = data.Read(byteArray, 0, 8192);
        while (bytesRead > 0)
        {
            dataStorage.Write(byteArray, 0, bytesRead);
            bytesRead = data.Read(byteArray, 0, 8192);
        }
        data.Close();
        dataStorage.Seek(0, SeekOrigin.Begin);

        return dataStorage;
    }
}
```

## <a name="the-wsstreamedhttpbinding-sample-client"></a>WSStreamedHttpBinding 샘플 클라이언트

`WSStreamedHttpBinding`을 사용하여 상호 작용하는 데 사용되는 클라이언트는 클라이언트 하위 디렉터리에 있습니다. 이 샘플에 사용 된 인증서는 Makecert.exe를 사용 하 여 만든 테스트 인증서 이므로 브라우저에서와 https://localhost/servicemodelsamples/service.svc 같은 HTTPS 주소에 액세스 하려고 하면 보안 경고가 표시 됩니다. WCF 클라이언트가 테스트 인증서를 사용 하 여 작동 하도록 허용 하기 위해 일부 추가 코드를 클라이언트에 추가 하 여 보안 경고를 표시 하지 않습니다. 코드 및 함께 사용되는 클래스는 프로덕션 인증서를 사용할 때에는 필요가 없습니다.

```csharp
// WARNING: This code is only required for test certificates such as those created by makecert. It is
// not recommended for production code.
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");
```
