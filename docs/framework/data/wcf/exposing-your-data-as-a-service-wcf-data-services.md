---
title: 서비스로 데이터 노출(WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, configuring
- getting started, WCF Data Services
- WCF Data Services, getting started
ms.assetid: df0bbcee-f66f-4a88-abb4-4e73c8b9c908
ms.openlocfilehash: 1dc1f0ec12c50c4c97b141a34b468e3367ead75e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780306"
---
# <a name="expose-your-data-as-a-service-wcf-data-services"></a>데이터를 서비스로 제공 (WCF Data Services)

WCF Data Services는 Visual Studio와 통합 되므로 데이터를 피드로 노출 하는 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 서비스를 보다 쉽게 정의할 수 있습니다. OData 피드를 노출 하는 데이터 서비스를 만들려면 다음 기본 단계를 수행 해야 합니다.

1. **데이터 모델을 정의 합니다.** WCF Data Services는 [ADO.NET Entity Framework](../adonet/ef/index.md)기반으로 하는 데이터 모델을 기본적으로 지원 합니다. 자세한 내용은 [방법: ADO.NET Entity Framework 데이터 원본을](create-a-data-service-using-an-adonet-ef-data-wcf.md)사용 하 여 데이터 서비스를 만듭니다.

     또한 WCF Data Services는 <xref:System.Linq.IQueryable%601> 인터페이스의 인스턴스를 반환 하는 CLR (공용 언어 런타임) 개체를 기반으로 하는 데이터 모델을 지원 합니다. 따라서 .NET Framework의 목록, 배열 및 컬렉션을 기반으로 하는 데이터 서비스를 배포할 수 있습니다. 이러한 데이터 구조에 대해 만들기, 업데이트 및 삭제 작업을 수행하려면 <xref:System.Data.Services.IUpdatable> 인터페이스도 구현해야 합니다. 자세한 내용은 [방법: 리플렉션 공급자](create-a-data-service-using-rp-wcf-data-services.md)를 사용 하 여 데이터 서비스를 만듭니다.

     고급 시나리오를 위해 WCF Data Services에는 런타임에 바인딩된 데이터 형식을 기반으로 데이터 모델을 정의할 수 있는 공급자 집합이 포함 되어 있습니다. 자세한 내용은 [사용자 지정 데이터 서비스 공급자](custom-data-service-providers-wcf-data-services.md)를 참조 하세요.

2. **데이터 서비스를 만듭니다.** 가장 기본적인 데이터 서비스는 <xref:System.Data.Services.DataService%601> 클래스에서 상속하는 클래스를 엔터티 컨테이너의 네임스페이스로 정규화된 이름인 `T` 형식으로 노출합니다. 자세한 내용은 [Defining WCF Data Services](defining-wcf-data-services.md)의 개발 및 배포에 대한 정보를 제공합니다.

3. **데이터 서비스를 구성 합니다.** 기본적으로 WCF Data Services는 엔터티 컨테이너에 의해 노출 되는 리소스에 대 한 액세스를 사용 하지 않도록 설정 합니다. <xref:System.Data.Services.DataServiceConfiguration> 인터페이스를 사용 하면 리소스 및 서비스 작업에 대 한 액세스를 구성 하 고, 지원 되는 버전의 OData를 지정 하 고, 일괄 처리 동작 또는 반환할 수 있는 최대 엔터티 수와 같은 다른 서비스 전체 동작을 정의할 수 있습니다. 단일 응답으로 자세한 내용은 [데이터 서비스 구성](configuring-the-data-service-wcf-data-services.md)합니다.

Northwind 샘플 데이터베이스를 기반으로 하는 간단한 데이터 서비스를 만드는 방법에 대 한 예제는 [빠른](quickstart-wcf-data-services.md)시작을 참조 하세요.

## <a name="see-also"></a>참고자료

- [시작](getting-started-with-wcf-data-services.md)
- [개요](wcf-data-services-overview.md)
