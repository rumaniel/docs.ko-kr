---
title: 쿼리 지원
ms.date: 03/30/2017
ms.assetid: 093c22f5-3294-4642-857a-5252233d6796
ms.openlocfilehash: e281b5ae7a41bd282f8e7c7eb9db6f99ef5487f3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69948933"
---
# <a name="support-for-queries"></a>쿼리 지원
SQL 워크플로 인스턴스 저장소는 잘 알려진 속성 집합을 저장소에 기록합니다. 사용자는 이러한 속성을 기반으로 인스턴스를 쿼리할 수 있습니다. 다음은 잘 알려진 일부 속성 목록입니다.  
  
- **사이트 이름입니다.** 서비스를 포함하는 웹 사이트의 이름입니다.  
  
- **상대 응용 프로그램 경로입니다.** 웹 사이트에 상대적인 애플리케이션 경로입니다.  
  
- **상대 서비스 경로입니다.** 애플리케이션에 상대적인 서비스 경로입니다.  
  
- **서비스 이름입니다.** 서비스의 이름입니다.  
  
- **서비스 네임 스페이스입니다.** 서비스에 사용되는 네임스페이스의 이름입니다.  
  
- **현재 컴퓨터입니다.**  
  
- **마지막 컴퓨터**입니다. 워크플로 서비스 인스턴스가 마지막으로 실행된 컴퓨터입니다.  
  
> [!NOTE]
> 워크플로 서비스 호스트를 사용하는 자체 호스팅 시나리오의 경우 마지막 네 속성만 채워집니다. 워크플로 애플리케이션 시나리오의 경우 마지막 속성만 채워집니다.  
  
 워크플로 런타임에서 처음 세 속성에 대한 값을 제공합니다. 워크플로 서비스 호스트는 **일시 중단 이유** 속성의 값을 제공 합니다. SQL 워크플로 인스턴스 저장소는 **마지막으로 업데이트 된 컴퓨터** 속성의 값을 제공 합니다.  
  
 또한 SQL 워크플로 인스턴스 저장소 기능을 사용하면 사용자 지정 속성을 지정하여 지속성 데이터베이스에 값을 저장한 다음 쿼리에서 사용할 수 있습니다. 사용자 지정 승격에 대 한 자세한 내용은 [저장소 확장성](store-extensibility.md)을 참조 하세요.  
  
## <a name="views"></a>뷰  
 인스턴스 저장소에는 다음 뷰가 포함됩니다. 자세한 내용은 [지 속성 데이터베이스 스키마](persistence-database-schema.md) 를 참조 하세요.  
  
### <a name="the-instances-view"></a>Instances 뷰  
 인스턴스 뷰에는 다음 필드가 포함됩니다.  
  
1. **ID**  
  
2. **PendingTimer**  
  
3. **CreationTime**  
  
4. **LastUpdatedTime**  
  
5. **ServiceDeploymentId**  
  
6. **SuspensionExceptionName**  
  
7. **SuspensionReason**  
  
8. **ActiveBookmarks**  
  
9. **CurrentMachine**  
  
10. **LastMachine**  
  
11. **ExecutionStatus**  
  
12. **IsInitialized**  
  
13. **IsSuspended**  
  
14. **IsCompleted**  
  
15. **EncodingOption**  
  
16. **ReadWritePrimitiveDataProperties**  
  
17. **WriteOnlyPrimitiveDataProperties**  
  
18. **ReadWriteComplexDataProperties**  
  
19. **WriteOnlyComplexDataProperties**  
  
### <a name="the-servicedeployments-view"></a>ServiceDeployments 뷰  
 ServiceDeployments 뷰에는 다음 필드가 포함됩니다.  
  
1. **SiteName**  
  
2. **RelativeServicePath**  
  
3. **RelativeApplicationPath**  
  
4. **ServiceName**  
  
5. **ServiceNamespace**  
  
### <a name="the-instancepromotedproperties-view"></a>InstancePromotedProperties 뷰  
 InstancePromotedProperties 뷰에는 다음 필드가 포함됩니다. 승격 된 속성에 대 한 자세한 내용은 [저장소 확장성](store-extensibility.md) 항목을 참조 하세요.  
  
1. **InstanceId**  
  
2. **EncodingOption**  
  
3. **PromotionName**  
  
4. **값 #** ( **Value1** 에서 **Value64**까지의 필드 범위).
