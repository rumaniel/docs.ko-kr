---
title: 독립형 진단 피드 샘플
ms.date: 03/30/2017
ms.assetid: d31c6c1f-292c-4d95-8e23-ed8565970ea5
ms.openlocfilehash: 6b83bda154a76fe10487da00359e0ceace8ce8cb
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044675"
---
# <a name="stand-alone-diagnostics-feed-sample"></a>독립형 진단 피드 샘플
이 샘플에서는 Windows Communication Foundation (WCF)를 사용 하 여 배포 하기 위해 RSS/Atom 피드를 만드는 방법을 보여 줍니다. 개체 모델의 기본 사항 및 Windows Communication Foundation (WCF) 서비스에서 설정 하는 방법을 보여 주는 기본적인 "Hello World" 프로그램입니다.  
  
 WCF는 배포 피드를 특수 데이터 형식을 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter>반환 하는 서비스 작업으로 모델링 합니다. <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter>의 인스턴스는 피드를 RSS 2.0 및 ATOM 1.0 형식으로 serialize할 수 있습니다. 다음 샘플 코드에서는 사용된 계약을 보여 줍니다.  
  
```  
[ServiceContract(Namespace = "")]  
    interface IDiagnosticsService  
    {  
        [OperationContract]  
        //The [WebGet] attribute controls how WCF dispatches  
        //HTTP requests to service operations based on a URI suffix  
        //(the part of the request URI after the endpoint address)  
        //using the HTTP GET method. The UriTemplate specifies a relative  
        //path of 'feed', and specifies that the format is  
        //supplied using a query string.   
        [WebGet(UriTemplate="feed?format={format}")]  
        [ServiceKnownType(typeof(Atom10FeedFormatter))]  
        [ServiceKnownType(typeof(Rss20FeedFormatter))]  
        SyndicationFeedFormatter GetProcesses(string format);  
    }  
```  
  
 작업 `GetProcesses` 에는 WCF가 서비스 <xref:System.ServiceModel.Web.WebGetAttribute> 작업에 HTTP GET 요청을 디스패치 하는 방법을 제어 하 고 전송 되는 메시지의 형식을 지정 하는 데 사용할 수 있는 특성으로 주석이 추가 됩니다.  
  
 모든 WCF 서비스와 마찬가지로 배포 피드는 모든 관리 되는 응용 프로그램에서 자체 호스팅될 수 있습니다. 배포 서비스가 제대로 작동하려면 특정 바인딩(<xref:System.ServiceModel.WebHttpBinding>) 및 특정 엔드포인트 동작(<xref:System.ServiceModel.Description.WebHttpBehavior>)이 필요합니다. 새 <xref:System.ServiceModel.Web.WebServiceHost> 클래스는 특정 구성 없이 이러한 엔드포인트를 만들기 위해 다음과 같이 편리한 API를 제공합니다.  
  
```  
WebServiceHost host = new WebServiceHost(typeof(ProcessService), new Uri("http://localhost:8000/diagnostics"));  
  
            //The WebServiceHost will automatically provide a default endpoint at the base address  
            //using the proper binding (the WebHttpBinding) and endpoint behavior (the WebHttpBehavior)  
```  
  
 또는 IIS에서 호스트되는 .svc 파일 내에서 <xref:System.ServiceModel.Activation.WebServiceHostFactory>를 사용하여 동일한 기능을 제공할 수 있습니다(이 방법은 샘플 코드에서 설명하지 않음).  
  
```  
<%@ ServiceHost Language="C#|VB" Debug="true" Service="ProcessService" %>  
```  
  
 이 서비스는 표준 HTTP GET을 사용하여 요청을 받기 때문에 RSS 또는 ATOM 인식 클라이언트를 사용하여 서비스에 액세스할 수 있습니다. 예를 들어 RSS 인식 브라우저에서 또는 `http://localhost:8000/diagnostics/feed/?format=atom` `http://localhost:8000/diagnostics/feed/?format=rss` 으로 이동 하 여이 서비스의 출력을 볼 수 있습니다.
  
 또한 [WCF 배포 개체 모델이 Atom 및 RSS에 매핑되는 방법을](../../../../docs/framework/wcf/feature-details/how-the-wcf-syndication-object-model-maps-to-atom-and-rss.md) 사용 하 여 배포 된 데이터를 읽고 명령적 코드를 사용 하 여 처리할 수 있습니다.  
  
```  
XmlReader reader = XmlReader.Create( "http://localhost:8000/diagnostics/feed/?format=rss",  
new XmlReaderSettings()  
{  
//MaxCharactersInDocument can be used to control the maximum amount of data   
//read from the reader and helps prevent OutOfMemoryException  
MaxCharactersInDocument = 1024 * 64  
} );  
  
SyndicationFeed feed = SyndicationFeed.Load( reader );  
  
foreach (SyndicationItem i in feed.Items)  
{  
        XmlSyndicationContent content = i.Content as XmlSyndicationContent;  
        ProcessData pd = content.ReadContent<ProcessData>();  
  
        Console.WriteLine(i.Title.Text);  
        Console.WriteLine(pd.ToString());  
}  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)의 지침 설정에 설명 된 대로 컴퓨터에서 HTTP 및 HTTPS에 대 한 올바른 주소 등록 권한이 있는지 확인 합니다.  
  
2. 솔루션을 빌드합니다.  
  
3. 콘솔 애플리케이션을 실행합니다.  
  
4. 콘솔 응용 프로그램이 실행 되는 동안 RSS 인식 `http://localhost:8000/diagnostics/feed/?format=atom` 브라우저로 `http://localhost:8000/diagnostics/feed/?format=rss` 이동 하거나 사용 합니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Syndication\DiagnosticsFeed`  
  
## <a name="see-also"></a>참고자료

- [WCF 웹 HTTP 프로그래밍 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
- [WCF 배포](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)
