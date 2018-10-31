---
title: 인터넷 요청 만들기
ms.date: 03/30/2017
helpviewer_keywords:
- WebRequest class, sending and receiving data
- Networking
- HttpWebResponse class, sending and receiving data
- requesting data from Internet, creating requests
- Network Resources
- Internet, requesting data
- data requests, creating requests
ms.assetid: faab683e-3f1e-4eee-b5e9-59f7245033d5
ms.openlocfilehash: ff346c5b4241f7ac037088adbe068bab2232d12f
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50190686"
---
# <a name="creating-internet-requests"></a>인터넷 요청 만들기
응용 프로그램은 <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType> 메서드를 통해 <xref:System.Net.WebRequest> 인스턴스를 만듭니다. 이것은 전달된 URI 구성표에 따라 **WebRequest**에서 파생된 클래스를 만드는 정적 메서드입니다.  
  
## <a name="web-file-and-ftp-requests"></a>웹, 파일 및 FTP 요청  
 .NET Framework는 HTTP 및 HTTPS 요청을 처리하기 위해 **WebRequest**에서 파생된 <xref:System.Net.HttpWebRequest> 클래스를 제공합니다. 대부분의 경우 **WebRequest** 클래스는 요청을 만드는 데 필요한 모든 속성을 제공합니다. 그러나 필요한 경우 **WebRequest.Create** 메서드를 통해 생성된 **WebRequest** 개체를 **HttpWebRequest** 형식에 캐스팅하여 요청의 HTTP 관련 속성에 액세스할 수 있습니다. 마찬가지로 **HttpWebResponse** 개체는 HTTP 및 HTTPS 요청의 응답을 처리합니다. **HttpWebResponse** 개체의 HTTP 관련 속성에 액세스하려면 **WebResponse** 개체를 **HttpWebResponse** 형식에 캐스팅해야 합니다.  
  
 .NET Framework는 “file:” URI 구성표를 사용하는 리소스에 대한 요청을 처리하기 위해 <xref:System.Net.FileWebRequest> 및 <xref:System.Net.FileWebResponse> 클래스를 제공합니다. 마찬가지로 “ftp:” 구성표를 사용하는 리소스에 대한 요청을 처리하기 위해 <xref:System.Net.FtpWebRequest> 및 <xref:System.Net.FtpWebResponse> 클래스가 제공됩니다. 이러한 구성표를 사용하는 리소스에 대한 요청인 경우 **WebRequest.Create** 메서드를 사용하여 요청 생성에 사용할 개체를 가져올 수 있습니다.  
  
 다른 응용 프로그램 수준 프로토콜을 사용하는 요청을 처리하기 위해 **WebRequest** 및 **WebResponse**에서 파생된 프로토콜별 클래스를 구현해야 합니다. 자세한 내용은 [플러그형 프로토콜 프로그래밍](../../../docs/framework/network-programming/programming-pluggable-protocols.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [방법: WebRequest 클래스를 사용하여 데이터 요청](../../../docs/framework/network-programming/how-to-request-data-using-the-webrequest-class.md)  
 [데이터 요청](../../../docs/framework/network-programming/requesting-data.md)
