---
title: WCF Data Services 클라이언트 라이브러리
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, client library
- DataServiceQuery class, about DataServiceQuery class
- DataServiceContext class, about DataServiceContext class
ms.assetid: 21075e50-8917-413e-a8ea-35a0f6e65aa5
ms.openlocfilehash: 545442b0086361c8ce8c0482801afc10b1fee96e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779675"
---
# <a name="wcf-data-services-client-library"></a>WCF Data Services 클라이언트 라이브러리
HTTP 요청을 보내고 데이터 서비스에서 반환하는 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 피드를 처리할 수 있는 애플리케이션은 모두 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 기반 데이터 서비스와 상호 작용할 수 있습니다. 이 상호 운용성을 통해 광범위한 웹 사용 애플리케이션에서 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 기반 서비스에 액세스할 수 있습니다. [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]에는 .NET Framework 또는 Silverlight 기반 응용 프로그램에서 피드를 사용할 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 때 보다 다양 한 프로그래밍 환경을 제공 하는 클라이언트 라이브러리가 포함 되어 있습니다.  
  
 클라이언트 라이브러리의 두 가지 주요 클래스는 <xref:System.Data.Services.Client.DataServiceContext> 클래스와 <xref:System.Data.Services.Client.DataServiceQuery%601> 클래스입니다. <xref:System.Data.Services.Client.DataServiceContext> 클래스는 지정한 데이터 서비스에 대해 지원되는 작업을 캡슐화합니다. [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 서비스는 상태 비저장 특성을 갖지만 컨텍스트는 그렇지 않습니다. 따라서 변경 관리 등의 기능 <xref:System.Data.Services.Client.DataServiceContext> 을 지원 하기 위해 클래스를 사용 하 여 데이터 서비스와의 상호 작용 간에 클라이언트의 상태를 유지할 수 있습니다. 또한 이 클래스는 ID를 관리하고 변경 내용을 추적합니다. <xref:System.Data.Services.Client.DataServiceQuery%601> 클래스는 특정 엔터티 집합에 대한 쿼리를 나타냅니다.  
  
 이 단원에서는 클라이언트 라이브러리를 사용하여 .NET Framework 클라이언트 애플리케이션에서 데이터에 액세스하고 변경하는 방법에 대해 설명합니다. Silverlight 기반 응용 프로그램에서 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 클라이언트 라이브러리를 사용 하는 방법에 대 한 자세한 내용은 [WCF Data Services (silverlight)](https://go.microsoft.com/fwlink/?LinkId=186016)를 참조 하세요. 다른 종류의 응용 프로그램에서 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 피드를 사용할 수 있는 다른 클라이언트 라이브러리를 사용할 수 있습니다. 자세한 내용은 [ODATA SDK](https://go.microsoft.com/fwlink/?LinkID=185796)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [데이터 서비스 클라이언트 라이브러리 생성](generating-the-data-service-client-library-wcf-data-services.md)  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 피드를 기반으로 하는 클라이언트 데이터 서비스 클래스 및 클라이언트 라이브러리를 생성 하는 방법에 대해 설명 합니다.  
  
 [데이터 서비스 쿼리](querying-the-data-service-wcf-data-services.md)  
 클라이언트 라이브러리를 사용하여 .NET Framework 기반 애플리케이션에서 데이터 서비스를 쿼리하는 방법에 대해 설명합니다.  
  
 [지연 콘텐츠 로드](loading-deferred-content-wcf-data-services.md)  
 초기 쿼리 응답에 포함되지 않은 추가 콘텐츠를 로드하는 방법에 대해 설명합니다.  
  
 [데이터 서비스 업데이트](updating-the-data-service-wcf-data-services.md)  
 클라이언트 라이브러리를 사용하여 엔터티와 관계를 만들고 수정 및 삭제하는 방법에 대해 설명합니다.  
  
 [비동기 작업](asynchronous-operations-wcf-data-services.md)  
 비동기 방식으로 데이터 서비스와 작업할 수 있도록 클라이언트 라이브러리에서 제공하는 기능에 대해 설명합니다.  
  
 [일괄 처리 작업](batching-operations-wcf-data-services.md)  
 클라이언트 라이브러리를 사용하여 여러 요청을 데이터 서비스에 단일 일괄 처리로 보내는 방법에 대해 설명합니다.  
  
 [컨트롤에 데이터 바인딩](binding-data-to-controls-wcf-data-services.md)  
 데이터 서비스에서 반환 된 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 피드에 컨트롤을 바인딩하는 방법에 대해 설명 합니다.  
  
 [서비스 작업 호출](calling-service-operations-wcf-data-services.md)  
 클라이언트 라이브러리를 사용하여 서비스 작업을 호출하는 방법에 대해 설명합니다.  
  
 [데이터 서비스 컨텍스트 관리](managing-the-data-service-context-wcf-data-services.md)  
 클라이언트 라이브러리의 동작을 관리하는 옵션에 대해 설명합니다.  
  
 [이진 데이터 작업](working-with-binary-data-wcf-data-services.md)  
 데이터 서비스에서 데이터 스트림으로 반환하는 이진 데이터에 액세스하고 해당 데이터를 변경하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [WCF Data Services 정의](defining-wcf-data-services.md)
- [시작](getting-started-with-wcf-data-services.md)
