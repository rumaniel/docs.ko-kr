---
title: <backupList>
ms.date: 03/30/2017
ms.assetid: a3d9d1f9-4a53-45e9-a880-86c8bee0b833
ms.openlocfilehash: 478211755b9131c03b72777ee95ff7223b9092c9
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70850280"
---
# <a name="backuplist"></a>\<backupList>
기본 끝점에 연결할 수 없는 경우 라우팅 서비스에서 사용할 끝점 집합을 열거 하는 백업 목록을 정의 하기 위한 구성 섹션을 나타냅니다. 목록의 첫 번째 엔드포인트가 다운되는 경우 라우팅 서비스는 자동으로 목록의 다음 엔드포인트로 장애 조치(failover)됩니다.  따라서 복잡한 패턴을 처리하는 방법이나 모든 서비스가 배포되는 위치를 클라이언트 애플리케이션에 지정할 필요 없이 애플리케이션의 안정성을 빠르게 향상시킬 수 있습니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<라우팅 >** ](routing.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<backupLists >** ](backuplists.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<backupList >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<routing>
  <backupLists>
    <backupList name="String">
      <add endpointName="String" />
    </backupList>
  </backupLists>
</routing>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|name|이 엔드포인트 목록을 식별하는 데 사용되는 이름을 지정하는 문자열입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<filter>](filter.md)||  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<routing>](routing.md)|백업 엔드포인트의 목록입니다.|  
  
## <a name="remarks"></a>설명  
 이 섹션에는 기본 엔드포인트로 메시지를 보낼 때 통신 예외가 발생하면 이 메시지를 전송할 엔드포인트의 정렬된 컬렉션이 포함됩니다.  
  
 `endpointName` [ \<추가 >](add-of-entries.md) 의 특성에 나열 된 기본 끝점으로의 보내기가 통신 예외와 함께 실패 하는 경우 라우팅 서비스는이 구성 섹션에 있는 첫 번째 끝점으로 메시지를 보내려고 시도 합니다. 이것도 통신 예외가 발생하여 실패하는 경우 라우팅 서비스는 보내기가 성공할 때까지, 통신 예외가 아닌 다른 원인으로 보내기가 실패할 때까지 또는 컬렉션의 모든 엔드포인트에 대한 보내기가 실패할 때까지 이 섹션에 포함된 다음 엔드포인트로 메시지를 보내려고 시도합니다.  
  
 다음 예제에서는 "Destination" 이라는 기본 끝점으로 송신 통신 예외가 반환 하는 경우 서비스를 "alternateservicequeue"로 메시지를 보낼 시도 됩니다. 이 시도에 대해서도 통신 예외가 반환되면 라우팅 서비스는 컬렉션의 다음 엔드포인트로 메시지를 보내려고 시도합니다.  
  
```xml  
<filterTables>
  <filterTable name="filterTable1">
    <add filterName="MatchAllFilter1"
         endpointName="Destination"
         backupList="backupEndpointList" />
  </filterTable>
</filterTables>
<backupLists>
  <backupList name="backupEndpointList">
    <add endpointName="backupServiceQueue" />
    <add endpointName="alternateServiceQueue" />
  </backupList>
</backupLists>
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Routing.Configuration.BackupEndpointCollection?displayProperty=nameWithType>
