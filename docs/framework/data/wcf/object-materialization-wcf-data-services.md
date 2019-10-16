---
title: 개체 구체화(WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, client library
- WCF Data Services, querying
ms.assetid: f0dbf7b0-0292-4e31-9ae4-b98288336dc1
ms.openlocfilehash: 89357b1d05526438c939a73663c5b7b6273df4ac
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790396"
---
# <a name="object-materialization-wcf-data-services"></a>개체 구체화(WCF Data Services)

**서비스 참조 추가** 대화 상자를 사용 하 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 여 .NET Framework 기반 클라이언트 응용 프로그램에서 피드를 사용 하는 경우 피드에서 노출 하는 데이터 모델의 각 엔터티 형식에 대해 해당 하는 데이터 클래스가 생성 됩니다. 자세한 내용은 [데이터 서비스 클라이언트 라이브러리 생성](generating-the-data-service-client-library-wcf-data-services.md)을 참조 하십시오. 쿼리에서 반환되는 엔터티 데이터는 이러한 생성된 클라이언트 데이터 서비스 클래스 중 하나의 인스턴스로 구체화됩니다. 추적 되는 개체에 대 한 병합 옵션 및 id 확인에 대 한 자세한 내용은 [데이터 서비스 컨텍스트 관리](managing-the-data-service-context-wcf-data-services.md)를 참조 하세요.

[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]를 사용하면 도구에서 생성된 데이터 클래스를 사용하지 않고 고유한 클라이언트 데이터 서비스 클래스를 정의할 수도 있습니다. 이에 따라 POCO(Plain Old CLR Object) 데이터 클래스라고도 하는 고유 데이터 클래스를 사용할 수 있습니다. 이러한 유형의 사용자 지정 데이터 클래스를 사용 하는 경우 또는 <xref:System.Data.Services.Common.DataServiceKeyAttribute> <xref:System.Data.Services.Common.DataServiceEntityAttribute> 중 하나를 사용 하 여 데이터 클래스의 특성을 지정 하 고 클라이언트의 형식 이름이 데이터 서비스의 데이터 모델에 있는 형식 이름과 일치 하는지 확인 해야 합니다.

라이브러리는 쿼리 응답 메시지를 받은 후 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 피드의 반환 된 데이터를 쿼리 형식의 클라이언트 데이터 서비스 클래스의 인스턴스로 구체화 합니다. 이러한 개체를 구체화하는 일반적인 프로세스는 다음과 같습니다.

1. 클라이언트 라이브러리는 다음 중 한 가지 방법으로 응답 메시지 피드의 `entry` 요소에서 serialize된 형식을 읽고 올바른 형식의 새 인스턴스를 만들려고 시도합니다.

    - 피드에 선언된 형식의 이름이 <xref:System.Data.Services.Client.DataServiceQuery%601>의 형식 이름과 동일한 경우 이 형식의 새 인스턴스가 빈 생성자를 사용하여 만들어집니다.

    - 피드에 선언된 형식의 이름이 <xref:System.Data.Services.Client.DataServiceQuery%601>의 형식에서 파생된 형식의 이름과 동일한 경우 이 파생 형식의 새 인스턴스가 빈 생성자를 사용하여 만들어집니다.

    - 피드에 선언된 형식과 일치하는 <xref:System.Data.Services.Client.DataServiceQuery%601>의 형식이나 파생 형식을 찾을 수 없는 경우 쿼리된 형식의 새 인스턴스가 빈 생성자를 사용하여 만들어집니다.

    - <xref:System.Data.Services.Client.DataServiceContext.ResolveType%2A> 속성이 설정된 경우 제공된 대리자가 호출되어 기본 이름 기반 형식 매핑을 재정의하고 <xref:System.Func%602>에서 반환되는 형식의 새 인스턴스가 대신 만들어집니다. 이 대리자가 null 값을 반환하는 경우 쿼리된 형식의 새 인스턴스가 대신 만들어집니다. 상속 시나리오를 지원하려면 기본 이름 기반 형식 이름 매핑을 재정의해야 할 수 있습니다.

2. 클라이언트 라이브러리는 엔터티의 ID 값인 `id`의 `entry` 요소에서 URI 값을 읽습니다. <xref:System.Data.Services.Client.DataServiceContext.MergeOption%2A>의 <xref:System.Data.Services.Client.MergeOption.NoTracking> 값을 사용하지 않는 경우 ID 값이 <xref:System.Data.Services.Client.DataServiceContext>에서 개체를 추적하는 데 사용됩니다. ID 값은 엔터티가 쿼리 응답에서 여러 번 반환되는 경우에도 한 엔터티 인스턴스만 만들어지도록 하는 데도 사용됩니다.

3. 클라이언트 라이브러리는 피드 항목에서 속성을 읽고 새로 만들어진 개체에 대해 해당 속성을 설정합니다. ID 값이 동일한 개체가 이미 <xref:System.Data.Services.Client.DataServiceContext>에 있는 경우 <xref:System.Data.Services.Client.MergeOption>의 <xref:System.Data.Services.Client.DataServiceContext> 설정에 따라 속성이 설정됩니다. 해당 속성이 클라이언트 형식에 없는 경우 응답에 속성 값이 포함될 수도 있습니다. 이러한 경우 <xref:System.Data.Services.Client.DataServiceContext.IgnoreMissingProperties%2A>의 <xref:System.Data.Services.Client.DataServiceContext> 속성 값에 따라 동작이 결정됩니다. 이 속성이 `true`로 설정되었으면 없는 속성이 무시되고, 그렇지 않으면 오류가 발생합니다. 속성은 다음과 같이 설정됩니다.

    - 스칼라 속성은 응답 메시지의 항목에 있는 해당 값으로 설정됩니다.

    - 복합 속성은 응답에 있는 복합 형식의 속성을 사용하여 설정된 새로운 복합 형식 인스턴스로 설정됩니다.

    - 관련 엔터티의 컬렉션을 반환하는 탐색 속성은 <xref:System.Collections.Generic.ICollection%601>의 새 인스턴스나 기존 인스턴스로 설정됩니다. 여기서 `T`는 관련 엔터티의 형식입니다. 이 컬렉션은 관련 개체가 <xref:System.Data.Services.Client.DataServiceContext>로 로드되지 않은 경우 비어 있습니다. 자세한 내용은 [지연 된 콘텐츠 로드](loading-deferred-content-wcf-data-services.md)를 참조 하세요.

      > [!NOTE]
      > 생성된 클라이언트 데이터 클래스가 데이터 바인딩을 지원하는 경우 탐색 속성은 <xref:System.Data.Services.Client.DataServiceCollection%601> 클래스의 인스턴스를 대신 반환합니다. 자세한 내용은 [컨트롤에 데이터 바인딩](binding-data-to-controls-wcf-data-services.md)합니다.

4. <xref:System.Data.Services.Client.DataServiceContext.ReadingEntity> 이벤트가 발생합니다.

5. 클라이언트 라이브러리는 개체를 <xref:System.Data.Services.Client.DataServiceContext>에 연결합니다. <xref:System.Data.Services.Client.MergeOption>이 <xref:System.Data.Services.Client.MergeOption.NoTracking>인 경우에는 개체가 연결되지 않습니다.

## <a name="see-also"></a>참고자료

- [데이터 서비스 쿼리](querying-the-data-service-wcf-data-services.md)
- [프로젝트 쿼리](query-projections-wcf-data-services.md)
