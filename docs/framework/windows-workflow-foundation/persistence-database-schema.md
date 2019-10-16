---
title: 지속성 데이터베이스 스키마
ms.date: 03/30/2017
ms.assetid: 34f69f4c-df81-4da7-b281-a525a9397a5c
ms.openlocfilehash: 65d8b2f7a6283d65823e1a186239d398ee4a530a
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038331"
---
# <a name="persistence-database-schema"></a>지속성 데이터베이스 스키마
이 항목에서는 SQL 워크플로 인스턴스 저장소에서 지원하는 공용 뷰에 대해 설명합니다.  
  
## <a name="instances-view"></a>인스턴스 뷰  
 **인스턴스** 뷰에는 데이터베이스의 모든 워크플로 인스턴스에 대 한 일반 정보가 포함 되어 있습니다.  
  
|열 이름|열 유형|Description|  
|-----------------|-----------------|-----------------|  
|InstanceId|UniqueIdentifier|워크플로 인스턴스의 ID입니다.|  
|PendingTimer|DateTime|워크플로가 Delay 활동에서 차단되었으며 타이머가 만료된 후 다시 시작될 것임을 나타냅니다. 워크플로가 차단되지 않고 타이머가 만료될 때까지 기다리는 경우 이 값은 Null일 수 있습니다.|  
|CreationTime|DateTime|워크플로가 만들어진 시점을 나타냅니다.|  
|LastUpdatedTime|DateTime|워크플로가 데이터베이스에 마지막으로 유지된 시간을 나타냅니다.|  
|ServiceDeploymentId|BigInt|[ServiceDeployments] 뷰의 외래 키 역할을 합니다. 현재 워크플로 인스턴스가 웹 호스팅 서비스의 인스턴스인 경우 이 열은 값을 포함하고, 그렇지 않으면 NULL로 설정됩니다.|  
|SuspensionExceptionName|Nvarchar(450)|워크플로를 일시 중단시킨 예외의 형식(예: InvalidOperationException)을 나타냅니다.|  
|SuspensionReason|Nvarchar(max)|워크플로 인스턴스가 일시 중단된 이유를 나타냅니다. 예외 때문에 인스턴스가 일시 중단된 경우에는 이 열에 예외와 관련된 메시지가 포함되고,<br /><br /> 인스턴스를 수동으로 일시 중단한 경우에는 이 열에 인스턴스를 일시 중단시킨 사용자 지정 이유가 포함됩니다.|  
|ActiveBookmarks|Nvarchar(max)|워크플로 인스턴스가 유휴 상태인 경우 이 속성은 인스턴스가 차단된 책갈피를 나타내고, 인스턴스가 유휴 상태가 아닌 경우 이 열은 NULL입니다.|  
|CurrentMachine|Nvarchar(128)|현재 워크플로 인스턴스가 메모리에 로드된 컴퓨터의 이름을 나타냅니다.|  
|LastMachine|Nvarchar(450)|워크플로 인스턴스를 마지막으로 로드한 컴퓨터를 나타냅니다.|  
|ExecutionStatus|Nvarchar(450)|워크플로의 현재 실행 상태를 나타냅니다. 가능한 상태에는 **실행**중, **유휴**상태, **닫힘**됨이 있습니다.|  
|IsInitialized|비트|워크플로 인스턴스가 초기화되었는지 여부를 나타냅니다. 초기화된 워크플로 인스턴스는 한 번 이상 유지된 워크플로 인스턴스입니다.|  
|IsSuspended|비트|워크플로 인스턴스가 일시 중단되었는지 여부를 나타냅니다.|  
|IsCompleted|비트|워크플로 인스턴스의 실행이 완료되었는지 여부를 나타냅니다. **참고:**  Iif **InstanceCompletionAction** 속성은 **DeleteAll**로 설정 되 고, 완료 되 면 뷰에서 인스턴스가 제거 됩니다.|  
|EncodingOption|TinyInt|데이터 속성을 serialize하는 데 사용된 인코딩에 대해 설명합니다.<br /><br /> -0 – 인코딩 안 함<br />-1 – GzipStream|  
|ReadWritePrimitiveDataProperties|Varbinary(max)|인스턴스가 로드될 때 워크플로 런타임에 다시 제공될 serialize된 인스턴스 데이터 속성을 포함합니다.<br /><br /> 각각의 기본 속성은 네이티브 CLR 형식이며, 이는 blob를 deserialize하는 데 특별한 어셈블리가 필요하지 않음을 의미합니다.|  
|WriteOnlyPrimitiveDataProperties|Varbinary(max)|인스턴스가 로드될 때 워크플로 런타임에 다시 제공되지 않는 serialize된 인스턴스 데이터 속성을 포함합니다.<br /><br /> 각각의 기본 속성은 네이티브 CLR 형식이며, 이는 blob를 deserialize하는 데 특별한 어셈블리가 필요하지 않음을 의미합니다.|  
|ReadWriteComplexDataProperties|Varbinary(max)|인스턴스가 로드될 때 워크플로 런타임에 다시 제공될 serialize된 인스턴스 데이터 속성을 포함합니다.<br /><br /> deserializer에는 이 blob에 저장된 모든 개체 형식에 대한 정보가 필요합니다.|  
|WriteOnlyComplexDataProperties|Varbinary(max)|인스턴스가 로드될 때 워크플로 런타임에 다시 제공되지 않는 serialize된 인스턴스 데이터 속성을 포함합니다.<br /><br /> deserializer에는 이 blob에 저장된 모든 개체 형식에 대한 정보가 필요합니다.|  
|IdentityName|Nvarchar(max)|워크플로 정의의 이름입니다.|  
|IdentityPackage|Nvarchar(max)|워크플로가 만들어질 때 지정된 패키지 정보입니다(예:어셈블리 이름).|  
|빌드|BigInt|워크플로 버전의 빌드 번호입니다.|  
|최대|BigInt|워크플로 버전의 주 번호입니다.|  
|최소|BigInt|워크플로 버전의 부 번호입니다.|  
|Revision|BigInt|워크플로 버전의 개정 번호입니다.|  
  
> [!CAUTION]
> **Instances** 뷰에는 Delete 트리거도 포함 됩니다. 적절한 사용 권한을 가진 사용자는 데이터베이스에서 워크플로 인스턴스를 강제로 제거하는 삭제 문을 이 뷰에 대해 실행할 수 있습니다. 워크플로 런타임에 인스턴스를 삭제하면 의도하지 않은 결과가 발생할 수 있으므로 뷰에서 직접 삭제하는 방법은 다른 방법이 없는 경우에만 사용하는 것이 좋습니다. 대신 워크플로 인스턴스 관리 엔드포인트를 사용하여 워크플로 런타임에서 인스턴스를 종료하게 하세요. 뷰에서 많은 수의 인스턴스를 삭제하려는 경우에는 이러한 인스턴스에서 작동할 수 있는 활성 런타임이 없는지 확인하세요.  
  
## <a name="servicedeployments-view"></a>ServiceDeployments 뷰  
 **Servicedeployments** 뷰에는 모든 웹 (IIS/WAS) 호스팅 워크플로 서비스에 대 한 배포 정보가 포함 되어 있습니다. 웹 호스트 되는 각 워크플로 인스턴스에는이 뷰의 행을 참조 하는 **Servicedeploymentid** 가 포함 됩니다.  
  
|열 이름|열 유형|Description|  
|-----------------|-----------------|-----------------|  
|ServiceDeploymentId|BigInt|이 뷰의 기본 키입니다.|  
|SiteName|Nvarchar(max)|워크플로 서비스 (예: **기본 웹 사이트**)를 포함 하는 사이트의 이름을 나타냅니다.|  
|RelativeServicePath|Nvarchar(max)|워크플로 서비스를 가리키는 사이트에 상대적인 가상 경로를 나타냅니다. (.  **/app1/PurchaseOrderService.svc**).|  
|RelativeApplicationPath|Nvarchar(max)|워크플로 서비스가 포함된 애플리케이션을 가리키는 사이트에 상대적인 가상 경로를 나타냅니다. (예: **/app1**).|  
|ServiceName|Nvarchar(max)|워크플로 서비스의 이름을 나타냅니다. (예: **PurchaseOrderService**).|  
|ServiceNamespace|Nvarchar(max)|워크플로 서비스의 네임스페이스를 나타냅니다. (예: **MyCompany**).|  
  
 ServiceDeployments 뷰에는 삭제 트리거도 포함되어 있습니다. 적절한 사용 권한을 가진 사용자는 이 뷰에 대해 삭제 문을 실행하여 데이터베이스에서 ServiceDeployment 항목을 제거할 수 있습니다. 다음 사항에 유의합니다.  
  
1. 이 뷰에서 항목을 삭제하려면 먼저 전체 데이터베이스를 잠궈야 하므로 이 작업은 부담이 되는 작업입니다. 이 작업은 워크플로 인스턴스가 존재하지 않는 ServiceDeployment 항목을 참조하는 일이 발생하지 않게 하려는 경우 필요합니다. 다운 시간이나 유지 관리 창에 있는 동안에만 이 뷰에서 삭제하는 작업을 수행하기 바랍니다.  
  
2. **인스턴스** 뷰의 항목에서 참조 하는 servicedeployment 행을 삭제 하려고 하면 작업이 수행 되지 않습니다. 참조가 없는 ServiceDeployment 행만 삭제할 수 있습니다.  
  
## <a name="instancepromotedproperties-view"></a>InstancePromotedProperties 뷰  
 **InstancePromotedProperties** 보기에는 사용자가 지정한 모든 승격 된 속성에 대 한 정보가 포함 되어 있습니다. 승격된 속성은 사용자가 인스턴스를 검색할 때 쿼리에 사용할 수 있는 고급 속성 역할을 합니다.  예를 들어 사용자는 항상 **Value1** 열에 주문 비용을 저장 하는 PurchaseOrder 승격을 추가할 수 있습니다. 그러면 사용자는 가격이 특정 값을 초과하는 모든 구매 주문을 쿼리할 수 있습니다.  
  
|열 유형|열 유형|Description|  
|-|-|-|  
|InstanceId|UniqueIdentifier|워크플로 인스턴스의 ID입니다.|  
|EncodingOption|TinyInt|승격된 이진 속성을 serialize하는 데 사용된 인코딩에 대해 설명합니다.<br /><br /> -0 – 인코딩 안 함<br />-1 – GZipStream|  
|PromotionName|Nvarchar(400)|이 인스턴스와 관련된 승격의 이름입니다. PromotionName은 이 행의 제네릭 열에 컨텍스트를 추가하는 데 필요합니다.<br /><br /> 예를 들어 PurchaseOrder의 PromotionName은 Value1에는 주문 가격이 포함되고 Value2에는 주문한 고객의 이름이 포함되고 Value 3에는 고객의 주소가 포함됨을 나타낼 수 있습니다.|  
|Value[1-32]|SqlVariant|Value[1-32]에는 SqlVariant 열에 저장할 수 있는 값이 포함됩니다. 32개보다 많은 SqlVariant는 단일 승격에 포함될 수 없습니다.|  
|Value[33-64]|Varbinary(max)|Value[33-64]에는 serialize된 값이 포함됩니다. 예를 들어 Value33에는 구매할 품목의 JPEG이 포함될 수 있습니다. 32개보다 많은 이진 속성은 단일 승격에 포함될 수 없습니다.|  
  
 InstancePromotedProperties 뷰는 스키마 바인딩 뷰이며, 이는 이 뷰에 대한 쿼리를 최적화하기 위해 사용자가 하나 이상의 열에 대한 인덱스를 추가할 수 있음을 의미합니다.  
  
> [!NOTE]
> 인덱싱된 뷰에는 추가 스토리지가 필요하며 처리 오버헤드가 추가됩니다. 자세한 내용은 [SQL Server 2008 인덱싱된 뷰를 사용 하 여 성능 향상](https://go.microsoft.com/fwlink/?LinkId=179529) 을 참조 하세요.
