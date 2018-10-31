---
title: 연결 관리
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Internet, connections
- HTTP, classes for connecting
- requesting data from Internet, connections
- sending data, connections
- receiving data, connections
- ServicePoint class, about ServicePoint class
- response to Internet request, connections
- connections [.NET Framework], classes
- network resources, connections
- downloading Internet resources, connections
- ServicePointManager class, about ServicePointManager class
ms.assetid: 9b3d3de7-189f-4f7d-81ae-9c29c441aaaa
ms.openlocfilehash: 4fd7d01a3592c76fc1bb4ff8afe280c50cdf9f12
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50181305"
---
# <a name="managing-connections"></a>연결 관리
HTTP를 사용하여 데이터 리소스에 연결하는 응용 프로그램은 .NET Framework의 <xref:System.Net.ServicePoint> 및 <xref:System.Net.ServicePointManager> 클래스를 사용하여 인터넷에 대한 연결을 관리하고 최적의 규모 및 성능을 달성하도록 지원합니다.  
  
 **ServicePoint** 클래스는 응용 프로그램이 인터넷 리소스에 액세스하기 위해 연결할 수 있는 엔드포인트를 제공합니다. 각 **ServicePoint**에는 성능을 향상시키기 위해 연결 간 최적화 정보를 공유하여 인터넷 서버와의 연결을 최적화시킬 수 있는 정보가 들어 있습니다.  
  
 각 **ServicePoint**는 URI(Uniform Resource Identifier)로 식별되며 URI의 구성표 식별자 및 호스트 조각에 따라 분류됩니다. 예를 들어 동일한 **ServicePoint** 인스턴스에는 동일한 구성표 식별자(http) 및 호스트 조각(`www.contoso.com`)이 있으므로 이 인스턴스에서는 URI(`http://www.contoso.com/index.htm` 및 `http://www.contoso.com/news.htm?date=today`)에 요청을 제공합니다. 응용 프로그램이 이미 `www.contoso.com` 서버에 영구적으로 연결되어 있는 경우 해당 연결을 사용하여 두 요청을 모두 검색하므로 두 연결을 만들 필요가 없습니다.  
  
 **ServicePointManager**는 **ServicePoint** 인스턴스의 생성과 소멸을 관리하는 정적 클래스입니다. 응용 프로그램에서 기존 **ServicePoint** 인스턴스의 컬렉션에 없는 인터넷 리소스를 요청하면 **ServicePointManager**에서 **ServicePoint**를 만듭니다. **ServicePoint** 인스턴스는 최대 유휴 시간이 초과되거나 기존 **ServicePoint** 인스턴스의 수가 응용 프로그램의 **ServicePoint** 인스턴스 최대 수를 초과할 때 소멸됩니다. **ServicePointManager**에서 <xref:System.Net.ServicePointManager.MaxServicePointIdleTime%2A> 및 <xref:System.Net.ServicePointManager.MaxServicePoints%2A> 속성을 설정하여 유휴 시간의 기본 최대값과 **ServicePoint** 인스턴스의 최대 수를 모두 제어할 수 있습니다.  
  
 클라이언트와 서버 사이의 연결 수는 응용 프로그램 처리량에 상당한 영향을 미칠 수 있습니다. 기본적으로 <xref:System.Net.HttpWebRequest> 클래스를 사용하는 응용 프로그램에서는 지정된 서버에 대한 영구적 연결을 최대 2개 사용하지만 응용 프로그램별로 최대 연결 수를 설정할 수 있습니다.  
  
> [!NOTE]
>  HTTP/1.1 사양에 따르면 응용 프로그램으로부터의 연결은 서버당 두 개의 연결로 제한됩니다.  
  
 최적의 연결 수는 응용 프로그램이 실행되는 실제 조건에 따라 달라집니다. 응용 프로그램에 사용 가능한 연결 수를 늘려도 응용 프로그램 성능에 영향을 미치지 않을 수 있습니다. 연결이 추가되는 경우 미치는 영향을 판별하려면 연결 수를 변경하면서 성능 테스트를 실행합니다. 다음 코드 샘플에 표시된 대로 응용 프로그램 초기화 시 **ServicePointManager** 클래스의 정적 <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A> 속성을 변경하여 해당 응용 프로그램에서 사용하는 연결 수를 변경할 수 있습니다.  
  
```csharp  
// Set the maximum number of connections per server to 4.  
ServicePointManager.DefaultConnectionLimit = 4;  
```  
  
```vb  
' Set the maximum number of connections per server to 4.  
ServicePointManager.DefaultConnectionLimit = 4  
```  
  
 **ServicePointManager.DefaultConnectionLimit** 속성을 변경해도 이전에 초기화된 **ServicePoint** 인스턴스에는 영향을 미치지 않습니다. 다음 코드에서는 `http://www.contoso.com` 서버의 기존 **ServicePoint**에 대한 연결 한계를 `newLimit`에 저장된 값으로 변경합니다.  
  
```csharp  
Uri uri = new Uri("http://www.contoso.com/");  
ServicePoint sp = ServicePointManager.FindServicePoint(uri);  
sp.ConnectionLimit = newLimit;  
```  
  
```vb  
Dim uri As New Uri("http://www.contoso.com/")  
Dim sp As ServicePoint = ServicePointManager.FindServicePoint(uri)  
sp.ConnectionLimit = newLimit  
```  
  
## <a name="see-also"></a>참고 항목  
 [연결 그룹화](../../../docs/framework/network-programming/connection-grouping.md)  
 [응용 프로그램 프로토콜 사용](../../../docs/framework/network-programming/using-application-protocols.md)
