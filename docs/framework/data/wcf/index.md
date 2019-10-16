---
title: WCF Data Services 4.5
ms.date: 03/30/2017
helpviewer_keywords:
- Astoria
- WCF Data Services, getting started
ms.assetid: 73d2bec3-7c92-4110-b905-11bb0462357a
ms.openlocfilehash: 017fe2177cf824d461b4c51ea805f75b6ddbe064
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779997"
---
# <a name="wcf-data-services-45"></a>WCF Data Services 4.5

WCF Data Services (이전의 "ADO.NET Data Services")는 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] [representational 상태의 의미 체계를 사용 하 여 웹 또는 인트라넷을 통해 데이터를 노출 하 고 사용 하기 위해을 사용 하는 서비스를 만들 수 있는 .NET Framework의 구성 요소입니다. 전송 (REST)](https://go.microsoft.com/fwlink/?LinkId=113919). OData는 URI로 주소를 지정할 수 있는 리소스로 데이터를 노출합니다. 데이터는 표준 HTTP 동사인 GET, PUT, POST 및 DELETE를 사용하여 액세스되고 변경됩니다. OData는 [엔터티 데이터 모델](../adonet/entity-data-model.md) 의 엔터티-관계 규칙을 사용 하 여 리소스를 연결로 관련 된 엔터티 집합으로 노출 합니다.

WCF Data Services는 OData 프로토콜을 사용 하 여 리소스의 주소를 지정 하 고 업데이트 합니다. 이러한 방식으로 OData를 지 원하는 모든 클라이언트에서 이러한 서비스에 액세스할 수 있습니다. OData를 사용 하면 잘 알려진 전송 형식을 사용 하 여 리소스를 요청 하 고 리소스에 데이터를 쓸 수 있습니다. 데이터를 XML로 교환 및 업데이트 하기 위한 표준 집합인 Atom, AJAX 응용 프로그램에서 광범위 하 게 사용 되는 텍스트 기반 데이터 교환 형식인 JSON (JavaScript Object Notation)입니다.

WCF Data Services는 다양 한 원본에서 가져온 데이터를 OData 피드로 노출할 수 있습니다. Visual Studio 도구를 사용 하면 ADO.NET Entity Framework 데이터 모델을 사용 하 여 OData 기반 서비스를 쉽게 만들 수 있습니다. CLR (공용 언어 런타임) 클래스와 런타임에 바인딩된 데이터 나 형식화 되지 않은 데이터를 기반으로 하 여 OData 피드를 만들 수도 있습니다.

또한 WCF Data Services에는 클라이언트 라이브러리 집합, 일반 .NET Framework 클라이언트 응용 프로그램 및 Silverlight 기반 응용 프로그램용 기타 기능이 포함 되어 있습니다. 이러한 클라이언트 라이브러리는 .NET Framework 및 Silverlight와 같은 환경에서 OData 피드에 액세스할 때 개체 기반 프로그래밍 모델을 제공 합니다.

## <a name="where-should-i-start"></a>시작 지점

관심 사항에 따라 다음 항목 중 하나를 사용 하 여 WCF Data Services 시작 하는 것이 좋습니다.

바로 시작...

- [빠른 시작](quickstart-wcf-data-services.md)

- [시작](getting-started-with-wcf-data-services.md)

- [Silverlight 빠른 시작](https://go.microsoft.com/fwlink/?LinkID=192782)

- [Windows Phone 개발을 위한 Silverlight 빠른 시작](https://go.microsoft.com/fwlink/?LinkID=214535)

코드를 표시 하기만 합니다.

- [빠른 시작](quickstart-wcf-data-services.md)

- [방법: 데이터 서비스 쿼리 실행](how-to-execute-data-service-queries-wcf-data-services.md)

- [방법: Windows Presentation Foundation 요소에 데이터 바인딩](bind-data-to-wpf-elements-wcf-data-services.md)

OData에 대 한 자세한 내용을 확인 하려면 ...

- [백서 OData 소개](https://go.microsoft.com/fwlink/?LinkId=220867)

- [Open Data Protocol 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=184554)

- [OData: SDK](https://go.microsoft.com/fwlink/?LinkID=185248)

- [OData: 질문과 대답](https://go.microsoft.com/fwlink/?LinkId=185867)

일부 비디오를 시청 하려고 합니다.

- [WCF Data Services 초보자 가이드](https://go.microsoft.com/fwlink/?LinkId=220864)

- [WCF Data Services 개발자 비디오](https://go.microsoft.com/fwlink/?LinkId=220861)

- [OData: 개발자 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=185866)

종단 간 샘플을 확인 하려고 합니다.

- [MSDN 샘플 갤러리의 WCF Data Services 설명서 샘플](https://go.microsoft.com/fwlink/?LinkID=220865)

- [MSDN 샘플 갤러리의 기타 WCF Data Services 샘플](https://go.microsoft.com/fwlink/?LinkId=220866)

- [OData: SDK](https://go.microsoft.com/fwlink/?LinkID=185248)

Visual Studio와의 통합 방식

- [데이터 서비스 클라이언트 라이브러리 생성](generating-the-data-service-client-library-wcf-data-services.md)

- [데이터 서비스 만들기](creating-the-data-service.md)

- [Entity Framework 공급자](entity-framework-provider-wcf-data-services.md)

수행 가능 작업

- [개요](wcf-data-services-overview.md)

- [백서 OData 소개](https://go.microsoft.com/fwlink/?LinkId=220867)

- [애플리케이션 시나리오](application-scenarios-wcf-data-services.md)

Silverlight를 사용 하려는 경우 ...

- [Silverlight 빠른 시작](https://go.microsoft.com/fwlink/?LinkID=192782)

- [WCF Data Services(Silverlight)](https://go.microsoft.com/fwlink/?LinkID=143149)

- [Silverlight 시작](https://go.microsoft.com/fwlink/?LinkId=148366)

LINQ를 사용 하려고 합니다.

- [데이터 서비스 쿼리](querying-the-data-service-wcf-data-services.md)

- [LINQ 고려 사항](linq-considerations-wcf-data-services.md)

- [방법: 데이터 서비스 쿼리 실행](how-to-execute-data-service-queries-wcf-data-services.md)

추가 정보가 필요 합니다.

- [WCF Data Services 팀 블로그](https://go.microsoft.com/fwlink/?LinkID=150511)

- [리소스](wcf-data-services-resources.md)

- [WCF Data Services 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=220868)

- [Open Data Protocol 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=184554)

## <a name="in-this-section"></a>섹션 내용

[개요](wcf-data-services-overview.md)

WCF Data Services에서 사용 가능한 기능에 대 한 개요를 제공 합니다.

[WCF Data Services 5.0의 새로운 기능](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/ee373845(v=vs.103))

WCF Data Services의 새로운 기능 및 새로운 OData 기능에 대 한 지원을 설명 합니다.

[시작](getting-started-with-wcf-data-services.md)

WCF Data Services를 사용 하 여 OData 피드를 노출 하 고 사용 하는 방법을 설명 합니다.

[WCF Data Services 정의](defining-wcf-data-services.md)

OData 피드를 노출 하는 데이터 서비스를 만들고 구성 하는 방법을 설명 합니다.

[WCF Data Services 클라이언트 라이브러리](wcf-data-services-client-library.md)

클라이언트 라이브러리를 사용 하 여 .NET Framework 클라이언트 응용 프로그램에서 OData 피드를 사용 하는 방법을 설명 합니다.

## <a name="see-also"></a>참고자료

- [REST(Representational State Transfer)](https://go.microsoft.com/fwlink/?LinkId=113919)
