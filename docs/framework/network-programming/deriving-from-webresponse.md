---
title: WebResponse에서 파생
ms.date: 03/30/2017
helpviewer_keywords:
- Deriving from WebResponse
ms.assetid: f11d4866-a199-4087-9306-a5a4c18b13db
ms.openlocfilehash: a065e04e6683279b4541d9a723ed9c7442dec9dc
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50088600"
---
# <a name="deriving-from-webresponse"></a>WebResponse에서 파생
<xref:System.Net.WebResponse> 클래스는 .NET Framework 플러그형 프로토콜 모델에 적합한 프로토콜별 응답을 만들기 위한 기본 메서드 및 속성을 제공하는 추상 기본 클래스입니다. <xref:System.Net.WebRequest> 클래스를 사용하여 리소스의 데이터를 요청하는 응용 프로그램은 **WebResponse**로 응답을 받습니다. 프로토콜별 **WebResponse** 하위 항목은 **WebResponse** 클래스의 추상 멤버를 구현해야 합니다.  
  
 연결된 **WebRequest** 클래스는 **WebResponse** 하위 항목을 만들어야 합니다. 예를 들어 <xref:System.Net.HttpWebResponse> 인스턴스는 <xref:System.Net.HttpWebRequest.GetResponse%2A?displayProperty=nameWithType> 또는 <xref:System.Net.HttpWebRequest.EndGetResponse%2A?displayProperty=nameWithType>를 호출한 결과로만 만들어집니다. 각 **WebResponse**는 리소스에 대한 요청 결과를 포함하고 다시 사용되지 않습니다.  
  
## <a name="contentlength-property"></a>ContentLength 속성  
 <xref:System.Net.WebResponse.ContentLength%2A> 속성은 <xref:System.Net.WebResponse.GetResponseStream%2A> 메서드에서 반환된 스트림에 사용 가능한 데이터 크기(바이트)를 나타냅니다. **ContentLength** 속성은 서버에서 반환된 헤더 또는 메타데이터 정보 크기(바이트)를 나타내지 않고, 요청된 리소스 자치의 데이터 크기(바이트)만 나타냅니다.  
  
## <a name="contenttype-property"></a>ContentType 속성  
 <xref:System.Net.WebResponse.ContentType%2A> 속성은 서버에서 보내는 콘텐츠 형식을 식별하기 위해 프로토콜을 통해 클라이언트에 보내야 하는 특수 정보를 제공합니다. 일반적으로 이것은 반환된 데이터의 MIME 콘텐츠 형식입니다.  
  
## <a name="headers-property"></a>Headers 속성  
 <xref:System.Net.WebResponse.Headers%2A> 속성에는 응답과 연결된 메타데이터 이름/값 쌍의 임의 컬렉션이 포함됩니다. 이름/값 쌍으로 표시될 수 있는 프로토콜에 필요한 모든 메타데이터가 **Headers** 속성에 포함될 수 있습니다.  
  
 헤더 메타데이터를 사용하기 위해 **Headers** 속성을 사용할 필요가 없습니다. 프로토콜별 메타데이터는 속성으로 노출됩니다. 예를 들어 <xref:System.Net.HttpWebResponse.LastModified%2A?displayProperty=nameWithType> 속성은 **Last-Modified** HTTP 헤더를 노출합니다. 헤더 메타데이터를 속성으로 노출할 경우 **Headers** 속성을 사용하여 동일한 속성을 설정하도록 허용하면 안 됩니다.  
  
## <a name="responseuri-property"></a>ResponseUri 속성  
 <xref:System.Net.WebResponse.ResponseUri%2A> 속성에는 실제로 응답을 제공하는 리소스의 URI가 포함됩니다. 리디렉션을 지원하지 않는 프로토콜이 경우 **ResponseUri**는 응답을 만든 **WebRequest**의 <xref:System.Net.WebRequest.RequestUri%2A> 속성과 같습니다. 프로토콜이 요청 리디렉션을 지원할 경우 **ResponseUri**에는 응답의 URI가 포함됩니다.  
  
## <a name="close-method"></a>Close 메서드  
 <xref:System.Net.WebResponse.Close%2A> 메서드는 요청 및 응답을 통해 생성된 모든 연결을 닫고 응답에서 사용된 리소스를 정리합니다. **Close** 메서드는 응답에서 사용된 모든 스트림 인스턴스를 닫지만 응답 스트림이 이전에 <xref:System.IO.Stream.Close%2A?displayProperty=nameWithType> 메서드 호출을 통해 닫힌 경우 예외를 throw하지 않습니다.  
  
## <a name="getresponsestream-method"></a>GetResponseStream 메서드  
 <xref:System.Net.WebResponse.GetResponseStream%2A> 메서드는 요청된 리소스의 응답이 포함된 스트림을 반환합니다. 응답 스트림에는 리소스에서 반환된 데이터만 포함되고 응답에 포함된 모든 헤더 또는 메타데이터는 프로토콜별 속성 또는 **Headers** 속성을 통해 응답에서 삭제되고 응용 프로그램에 노출되어야 합니다.  
  
 **GetResponseStream** 메서드에서 반환되는 스트림 인스턴스는 응용 프로그램이 소유하고 **WebResponse**를 닫지 않고도 닫을 수 있습니다. 규칙에 따라 **WebResponse.Close** 메서드를 호출하면 **GetResponse**에서 반환된 스트림도 닫힙니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Net.WebResponse>  
 <xref:System.Net.HttpWebResponse>  
 <xref:System.Net.FileWebResponse>  
 [플러그형 프로토콜 프로그래밍](../../../docs/framework/network-programming/programming-pluggable-protocols.md)  
 [WebRequest에서 파생](../../../docs/framework/network-programming/deriving-from-webrequest.md)
