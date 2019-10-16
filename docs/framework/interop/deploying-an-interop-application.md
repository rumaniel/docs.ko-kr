---
title: Interop 애플리케이션 배포
ms.date: 03/30/2017
helpviewer_keywords:
- deploying applications [.NET Framework], interop
- strong-named assemblies, interop applications
- unsigned assemblies
- private assemblies
- exposing COM components to .NET Framework
- interoperation with unmanaged code, deploying applications
- shared assemblies
- COM interop, deploying applications
- interoperation with unmanaged code, exposing COM components
- signed assemblies
- COM interop, exposing COM components
ms.assetid: ea8a403e-ae03-4faa-9d9b-02179ec72992
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 080ef48ade496a55f414b64158a40fe0e551c2aa
ms.sourcegitcommit: 29a9b29d8b7d07b9c59d46628da754a8bff57fa4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2019
ms.locfileid: "69567291"
---
# <a name="deploying-an-interop-application"></a>Interop 애플리케이션 배포
Interop 애플리케이션에는 일반적으로 .NET 클라이언트 어셈블리, 고유한 COM 형식 라이브러리를 나타내는 하나 이상의 interop 어셈블리 및 하나 이상의 등록된 COM 구성 요소가 포함됩니다. Visual Studio 및 Windows SDK에서는 [형식 라이브러리를 어셈블리로 가져오기](importing-a-type-library-as-an-assembly.md)에 설명된 대로 형식 라이브러리를 interop 어셈블리로 가져오고 변환하는 도구를 제공합니다. Interop 애플리케이션을 배포하는 두 가지 방법은 다음과 같습니다.  
  
- 포함된 interop 형식 사용: .NET Framework 4부터 interop 어셈블리의 형식 정보를 실행 파일에 포함하도록 컴파일러에 지시할 수 있습니다. 컴파일러는 애플리케이션에서 사용하는 형식 정보만 포함합니다. Interop 어셈블리를 애플리케이션에 배포할 필요는 없습니다. 이것이 권장되는 방법입니다.  
  
- Interop 어셈블리 배포: interop 어셈블리에 대한 표준 참조를 만들 수 있습니다. 이 경우 interop 어셈블리를 애플리케이션에 배포해야 합니다. 이 방법을 적용하는데 전용 COM 구성 요소를 사용하지 않을 경우 관리 코드에 통합하려는 COM 구성 요소의 작성자가 게시한 PIA(주 interop 어셈블리)를 항상 참조하세요. 주 interop 어셈블리를 생성 및 사용하는 방법에 대한 자세한 내용은 [주 Interop 어셈블리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aax7sdch(v=vs.100))를 참조하세요.  
  
 포함된 interop 형식을 사용할 경우 배포는 간단하고 직관적입니다. 특별히 수행할 작업이 없습니다. 이 문서의 나머지 부분에서는 애플리케이션에 interop 어셈블리를 배포하기 위한 시나리오를 설명합니다.  
  
## <a name="deploying-interop-assemblies"></a>Interop 어셈블리 배포  
 어셈블리는 강력한 이름을 가질 수 있습니다. 강력한 이름의 어셈블리에는 고유한 ID를 제공하는 게시자의 공개 키가 포함됩니다. [형식 라이브러리 가져오기(Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md)에서 생성되는 어셈블리는 게시자가 **/keyfile** 옵션을 사용하여 서명할 수 있습니다. 서명된 어셈블리를 전역 어셈블리 캐시에 설치할 수 있습니다. 서명되지 않은 어셈블리는 사용자 컴퓨터에 프라이빗 어셈블리로 설치해야 합니다.  
  
### <a name="private-assemblies"></a>프라이빗 어셈블리  
 전용으로 사용할 어셈블리를 설치하려면 애플리케이션 실행 파일과 가져온 COM 형식을 포함하는 interop 어셈블리가 둘 다 동일한 디렉터리 구조에 설치되어야 합니다. 다음 그림에서는 개별 애플리케이션 디렉터리에 있는 Client1.exe 및 Client2.exe에서 전용으로 사용할 서명되지 않은 interop 어셈블리를 보여 줍니다. 이 예제에서 LOANLib.dll이라는 interop 어셈블리는 두 번 설치됩니다.  
  
 ![디렉터리 구조 및 Windows 레지스트리](./media/deploying-an-interop-application/com-private-deployment.gif "전용 배포에 대한 디렉터리 구조 및 레지스트리 항목")  
  
 애플리케이션과 연결된 모든 COM 구성 요소는 Windows 레지스트리에 설치해야 합니다. 그림의 Client1.exe 및 Client2.exe가 서로 다른 컴퓨터에 설치된 경우에는 두 컴퓨터에 모두 COM 구성 요소를 등록해야 합니다.  
  
### <a name="shared-assemblies"></a>공유 어셈블리  
 여러 애플리케이션에서 공유되는 어셈블리는 전역 어셈블리 캐시라는 중앙 집중식 리포지토리에 설치해야 합니다. .NET 클라이언트는 전역 어셈블리 캐시에서 시그니처 및 설치된 interop 어셈블리의 동일한 복사본에 액세스할 수 있습니다. 주 interop 어셈블리를 생성 및 사용하는 방법에 대한 자세한 내용은 [주 Interop 어셈블리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aax7sdch(v=vs.100))를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [.NET Framework에 COM 구성 요소 노출](exposing-com-components.md)
- [형식 라이브러리를 어셈블리로 가져오기](importing-a-type-library-as-an-assembly.md)
- [관리 코드에서 COM 형식 사용](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3y76b69k(v=vs.100))
- [Interop 프로젝트 컴파일](compiling-an-interop-project.md)
