---
title: Microsoft.VisualStudio.Activities.Asr.ClientActivityBuilder..ctor
ms.date: 03/30/2017
ms.topic: reference
api_name:
- Microsoft.VisualStudio.Activities.Asr.ClientActivityBuilder..ctor
api_location:
- Microsoft.VisualStudio.Activities.dll
api_type:
- Assembly
ms.assetid: 6b44b13c-7a23-4df2-8f9f-45e2b1430002
ms.openlocfilehash: 99f2eb9447bdf43cb57cfe86f35d2c09044ed470
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69947622"
---
# <a name="microsoftvisualstudioactivitiesasrclientactivitybuilderctor"></a>Microsoft.VisualStudio.Activities.Asr.ClientActivityBuilder..ctor
[VisualStudio](microsoft-visualstudio-activities-asr-clientactivitybuilder.md) 의 인스턴스를 만듭니다 .이 클래스의 인스턴스를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```csharp  
public ClientActivityBuilder(OperationDescription operationDescription, string configurationName, string proxyNamespace);  
```  
  
## <a name="parameters"></a>매개 변수  
  
## <a name="parameter-values"></a>매개 변수 값  
 *operationDescription*  
  
 : 작업 이름, 반환 형식 및 매개 변수 정보를 비롯하여 생성되는 워크플로 활동에서 수행될 작업에 대해 설명합니다. 이 매개 변수 값은 **null**이 아니어야 합니다. 메시지 계약을 사용하고 한 메시지에 인수를 사용하는 동기 작업을 설명해야 합니다. 이러한 조건이 충족되지 않으면 생성자 및 이 클래스의 기타 메서드를 사용한 런타임 결과는 정의되지 않습니다.  
  
 *configurationName*  
  
 : 엔드포인트 구성 이름을 지정합니다. 이 매개 변수 값은 **null** 이거나 비워 둘 수 없습니다. 이러한 조건이 충족되지 않으면 생성자 및 이 클래스의 기타 메서드를 사용한 런타임 결과는 정의되지 않습니다.  
  
 *proxyNamespace*  
  
 : 작업의 서비스 네임스페이스를 지정합니다. 이 매개 변수 값은 **null** 이거나 비워 둘 수 없습니다. 이러한 조건이 충족되지 않으면 생성자 및 이 클래스의 기타 메서드를 사용한 런타임 결과는 정의되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [Microsoft.VisualStudio.Activities.Asr.ClientActivityBuilder](microsoft-visualstudio-activities-asr-clientactivitybuilder.md)
