---
title: '방법: 기본 WCF 웹 HTTP 서비스 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 877662d3-d372-4e08-b417-51f66a0095cd
ms.openlocfilehash: e9646235f9423f2a4df9cfe09a5e83a91dcdcace
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70895185"
---
# <a name="how-to-create-a-basic-wcf-web-http-service"></a>방법: 기본 WCF 웹 HTTP 서비스 만들기

WCF (Windows Communication Foundation)를 사용 하면 웹 끝점을 노출 하는 서비스를 만들 수 있습니다. 웹 엔드포인트는 XML 또는 JSON으로 데이터를 보내며 SOAP 봉투가 없습니다. 이 항목에서는 이러한 엔드포인트를 노출하는 방법을 보여 줍니다.

> [!NOTE]
> 웹 엔드포인트의 보안을 유지하는 유일한 방법은 전송 보안을 사용하여 HTTPS를 통해 웹 엔드포인트를 노출하는 것입니다. 메시지 기반 보안을 사용하는 경우 보안 정보는 일반적으로 SOAP 헤더에 배치되고 비 SOAP 엔드포인트에 보낸 메시지에 SOAP 봉투가 없기 때문에 보안 정보를 배치할 장소가 없으며 전송 보안을 사용해야 합니다.

## <a name="to-create-a-web-endpoint"></a>웹 엔드포인트를 만들려면

1. <xref:System.ServiceModel.ServiceContractAttribute>, <xref:System.ServiceModel.Web.WebInvokeAttribute> 및 <xref:System.ServiceModel.Web.WebGetAttribute> 특성으로 표시된 인터페이스를 사용하여 서비스 계약을 정의합니다.

     [!code-csharp[htBasicService#0](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#0)]
     [!code-vb[htBasicService#0](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#0)]

    > [!NOTE]
    > 기본적으로 <xref:System.ServiceModel.Web.WebInvokeAttribute>는 POST 호출을 작업에 매핑합니다. 그러나 "method=" 매개 변수를 지정하여 작업에 매핑할 HTTP 메서드(예: HEAD, PUT 또는 DELETE)를 지정할 수 있습니다. <xref:System.ServiceModel.Web.WebGetAttribute>는 "method=" 매개 변수를 사용하지 않고 GET 호출만 서비스 작업에 매핑합니다.

2. 서비스 계약을 구현합니다.

     [!code-csharp[htBasicService#1](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#1)]
     [!code-vb[htBasicService#1](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#1)]

## <a name="to-host-the-service"></a>서비스를 호스트하려면

1. <xref:System.ServiceModel.Web.WebServiceHost> 개체를 만듭니다.

     [!code-csharp[htBasicService#2](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#2)]
     [!code-vb[htBasicService#2](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#2)]

2. <xref:System.ServiceModel.Description.ServiceEndpoint>를 <xref:System.ServiceModel.Description.WebHttpBehavior>와 함께 추가합니다.

     [!code-csharp[htBasicService#3](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#3)]
     [!code-vb[htBasicService#3](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#3)]

    > [!NOTE]
    > 엔드포인트를 추가하지 않으면 <xref:System.ServiceModel.Web.WebServiceHost>는 자동으로 기본 엔드포인트를 만듭니다. <xref:System.ServiceModel.Web.WebServiceHost>는 또한 <xref:System.ServiceModel.Description.WebHttpBehavior>를 추가하고 메타데이터 엔드포인트가 기본 HTTP 엔드포인트와 간섭하지 않도록 HTTP 도움말 페이지 및 WSDL(웹 서비스 기술 언어) GET 기능을 비활성화합니다.
    >
    >  비 SOAP 엔드포인트를 ""의 URL과 함께 추가하면 엔드포인트에서 작업 호출 시도 시 예기치 못한 동작이 발생합니다. 이는 끝점의 수신 대기 URI가 도움말 페이지의 URI (WCF 서비스의 기본 주소를 찾아볼 때 표시 되는 페이지)와 동일 하기 때문입니다.

     이러한 동작이 발생되지 않도록 하기 위해 다음 작업 중 하나를 수행할 수 있습니다.

    - 항상 비 SOAP 엔드포인트에 공백 없는 URI를 지정합니다.

    - 도움말 페이지를 끕니다. 다음 코드를 사용 하 여이 작업을 수행할 수 있습니다.

     [!code-csharp[htBasicService#4](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/snippets.cs#4)]
     [!code-vb[htBasicService#4](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/snippets.vb#4)]

3. 서비스 호스트를 열고 사용자가 Enter 키를 누를 때까지 기다립니다.

     [!code-csharp[htBasicService#5](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/snippets.cs#5)]
     [!code-vb[htBasicService#5](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/snippets.vb#5)]

     이 샘플에서는 콘솔 애플리케이션에서 웹 스타일 서비스를 호스팅하는 방법을 보여 줍니다. IIS 내에서도 이러한 서비스를 호스팅할 수 있습니다. 이 작업을 수행하려면 다음 코드에서처럼 .svc 파일에서 <xref:System.ServiceModel.Activation.WebServiceHostFactory> 클래스를 지정합니다.

    ```text
    <%ServiceHost
        language=c#
        Debug="true"
        Service="Microsoft.Samples.Service"
        Factory=System.ServiceModel.Activation.WebServiceHostFactory%>
    ```

## <a name="to-call-service-operations-mapped-to-get-in-internet-explorer"></a>Internet Explorer에서 GET에 매핑된 서비스 작업을 호출하려면

1. Internet Explorer를 열고 "`http://localhost:8000/EchoWithGet?s=Hello, world!`"를 입력 한 다음 enter 키를 누릅니다. URL에는 서비스의 기준 주소 (`http://localhost:8000/`), 끝점의 상대 주소 (""), 호출할 서비스 작업 ("EchoWithGet") 및 앰퍼샌드 (&)로 구분 된 명명 된 매개 변수 목록이 표시 된 다음 물음표가 포함 됩니다.

## <a name="to-call-service-operations-in-code"></a>코드에서 서비스 작업을 호출하려면

1. <xref:System.ServiceModel.ChannelFactory%601> 블록 내에서 `using` 인스턴스를 만듭니다.

     [!code-csharp[htBasicService#6](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#6)]
     [!code-vb[htBasicService#6](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#6)]

2. <xref:System.ServiceModel.Description.WebHttpBehavior>가 호출하는 엔드포인트에 <xref:System.ServiceModel.ChannelFactory%601>를 추가합니다.

     [!code-csharp[htBasicService#7](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#7)]
     [!code-vb[htBasicService#7](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#7)]

3. 채널을 만들고 서비스를 호출합니다.

     [!code-csharp[htBasicService#8](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#8)]
     [!code-vb[htBasicService#8](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#8)]

4. <xref:System.ServiceModel.Web.WebServiceHost>를 닫습니다.

     [!code-csharp[htBasicService#9](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#9)]
     [!code-vb[htBasicService#9](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#9)]

## <a name="example"></a>예제

다음은 이 예제에 해당되는 전체 코드 목록입니다.

[!code-csharp[htBasicService#10](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#10)]
[!code-vb[htBasicService#10](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#10)]

## <a name="compiling-the-code"></a>코드 컴파일

Service.cs를 컴파일할 때 System.ServiceModel.dll 및 System.ServiceModel.Web.dll을 참조합니다.

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.WebHttpBinding>
- <xref:System.ServiceModel.Web.WebGetAttribute>
- <xref:System.ServiceModel.Web.WebInvokeAttribute>
- <xref:System.ServiceModel.Web.WebServiceHost>
- <xref:System.ServiceModel.Description.WebHttpBehavior>
- [WCF 웹 HTTP 프로그래밍 모델](wcf-web-http-programming-model.md)
