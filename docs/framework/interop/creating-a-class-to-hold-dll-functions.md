---
title: DLL 함수가 포함된 클래스 만들기
ms.date: 03/30/2017
helpviewer_keywords:
- COM interop, DLL functions
- unmanaged functions
- COM interop, platform invoke
- interoperation with unmanaged code, DLL functions
- interoperation with unmanaged code, platform invoke
- platform invoke, creating class for functions
- DLL functions
ms.assetid: e08e4c34-0223-45f7-aa55-a3d8dd979b0f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 275aa5bb664e9f5a50f44a72f2506d7984234b31
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051833"
---
# <a name="creating-a-class-to-hold-dll-functions"></a>DLL 함수가 포함된 클래스 만들기
자주 사용되는 DLL 함수를 관리되는 클래스로 래핑하는 것은 플랫폼 기능을 캡슐화하는 효과적인 방법입니다. 매번 래핑할 필요는 없지만 DLL 함수 정의는 번거롭고 오류가 발생할 수 있으므로 클래스 래퍼를 제공하는 것이 편리합니다. Visual Basic 또는 C#으로 프로그래밍할 경우 클래스 또는 Visual Basic 모듈 내에서 DLL 함수를 선언해야 합니다.  
  
 클래스 내에서 호출할 각 DLL 함수에 대한 정적 메서드를 정의합니다. 정의에는 메서드 인수를 전달하는 데 사용되는 문자 집합 또는 호출 규칙 같은 추가 정보가 포함될 수 있습니다. 이 정보를 생략하면 기본 설정을 선택합니다. 선언 옵션 및 기본 설정의 전체 목록을 보려면 [관리 코드에서 프로토타입 만들기](creating-prototypes-in-managed-code.md)를 참조하세요.  
  
 래핑되면 다른 클래스의 정적 메서드를 호출할 때 클래스의 메서드를 호출할 수 있습니다. 플랫폼 호출은 기본 내보낸 함수를 자동으로 처리합니다.  
  
 플랫폼 호출에 대한 관리되는 클래스를 디자인할 때 클래스와 DLL 함수 간 관계를 고려하세요. 예를 들어 다음 작업을 할 수 있습니다.  
  
- 기존 클래스 내에서 DLL 함수를 선언합니다.  
  
- 각 DLL 함수에 대한 개별 클래스를 만들어 함수를 격리하고 찾기 쉽게 유지합니다.  
  
- 관련 DLL 함수 집합에 대한 클래스 하나를 만들어 논리적 그룹화를 구성하고 오버헤드를 줄입니다.  
  
 원하는 대로 클래스 및 해당 메서드의 이름을 지정할 수 있습니다. 플랫폼 호출에서 사용되는 .NET 기반 선언을 생성하는 방법을 보여 주는 예제는 [플랫폼 호출을 사용하여 데이터 마샬링](marshaling-data-with-platform-invoke.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [관리되지 않는 DLL 함수 사용](consuming-unmanaged-dll-functions.md)
- [DLL 함수 식별](identifying-functions-in-dlls.md)
- [관리 코드에서 프로토타입 만들기](creating-prototypes-in-managed-code.md)
- [DLL 함수 호출](calling-a-dll-function.md)
