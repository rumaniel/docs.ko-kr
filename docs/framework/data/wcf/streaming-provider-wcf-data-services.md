---
title: 스트리밍 공급자(WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, providers
- WCF Data Services, binary data
- streaming data provider [WCF Data Services]
- WCF Data Services, streams
ms.assetid: f0978fe4-5f9f-42aa-a5c2-df395d7c9495
ms.openlocfilehash: 4d51011fddb856cf1ebd00943e9b79776d9181d0
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854115"
---
# <a name="streaming-provider-wcf-data-services"></a>스트리밍 공급자(WCF Data Services)

데이터 서비스에서 BLOB(Binary Large Object) 데이터를 노출할 수 있습니다. 이 이진 데이터는 비디오 및 오디오 스트림, 이미지, 문서 파일 또는 다른 형식의 이진 미디어를 나타낼 수 있습니다. 데이터 모델의 엔터티에 이진 속성이 하나 이상 포함되어 있는 경우 데이터 서비스가 이 이진 데이터를 응답 피드의 항목 안에 base-64로 인코딩하여 반환합니다. 이러한 방식으로 많은 이진 데이터를 로드 하 고 serialize 하면 성능에 영향 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 을 줄 수 있기 때문에는 자신이 속한 엔터티와 독립적으로 이진 데이터를 검색 하기 위한 메커니즘을 정의 합니다. 이 작업은 엔터티의 이진 데이터를 하나 이상의 데이터 스트림으로 구분하여 수행됩니다.

- 미디어 리소스 - 비디오, 오디오, 이미지 또는 다른 형식의 미디어 리소스 스트림과 같은 엔터티에 속하는 이진 데이터입니다.

- 미디어 링크 항목 - 관련 미디어 리소스 스트림에 대한 참조가 있는 엔터티입니다.

[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]에서 스트리밍 데이터 공급자를 이진 리소스 스트림을 정의합니다. 스트리밍 공급자 구현에서는 특정 엔터티와 <xref:System.IO.Stream> 연결 된 미디어 리소스 스트림과 함께 데이터 서비스를 개체로 제공 합니다. 이 구현을 사용하면 데이터 서비스가 HTTP를 통해 미디어 리소스를 받아들이고 지정된 MIME 형식의 이진 데이터 스트림으로 반환합니다.

이진 데이터의 스트리밍을 지원하도록 데이터 서비스를 구성하려면 다음 단계를 수행해야 합니다.

1. 데이터 모델에서 하나 이상의 엔터티 특성을 미디어 링크 항목으로 지정합니다. 이러한 엔터티에는 스트리밍할 이진 데이터가 포함되면 안 됩니다. 엔터티의 모든 이진 속성은 항상 base-64로 인코딩된 이진 데이터로 항목에 반환됩니다.

2. T:System.Data.Services.Providers.IDataServiceStreamProvider 인터페이스를 구현합니다.

3. <xref:System.IServiceProvider> 인터페이스를 구현하는 데이터 서비스를 정의합니다. 데이터 서비스는 <xref:System.IServiceProvider.GetService%2A> 구현을 사용하여 스트리밍 데이터 공급자 구현에 액세스합니다. 이 메서드는 적절한 스트리밍 공급자 구현을 반환합니다.

4. 웹 애플리케이션 구성에서 큰 메시지 스트림을 사용하도록 설정합니다.

5. 서버나 데이터 소스의 이진 리소스에 대한 액세스를 사용하도록 설정합니다.

이 항목의 예제는 샘플 스트리밍 사진 서비스를 기반으로 하며, post [Data Services streaming Provider 시리즈에서 자세히 설명 합니다. 스트리밍 공급자 구현 (1 부)](https://go.microsoft.com/fwlink/?LinkID=198989) 이 샘플 서비스의 소스 코드는 MSDN 코드 갤러리의 [스트리밍 사진 데이터 서비스 샘플 페이지](https://go.microsoft.com/fwlink/?LinkID=198988) 에서 사용할 수 있습니다.

## <a name="defining-a-media-link-entry-in-the-data-model"></a>데이터 모델에서 미디어 링크 항목 정의

데이터 소스 공급자는 엔터티가 데이터 모델에서 미디어 링크 항목으로 정의되는 방식을 결정합니다.

**Entity Framework 공급자**

엔터티가 미디어 링크 항목임을 나타내려면 다음 예제와 같이 개념적 모델의 엔터티 형식 정의에 `HasStream` 특성을 추가합니다.

[!code-xml[Astoria Photo Streaming Service#HasStream](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_photo_streaming_service/xml/photodata.edmx#hasstream)]

또한 데이터 모델을 정의하는 .edmx 또는 .csdl 파일의 루트나 엔터티에 `xmlns:m=http://schemas.microsoft.com/ado/2007/08/dataservices/metadata` 네임스페이스를 추가해야 합니다.

Entity Framework 공급자를 사용 하 고 미디어 리소스를 노출 하는 데이터 서비스에 대 한 예제는 post [Data Services Streaming provider 시리즈를 참조 하세요. 스트리밍 공급자 구현 (1 부)](https://go.microsoft.com/fwlink/?LinkID=198989)

**리플렉션 공급자**

엔터티가 미디어 링크 항목임을 나타내려면 리플렉션 공급자에서 엔터티 형식을 정의하는 클래스에 <xref:System.Data.Services.Common.HasStreamAttribute>를 추가합니다.

**사용자 지정 데이터 서비스 공급자**

사용자 지정 서비스 공급자를 사용하는 경우 <xref:System.Data.Services.Providers.IDataServiceMetadataProvider> 인터페이스를 구현하여 데이터 서비스에 대한 메타데이터를 정의합니다. 자세한 내용은 [사용자 지정 데이터 서비스 공급자](custom-data-service-providers-wcf-data-services.md)를 참조 하세요. 미디어 링크 항목인 엔터티 형식을 나타내는 <xref:System.Data.Services.Providers.ResourceType>에서 <xref:System.Data.Services.Providers.ResourceType.IsMediaLinkEntry%2A> 속성을 `true`로 설정하여 이진 리소스 스트림이 <xref:System.Data.Services.Providers.ResourceType>에 속해 있음을 나타냅니다.

## <a name="implementing-the-idataservicestreamprovider-interface"></a>IDataServiceStreamProvider 인터페이스 구현

이진 데이터 스트림을 지원하는 데이터 서비스를 만들려면 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 인터페이스를 구현해야 합니다. 이 구현을 통해 데이터 서비스에서 이진 데이터를 스트림으로 클라이언트에 반환하고 클라이언트에서 전송되는 스트림으로 이진 데이터를 사용할 수 있습니다. 데이터 서비스는 스트림으로 이진 데이터에 액세스해야 할 때마다 이 인터페이스의 인스턴스를 만듭니다. <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 인터페이스는 다음 멤버를 지정합니다.

|멤버 이름|설명|
|-----------------|-----------------|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.DeleteStream%2A>|이 메서드는 미디어 링크 항목이 삭제될 때 해당 미디어 리소스를 삭제하기 위해 데이터 서비스에서 호출됩니다. <xref:System.Data.Services.Providers.IDataServiceStreamProvider>를 구현하는 경우 이 메서드에는 제공된 미디어 링크 항목과 연결된 미디어 리소스를 삭제하는 코드가 포함됩니다.|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetReadStream%2A>|이 메서드는 미디어 리소스를 스트림으로 반환하기 위해 데이터 서비스에서 호출됩니다. <xref:System.Data.Services.Providers.IDataServiceStreamProvider>를 구현하는 경우 이 메서드에는 제공된 미디어 링크 항목과 연결된 미디어 리소스를 반환하기 위해 데이터 서비스에서 사용되는 스트림을 제공하는 코드가 포함됩니다.|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetReadStreamUri%2A>|이 메서드는 미디어 링크 항목의 미디어 리소스를 요청하는 데 사용되는 URI를 반환하기 위해 데이터 서비스에서 호출됩니다. 이 값은 미디어 링크 항목의 콘텐츠 요소에서 데이터 스트림을 요청할 때 사용되는 `src` 특성을 만드는 데 사용됩니다. 이 메서드가 `null`을 반환하면 데이터 서비스에서 자동으로 URI를 결정합니다. 스트림 공급자를 사용하지 않고 이진 데이터에 직접 액세스할 수 있는 권한을 클라이언트에 제공해야 할 때 이 메서드를 사용합니다.|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetStreamContentType%2A>|이 메서드는 지정된 미디어 링크 항목과 연결된 미디어 리소스의 Content-Type 값을 반환하기 위해 데이터 서비스에서 호출됩니다.|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetStreamETag%2A>|이 메서드는 지정된 엔터티와 연결된 데이터 스트림의 eTag를 반환하기 위해 데이터 서비스에서 호출됩니다. 이 메서드는 이진 데이터의 동시성을 관리할 때 사용됩니다. 이 메서드가 null을 반환하는 경우 데이터 서비스는 동시성을 추적하지 않습니다.|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A>|이 메서드는 클라이언트에서 전송된 스트림을 받을 때 사용되는 스트림을 가져오기 위해 데이터 서비스에서 호출됩니다. <xref:System.Data.Services.Providers.IDataServiceStreamProvider>를 구현하는 경우 데이터 서비스가 수신된 스트림 데이터를 쓰는 쓰기 가능한 스트림을 반환해야 합니다.|
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.ResolveType%2A>|삽입될 미디어 리소스의 데이터 스트림과 연결된 미디어 링크 항목에 대해 데이터 서비스 런타임이 만들어야 하는 형식을 나타내는 네임스페이스로 한정된 형식 이름을 반환합니다.|

## <a name="creating-the-streaming-data-service"></a>스트리밍 데이터 서비스 만들기

[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 런타임에 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 구현에 대한 액세스 권한을 제공하려면 만든 데이터 서비스에서 <xref:System.IServiceProvider> 인터페이스도 구현해야 합니다. 다음 예제에서는 <xref:System.IServiceProvider.GetService%2A>를 구현하는 `PhotoServiceStreamProvider` 클래스의 인스턴스를 반환하기 위해 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 메서드를 구현하는 방법을 보여 줍니다.

[!code-csharp[Astoria Photo Streaming Service#PhotoServiceStreamingProvider](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_photo_streaming_service/cs/photodata.svc.cs#photoservicestreamingprovider)]
[!code-vb[Astoria Photo Streaming Service#PhotoServiceStreamingProvider](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_photo_streaming_service/vb/photodata.svc.vb#photoservicestreamingprovider)]

데이터 서비스를 만드는 방법에 대 한 일반적인 내용은 [데이터 서비스 구성](configuring-the-data-service-wcf-data-services.md)을 참조 하세요.

## <a name="enabling-large-binary-streams-in-the-hosting-environment"></a>호스팅 환경에서 큰 이진 스트림 사용

ASP.NET 웹 응용 프로그램에서 데이터 서비스를 만들 때 WCF (Windows Communication Foundation)를 사용 하 여 HTTP 프로토콜 구현을 제공 합니다. 기본적으로 WCF는 HTTP 메시지의 크기를 65K바이트로 제한합니다. 데이터 서비스에서 보내고 받는 큰 이진 데이터를 스트리밍할 수 있으려면 큰 이진 파일을 사용할 수 있고 전송에 스트림을 사용하도록 웹 애플리케이션도 구성해야 합니다. 이렇게 하려면 애플리케이션의 Web.config 파일에 있는 `<configuration />` 요소에 다음을 추가합니다.

> [!NOTE]
> <xref:System.ServiceModel.TransferMode.Streamed?displayProperty=nameWithType> 전송 모드를 사용 하 여 요청 및 응답 메시지의 이진 데이터를 스트리밍하 고 WCF에 의해 버퍼링 되지 않았는지 확인 해야 합니다.

자세한 내용은 [스트리밍 메시지 전송](../../wcf/feature-details/streaming-message-transfer.md) 및 [전송 할당량](../../wcf/feature-details/transport-quotas.md)을 참조 하세요.

기본적으로 인터넷 정보 서비스(IIS)는 요청 크기를 4MB로 제한합니다. 데이터 서비스에서 IIS를 실행할 때 4mb 보다 큰 스트림을 받을 수 있도록 하려면 다음과 같이 `maxRequestLength` `<system.web />` 구성 섹션에서 [httpRuntime 요소 (ASP.NET Settings 스키마)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/e1f13641(v=vs.100)) 의 특성도 설정 해야 합니다. 예 들어

## <a name="using-data-streams-in-a-client-application"></a>클라이언트 애플리케이션에서 데이터 스트림 사용

[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 클라이언트 라이브러리를 사용하면 클라이언트에서 이진 스트림으로 노출된 이러한 리소스를 검색하고 업데이트할 수 있습니다. 자세한 내용은 [이진 데이터 작업](working-with-binary-data-wcf-data-services.md)을 참조 하세요.

## <a name="considerations-for-working-with-a-streaming-provider"></a>스트리밍 공급자로 작업하기 위한 고려 사항

스트리밍 공급자를 구현하는 경우와 데이터 서비스에서 미디어 리소스에 액세스하는 경우 고려할 사항은 다음과 같습니다.

- 미디어 리소스에 대한 병합 요청은 지원되지 않습니다. 기존 엔터티의 미디어 리소스를 변경하려면 PUT 요청을 사용하세요.

- POST 요청을 사용하여 새 미디어 링크 항목을 만들 수 없습니다. 대신 POST 요청을 실행하여 새 미디어 리소스를 만들어야 하며, 이 경우 데이터 서비스에서 기본값을 사용하여 새 미디어 링크 항목을 만듭니다. 이 새 엔터티는 이후 병합 또는 PUT 요청으로 업데이트할 수 있습니다. 또한 엔터티를 캐시하는 것을 고려할 수 있으며 속성 값을 POST 요청의 Slug 헤더 값으로 설정하는 등, 삭제기에서 업데이트를 수행할 수 있습니다.

- POST 요청을 받으면 데이터 서비스는 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A>를 호출하여 미디어 링크 항목을 만들기 전에 <xref:System.Data.Services.IUpdatable.SaveChanges%2A>을 호출하여 미디어 리소스를 만듭니다.

- <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A> 구현에서 <xref:System.IO.MemoryStream> 개체를 반환하면 안 됩니다. 이러한 종류의 스트림을 사용하는 경우 서비스가 매우 큰 데이터 스트림을 받으면 메모리 리소스 문제가 발생합니다.

- 데이터베이스에 미디어 리소스를 저장하는 경우 고려할 사항은 다음과 같습니다.

  - 미디어 리소스인 이진 속성이 데이터 모델에 포함되면 안 됩니다. 데이터 모델에서 노출된 모든 속성은 응답 피드의 항목에 반환됩니다.

  - 큰 이진 스트림의 성능을 높이려면 사용자 지정 스트림 클래스를 만들어 데이터베이스에 이진 데이터를 저장하는 것이 좋습니다. 이 클래스는 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A> 구현에 의해 반환되며 이진 데이터를 청크로 데이터베이스에 보냅니다. SQL Server 데이터베이스의 경우 이진 데이터가 1MB 보다 크면 FILESTREAM을 사용 하 여 데이터베이스에 데이터를 스트리밍하는 것이 좋습니다.

  - 사용하는 데이터베이스가 데이터 서비스를 통해 받을 큰 이진 스트림을 저장하도록 디자인되었는지 확인합니다.

  - 클라이언트가 POST 요청을 보내 단일 요청에서 미디어 리소스와 함께 미디어 링크 항목을 삽입하면 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A>이 호출되어 데이터 서비스가 새 엔터티를 데이터베이스에 삽입하기 전에 스트림을 가져옵니다. 스트리밍 공급자 구현에서 이 데이터 서비스 동작을 처리할 수 있어야 합니다. 엔터티가 데이터베이스에 삽입된 후까지 파일에 데이터 스트림을 저장하거나 이진 데이터를 저장하려면 별도의 데이터 테이블을 사용하는 것이 좋습니다.

- <xref:System.Data.Services.Providers.IDataServiceStreamProvider.DeleteStream%2A>, <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetReadStream%2A> 또는 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A> 메서드를 구현하는 경우 메서드 매개 변수로 제공되는 eTag 및 Content-Type 값을 사용해야 합니다. <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 공급자 구현에서 eTag 또는 Content-Type 헤더를 설정하지 마세요.

- 기본적으로 클라이언트는 청크된 HTTP Transfer-Encoding을 사용하여 큰 이진 스트림을 보냅니다. ASP.NET 개발 서버는 이러한 종류의 인코딩을 지원 하지 않으므로이 웹 서버를 사용 하 여 많은 이진 스트림을 허용 해야 하는 스트리밍 데이터 서비스를 호스트할 수 없습니다. ASP.NET 개발 서버에 대 한 자세한 내용은 [Visual Studio에서 ASP.NET 웹 프로젝트용 웹 서버](https://docs.microsoft.com/previous-versions/aspnet/58wxa9w5(v=vs.120))를 참조 하세요.

<a name="versioning"></a>

## <a name="versioning-requirements"></a>버전 관리 요구 사항

스트리밍 공급자에 대한 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 프로토콜 버전 관리 요구 사항은 다음과 같습니다.

- 스트리밍 공급자의 경우 데이터 서비스가 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 프로토콜 버전 2.0 이상을 지원해야 합니다.

자세한 내용은 [데이터 서비스 버전 관리](data-service-versioning-wcf-data-services.md)합니다.

## <a name="see-also"></a>참고자료

- [Data Services 공급자](data-services-providers-wcf-data-services.md)
- [사용자 지정 데이터 서비스 공급자](custom-data-service-providers-wcf-data-services.md)
- [이진 데이터 작업](working-with-binary-data-wcf-data-services.md)
