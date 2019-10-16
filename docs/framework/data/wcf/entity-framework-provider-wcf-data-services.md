---
title: Entity Framework 공급자(WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, providers
ms.assetid: 650b5eb6-c71d-4dc1-8b64-b6beaf752114
ms.openlocfilehash: 5a40eeafafef56902a9ae5037e6bc946b598f752
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854086"
---
# <a name="entity-framework-provider-wcf-data-services"></a>Entity Framework 공급자(WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]와 마찬가지로 ADO.NET Entity Framework는 엔터티-관계 모델의 한 형식인 엔터티 데이터 모델을 기반으로 합니다. Entity Framework은 *개념적 모델*이라고 하는 엔터티 데이터 모델의 구현에 대해 작업을 데이터 소스에 대 한 동등한 작업으로 변환 합니다. 따라서 Entity Framework는 관계형 데이터를 기반으로 하는 데이터 서비스에 적합한 공급자이며, Entity Framework를 지원하는 데이터 공급자가 있는 모든 데이터베이스를 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]와 함께 사용할 수 있습니다. 현재 Entity Framework을 지 원하는 데이터 원본 목록은 Entity Framework의 타사 [공급자](https://go.microsoft.com/fwlink/?LinkId=143699)를 참조 하십시오.  
  
 개념적 모델에서 엔터티 컨테이너는 서비스 루트입니다. 먼저 Entity Framework에서 개념적 모델을 정의해야 데이터 서비스가 데이터를 노출할 수 있습니다. 자세한 내용은 [방법: ADO.NET Entity Framework 데이터 원본을](create-a-data-service-using-an-adonet-ef-data-wcf.md)사용 하 여 데이터 서비스를 만듭니다.  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]는 엔터티의 동시성 토큰을 정의할 수 있도록 하 여 낙관적 동시성 모델을 지원 합니다. 엔터티의 속성을 하나 이상 포함하는 이 동시성 토큰은 요청되거나 업데이트 또는 삭제되고 있는 데이터가 변경되었는지 여부를 데이터 서비스에서 확인하는 데 사용됩니다. 요청의 eTag에서 가져온 토큰 값이 엔터티의 현재 값과 다르면 데이터 서비스에서 예외가 발생합니다. 속성이 동시성 토큰의 일부임을 나타내려면 Entity Framework 공급자가 정의한 데이터 모델에 특성 `ConcurrencyMode="Fixed"` 을 적용 해야 합니다. 동시성 토큰에는 키 속성이나 탐색 속성이 포함될 수 없습니다. 자세한 내용은 [데이터 서비스 업데이트](updating-the-data-service-wcf-data-services.md)를 참조 하세요.  
  
 Entity Framework에 대해 자세히 알아보려면 [Entity Framework 개요](../adonet/ef/overview.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [Data Services 공급자](data-services-providers-wcf-data-services.md)
- [리플렉션 공급자](reflection-provider-wcf-data-services.md)
- [엔터티 데이터 모델](../adonet/entity-data-model.md)
