---
title: DLL 함수 호출
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged functions, calling
- unmanaged functions
- COM interop, platform invoke
- platform invoke, calling unmanaged functions
- interoperation with unmanaged code, platform invoke
- DLL functions
ms.assetid: 113646de-7ea0-4f0e-8df0-c46dab3e8733
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b842f44711d38a996b9d710dbe8bd369d30c5443
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051878"
---
# <a name="calling-a-dll-function"></a>DLL 함수 호출
관리되지 않는 DLL 함수 호출은 다른 관리 코드 호출과 거의 동일하지만 처음에 DLL 함수를 혼동하게 만드는 차이점이 있습니다. 이 섹션에서는 몇 가지 비정상적인 호출 관련 문제를 설명하는 항목을 소개합니다.  
  
 플랫폼 호출에서 반환되는 구조는 관리 코드와 비관리 코드에 동일한 표현이 있는 데이터 형식이어야 합니다. 이러한 형식은 변환이 필요하지 않으므로 *blittable 형식*이라고 합니다([blittable 형식 및 비 Blittable 형식](blittable-and-non-blittable-types.md) 참조). 비 blittable 구조를 반환 형식으로 사용하는 함수를 호출하려면 비 blittable 형식과 동일한 크기의 blittable 도우미 형식을 정의하고 함수가 반환된 후 데이터를 변환합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [구조체 전달](passing-structures.md)  
 미리 정의된 레이아웃으로 데이터 구조를 전달하는 문제를 식별합니다.  
  
 [콜백 함수](callback-functions.md)  
 콜백 함수에 대한 기본 정보를 제공합니다.  
  
 [방법: 콜백 함수 구현](how-to-implement-callback-functions.md)  
 관리 코드에서 콜백 함수를 구현하는 방법을 설명합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [관리되지 않는 DLL 함수 사용](consuming-unmanaged-dll-functions.md)  
 플랫폼 호출을 사용하여 관리되지 않는 DLL 함수를 호출하는 방법을 설명합니다.  
  
 [플랫폼 호출을 사용하여 데이터 마샬링](marshaling-data-with-platform-invoke.md)  
 메서드 매개 변수를 선언하고 관리되지 않는 라이브러리에서 내보낸 함수에 인수를 전달하는 방법을 설명합니다.
