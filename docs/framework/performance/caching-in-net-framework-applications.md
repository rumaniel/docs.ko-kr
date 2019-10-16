---
title: .NET Framework 애플리케이션에서 캐싱
ms.date: 03/30/2017
helpviewer_keywords:
- ASP.NET caching
- caching [.NET Framework]
- caching [ASP.NET]
ms.assetid: c4b47ee0-4b82-4124-9bce-818088385e34
ms.openlocfilehash: 704efed96c18f23d34d8a583d3121fc08b9e22e1
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046781"
---
# <a name="caching-in-net-framework-applications"></a>.NET Framework 애플리케이션에서 캐싱
캐싱을 사용하면 빠른 액세스를 위해 데이터를 메모리에 저장할 수 있습니다. 데이터에 다시 액세스할 때 애플리케이션은 원래 소스에서 검색하는 대신 캐시에서 데이터를 가져올 수 있습니다. 이 경우 성능과 확장성이 향상됩니다. 또한 캐싱을 사용하면 데이터 소스를 일시적으로 사용할 수 없는 경우에도 데이터를 사용할 수 있습니다.  
  
 .NET Framework에서는 ASP.NET을 포함하여 Windows 클라이언트와 서버 애플리케이션 둘 다의 성능과 확장성을 개선하는 데 사용할 수 있는 캐싱 기능을 제공합니다.  
  
> [!NOTE]
> .NET Framework 3.5 및 이전 버전에서 ASP.NET는 <xref:System.Web.Caching> 네임 스페이스에 메모리 내 캐시 구현을 제공 했습니다. 이전 버전의 .NET Framework에서 캐싱은 <xref:System.Web> 네임 스페이스 에서만 사용할 수 있으므로 ASP.NET 클래스에 대 한 종속성이 필요 했습니다. .NET Framework 4에서는 <xref:System.Runtime.Caching> 네임스페이스에 웹 애플리케이션과 비웹 애플리케이션 둘 다에 사용 가능한 API가 포함되어 있습니다.  
  
## <a name="caching-data"></a>데이터 캐싱  
 <xref:System.Runtime.Caching> 네임스페이스의 클래스를 사용하여 정보를 캐시할 수 있습니다. 이 네임스페이스의 캐싱 클래스는 다음과 같은 기능을 제공합니다.  
  
- 사용자 지정 캐시 구현을 만들기 위한 기초를 제공하는 추상 형식  
  
- 구체적인 메모리 내 개체 캐시 구현  
  
 추상 기본 캐싱 클래스(<xref:System.Runtime.Caching.ObjectCache>)는 다음과 같은 캐싱 작업을 정의합니다.  
  
- 캐시 항목 만들기 및 관리  
  
- 만료 및 제거 정보 지정  
  
- 캐시 항목의 변경 내용에 대한 응답으로 발생하는 이벤트 트리거  
  
 <xref:System.Runtime.Caching.MemoryCache> 클래스는 <xref:System.Runtime.Caching.ObjectCache> 클래스의 메모리 내 개체 캐시 구현입니다. 대부분의 캐싱 작업에 <xref:System.Runtime.Caching.MemoryCache> 클래스를 사용할 수 있습니다.  
  
> [!NOTE]
> <xref:System.Runtime.Caching.MemoryCache> 클래스는 <xref:System.Web.Caching> 네임스페이스에 정의된 ASP.NET 캐시 개체에서 모델링됩니다. 따라서 내부 캐싱 논리가 이전 버전의 ASP.NET에서 제공된 논리와 유사합니다.  
  
 을 사용 하 여 WPF 응용 프로그램 [에서 캐시 하는 방법에 대 한 예제는 연습: WPF 응용 프로그램](../wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application.md)에서 응용 프로그램 데이터 캐싱  
  
## <a name="caching-in-aspnet-applications"></a>ASP.NET 애플리케이션의 캐싱  
 <xref:System.Runtime.Caching> 네임스페이스의 캐싱 클래스는 ASP.NET에서 데이터를 캐시하기 위한 기능을 제공합니다.  
  
> [!NOTE]
> 응용 프로그램이 .NET Framework 3.5 이전 버전을 대상으로 하는 경우 <xref:System.Web.Caching> 네임 스페이스에 정의 된 캐싱 클래스를 사용 해야 합니다. 자세한 내용은 [ASP.NET 캐싱 개요](https://docs.microsoft.com/previous-versions/aspnet/ms178597(v=vs.100))를 참조하세요.  
  
> [!NOTE]
> 새 애플리케이션을 개발하는 경우 <xref:System.Runtime.Caching.MemoryCache> 클래스를 사용하는 것이 좋습니다. <xref:System.Runtime.Caching> 네임스페이스에 제공된 API는 <xref:System.Web.Caching.Cache> 네임스페이스에 제공된 API와 비슷합니다. 따라서 이전 버전의 ASP.NET에서 캐싱을 사용한 경우 API가 익숙할 것입니다. ASP.NET 응용 프로그램에서 캐싱을 사용 하는 방법에 대 한 예제 [를 보려면 연습: ASP.NET](https://docs.microsoft.com/previous-versions/ff477235(v=vs.100))에서 응용 프로그램 데이터를 캐시 합니다.  
  
### <a name="output-caching"></a>출력 캐싱  
 애플리케이션 데이터를 수동으로 캐시하려면 ASP.NET의 <xref:System.Runtime.Caching.MemoryCache> 클래스를 사용할 수 있습니다. ASP.NET은 페이지, 컨트롤 및 HTTP 응답의 생성된 출력을 메모리에 저장하는 출력 캐싱도 지원합니다. ASP.NET 웹 페이지에서 선언적으로 또는 Web.config 파일의 설정을 사용하여 출력 캐싱을 구성할 수 있습니다. 자세한 내용은 [caching 요소에 대한 outputCache 요소(ASP.NET 설정 스키마)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms228124(v=vs.100))를 참조하세요.  
  
 ASP.NET에서는 사용자 지정 출력 캐시 공급자를 만들어 출력 캐싱을 확장할 수 있습니다. 사용자 지정 공급자를 사용하면 디스크, 클라우드 저장소, 분산된 캐시 엔진 등의 다른 저장소 디바이스를 사용하여 캐시된 콘텐츠를 저장할 수 있습니다. 사용자 지정 출력 캐시 공급자를 만들려면 <xref:System.Web.Caching.OutputCacheProvider> 클래스에서 파생되는 클래스를 만들고 사용자 지정 출력 캐시 공급자를 사용하도록 애플리케이션을 구성합니다.  
  
## <a name="caching-in-wcf-rest-services"></a>WCF REST 서비스의 캐싱  
 WCF REST 서비스의 경우 .NET Framework를 통해 ASP.NET에서 사용 가능한 선언적 출력 캐싱을 활용할 수 있습니다. 이렇게 하면 WCF REST 서비스 작업의 응답을 캐시할 수 있습니다. 사용자가 캐시용으로 구성된 서비스에 HTTP GET 요청을 보내면 ASP.NET이 캐시된 응답을 다시 보내고 서비스 메서드가 호출되지 않습니다. 캐시가 만료된 후 다음에 사용자가 HTTP GET 요청을 보낼 때 서비스 메서드가 호출되고 응답이 다시 캐시됩니다.  
  
 .NET Framework를 사용하면 조건부 HTTP GET 캐싱을 구현할 수도 있습니다. REST 시나리오에서 조건부 HTTP GET 요청은 [HTTP 사양](https://go.microsoft.com/fwlink/?LinkId=165800)에 설명된 것처럼 지능적인 HTTP 캐싱을 구현하기 위해 서비스에서 자주 사용됩니다. 자세한 내용은 [WCF 웹 HTTP 서비스에 대한 캐싱 지원](https://go.microsoft.com/fwlink/?LinkId=184598)을 참조하세요.  
  
## <a name="extending-caching-in-the-net-framework"></a>.NET Framework의 캐싱 기능 확장  
 .NET Framework의 캐싱 기능은 확장 가능하도록 설계되었습니다. <xref:System.Runtime.Caching.ObjectCache> 클래스를 사용하여 사용자 지정 캐시 구현을 만들 수 있습니다. 이 클래스는 Windows Forms, WPF(Windows Presentation Foundation), WCF(Windows Communications Foundation) 등 관리되는 모든 애플리케이션에서 사용할 수 있는 멤버를 제공합니다. 다른 스토리지 메커니즘을 사용하는 캐시 클래스를 만들기 위해 또는 캐시 작업을 보다 세부적으로 제어하려는 경우 이 작업을 수행하는 것이 좋습니다.  
  
 캐싱을 확장하려면 다음 작업을 수행할 수 있습니다.  
  
- <xref:System.Runtime.Caching.ObjectCache> 클래스에서 파생되는 사용자 지정 클래스를 만든 다음 파생 클래스에 사용자 지정 캐시 구현을 제공합니다.  
  
- <xref:System.Runtime.Caching.MemoryCache> 클래스에서 파생되는 클래스를 만들고 파생 클래스를 사용자 지정하거나 확장합니다. 이 작업을 수행하는 방법의 예제는 [ASP.NET 애플리케이션에서 여러 캐시 개체를 사용하여 애플리케이션 데이터 캐시](https://blogs.msdn.microsoft.com/aspnetue/2010/03/22/caching-application-data-by-using-multiple-cache-objects-in-an-asp-net-application/)를 참조하세요.  
  
- <xref:System.Web.Caching.OutputCacheProvider> 클래스에서 파생되는 클래스를 만들고 사용자 지정 출력 캐시 공급자를 사용하도록 응용 프로그램을 구성합니다.  
  
 자세한 내용은 Scott Guthrie 블로그의 [Extensible Output Caching with ASP.NET 4 (VS 2010 and .NET 4.0 Series)](https://go.microsoft.com/fwlink/?LinkId=185772)(ASP.NET 4(VS 2010 및 .NET 4.0 시리즈)에서 확장 가능한 출력 캐싱) 항목을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Caching.ObjectCache>
- <xref:System.Runtime.Caching.MemoryCache>
- [연습: WPF 응용 프로그램에서 응용 프로그램 데이터 캐싱](../wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application.md)
- [연습: ASP.NET에서 응용 프로그램 데이터 캐싱](https://docs.microsoft.com/previous-versions/ff477235(v=vs.100))
