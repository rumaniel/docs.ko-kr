---
title: 사용자 지정 필터
ms.date: 03/30/2017
ms.assetid: 97cf247d-be0a-4057-bba9-3be5c45029d5
ms.openlocfilehash: ade387524c9ca6c8ef337ccf6a5b3453b7df976b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69945373"
---
# <a name="custom-filters"></a>사용자 지정 필터
사용자 지정 필터를 사용하면 시스템 제공 메시지 필터를 사용하여 정의할 수 없는 일치 논리를 정의할 수 있습니다. 예를 들어 특정 메시지 요소를 해시한 다음 값을 검사하여 필터가 true를 반환하는지 아니면 false를 반환하는지를 확인하는 사용자 지정 필터를 만들 수 있습니다.  
  
## <a name="implementation"></a>구현  
 사용자 지정 필터는 <xref:System.ServiceModel.Dispatcher.MessageFilter> 추상 기본 클래스의 구현입니다. 사용자 지정 필터를 구현하는 경우 생성자가 단일 문자열 매개 변수를 필요에 따라 허용할 수 있습니다. 이 매개 변수에는 런타임에 필터가 일치를 수행하는 데 필요한 값이나 구성을 제공하기 위해 MessageFilter 생성자에게 전달되는 구성 정보가 포함되어 있습니다. 예를 들어 이 정보를 사용하여 평가할 메시지 내에서 필터가 검색하는 값을 제공할 수 있습니다. 다음 예제에서는 문자열 매개 변수를 허용하는 사용자 지정 메시지 필터의 기본 구현을 보여 줍니다.  
  
```csharp  
public class MyMessageFilter: MessageFilter  
{  
    string filterData;  
    public MyMessageFilter(string filterData)  
    {  
        if(string.IsNullOrEmpty(filterData)  
            throw new ArgumentNullException("filterData");  
        this.filterData=filterData;  
    }  
    public override bool Match(System.ServiceModel.Channels.Message message)  
    {  
        ...  
        return retValue;  
    }  
    public override bool Match(System.ServiceModel.Channels.MessageBuffer buffer)  
    {  
        ...  
        return retValue;  
    }  
}  
```  
  
> [!NOTE]
> 실제 구현에서 Match 메서드는 메시지를 검사 하 여이 메시지 필터가 **true** 또는 **false**를 반환 해야 하는지 여부를 결정 하는 논리를 포함 합니다.  
  
### <a name="performance"></a>성능  
 사용자 지정 필터를 구현하는 경우에는 필터에서 메시지 평가를 완료하는 데 필요한 최대 시간을 고려해야 합니다. 메시지는 일치 항목을 찾을 때까지 여러 필터에 대해 평가될 수 있으므로 모든 필터가 평가되기 전에 클라이언트 요청이 시간 초과되지 않도록 해야 합니다. 따라서 메시지가 필터 조건과 일치하는지 확인하려면 메시지의 내용 또는 특성을 평가하는 데 필요한 코드만 사용자 지정 필터에 포함해야 합니다.  
  
 일반적으로 사용자 지정 필터를 구현할 때는 다음 사항을 피해야 합니다.  
  
- IO(예: 디스크 또는 데이터베이스에 데이터 저장)  
  
- 불필요한 처리(예: 문서의 여러 레코드 반복)  
  
- 차단 작업(예: 공유 리소스에 대한 잠금 확보 또는 데이터베이스에 대한 조회 수행이 필요한 호출)  
  
 프로덕션 환경에서 사용자 지정 필터를 사용하기 전에 성능 테스트를 실행하여 필터에서 메시지를 평가하는 데 소요되는 평균 시간을 확인해야 합니다. 필터 테이블에 사용되는 다른 필터의 평균 처리 시간을 조합하면 클라이언트 애플리케이션에서 지정하는 최대 제한 시간 값을 정확하게 확인할 수 있습니다.  
  
## <a name="usage"></a>사용  
 라우팅 서비스에서 사용자 지정 필터를 사용 하려면 "Custom" 유형의 새 필터 항목인 메시지 필터의 정규화 된 유형 이름과 어셈블리 이름을 지정 하 여 필터 테이블에 추가 해야 합니다.  다른 MessageFilter와 마찬가지로 사용자 지정 필터의 생성자에게 전달될 filterData 문자열을 지정할 수 있습니다.  
  
 다음 예제에서는 라우팅 서비스에서 사용자 지정 필터를 사용하는 방법을 보여 줍니다.  
  
```xml  
<!--ROUTING SECTION -->  
<routing>  
  <filters>  
    <filter name="CustomFilter1" filterType="Custom"   
            customType="CustomAssembly.MyMessageFilter,   
            CustomAssembly" filterData="custom data" />  
  </filters>  
  <filterTables>  
    <table name="routingTable1">  
      <filters>  
        <add filterName="CustomFilter1" endpointName="CalculatorService" />  
      </filters>  
    </table>  
  </filterTables>  
</routing>  
```  
  
```csharp  
RoutingConfiguration rc = new RoutingConfiguration();  
List<ServiceEndpoint> endpointList = new List<ServiceEndpoint>();  
endpointList.Add(client);  
rc.FilterTable.Add(new MyMessageFilter("CustomData"), endpointList);  
```
