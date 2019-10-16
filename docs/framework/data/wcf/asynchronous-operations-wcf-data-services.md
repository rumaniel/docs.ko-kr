---
title: 비동기 작업(WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, asynchronous operations
- asynchronous operations [WCF Data Services]
- WCF Data Services, client library
ms.assetid: 679644c7-e3fc-422c-b14a-b44b683900d0
ms.openlocfilehash: bb62b9ad214e5e268c3905df486f5914437b36d3
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780524"
---
# <a name="asynchronous-operations-wcf-data-services"></a>비동기 작업(WCF Data Services)
웹 애플리케이션의 경우 내부 네트워크 내에서 실행되는 애플리케이션보다 클라이언트와 서버 간에 보다 긴 대기 시간을 허용해야 합니다. 애플리케이션의 성능과 사용자 환경을 최적화하려면 웹을 통해 <xref:System.Data.Services.Client.DataServiceContext> 서버에 액세스할 때 <xref:System.Data.Services.Client.DataServiceQuery%601> 및 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 클래스의 비동기 메서드를 사용하는 것이 좋습니다.  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 서버가 HTTP 요청을 비동기적으로 처리하지만 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 클라이언트 라이브러리의 일부 메서드는 동기적이며 실행을 계속하기 전에 전체 요청-응답 교환이 완료될 때까지 기다립니다. [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 클라이언트 라이브러리의 비동기 메서드는 이 교환이 완료될 때까지 기다리지 않으며 그 동안에 애플리케이션에서 사용자 인터페이스의 응답을 유지할 수 있도록 합니다.  
  
 <xref:System.Data.Services.Client.DataServiceContext> 및<xref:System.Data.Services.Client.DataServiceQuery%601> 클래스에서 각각 *Begin* 및 *End* 로 시작 하는 메서드 쌍을 사용 하 여 비동기 작업을 수행할 수 있습니다. *Begin* 메서드는 작업이 완료 될 때 서비스에서 호출 하는 대리자를 등록 합니다. *End* 메서드는 완료 된 작업의 콜백을 처리 하도록 등록 된 대리자에서 호출 해야 합니다. *End* 메서드를 호출 하 여 비동기 작업을 완료 하는 경우 작업을 시작 하는 데 <xref:System.Data.Services.Client.DataServiceQuery%601> 사용한 <xref:System.Data.Services.Client.DataServiceContext> 것과 동일한 또는 인스턴스에서 작업을 수행 해야 합니다. 각 *Begin* 메서드는 상태 `state` 개체를 콜백에 전달할 수 있는 매개 변수를 사용 합니다. 이 상태 개체는 콜백과 함께 제공 <xref:System.IAsyncResult> 된에서 검색 되 고 해당 *End* 메서드를 호출 하 여 비동기 작업을 완료 하는 데 사용 됩니다. 예를 들어, <xref:System.Data.Services.Client.DataServiceQuery%601> 인스턴스의 `state` 메서드를 호출할 때 이 인스턴스를 <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> 매개 변수로 제공하면 동일한 <xref:System.Data.Services.Client.DataServiceQuery%601> 인스턴스가 <xref:System.IAsyncResult>에 의해 반환됩니다. 이 <xref:System.Data.Services.Client.DataServiceQuery%601> 인스턴스는 <xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A> 메서드를 호출하여 쿼리 작업을 완료하는 데 사용됩니다. 자세한 내용은 [방법: 비동기 데이터 서비스 쿼리](how-to-execute-asynchronous-data-service-queries-wcf-data-services.md)를 실행 합니다.  
  
> [!NOTE]
> Silverlight용 .NET Framework에서 제공되는 클라이언트 라이브러리는 비동기 작업만 지원합니다. 자세한 내용은 [WCF Data Services (Silverlight)](https://go.microsoft.com/fwlink/?LinkID=143149)를 참조 하세요.  
  
 .NET Framework 클라이언트 라이브러리는 다음 비동기 작업을 지원합니다.  
  
|연산|메서드|  
|---------------|-------------|  
|<xref:System.Data.Services.Client.DataServiceQuery%601> 실행|-   <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A><br />-   <xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A>|  
|<xref:System.Data.Services.Client.DataServiceContext>에서 쿼리 실행|-   <xref:System.Data.Services.Client.DataServiceContext.BeginExecute%2A><br />-   <xref:System.Data.Services.Client.DataServiceContext.EndExecute%2A>|  
|<xref:System.Data.Services.Client.DataServiceContext>에서 일괄 처리 쿼리 실행|-   <xref:System.Data.Services.Client.DataServiceContext.BeginExecuteBatch%2A><br />-   <xref:System.Data.Services.Client.DataServiceContext.EndExecuteBatch%2A>|  
|<xref:System.Data.Services.Client.DataServiceContext>에 관련 엔터티 로드|-   <xref:System.Data.Services.Client.DataServiceContext.BeginLoadProperty%2A><br />-   <xref:System.Data.Services.Client.DataServiceContext.EndLoadProperty%2A>|  
|<xref:System.Data.Services.Client.DataServiceContext>에 개체 변경 내용 저장|-   <xref:System.Data.Services.Client.DataServiceContext.BeginSaveChanges%2A><br />-   <xref:System.Data.Services.Client.DataServiceContext.EndSaveChanges%2A>|  
  
## <a name="threading-considerations-for-asynchronous-operations"></a>비동기 작업에 대한 스레딩 고려 사항  
 다중 스레드 응용 프로그램에서 비동기 작업의 콜백으로 등록 된 대리자는 *Begin* 메서드를 호출 하는 데 사용 된 것과 동일한 스레드에서 호출 하지 않아도 됩니다 .이 대리자는 초기 요청을 만듭니다. 특정 스레드에서 콜백을 호출 해야 하는 응용 프로그램에서는 응답을 처리 하는 *End* 메서드 실행을 명시적으로 원하는 스레드에 마샬링해야 합니다. 예를 들어, WPF(Windows Presentation Foundation) 기반 애플리케이션과 Silverlight 기반 애플리케이션에서는 <xref:System.Windows.Threading.Dispatcher.BeginInvoke%2A> 개체의 <xref:System.Windows.Threading.Dispatcher> 메서드를 사용하여 응답을 UI 스레드로 다시 마샬링해야 합니다. 자세한 내용은 [데이터 서비스 쿼리 (WCF Data Services/Silverlight)](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc903932(v=vs.95))를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [WCF Data Services 클라이언트 라이브러리](wcf-data-services-client-library.md)
