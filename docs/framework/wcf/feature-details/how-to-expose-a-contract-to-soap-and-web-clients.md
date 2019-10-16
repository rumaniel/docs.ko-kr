---
title: '방법: SOAP 및 웹 클라이언트에 계약 공개'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: bb765a48-12f2-430d-a54d-6f0c20f2a23a
ms.openlocfilehash: 303367c85e311ac5c07c11b849b5586354980a3c
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65636149"
---
# <a name="how-to-expose-a-contract-to-soap-and-web-clients"></a>방법: SOAP 및 웹 클라이언트에 계약 공개

기본적으로 Windows Communication Foundation (WCF) 사용 가능 끝점 SOAP 클라이언트에만 합니다. [방법: 기본 WCF 웹 HTTP 서비스 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-wcf-web-http-service.md), 끝점 비 SOAP 클라이언트에 제공 됩니다. 동일한 계약을 웹 엔드포인트 및 SOAP 엔드포인트로 모두 사용해야 하는 경우가 있습니다. 이 항목에서는 이 작업을 수행하는 방법을 보여 줍니다.

## <a name="to-define-the-service-contract"></a>서비스 계약을 정의하려면

1. 사용 하 여 표시 된 인터페이스를 사용 하 여 서비스 계약을 정의 합니다 <xref:System.ServiceModel.ServiceContractAttribute>, <xref:System.ServiceModel.Web.WebInvokeAttribute> 및 <xref:System.ServiceModel.Web.WebGetAttribute> 특성에 다음 코드 에서처럼:

    [!code-csharp[htSoapWeb#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#0)]
    [!code-vb[htSoapWeb#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#0)]

    > [!NOTE]
    > 기본적으로 <xref:System.ServiceModel.Web.WebInvokeAttribute>는 POST 호출을 작업에 매핑합니다. 그러나 "method=" 매개 변수를 지정하여 작업에 매핑할 메서드를 지정할 수 있습니다. <xref:System.ServiceModel.Web.WebGetAttribute>는 "method=" 매개 변수를 사용하지 않고 GET 호출만 서비스 작업에 매핑합니다.

2. 다음 코드 에서처럼 서비스 계약을 구현 합니다.

     [!code-csharp[htSoapWeb#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#1)]
     [!code-vb[htSoapWeb#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#1)]

## <a name="to-host-the-service"></a>서비스를 호스트하려면

1. 만들기는 <xref:System.ServiceModel.ServiceHost> 다음 코드 에서처럼 개체:

     [!code-csharp[htSoapWeb#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#2)]
     [!code-vb[htSoapWeb#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#2)]

2. 추가 된 <xref:System.ServiceModel.Description.ServiceEndpoint> 사용 하 여 <xref:System.ServiceModel.BasicHttpBinding> SOAP 끝점의 경우 다음 코드 에서처럼:

     [!code-csharp[htSoapWeb#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#3)]
     [!code-vb[htSoapWeb#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#3)]

3. 추가 <xref:System.ServiceModel.Description.ServiceEndpoint> 사용 하 여 <xref:System.ServiceModel.WebHttpBinding> 비 SOAP 끝점에 대 한 추가 <xref:System.ServiceModel.Description.WebHttpBehavior> 끝점에 다음 코드 에서처럼:

     [!code-csharp[htSoapWeb#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#4)]
     [!code-vb[htSoapWeb#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#4)]

4. 호출 `Open()` 에 <xref:System.ServiceModel.ServiceHost> 인스턴스를 다음 코드 에서처럼 서비스 호스트를 엽니다.

     [!code-csharp[htSoapWeb#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#5)]
     [!code-vb[htSoapWeb#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#5)]

## <a name="to-call-service-operations-mapped-to-get-in-internet-explorer"></a>Internet Explorer에서 GET에 매핑된 서비스 작업을 호출하려면

1. Internet Explorer를 열고 입력 "`http://localhost:8000/Web/EchoWithGet?s=Hello, world!`" ENTER 키를 누릅니다. 서비스의 기본 주소를 포함 하는 URL (`http://localhost:8000/`), 끝점의 상대 주소 (""), 앰퍼샌드를 구분 하는 명명 된 매개 변수 목록이 뒤에 서비스 작업 호출 ("EchoWithGet") 및 물음표 (&).

## <a name="to-call-service-operations-on-the-web-endpoint-in-code"></a>코드의 웹 엔드포인트에서 서비스 작업을 호출하려면

1. 다음 코드와 같이 <xref:System.ServiceModel.Web.WebChannelFactory%601> 블록 내에서 `using` 인스턴스를 만듭니다.

     [!code-csharp[htSoapWeb#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#6)]
     [!code-vb[htSoapWeb#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#6)]

> [!NOTE]
> `Close()`는 `using` 블록의 끝에 있는 채널에서 자동으로 호출됩니다.

1. 다음 코드와 같이 채널을 만들고 서비스를 호출합니다.

     [!code-csharp[htSoapWeb#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#8)]
     [!code-vb[htSoapWeb#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#8)]

## <a name="to-call-service-operations-on-the-soap-endpoint"></a>SOAP 엔드포인트에서 서비스 작업을 호출하려면

1. 다음 코드와 같이 <xref:System.ServiceModel.ChannelFactory> 블록 내에서 `using` 인스턴스를 만듭니다.

    [!code-csharp[htSoapWeb#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#10)]
    [!code-vb[htSoapWeb#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#10)]

2. 다음 코드와 같이 채널을 만들고 서비스를 호출합니다.

    [!code-csharp[htSoapWeb#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#11)]
    [!code-vb[htSoapWeb#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#11)]

## <a name="to-close-the-service-host"></a>서비스 호스트를 닫으려면

1. 다음 코드와 같이 서비스 호스트를 닫습니다.

    [!code-csharp[htSoapWeb#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#9)]
    [!code-vb[htSoapWeb#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#9)]

## <a name="example"></a>예제

다음은 전체 코드 목록은이 항목에 대 한입니다.

[!code-csharp[htSoapWeb#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#13)]
[!code-vb[htSoapWeb#13](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#13)]

## <a name="compiling-the-code"></a>코드 컴파일

 Service.cs를 컴파일할 때 System.ServiceModel.dll 및 System.ServiceModel.Web.dll을 참조합니다.

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.WebHttpBinding>
- <xref:System.ServiceModel.Web.WebGetAttribute>
- <xref:System.ServiceModel.Web.WebInvokeAttribute>
- <xref:System.ServiceModel.Web.WebServiceHost>
- <xref:System.ServiceModel.ChannelFactory>
- <xref:System.ServiceModel.Description.WebHttpBehavior>
- [WCF 웹 HTTP 프로그래밍 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
