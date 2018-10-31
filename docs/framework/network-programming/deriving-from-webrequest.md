---
title: WebRequest에서 파생
ms.date: 03/30/2017
helpviewer_keywords:
- WebRequest class, pluggable protocols
- protocol-specific request handler
- sending data, pluggable protocols
- pluggable protocols, class criteria
- Internet, pluggable protocols
- receiving data, pluggable protocols
- protocols, pluggable
ms.assetid: 9810c177-973e-43d7-823c-14960bd625ea
ms.openlocfilehash: 859593c6c53d9f6dc89047efae1c682a6a9873a7
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50181266"
---
# <a name="deriving-from-webrequest"></a>WebRequest에서 파생
<xref:System.Net.WebRequest> 클래스는 .NET Framework 플러그형 프로토콜 모델에 적합한 프로토콜별 요청 처리기를 만들기 위한 기본 메서드 및 속성을 제공하는 추상 기본 클래스입니다. **WebRequest** 클래스를 사용하는 응용 프로그램은 사용되는 프로토콜을 지정할 필요 없이 지원되는 모든 프로토콜을 사용하여 데이터를 요청할 수 있습니다.  
  
 프로토콜별 클래스를 플러그형 프로토콜로 사용하려면 다음 두 가지 조건을 충족해야 합니다. 클래스는 <xref:System.Net.IWebRequestCreate> 인터페이스를 구현하고 <xref:System.Net.WebRequest.RegisterPrefix%2A?displayProperty=nameWithType> 메서드에 등록되어야 합니다. 클래스는 플러그형 인터페이스를 제공하도록 **WebRequest**의 모든 추상 메서드 및 속성을 재정의해야 합니다.  
  
 **WebRequest** 인스턴스는 일회용입니다. 또 다른 요청을 만들려면 새 **WebRequest**를 만듭니다. **WebRequest**는 개발자가 템플릿 **WebRequest**를 직렬화하고 나서 추가 요청을 위한 템플릿을 다시 구성할 수 있도록 <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 지원합니다.  
  
## <a name="iwebrequest-create-method"></a>IWebRequest Create 메서드  
 <xref:System.Net.IWebRequestCreate.Create%2A> 메서드는 프로토콜별 클래스의 새 인스턴스를 초기화해야 합니다. 새 **WebRequest**가 생성되면 <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType> 메서드는 요청된 URI를 **RegisterPrefix** 메서드에 등록된 URI 접두사와 일치시킵니다. 적절한 프로토콜별 하위 항목의 **Create** 메서드는 프로토콜별 필드를 수정할 필요 없이 프로토콜에 대한 표준 요청/응답 트랜잭션을 수행할 수 있는 하위 항목의 초기화된 인스턴스를 반환해야 합니다.  
  
## <a name="connectiongroupname-property"></a>ConnectionGroupName 속성  
 <xref:System.Net.WebRequest.ConnectionGroupName%2A> 속성을 사용하여 단일 연결을 통해 여러 요청이 생성될 수 있도록 리소스 연결 그룹의 이름을 지정합니다. 연결 공유를 구현하려면 연결 풀링 및 할당에 대한 프로토콜별 메서드를 사용해야 합니다. 예를 들어 제공된 <xref:System.Net.ServicePointManager> 클래스는 <xref:System.Net.HttpWebRequest> 클래스에 대한 연결 공유를 구현합니다. **ServicePointManager** 클래스는 각 연결 그룹의 특정 서버에 대한 연결을 제공하는 <xref:System.Net.ServicePoint>를 만듭니다.  
  
## <a name="contentlength-property"></a>ContentLength 속성  
 <xref:System.Net.WebRequest.ContentLength%2A> 속성은 데이터를 업로드할 때 서버에 전송될 데이터 크기(바이트)를 지정합니다.  
  
 일반적으로 **ContentLength** 속성이 0보다 큰 값으로 설정될 경우 업로드가 수행되도록 지정하려면 <xref:System.Net.WebRequest.Method%2A> 속성을 설정해야 합니다.  
  
## <a name="contenttype-property"></a>ContentType 속성  
 <xref:System.Net.WebRequest.ContentType%2A> 속성은 보내는 콘텐츠 형식을 식별하기 위해 프로토콜을 통해 서버에 보내야 하는 특수 정보를 제공합니다. 일반적으로 이것은 업로드된 데이터의 MIME 콘텐츠 형식입니다.  
  
## <a name="credentials-property"></a>Credentials 속성  
 <xref:System.Net.WebRequest.Credentials%2A> 속성에는 서버에서 요청을 인증하는 데 필요한 정보가 포함됩니다. 프로토콜에 대한 인증 프로세스의 세부 정보를 구현해야 합니다. <xref:System.Net.AuthenticationManager> 클래스는 요청을 인증하고 인증 토큰을 제공해야 합니다. 프로토콜에서 사용되는 자격 증명을 제공하는 클래스는 <xref:System.Net.ICredentials> 인터페이스를 구현해야 합니다.  
  
## <a name="headers-property"></a>Headers 속성  
 <xref:System.Net.WebRequest.Headers%2A> 속성에는 요청과 연결된 메타데이터 이름/값 쌍의 임의 컬렉션이 포함됩니다. 이름/값 쌍으로 표시될 수 있는 프로토콜에 필요한 모든 메타데이터가 **Headers** 속성에 포함될 수 있습니다. 일반적으로 이 정보는 <xref:System.Net.WebRequest.GetRequestStream%2A> 또는 <xref:System.Net.WebRequest.GetResponse%2A> 메서드를 호출하기 전에 설정해야 합니다. 요청이 생성된 후에는 메타데이터를 읽기 전용으로 간주합니다.  
  
 헤더 메타데이터를 사용하기 위해 **Headers** 속성을 사용할 필요가 없습니다. 프로토콜별 메타데이터는 속성으로 노출됩니다. 예를 들어 <xref:System.Net.HttpWebRequest.UserAgent%2A?displayProperty=nameWithType> 속성은 **User-Agent** HTTP 헤더를 노출합니다. 헤더 메타데이터를 속성으로 노출할 경우 **Headers** 속성을 사용하여 동일한 속성을 설정하도록 허용하면 안 됩니다.  
  
## <a name="method-property"></a>Method 속성  
 <xref:System.Net.WebRequest.Method%2A> 속성에는 요청을 통해 서버에서 수행하도록 요청할 동사 또는 작업이 포함됩니다. **Method** 속성의 기본값은 프로토콜별 속성을 설정할 필요 없이 표준 요청/응답 작업을 사용하도록 설정해야 합니다. 예를 들어 <xref:System.Net.HttpWebResponse.Method%2A> 메서드는 기본적으로 웹 서버에서 리소스를 요청하고 응답을 반환하는 GET으로 설정됩니다.  
  
 일반적으로 **Method** 속성이 업로드가 수행 중임을 나타내는 동사 또는 작업으로 설정될 경우 **ContentLength** 속성을 0보다 큰 값으로 설정해야 합니다.  
  
## <a name="preauthenticate-property"></a>PreAuthenticate 속성  
 응용 프로그램은 <xref:System.Net.WebRequest.PreAuthenticate%2A> 속성을 설정하여 인증 질문을 기다리지 않고 초기 요청을 통해 인증 정보를 보내도록 지정합니다. **PreAuthenticate** 속성은 프로토콜이 초기 요청을 통해 전송된 인증 자격 증명을 지원하는 경우에만 유효합니다.  
  
## <a name="proxy-property"></a>Proxy 속성  
 <xref:System.Net.WebRequest.Proxy%2A> 속성에는 요청된 리소스에 액세스하는 데 사용되는 <xref:System.Net.IWebProxy> 인터페이스가 포함됩니다. **Proxy** 속성은 프로토콜이 프록시 설정된 요청을 지원할 경우에만 유효합니다. 프로토콜에 필요한 경우 기본 프록시를 설정해야 합니다.  
  
 회사 방화벽을 사용하는 것과 같은 일부 환경에서는 프로토콜에 프록시를 사용해야 할 수 있습니다. 이 경우 **IWebProxy** 인터페이스를 구현하여 프로토콜에 작동하는 프록시 클래스를 만들어야 합니다.  
  
## <a name="requesturi-property"></a>RequestUri 속성  
 <xref:System.Net.WebRequest.RequestUri%2A> 속성에는 **WebRequest.Create** 메서드에 전달된 URI가 포함됩니다. 이 속성은 읽기 전용이고 **WebRequest**가 생성된 후에는 변경할 수 없습니다. 프로토콜이 리디렉션을 지원할 경우 다른 URI로 식별되는 리소스에서 응답이 나올 수 있습니다. 응답한 URI에 대한 액세스 권한을 제공해야 할 경우 해당 URI가 포함된 추가 속성을 제공해야 합니다.  
  
## <a name="timeout-property"></a>제한 시간 속성  
 <xref:System.Net.WebRequest.Timeout%2A> 속성에는 요청 시간이 초과되고 예외가 throw되기 전에 대기할 시간 길이(밀리초)가 포함됩니다. **Timeout**은 <xref:System.Net.WebRequest.GetResponse%2A> 메서드를 통해 생성된 비동기 요청에만 적용되고, 비동기 요청은 <xref:System.Net.WebRequest.Abort%2A> 메서드를 사용하여 보류 중인 요청을 취소해야 합니다.  
  
 **Timeout** 속성 설정은 프로토콜별 클래스가 시간 제한 프로세스를 구현할 경우에만 유효합니다.  
  
## <a name="abort-method"></a>Abort 메서드  
 <xref:System.Net.WebRequest.Abort%2A> 메서드는 서버에 대한 보류 중인 비동기 요청을 취소합니다. 요청이 취소된 후 **GetResponse**, **BeginGetResponse**, **EndGetResponse**, **GetRequestStream**, **BeginGetRequestStream** 또는 **EndGetRequestStream**을 호출하면 <xref:System.Net.WebException>이 throw되고 <xref:System.Net.WebException.Status%2A> 속성이 <xref:System.Net.WebExceptionStatus>로 설정됩니다.  
  
## <a name="begingetrequeststream-and-endgetrequeststream-methods"></a>BeginGetRequestStream 및 EndGetRequestStream 메서드  
 <xref:System.Net.WebRequest.BeginGetRequestStream%2A> 메서드는 데이터를 서버에 업로드하는 데 사용되는 스트림에 대한 비동기 요청을 시작합니다. <xref:System.Net.WebRequest.EndGetRequestStream%2A> 메서드는 비동기 요청을 완료하고 요청된 스트림을 반환합니다. 이러한 메서드는 표준 .NET Framework 비동기 패턴을 사용하여 **GetRequestStream** 메서드를 구현합니다.  
  
## <a name="begingetresponse-and-endgetresponse-methods"></a>BeginGetResponse 및 EndGetResponse 메서드  
 <xref:System.Net.WebRequest.BeginGetResponse%2A> 메서드는 서버에 대한 비동기 요청을 시작합니다. <xref:System.Net.WebRequest.EndGetResponse%2A> 메서드는 비동기 요청을 완료하고 요청된 응답을 반환합니다. 이러한 메서드는 표준 .NET Framework 비동기 패턴을 사용하여 **GetResponse** 메서드를 구현합니다.  
  
## <a name="getrequeststream-method"></a>GetRequestStream 메서드  
 <xref:System.Net.WebRequest.GetRequestStream%2A> 메서드는 요청된 서버에 데이터를 쓰는 데 사용되는 스트림을 반환합니다. 반환된 스트림은 검색되지 않는 쓰기 전용 스트림이어야 하고 서버에 기록되는 단방향 데이터 스트림으로 사용됩니다. 스트림은 <xref:System.IO.Stream.CanRead%2A> 및 <xref:System.IO.Stream.CanSeek%2A> 속성에 대해 false를 반환하고 <xref:System.IO.Stream.CanWrite%2A> 속성에 대해 true를 반환합니다.  
  
 **GetRequestStream** 메서드는 대개 서버에 대한 연결을 열고 스트림을 반환하기 전에 데이터가 서버에 전송되고 있음을 나타내는 헤더 정보를 보냅니다. **GetRequestStream**은 요청을 시작하므로 **GetRequestStream**을 호출한 후에는 일반적으로 **Header** 속성이나 **ContentLength** 속성을 설정할 수 없습니다.  
  
## <a name="getresponse-method"></a>GetResponse 메서드  
 <xref:System.Net.WebRequest.GetResponse%2A> 메서드는 서버의 응답을 나타내는 <xref:System.Net.WebResponse> 클래스의 프로토콜별 하위 항목을 반환합니다. 요청이 이미 **GetRequestStream** 메서드를 통해 시작된 경우가 아니면 **GetResponse** 메서드는 **RequestUri**로 식별되는 리소스 연결을 만들고, 생성되는 요청의 형식을 나타내는 헤더 정보를 보내고 나서, 리소스의 응답을 받습니다.  
  
 **GetResponse** 메서드가 호출된 후에는 모든 속성을 읽기 전용으로 간주해야 합니다. **WebRequest** 인스턴스는 일회용이고, 또 다른 요청을 만들려면 새 **WebRequest**를 만들어야 합니다.  
  
 **GetResponse** 메서드는 들어오는 응답을 포함할 적절한 **WebResponse** 하위 항목을 만들어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Net.WebRequest>  
 <xref:System.Net.HttpWebRequest>  
 <xref:System.Net.FileWebRequest>  
 [플러그형 프로토콜 프로그래밍](../../../docs/framework/network-programming/programming-pluggable-protocols.md)  
 [WebResponse에서 파생](../../../docs/framework/network-programming/deriving-from-webresponse.md)
