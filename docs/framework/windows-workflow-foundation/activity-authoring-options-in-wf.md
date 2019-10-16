---
title: WF의 활동 제작 옵션
ms.date: 03/30/2017
ms.assetid: b9061f5f-12c3-47f0-adbe-1330e2714c94
ms.openlocfilehash: 219d759cd1390a83abfb90af509b21047085f6e9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61774233"
---
# <a name="activity-authoring-options-in-wf"></a>WF의 활동 제작 옵션
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]은 사용자 지정 활동을 만들기 위한 여러 옵션을 보여 줍니다. 지정한 활동을 작성하는 데 사용할 올바른 방법은 필요한 런타임 기능에 따라 결정됩니다.  
  
## <a name="deciding-which-base-activity-class-to-use-for-authoring-custom-activities"></a>사용자 지정 활동을 작성하는 데 사용할 기본 활동 클래스 결정  
 다음 표에서는 사용자 지정 활동 기본 클래스에서 사용할 수 있는 기능을 보여 줍니다.  
  
|기본 활동 클래스|사용 가능한 기능|  
|-------------------------|------------------------|  
|<xref:System.Activities.Activity>|시스템 제공 활동 그룹과 사용자 지정 활동 그룹을 복합 활동으로 작성합니다.|  
|<xref:System.Activities.CodeActivity>|재정의할 수 있는 <xref:System.Activities.CodeActivity%601.Execute%2A> 메서드를 제공하여 명령형 기능을 구현합니다. 추적, 변수 및 인수에 액세스할 수도 있습니다.|  
|<xref:System.Activities.NativeActivity>|<xref:System.Activities.CodeActivity>의 모든 기능과 활동 실행 중단, 자식 활동 실행 취소, 책갈피 사용, 활동 예약, 활동 작업 및 기능을 제공합니다.|  
|<xref:System.Activities.DynamicActivity>|<xref:System.ComponentModel.ICustomTypeDescriptor>를 통해 WF 디자이너 및 런타임 컴퓨터와 인터페이스하는 활동을 DOM 방식으로 만들어 새 형식을 정의하지 않고 새 활동을 만들 수 있습니다.|  
  
## <a name="authoring-activities-using-activity"></a>활동을 사용하여 활동 작성  
 <xref:System.Activities.Activity>에서 파생되는 활동은 다른 기존 활동을 어셈블하여 기능을 작성합니다. 이 활동은 기존의 사용자 지정 활동 및 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 활동 라이브러리의 활동일 수 있습니다. 이 활동을 어셈블하는 것은 사용자 지정 기능을 만드는 가장 기본적인 방법입니다. 이 방법은 시각적 디자인 환경을 사용하여 워크플로를 작성할 때 가장 일반적으로 사용됩니다.  
  
## <a name="authoring-activities-using-codeactivity-or-asynccodeactivity"></a>CodeActivity 또는 AsyncCodeActivity를 사용하여 활동 작성  
 <xref:System.Activities.CodeActivity> 또는 <xref:System.Activities.AsyncCodeActivity>에서 파생되는 활동은 사용자 지정 명령적 코드로 <xref:System.Activities.CodeActivity%601.Execute%2A> 메서드를 재정의하여 명령형 기능을 구현합니다. 런타임에서 활동이 실행될 때 사용자 지정 코드가 실행됩니다. 이 방법으로 만든 활동은 사용자 지정 기능에 액세스할 수 있지만, 실행 환경에 완전히 액세스하거나 자식 작업을 예약하는 기능, 책갈피 만들기, Cancel 또는 Abort 메서드에 대한 지원 등 런타임의 모든 기능에 액세스할 수 있는 것은 아닙니다. <xref:System.Activities.CodeActivity>가 실행되면 이 활동은 축소된 버전의 실행 환경에 액세스할 수 있습니다(<xref:System.Activities.CodeActivityContext> 또는 <xref:System.Activities.AsyncCodeActivityContext> 클래스 이용). <xref:System.Activities.CodeActivity>를 사용하여 만든 활동은 인수 및 변수 확인, 확장명 및 추적에 액세스할 수 있습니다. <xref:System.Activities.AsyncCodeActivity>를 사용하여 비동기 활동 예약을 수행할 수 있습니다.  
  
## <a name="authoring-activities-using-nativeactivity"></a>NativeActivity를 사용하여 활동 작성  
 <xref:System.Activities.NativeActivity>에서 파생되는 활동과 같이 <xref:System.Activities.CodeActivity>에서 파생되는 활동은 <xref:System.Activities.NativeActivity.Execute%2A>를 재정의하여 명령형 기능을 만들지만, <xref:System.Activities.NativeActivityContext> 메서드에 전달되는 <xref:System.Activities.NativeActivity.Execute%2A>를 통해 워크플로 런타임의 모든 기능에 액세스할 수도 있습니다. 이 컨텍스트에서는 자식 활동 예약 및 취소, <xref:System.Activities.ActivityAction> 및 <xref:System.Activities.ActivityFunc%601> 개체 실행, 워크플로로 트랜잭션을 이동, 비동기 프로세스 호출, 실행 취소와 중단, 실행 속성과 확장에 대한 액세스 및 책갈피(일시 중지된 워크플로를 다시 시작하기 위한 핸들)를 지원합니다.  
  
## <a name="authoring-activities-using-dynamicactivity"></a>DynamicActivity를 사용하여 활동 작성  
 다른 세 가지 활동 형식과 달리, <xref:System.Activities.DynamicActivity>(클래스 봉인됨)에서 새 형식을 파생하는 것이 아니라 활동 DOM(문서 개체 모델)을 사용하여 <xref:System.Activities.DynamicActivity.Properties%2A> 및 <xref:System.Activities.DynamicActivity.Implementation%2A> 속성에 기능을 어셈블하는 방법으로 새 기능을 만듭니다.  
  
## <a name="authoring-activities-that-return-a-result"></a>결과를 반환하는 활동 작성  
 대부분의 활동은 실행 후 결과를 반환해야 합니다. 이를 위해 언제든지 사용자 지정 <xref:System.Activities.OutArgument%601>을 활동에 정의할 수 있지만, 그 대신 <xref:System.Activities.Activity%601>을 사용하거나 <xref:System.Activities.CodeActivity%601> 또는 <xref:System.Activities.NativeActivity%601>에서 파생시켜도 됩니다. 각 기본 클래스에는 활동의 값 반환에 사용할 수 있는 Result라는 이름의 <xref:System.Activities.OutArgument%601>이 있습니다. 결과를 반환하는 활동은 한 활동에서 한 가지 결과만 반환해야 하거나, 여러 결과를 반환해야 하거나, 대신 별도의 <xref:System.Activities.OutArgument%601> 멤버를 사용해야 하는 경우에만 사용해야 합니다.
