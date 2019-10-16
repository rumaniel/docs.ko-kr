---
title: 비관리 코드와의 상호 운용
ms.date: 01/17/2018
helpviewer_keywords:
- unmanaged code, interoperation
- managed code, interoperation with unmanaged code
- .NET Framework, interoperation with unmanaged code
- unmanaged code
- interoperation with unmanaged code
- interoperation with unmanaged code, about interoperation
- components [.NET Framework], interoperation with unmanaged code
ms.assetid: ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: edec95ea729fdf26e384b6658c241ca307e60851
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61643116"
---
# <a name="interoperating-with-unmanaged-code"></a>비관리 코드와의 상호 운용

.NET Framework를 기반으로 COM 구성 요소, COM+ 서비스, 외부 형식 라이브러리 및 여러 가지 운영 체제 서비스와 상호 작용할 수 있습니다. 관리 개체 모델과 관리되지 않는 개체 모델 간에는 데이터 형식, 메서드 시그니처 및 오류 처리 메커니즘이 달라집니다. .NET Framework 구성 요소와 비관리 코드 간에 상호 운용을 간소화하고 마이그레이션 경로를 줄이기 위해 공용 언어 런타임은 클라이언트 및 서버에서 둘 다 이러한 개체 모델의 차이점을 숨깁니다.

런타임 제어를 기반으로 실행되는 코드를 관리 코드라고 합니다. 이와 달리 런타임 외부에서 실행되는 코드를 비관리 코드라고 합니다. 비관리 코드로는 COM 구성 요소, ActiveX 인터페이스, Windows API 함수 등이 있습니다.

## <a name="in-this-section"></a>단원 내용

[.NET Framework에 COM 구성 요소 노출](exposing-com-components.md)  
.NET Framework 애플리케이션에서 COM 구성 요소를 사용하는 방법을 설명합니다.

[.NET Framework 구성 요소를 COM에 노출](exposing-dotnet-components-to-com.md)  
COM 애플리케이션에서 .NET Framework 구성 요소를 사용하는 방법을 설명합니다.

[관리되지 않는 DLL 함수 사용](consuming-unmanaged-dll-functions.md)  
플랫폼 호출을 사용하여 관리되지 않는 DLL 함수를 호출하는 방법을 설명합니다.

[interop 마샬링](interop-marshaling.md)  
COM interop 및 플랫폼 호출에 대한 마샬링을 설명합니다.

[방법: HRESULT 및 예외 매핑](how-to-map-hresults-and-exceptions.md)  
실행과 HRESULT 간 매핑을 설명합니다.

[COM 래퍼](com-wrappers.md)  
COM interop에서 제공하는 래퍼에 대해 설명합니다.

[동일 형식 및 포함된 Interop 형식](type-equivalence-and-embedded-interop-types.md)  
COM 형식에 대한 형식 정보가 어셈블리에 포함되는 방식과 공용 언어 런타임에서 포함된 COM 형식이 동일한지 결정하는 방법을 설명합니다.

[방법: Tlbimp.exe를 사용하여 주 Interop 어셈블리 생성](how-to-generate-primary-interop-assemblies-using-tlbimp-exe.md)  
*Tlbimp.exe*(형식 라이브러리 가져오기)를 사용하여 주 interop 어셈블리를 생성하는 방법에 대해 설명합니다.

[방법: 주 Interop 어셈블리 등록](how-to-register-primary-interop-assemblies.md)  
주 interop 어셈블리를 프로젝트에서 참조할 수 있도록 등록하는 방법에 대해 설명합니다.

[등록이 필요 없는 COM interop](registration-free-com-interop.md)  
COM interop에서 Windows 레지스트리를 사용하지 않고 구성 요소를 활성화하는 방법에 대해 설명합니다.

[방법: 등록이 필요 없는 활성화를 위한 .NET Framework 기반 COM 구성 요소 구성](configure-net-framework-based-com-components-for-reg.md)  
애플리케이션 매니페스트를 만드는 방법과 구성 요소 매니페스트를 만들고 포함하는 방법에 대해 설명합니다.
