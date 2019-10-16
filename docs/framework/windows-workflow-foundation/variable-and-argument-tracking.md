---
title: 변수 및 인수 추적
ms.date: 03/30/2017
ms.assetid: 8f3d9d30-d899-49aa-b7ce-a8d0d32c4ff0
ms.openlocfilehash: 75ec8124200b146965214d161d0e6f246888542c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64640990"
---
# <a name="variable-and-argument-tracking"></a>변수 및 인수 추적
워크플로 실행을 추적할 때 데이터를 추출하는 것이 유용할 때가 많습니다. 이 기능은 추적 레코드 사후 실행에 액세스할 때 추가 컨텍스트를 제공합니다. [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]에서는 추적을 통해 워크플로의 활동 범위 내에서 표시 변수 또는 인수를 추출할 수 있습니다. 추적 프로필을 사용하여 데이터를 쉽게 추출할 수 있습니다.  
  
## <a name="variables-and-arguments"></a>변수 및 인수  
 변수 및 인수는 활동에서 ActivityStateRecord를 내보낼 때 추출됩니다.  변수는 활동 범위 내에 있는 경우에만 추출할 수 있습니다. 활동 내에서 추출할 변수는 다음과 같은 방식으로 지정합니다.  
  
- 변수 이름으로 변수를 지정할 경우 추적을 실행하면 추적 중인 현재 활동과 부모 활동에서 변수를 찾습니다. 즉, 현재 활동 범위와 부모 범위에서 변수를 검색합니다.  
  
- 이름을 사용 하 여 추출할 변수를 지정 하는 경우 = "*"를 다음 추적 중인 현재 활동 내의 모든 변수가 추출 됩니다. 이 경우 범위 내에 있지만 부모 활동에 정의된 변수는 추출되지 않습니다.  
  
 인수를 추출할 경우 추출되는 인수는 활동의 상태에 따라 다릅니다. 활동 상태가 Executing인 경우 `InArguments`만 추출할 수 있습니다. 다른 활동 상태(Closed, Faulted, Canceled)인 경우 모든 인수, InArguments 및 OutArguments를 추출할 수 있습니다.  
  
 다음 예제에서는 활동의 `Closed` 추적 레코드를 내보낼 때 변수와 인수를 추출하는 활동 상태 쿼리를 보여 줍니다. 변수 및 인수는 <xref:System.Activities.Tracking.ActivityStateRecord>를 통해서만 추출할 수 있으므로 <xref:System.Activities.Tracking.ActivityStateQuery>를 사용하여 추적 프로필 내에서 구독합니다.  
  
```xml  
<activityStateQuery activityName="SendEmailActivity">  
  <states>  
    <state name="Closed"/>  
  </states>  
  <variables>  
    <variable name="FromAddress"/>  
  </variables>  
  <arguments>  
    <argument name="Result"/>  
  </arguments>  
</activityStateQuery>  
```  
  
## <a name="protecting-information-stored-within-variables-and-arguments"></a>변수 및 인수에 저장된 정보 보호  
 추적된 변수 또는 인수는 기본적으로 WF 런타임에 의해 표시됩니다. 워크플로 개발자는 다음 단계를 수행하여 해당 변수 또는 인수에 액세스하지 못하게 할 수 있습니다.  
  
1. 변수 값을 암호화합니다.  
  
2. 추적 프로필 작성을 제어하여 변수 또는 인수 추출을 방지합니다.  
  
3. 사용자 지정 추적 참가자는 변수 또는 인수에 저장된 중요한 정보가 WF 코드를 통해 공개되지 않도록 해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [Windows Server App Fabric 모니터링](https://go.microsoft.com/fwlink/?LinkId=201273)
- [App Fabric을 사용 하 여 응용 프로그램 모니터링](https://go.microsoft.com/fwlink/?LinkId=201275)
