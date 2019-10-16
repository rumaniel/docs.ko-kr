---
title: WebContentTypeMapper 샘플
ms.date: 03/30/2017
ms.assetid: a4fe59e7-44d8-43c6-a1f8-40c45223adca
ms.openlocfilehash: 1b15651859fd17673caf898df02c2b74a85d7612
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038534"
---
# <a name="webcontenttypemapper-sample"></a>WebContentTypeMapper 샘플
이 샘플에서는 Windows Communication Foundation (WCF) 메시지 본문 형식에 새 콘텐츠 형식을 매핑하는 방법을 보여 줍니다.  
  
 요소 <xref:System.ServiceModel.Description.WebHttpEndpoint> 는 WCF가 동일한 끝점에서 JSON, XML 또는 원시 이진 메시지를 수신할 수 있도록 웹 메시지 인코더에 연결 합니다. 인코더는 요청의 HTTP 콘텐츠 형식을 확인하여 메시지의 본문 형식을 확인합니다. 이 샘플에서는 콘텐츠 형식과 본문 형식 간의 매핑을 사용자가 제어할 수 있게 하는 <xref:System.ServiceModel.Channels.WebContentTypeMapper> 클래스를 소개합니다.  
  
 WCF는 콘텐츠 형식에 대 한 기본 매핑 집합을 제공 합니다. 예를 들어, `application/json`은  JSON에 매핑되고 `text/xml`은 XML에 매핑됩니다. JSON 또는 XML에 매핑되지 않는 모든 콘텐츠 형식은 원시 이진 형식에 매핑됩니다.  
  
 푸시 스타일 API와 같은 일부 시나리오에서 서비스 개발자는 클라이언트가 반환하는 콘텐츠 형식을 제어하지 않습니다. 예를 들어, 클라이언트가 JSON을 `text/javascript` 대신에 `application/json`로 반환할 수 있습니다. 이 경우 서비스 개발자는 다음 샘플 코드와 같이 지정된 콘텐츠 형식을 올바르게 처리하기 위해 <xref:System.ServiceModel.Channels.WebContentTypeMapper>에서 파생되는 형식을 제공해야 합니다.  
  
```  
public class JsonContentTypeMapper : WebContentTypeMapper  
{  
    public override WebContentFormat  
               GetMessageFormatForContentType(string contentType)  
    {  
        if (contentType == "text/javascript")  
        {  
            return WebContentFormat.Json;  
        }  
        else  
        {  
            return WebContentFormat.Default;  
        }  
    }  
}  
```  
  
 이 형식은 <xref:System.ServiceModel.Channels.WebContentTypeMapper.GetMessageFormatForContentType%28System.String%29> 메서드를 재정의해야 합니다. 이 메서드는 `contentType` 인수를 평가하고 <xref:System.ServiceModel.Channels.WebContentFormat.Json>, <xref:System.ServiceModel.Channels.WebContentFormat.Xml>, <xref:System.ServiceModel.Channels.WebContentFormat.Raw> 또는 <xref:System.ServiceModel.Channels.WebContentFormat.Default> 값 중 하나를 반환해야 합니다. <xref:System.ServiceModel.Channels.WebContentFormat.Default> 반환은 기본 웹 메시지 인코더 매핑을 따릅니다. 위의 샘플 코드에서 `text/javascript` 콘텐츠 형식은 JSON에 매핑되고 다른 모든 매핑은 변경되지 않은 상태로 유지됩니다.  
  
 `JsonContentTypeMapper` 클래스를 사용하여 Web.config에서 다음을 사용합니다.  
  
```xml  
<system.serviceModel>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <standardEndpoint name="" contentTypeMapper="Microsoft.Samples.WebContentTypeMapper.JsonContentTypeMapper, JsonContentTypeMapper, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 JsonContentTypeMapper 사용을 위한 요구 사항을 확인하려면 위의 구성 파일에서 contentTypeMapper 특성을 제거합니다. 그러면 `text/javascript`를 사용하여 JSON 콘텐츠를 보내려고 할 때 클라이언트 페이지를 로드하는 데 실패합니다.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)에 설명 된 대로 WebContentTypeMapperSample 솔루션을 빌드합니다.  
  
3. (프로젝트 `http://localhost/ServiceModelSamples/JCTMClientPage.htm` 디렉터리 내에서 브라우저의 jctmclientpage을 열지 마십시오.)로 이동 합니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Ajax\WebContentTypeMapper`  
