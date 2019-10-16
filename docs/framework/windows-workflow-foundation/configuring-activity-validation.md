---
title: 활동 유효성 검사 구성
ms.date: 03/30/2017
ms.assetid: 25a4eccb-b8fc-4857-a01d-2683b6341219
ms.openlocfilehash: 6c971b56e269fbb330bd9ad0a551a9fb9ca01196
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64655110"
---
# <a name="configuring-activity-validation"></a>활동 유효성 검사 구성
활동 유효성 검사를 사용하면 활동 작성자 및 사용자가 활동을 실행하기 이전에 활동 구성 오류를 식별하여 보고할 수 있습니다. Windows WF (Workflow Foundation)는 다음 세 가지 유형의 활동 유효성 검사를 제공합니다.  
  
- `RequiredArgument` 및 `OverloadGroup` 특성  
  
- 필수 코드 기반 유효성 검사  
  
- 선언적 제약 조건  
  
 `RequiredArgument` 및 `OverloadGroup` 특성은 활동의 특정 인수가 필수 항목임을 나타냅니다. 필수 코드 기반 유효성 검사를 사용하면 활동 자체에 대한 유효성을 쉽게 검사할 수 있고, 선언적 제약 조건을 사용하면 활동 및 활동과 포함된 워크플로와의 관계에 대한 유효성을 검사할 수 있습니다. 활동이 유효성 검사 요구 사항에 따라 적절하게 구성되지 않은 경우 유효성 검사 오류 및 경고가 반환됩니다. Workflow Designer를 사용하여 포함된 워크플로를 만드는 경우에는 유효성 검사 오류 및 경고가 디자이너에 표시됩니다. 워크플로 디자이너 외부에서 워크플로를 만드는 경우에는 워크플로가 호출되면 유효성 검사 오류가 반환됩니다. 워크플로를 만드는 방법에 상관없이 유효성 검사 오류가 있는 워크플로는 실행할 수 없습니다. 이 단원에서는 이러한 유형의 활동 유효성 검사의 개요와 활동 유효성 검사를 호출하는 방법을 간략하게 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [필수 인수 및 오버로드 그룹](required-arguments-and-overload-groups.md)  
 `RequiredArgument` 및 `OverloadGroup` 특성을 사용하여 유효성 검사를 수행하는 방법에 대해 설명합니다.  
  
 [명령형 코드 기반 유효성 검사](imperative-code-based-validation.md)  
 <xref:System.Activities.CodeActivity> 및 <xref:System.Activities.NativeActivity> 기반 활동에 대해 코드 기반 유효성 검사를 사용하는 방법에 대해 설명합니다.  
  
 [선언적 제약 조건](declarative-constraints.md)  
 선언적 제약 조건을 사용하여 복잡한 활동 유효성 검사를 수행하는 방법에 대해 설명합니다.  
  
 [활동 유효성 검사 호출](invoking-activity-validation.md)  
 활동 유효성 검사가 자동으로 호출되는 시기와 유효성 검사를 명시적으로 호출하는 방법에 대해 설명합니다.  
  
## <a name="reference"></a>참조  
  
## <a name="related-sections"></a>관련 단원
