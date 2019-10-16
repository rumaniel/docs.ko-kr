---
title: 리플렉션 공급자(WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, providers
ms.assetid: ef5ba300-6d7c-455e-a7bd-d0cc6d211ad4
ms.openlocfilehash: c3e160f96be2a95262776994152a06b42b475887
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779812"
---
# <a name="reflection-provider-wcf-data-services"></a>리플렉션 공급자(WCF Data Services)

[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]는 Entity Framework를 통해 데이터 모델의 데이터를 노출할 뿐 아니라 엔터티 기반 모델에 엄격하게 정의되지 않은 데이터를 노출할 수 있습니다. 리플렉션 공급자는 <xref:System.Linq.IQueryable%601> 인터페이스를 구현하는 형식을 반환하는 클래스의 데이터를 노출합니다. [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]는 리플렉션을 사용하여 이러한 클래스의 데이터 모델을 유추하고 리소스에 대한 주소 기반 쿼리를 노출된 <xref:System.Linq.IQueryable%601> 형식에 대한 LINQ(Language-Integrated Query) 기반 쿼리로 변환할 수 있습니다.

> [!NOTE]
> <xref:System.Linq.Queryable.AsQueryable%2A> 인터페이스를 구현하는 모든 클래스에서 <xref:System.Linq.IQueryable%601> 메서드를 사용하여 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스를 반환할 수 있습니다. 이렇게 하면 가장 일반적인 컬렉션 형식을 데이터 서비스의 데이터 소스로 사용할 수 있습니다.

리플렉션 공급자는 형식 계층 구조를 지원합니다. 자세한 내용은 [방법: 리플렉션 공급자](create-a-data-service-using-rp-wcf-data-services.md)를 사용 하 여 데이터 서비스를 만듭니다.

## <a name="inferring-the-data-model"></a>데이터 모델 유추

데이터 서비스를 만들면 공급자가 리플렉션을 사용하여 데이터 모델을 유추합니다. 다음 목록에서는 리플렉션 공급자가 데이터 모델을 유추하는 방법을 보여 줍니다.

- 엔터티 컨테이너 - <xref:System.Linq.IQueryable%601> 인스턴스를 반환하는 속성으로 데이터를 노출하는 클래스입니다. 리플렉션 기반 데이터 모델의 주소를 지정할 때 엔터티 컨테이너는 서비스 루트를 나타냅니다. 지정된 네임스페이스에 대해 엔터티 컨테이너 클래스 하나만 지원됩니다.

- 엔터티 집합 - <xref:System.Linq.IQueryable%601> 인스턴스를 반환하는 속성은 엔터티 집합으로 처리됩니다. 엔터티 집합은 쿼리의 리소스로 직접 주소가 지정됩니다. 엔터티 컨테이너의 속성 하나만 지정된 형식의 <xref:System.Linq.IQueryable%601> 인스턴스를 반환할 수 있습니다.

- 엔터티 형식 - 엔터티 집합이 반환하는 `T`의 <xref:System.Linq.IQueryable%601> 형식입니다. 상속 계층 구조에 속하는 클래스는 리플렉션 공급자에 의해 동등한 엔터티 형식 계층 구조로 변환됩니다.

- 엔터티 키 - 엔터티 형식인 각 데이터 클래스에는 키 속성이 있어야 합니다. 이 속성은 <xref:System.Data.Services.Common.DataServiceKeyAttribute> 특성(`[DataServiceKeyAttribute]`)을 사용합니다.

    > [!NOTE]
    > <xref:System.Data.Services.Common.DataServiceKeyAttribute> 특성은 엔터티 형식의 인스턴스를 고유하게 식별하는 데 사용할 수 있는 속성에만 적용해야 합니다. 이 특성은 탐색 속성에 적용될 때 무시됩니다.

- 엔터티 형식 속성 - 엔터티 키를 제외하고 리플렉션 공급자는 엔터티 형식인 클래스의 액세스 가능한 비인덱서 속성을 다음과 같이 처리합니다.

  - 기본 형식을 반환하는 속성은 엔터티 형식의 속성으로 간주됩니다.

  - 엔터티 형식이기도 한 형식을 반환하는 속성은 다대일 또는 일대일 관계의 "일" 쪽을 나타내는 탐색 속성으로 간주됩니다.

  - 엔터티 형식의 <xref:System.Collections.Generic.IEnumerable%601>을 반환하는 속성은 일대다 또는 다대다 관계의 "다" 쪽을 나타내는 탐색 속성으로 간주됩니다.

  - 반환 형식이 값 형식인 속성은 복합 형식을 나타냅니다.

> [!NOTE]
> 엔터티 관계형 모델을 기반으로 하는 데이터 모델과 달리 리플렉션 공급자를 기반으로 하는 모델에서는 관계형 데이터가 인식되지 않습니다. Entity Framework를 사용하여 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]를 통해 관계형 데이터를 노출해야 합니다.

## <a name="data-type-mapping"></a>데이터 형식 매핑

.NET Framework 클래스에서 데이터 모델을 유추할 때 데이터 모델의 기본 형식은 다음과 같이 .NET Framework 데이터 형식에 매핑됩니다.

|.NET Framework 데이터 형식|데이터 모델 형식|
|------------------------------|---------------------|
|<xref:System.Byte> `[]`|`Edm.Binary`|
|<xref:System.Boolean>|`Edm.Boolean`|
|<xref:System.Byte>|`Edm.Byte`|
|<xref:System.DateTime>|`Edm.DateTime`|
|<xref:System.Decimal>|`Edm.Decimal`|
|<xref:System.Double>|`Edm.Double`|
|<xref:System.Guid>|`Edm.Guid`|
|<xref:System.Int16>|`Edm.Int16`|
|<xref:System.Int32>|`Edm.Int32`|
|<xref:System.Int64>|`Edm.Int64`|
|<xref:System.SByte>|`Edm.SByte`|
|<xref:System.Single>|`Edm.Single`|
|<xref:System.String>|`Edm.String`|

> [!NOTE]
> .NET Framework nullable 값 형식은 null이 할당될 수 없는 해당 값 형식과 동일한 데이터 모델 형식으로 매핑됩니다.

## <a name="enabling-updates-in-the-data-model"></a>데이터 모델에서 업데이트 사용

이러한 종류의 데이터 모델을 통해 노출되는 데이터를 업데이트하려면 리플렉션 공급자는 <xref:System.Data.Services.IUpdatable> 인터페이스를 정의합니다. 이 인터페이스는 노출된 형식의 업데이트를 저장하는 방법을 데이터 서비스에 지시합니다. 데이터 모델에 의해 정의된 리소스를 업데이트하려면 엔터티 컨테이너 클래스에서 <xref:System.Data.Services.IUpdatable> 인터페이스를 구현해야 합니다. <xref:System.Data.Services.IUpdatable> 인터페이스 구현에 대 한 예제를 보려면 [방법: LINQ to SQL 데이터 원본을](create-a-data-service-using-linq-to-sql-wcf.md)사용 하 여 데이터 서비스를 만듭니다.

<xref:System.Data.Services.IUpdatable> 인터페이스를 사용하려면 리플렉션 공급자를 통해 업데이트를 데이터 소스로 전파할 수 있도록 다음 멤버를 구현해야 합니다.

|멤버|설명|
|------------|-----------------|
|<xref:System.Data.Services.IUpdatable.AddReferenceToCollection%2A>|탐색 속성에서 액세스되는 관련 개체의 컬렉션에 개체를 추가하는 기능을 제공합니다.|
|<xref:System.Data.Services.IUpdatable.ClearChanges%2A>|보류 중인 데이터 변경 내용을 취소하는 기능을 제공합니다.|
|<xref:System.Data.Services.IUpdatable.CreateResource%2A>|지정한 컨테이너에 새 리소스를 만드는 기능을 제공합니다.|
|<xref:System.Data.Services.IUpdatable.DeleteResource%2A>|리소스를 삭제하는 기능을 제공합니다.|
|<xref:System.Data.Services.IUpdatable.GetResource%2A>|특정 쿼리 및 형식 이름으로 식별되는 리소스를 검색하는 기능을 제공합니다.|
|<xref:System.Data.Services.IUpdatable.GetValue%2A>|리소스의 속성 값을 반환하는 기능을 제공합니다.|
|<xref:System.Data.Services.IUpdatable.RemoveReferenceFromCollection%2A>|탐색 속성에서 액세스되는 관련 개체의 컬렉션에서 개체를 제거하는 기능을 제공합니다.|
|<xref:System.Data.Services.IUpdatable.ResetResource%2A>|지정한 리소스를 업데이트하는 기능을 제공합니다.|
|<xref:System.Data.Services.IUpdatable.ResolveResource%2A>|특정 개체 인스턴스가 나타내는 리소스를 반환하는 기능을 제공합니다.|
|<xref:System.Data.Services.IUpdatable.SaveChanges%2A>|보류 중인 변경 내용을 모두 저장하는 기능을 제공합니다.|
|<xref:System.Data.Services.IUpdatable.SetReference%2A>|탐색 속성을 사용하여 관련 개체 참조를 설정하는 기능을 제공합니다.|
|<xref:System.Data.Services.IUpdatable.SetValue%2A>|리소스의 속성 값을 설정하는 기능을 제공합니다.|

## <a name="handling-concurrency"></a>동시성 처리

[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]는 엔터티의 동시성 토큰을 정의할 수 있도록 하여 낙관적 동시성 모델을 지원합니다. 엔터티의 속성을 하나 이상 포함하는 이 동시성 토큰은 요청되거나 업데이트 또는 삭제되고 있는 데이터가 변경되었는지 여부를 데이터 서비스에서 확인하는 데 사용됩니다. 요청의 eTag에서 가져온 토큰 값이 엔터티의 현재 값과 다르면 데이터 서비스에서 예외가 발생합니다. 리플렉션 공급자에서 동시성 토큰을 정의하기 위해 <xref:System.Data.Services.ETagAttribute>가 엔터티 형식에 적용됩니다. 동시성 토큰에는 키 속성이나 탐색 속성이 포함될 수 없습니다. 자세한 내용은 [데이터 서비스 업데이트](updating-the-data-service-wcf-data-services.md)를 참조 하세요.

## <a name="using-linq-to-sql-with-the-reflection-provider"></a>리플렉션 공급자와 함께 LINQ to SQL 사용

Entity Framework는 기본적으로 지원되므로 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]에 관계형 데이터를 사용하는 경우 이 데이터 공급자를 사용하는 것이 좋습니다. 그러나 리플렉션 공급자를 통해 데이터 서비스에 LINQ to SQL 클래스를 사용할 수 있습니다. O <xref:System.Data.Linq.Table%601> /R 디자이너 (LINQ to SQL 개체 관계형 디자이너)에서 <xref:System.Data.Linq.DataContext> 생성 된의 메서드에 의해 반환 되는 결과 집합은 인터페이스를 <xref:System.Linq.IQueryable%601> 구현 합니다. 이렇게 하면 리플렉션 공급자가 이러한 메서드에 액세스하고 생성된 LINQ to SQL 클래스를 사용하여 SQL Server에서 엔터티 데이터를 반환할 수 있습니다. 그러나 LINQ to SQL은 <xref:System.Data.Services.IUpdatable> 인터페이스를 구현하지 않으므로 기존 <xref:System.Data.Linq.DataContext> partial 클래스를 확장하여 <xref:System.Data.Services.IUpdatable> 구현을 추가하는 partial 클래스를 추가해야 합니다. 자세한 내용은 [방법: LINQ to SQL 데이터 원본을](create-a-data-service-using-linq-to-sql-wcf.md)사용 하 여 데이터 서비스를 만듭니다.

## <a name="see-also"></a>참고자료

- [Data Services 공급자](data-services-providers-wcf-data-services.md)
