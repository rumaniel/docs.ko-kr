---
title: '방법: MEX가 아닌 바인딩을 통해 메타데이터 검색'
ms.date: 03/30/2017
ms.assetid: 2292e124-81b2-4317-b881-ce9c1ec66ecb
ms.openlocfilehash: 3721657eb72663450261b4bc8627b250b1a4a14e
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70856037"
---
# <a name="how-to-retrieve-metadata-over-a-non-mex-binding"></a>방법: MEX가 아닌 바인딩을 통해 메타데이터 검색
이 항목에서는 MEX가 아닌 바인딩을 통해 MEX 엔드포인트로부터 메타데이터를 검색하는 방법에 대해 설명합니다. 이 샘플의 코드는 [사용자 지정 보안 메타 데이터 끝점](../samples/custom-secure-metadata-endpoint.md) 샘플을 기반으로 합니다.  
  
### <a name="to-retrieve-metadata-over-a-non-mex-binding"></a>MEX가 아닌 바인딩을 통해 메타데이터를 검색하려면  
  
1. MEX 엔드포인트에서 사용하는 바인딩을 결정합니다. WCF (Windows Communication Foundation) 서비스의 경우 서비스의 구성 파일에 액세스 하 여 MEX 바인딩을 결정할 수 있습니다. 이 경우에는 MEX 바인딩이 다음 서비스 구성에서 정의됩니다.  
  
    ```xml  
    <services>  
        <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
                behaviorConfiguration="CalculatorServiceBehavior">  
         <!-- Use the base address provided by the host. -->  
         <endpoint address=""  
           binding="wsHttpBinding"  
           bindingConfiguration="Binding2"  
           contract="Microsoft.ServiceModel.Samples.ICalculator" />  
         <endpoint address="mex"  
           binding="wsHttpBinding"  
           bindingConfiguration="Binding1"  
           contract="IMetadataExchange" />  
         </service>  
     </services>  
     <bindings>  
       <wsHttpBinding>  
         <binding name="Binding1">  
           <security mode="Message">  
             <message clientCredentialType="Certificate" />  
           </security>  
         </binding>  
         <binding name="Binding2">  
           <reliableSession inactivityTimeout="00:01:00" enabled="true" />  
           <security mode="Message">  
             <message clientCredentialType="Certificate" />  
           </security>  
         </binding>  
       </wsHttpBinding>  
     </bindings>  
    ```  
  
2. 클라이언트 구성 파일에서는 동일한 사용자 지정 바인딩을 구성합니다. 여기서는 클라이언트가 MEX 엔드포인트로부터 메타데이터를 요청할 때 인증에 사용할 인증서를 서비스에 제공하기 위해 `clientCredentials` 동작도 정의할 수 있습니다. 사용자 지정 바인딩을 통해 메타데이터를 요청하기 위해 Svcutil.exe를 사용할 경우 다음 코드와 같이 MEX 엔드포인트 구성을 Svcutil.exe의 구성 파일(Svcutil.exe.config)에 추가해야 하며, 엔드포인트 구성의 이름은 MEX 엔드포인트 주소의 URI 체계와 일치해야 합니다.  
  
    ```xml  
    <system.serviceModel>  
      <client>  
        <endpoint name="http"  
                  binding="wsHttpBinding"  
                  bindingConfiguration="Binding1"  
                  behaviorConfiguration="ClientCertificateBehavior"  
                  contract="IMetadataExchange" />  
      </client>  
      <bindings>  
        <wsHttpBinding>  
          <binding name="Binding1">  
            <security mode="Message">  
              <message clientCredentialType="Certificate"/>  
            </security>  
          </binding>  
        </wsHttpBinding>  
      </bindings>  
      <behaviors>  
        <endpointBehaviors>  
          <behavior name="ClientCertificateBehavior">  
            <clientCredentials>  
              <clientCertificate findValue="client.com" storeLocation="CurrentUser" storeName="My" x509FindType="FindBySubjectName" />  
              <serviceCertificate>  
                <authentication certificateValidationMode="PeerOrChainTrust" />  
              </serviceCertificate>  
            </clientCredentials>  
          </behavior>  
        </endpointBehaviors>  
      </behaviors>    
    </system.serviceModel>  
    ```  
  
3. `MetadataExchangeClient`를 만들고 `GetMetadata`를 호출합니다. 이 작업을 수행하려면 두 가지 방법을 사용할 수 있습니다. 사용자 지정 바인딩을 구성에서 지정할 수도 있고, 다음 예제와 같이 코드에서 지정할 수도 있습니다.  
  
    ```csharp
    // The custom binding is specified in configuration.  
    EndpointAddress mexAddress = new EndpointAddress("http://localhost:8000/ServiceModelSamples/Service/mex");  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("http");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mexSet = mexClient.GetMetadata(mexAddress);  
  
    // The custom binding is specified in code.  
    // Specify the Metadata Exchange binding and its security mode.  
    WSHttpBinding mexBinding = new WSHttpBinding(SecurityMode.Message);  
    mexBinding.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;  
  
    // Create a MetadataExchangeClient and set the certificate details.  
    MetadataExchangeClient mexClient = new MetadataExchangeClient(mexBinding);  
    mexClient.SoapCredentials.ClientCertificate.SetCertificate(  
        StoreLocation.CurrentUser, StoreName.My,  
        X509FindType.FindBySubjectName, "client.com");  
    mexClient.SoapCredentials.ServiceCertificate.Authentication.  
        CertificateValidationMode =  
        X509CertificateValidationMode.PeerOrChainTrust;  
    mexClient.SoapCredentials.ServiceCertificate.SetDefaultCertificate(  
        StoreLocation.CurrentUser, StoreName.TrustedPeople,  
        X509FindType.FindBySubjectName, "localhost");  
    MetadataExchangeClient mexClient2 = new MetadataExchangeClient(customBinding);  
    mexClient2.ResolveMetadataReferences = true;  
    MetadataSet mexSet2 = mexClient2.GetMetadata(mexAddress);  
    ```  
  
4. 다음 코드에 표시된 것처럼 `WsdlImporter`를 만들고 `ImportAllEndpoints`를 호출합니다.  
  
    ```csharp
    WsdlImporter importer = new WsdlImporter(mexSet);  
    ServiceEndpointCollection endpoints = importer.ImportAllEndpoints();  
    ```  
  
5. 이제 서비스 엔드포인트의 컬렉션을 가지게 됩니다. 메타 데이터를 [가져오는 방법에 대 한 자세한 내용은 방법: 서비스 끝점](../feature-details/how-to-import-metadata-into-service-endpoints.md)으로 메타 데이터를 가져옵니다.  
  
## <a name="see-also"></a>참고자료

- [메타데이터](../feature-details/metadata.md)
