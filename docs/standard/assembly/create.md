---
title: 어셈블리 만들기
ms.date: 08/19/2019
helpviewer_keywords:
- assemblies [.NET Framework], multifile
- single-file assemblies
- assemblies [.NET Framework], creating
- multifile assemblies
ms.assetid: 54832ee9-dca8-4c8b-913c-c0b9d265e9a4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2dda45cca182d75bc77916cdf862ada9faead9ec
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972764"
---
# <a name="create-assemblies"></a>어셈블리 만들기

Visual Studio 등의 IDE 또는 Windows SDK에서 제공된 컴파일러와 도구를 사용하여 단일 파일 또는 다중 파일 어셈블리를 만들 수 있습니다. 가장 단순한 어셈블리는 간단한 이름을 가지고 단일 애플리케이션 도메인에 로드되는 단일 파일입니다. 이 어셈블리는 애플리케이션 디렉터리 외부에 있는 다른 어셈블리가 참조할 수 없고 버전 확인이 진행되지 않습니다. 어셈블리로 구성된 애플리케이션을 제거하려면 어셈블리가 있는 디렉터리를 삭제하면 됩니다. 대부분 개발자의 경우 애플리케이션을 배포하는 데는 이러한 기능이 포함된 어셈블리만 있으면 됩니다.

여러 코드 모듈 및 리소스 파일에서 복수 파일 어셈블리를 만들 수 있습니다. 여러 애플리케이션에서 공유될 수 있는 어셈블리를 만들 수도 있습니다. 공유 어셈블리에는 강력한 이름이 있어야 하고 공유 어셈블리는 전역 어셈블리 캐시에 배포될 수 있습니다.

코드 모듈 및 리소스를 어셈블리로 그룹화할 경우 다음 요소에 따라 여러 가지 옵션이 있습니다.

- 버전 관리

     같은 버전 정보를 포함해야 하는 모듈을 그룹화합니다.

- 배포

     배포 모델을 지원하는 코드 모듈 및 리소스를 그룹화합니다.

- 재사용

     몇 가지 목적으로 모듈이 논리적으로 함께 사용될 수 있는 경우 모듈을 그룹화합니다. 예를 들어 가끔 프로그램 유지 관리에 사용되는 형식 및 클래스로 구성되는 어셈블리는 같은 어셈블리에 포함될 수 있습니다. 또한 여러 애플리케이션과 공유하려는 형식은 어셈블리로 그룹화되어야 하고 해당 어셈블리는 강력한 이름으로 서명되어야 합니다.

- 보안

     같은 보안 권한이 필요한 형식이 포함된 모듈을 그룹화합니다.

- 범위 지정

     표시 유형을 같은 어셈블리로 제한해야 하는 형식이 포함된 모듈을 그룹화합니다.

공용 언어 런타임 어셈블리를 비관리 COM 애플리케이션에서 사용할 수 있도록 하려면 특별히 고려해야 할 사항이 있습니다. 비관리 코드 사용에 대한 자세한 내용은 [.NET Framework 구성 요소를 COM에 노출](../../framework/interop/exposing-dotnet-components-to-com.md)을 참조하세요.

## <a name="see-also"></a>참고 항목

- [어셈블리를 사용한 프로그램](program.md)
- [어셈블리 버전 관리](versioning.md)
- [방법: 단일 파일 어셈블리 빌드](../../framework/app-domains/build-single-file-assembly.md)
- [방법: 다중 파일 어셈블리 빌드](../../framework/app-domains/build-multifile-assembly.md)
- [런타임에서 어셈블리를 찾는 방법](../../framework/deployment/how-the-runtime-locates-assemblies.md)
- [다중 파일 어셈블리](../../framework/app-domains/multifile-assemblies.md)
