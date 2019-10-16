---
title: '방법: 비동기 데이터 서비스 쿼리 실행 (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, asynchronous operations
- asynchronous operations [WCF Data Services]
ms.assetid: 902a2dc1-d0e9-4b00-90a8-becc4cb1f6a7
ms.openlocfilehash: 14bfc138c5ece45184fb939f19aaf3d7e73e7294
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790576"
---
# <a name="how-to-execute-asynchronous-data-service-queries-wcf-data-services"></a>방법: 비동기 데이터 서비스 쿼리 실행 (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 클라이언트 라이브러리를 사용하면 쿼리를 실행하고 변경 내용을 저장하는 것과 같은 클라이언트-서버 작업을 비동기식으로 수행할 수 있습니다. 자세한 내용은 [비동기 작업](asynchronous-operations-wcf-data-services.md)합니다.  
  
> [!NOTE]
> 지정된 스레드에 대해 콜백을 호출해야 하는 애플리케이션에서는 <xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A> 메서드 실행을 명시적으로 마샬링해야 합니다. 자세한 내용은 [비동기 작업](asynchronous-operations-wcf-data-services.md)합니다.  
  
 이 항목의 예제에서는 Northwind 샘플 데이터 서비스 및 자동 생성된 클라이언트 데이터 서비스 클래스를 사용합니다. 이 서비스 및 클라이언트 데이터 클래스는 [WCF Data Services 빠른](quickstart-wcf-data-services.md)시작을 완료 하면 생성 됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> 메서드 호출을 통해 쿼리를 시작하여 비동기 쿼리를 실행하는 방법을 보여 줍니다. 인라인 대리자는 <xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A> 메서드를 호출하여 쿼리 결과를 표시합니다.  
  
 [!code-csharp[Astoria Northwind Client#ExecuteQueryAsync](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#executequeryasync)]
 [!code-vb[Astoria Northwind Client#ExecuteQueryAsync](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#executequeryasync)]  
  
## <a name="see-also"></a>참고자료

- [WCF Data Services 클라이언트 라이브러리](wcf-data-services-client-library.md)
