---
title: 어셈블리 및 전역 어셈블리 캐시 사용
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- global assembly cache, benefits
- ACLs [.NET Framework]
- GAC (global assembly cache), benefits
- access control lists [.NET Framework]
ms.assetid: 8a18e5c2-d41d-49ef-abcb-7c27e2469433
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0331e0ad30743d5f0bba125e8e61e636e1c2a5be
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053020"
---
# <a name="working-with-assemblies-and-the-global-assembly-cache"></a>어셈블리 및 전역 어셈블리 캐시 사용

여러 애플리케이션에서 어셈블리를 공유하려면 어셈블리를 전역 어셈블리 캐시에 설치하면 됩니다. 공용 언어 런타임이 설치된 각 컴퓨터에는 이 컴퓨터 수준의 코드 캐시가 있습니다. 전역 어셈블리 캐시에는 컴퓨터의 여러 애플리케이션에서 공유하도록 특별히 지정된 어셈블리가 저장됩니다. 전역 어셈블리 캐시에 설치하려면 어셈블리에 강력한 이름이 있어야 합니다.  
  
> [!NOTE]
> 전역 어셈블리 캐시에 배치된 어셈블리에는 같은 어셈블리 이름과 파일 이름(파일 이름 확장명 제외)이 있어야 합니다. 예를 들어 어셈블리 이름이 myAssembly인 어셈블리의 파일 이름은 myAssembly.exe 또는 myAssembly.dll이어야 합니다.  
  
필요할 경우에만 어셈블리를 전역 어셈블리 캐시에 설치하여 어셈블리를 공유해야 합니다. 일반적으로 어셈블리 공유가 명시적으로 필요하지 않은 경우에는 어셈블리 종속성은 pirvate으로 유지하고 어셈블리를 애플리케이션 디렉터리에 저장해야 합니다. 또한 어셈블리가 COM interop 또는 비관리 코드에 액세스 가능하게 설정하기 위해 어셈블리를 전역 어셈블리 캐시에 설치할 필요는 없습니다.  
  
어셈블리를 전역 어셈블리 캐시에 설치해야 하는 몇 가지 이유는 다음과 같습니다.  
  
- 공유된 위치.  
  
     애플리케이션에서 사용해야 하는 어셈블리는 전역 어셈블리 캐시에 포함될 수 있습니다. 예를 들어 모든 애플리케이션에서 전역 어셈블리 캐시에 있는 어셈블리를 사용해야 하는 경우 버전 정책 설명을 Machine.config 파일에 추가하여 참조를 어셈블리로 리디렉션할 수 있습니다.  
  
- 파일 보안.  
  
     관리자는 대부분 쓰기 및 실행 액세스를 제어하기 위해 ACL(액세스 제어 목록)을 사용하여 systemroot 디렉터리를 보호합니다. 전역 어셈블리 캐시는 systemroot 디렉터리에 설치되므로 해당 디렉터리의 ACL을 상속합니다. 관리자 권한을 가진 사용자만 전역 어셈블리 캐시에서 파일을 삭제하도록 허용하는 것이 좋습니다.  
  
- Side-by-side 버전 관리.  
  
     이름이 같지만 버전 정보가 서로 다른 여러 어셈블리 복사본을 전역 어셈블리 캐시에서 유지 관리할 수 있습니다.  
  
- 추가 검색 위치.  
  
     공용 언어 런타임은 구성 파일에서 코드베이스 정보를 검색 또는 사용하기 전에 어셈블리 요청과 일치하는 어셈블리가 전역 어셈블리 캐시에 있는지 확인합니다.  
  
 어셈블리를 전역 어셈블리 캐시에 명시적으로 설치하지 않으려고 하는 시나리오가 있습니다. 애플리케이션을 구성하는 어셈블리 중 하나를 전역 어셈블리 캐시에 배치하면 XCOPY를 사용하여 애플리케이션 디렉터리를 복사하는 방식으로 애플리케이션을 더 이상 복제하거나 설치할 수 없습니다. 이 경우 어셈블리를 전역 어셈블리 캐시로 이동해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
[방법: 글로벌 어셈블리 캐시에 어셈블리 설치](install-assembly-into-gac.md)  
어셈블리를 전역 어셈블리 캐시에 설치하는 방법을 설명합니다.  
  
[방법: 글로벌 어셈블리 캐시의 내용 보기](how-to-view-the-contents-of-the-gac.md)  
[Gacutil.exe(전역 어셈블리 캐시 도구)](../tools/gacutil-exe-gac-tool.md)를 사용하여 전역 어셈블리 캐시의 콘텐츠를 보는 방법을 설명합니다.  
  
[방법: 글로벌 어셈블리 캐시에서 어셈블리 제거](how-to-remove-an-assembly-from-the-gac.md)  
[Gacutil.exe(전역 어셈블리 캐시 도구)](../tools/gacutil-exe-gac-tool.md)를 사용하여 전역 어셈블리 캐시에서 어셈블리를 제거하는 방법을 설명합니다.  
  
[전역 어셈블리 캐시에서 서비스되는 구성 요소 사용](use-serviced-components-with-the-gac.md)  
서비스되는 구성 요소(관리되는 COM+ 구성 요소)를 전역 어셈블리 캐시에 배치하는 이유를 설명합니다.  
  
## <a name="related-sections"></a>관련 단원  

[어셈블리 만들기](../../standard/assembly/create.md)  
어셈블리 만들기에 대해 간략하게 설명합니다.  
  
[전역 어셈블리 캐시](gac.md)  
전역 어셈블리 캐시를 설명합니다.  
  
[방법: 어셈블리 콘텐츠 보기](../../standard/assembly/view-contents.md)  
[Ildasm.exe(IL 디스어셈블러)](../tools/ildasm-exe-il-disassembler.md)를 사용하여 어셈블리의 MSIL(Microsoft Intermediate Language) 정보를 보는 방법을 설명합니다.  
  
[런타임에서 어셈블리를 찾는 방법](../deployment/how-the-runtime-locates-assemblies.md)  
공용 언어 런타임이 애플리케이션을 구성하는 어셈블리를 찾고 로드하는 방법을 설명합니다.  
  
[어셈블리를 사용한 프로그래밍](../../standard/assembly/program.md)  
관리되는 애플리케이션의 빌드 블록인 어셈블리를 설명합니다.
