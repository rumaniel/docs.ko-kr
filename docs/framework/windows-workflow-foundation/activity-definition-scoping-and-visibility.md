---
title: 활동 정의 범위 지정 및 표시 유형
ms.date: 03/30/2017
ms.assetid: ccdffa07-9503-4eea-a61b-17f1564368b7
ms.openlocfilehash: 27c43323a176c841f3d90cb9c52f25599bc0686d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61945953"
---
# <a name="activity-definition-scoping-and-visibility"></a>활동 정의 범위 지정 및 표시 유형
활동 정의의 범위 지정 및 표시 유형은 개체의 범위 지정 및 표시 유형과 마찬가지로 다른 개체나 활동이 활동의 멤버에 액세스하는 기능입니다. 활동 정의는 다음 구현을 통해 수행됩니다.  
  
1. 활동이 사용자에게 노출하는 멤버(<xref:System.Activities.Argument>, <xref:System.Activities.Variable> 및 <xref:System.Activities.ActivityDelegate> 개체와 자식 활동) 결정  
  
2. 활동의 실행 논리 구현  
  
 구현에는 활동의 소비자에게 노출되기 보다는 구현의 세부 정보에 해당하는 멤버가 포함될 수 있습니다.  형식 정의와 마찬가지로 활동 모델을 통해 작성자는 정의할 활동의 정의와 관련하여 활동 멤버의 표시 유형을 한정할 수 있습니다.  이 표시 유형은 데이터 범위 지정과 같은 멤버 사용에 관련된 측면을 제어합니다.  
  
## <a name="scope"></a>범위  
 데이터 범위 지정 외에 활동 모델 표시 유형을 통해서도 유효성 검사, 디버깅 및 추적과 같은 활동의 다른 측면에 대한 액세스를 제한할 수 있습니다. 실행 속성은 표시 유형과 범위 지정을 사용하여 실행 특성을 정의의 특정 범위로 제한합니다. 보조 루트는 표시 유형과 범위 지정을 사용하여 <xref:System.Activities.Statements.CompensableActivity>에서 캡처된 상태를 보정 가능한 활동이 사용되는 정의의 범위로 제한합니다.  
  
## <a name="definition-and-usage"></a>정의 및 사용  
 기본 활동 클래스에서 상속 하 여 및에서 활동을 사용 하 여 새 활동을 작성 하 여 워크플로 작성 합니다 [기본 제공 활동 라이브러리](net-framework-4-5-built-in-activity-library.md)합니다. 활동을 사용하려면 활동 작성자가 정의의 각 구성 요소에 대한 표시 유형을 구성해야 합니다.  
  
### <a name="activity-members"></a>활동 멤버  
 활동 모델은 활동이 소비자에게 제공하는 인수, 변수, 대리자 및 자식 활동을 정의합니다. 이러한 각각의 멤버를 `public` 또는 `private`로 선언할 수 있습니다. public 멤버는 활동의 소비자가 구성하지만 `private` 멤버는 활동의 작성자가 정한 구현을 사용합니다. 데이터 범위 지정의 표시 유형 규칙은 다음과 같습니다.  
  
1. public 멤버와 public 자식 활동의 public 멤버는 public 변수를 참조할 수 있습니다.  
  
2. public 멤버와 public 자식 활동의 public 멤버는 인수 및 private 변수를 참조할 수 있습니다.  
  
 활동의 소비자가 설정할 수 있는 멤버는 private으로 설정해서는 안 됩니다.  
  
### <a name="authoring-models"></a>제작 모델  
 사용자 지정 활동은 <xref:System.Activities.NativeActivity>, <xref:System.Activities.Activity>, <xref:System.Activities.CodeActivity> 또는 <xref:System.Activities.AsyncCodeActivity>를 사용하여 정의됩니다. 이러한 클래스에서 파생되는 활동은 여러 다른 표시 유형을 사용하여 여러 다른 멤버 형식을 노출할 수 있습니다.  
  
#### <a name="nativeactivity"></a>NativeActivity  
 <xref:System.Activities.NativeActivity>에서 파생되는 활동에는 명령적 코드로 작성된 동작이 있으며 이러한 활동은 선택적으로 기존 활동을 사용하여 정의할 수도 있습니다. <xref:System.Activities.NativeActivity>에서 활동을 파생하면 런타임에서 노출되는 모든 기능에 대한 액세스 권한이 부여됩니다. 이러한 활동의 멤버는 `public`으로만 선언할 수 있는 인수를 제외하고 모두 public 또는 private 표시 유형을 사용하여 정의할 수 있습니다.  
  
 <xref:System.Activities.NativeActivity>에서 파생되는 클래스의 멤버는 <xref:System.Activities.NativeActivityMetadata> 메서드에 전달된 <xref:System.Activities.NativeActivity.CacheMetadata%2A> 구조체를 사용하여 런타임으로 선언됩니다.  
  
#### <a name="activity"></a>활동  
 <xref:System.Activities.Activity>를 사용하여 만든 활동에는 다른 활동 구성을 통해 엄격하게 디자인된 동작이 포함됩니다. <xref:System.Activities.Activity> 클래스에는 <xref:System.Activities.Activity.Implementation%2A>을 사용하여 런타임에 의해 얻은 구현 자식 활동이 하나 있습니다. <xref:System.Activities.Activity>에서 파생되는 활동은 public 인수, public 변수, 가져온 ActivityDelegates 및 가져온 Activities를 정의할 수 있습니다.  
  
 가져온 ActivityDelegates 및 Activities는 활동의 public 자식으로 선언되지만 활동에서 직접 예약할 수는 없습니다. 이 정보는 유효성 검사 중에 활동이 실행되지 않는 위치에서 부모와 만나는 유효성 검사를 실행하지 않도록 방지하는 데 사용됩니다. public 자식과 마찬가지로 가져온 자식도 활동 구현에서 참조하고 예약할 수 있습니다. 즉, Activity1 활동을 가져오는 활동은 Activity1을 예약하는 구현에 <xref:System.Activities.Statements.Sequence>를 포함할 수 있습니다.  
  
#### <a name="codeactivity-asynccodeactivity"></a>CodeActivity/AsyncCodeActivity  
 이 기본 클래스는 명령적 코드로 동작을 작성하는 데 사용됩니다. 이 클래스에서 파생되는 활동은 해당 활동에서 노출하는 인수에 대한 액세스 권한만 가집니다. 즉, 이러한 활동에서 노출할 수 있는 멤버는 public 인수뿐입니다. 다른 멤버나 표시 유형은 이 활동에 적용되지 않습니다.  
  
#### <a name="summary-of-visibilities"></a>표시 유형 요약  
 다음 표에는 이 섹션의 앞부분에 있는 정보가 요약되어 있습니다.  
  
|멤버 형식|NativeActivity|활동|CodeActivity/AsyncCodeActivity|  
|-----------------|--------------------|--------------|--------------------------------------|  
|인수|Public/Private|Public|적용할 수 없음|  
|변수|Public/Private|Public|적용할 수 없음|  
|자식 활동|Public/Private|Public, Implementation에 정의된 하나의 고정된 private 자식입니다.|적용할 수 없음|  
|ActivityDelegates|Public/Private|Public|적용할 수 없음|  
  
 일반적으로 활동 소비자가 설정할 수 없는 멤버는 public으로 설정해서는 안 됩니다.  
  
### <a name="execution-properties"></a>실행 속성  
 특정 실행 속성의 범위를 활동의 public 자식으로 지정하는 것이 유용한 경우도 있습니다. <xref:System.Activities.ExecutionProperties> 컬렉션에서는 이 기능에 <xref:System.Activities.ExecutionProperties.Add%2A> 메서드를 제공합니다. 이 메서드에는 특정 속성의 범위가 모든 자식으로 지정되는지 public인 자식으로만 지정되는지를 나타내는 부울 매개 변수가 있습니다. 이 매개 변수를 `true`로 설정하면 public 멤버 및 public 자식의 public 멤버만 속성을 볼 수 있습니다.  
  
### <a name="secondary-roots"></a>보조 루트  
 보조 루트는 보정 활동의 상태를 관리하기 위한 런타임의 내부 메커니즘입니다. <xref:System.Activities.Statements.CompensableActivity>가 실행을 마치면 상태가 바로 정리되지 않습니다. 대신 보정 에피소드가 완료될 때까지 보조 루트의 런타임에서 상태를 유지 관리합니다. 보조 루트로 캡처된 위치 환경은 보정 가능한 활동이 사용되는 정의의 범위에 해당합니다.
