---
title: 최선의 어셈블리 로드 방법
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies,binding
- LoadFrom method
- default load context
- TypeLoadException class,causes
- assembly loading errors
- load contexts
- assemblies,loading
- LoadWithPartialName method
- load-from context
ms.assetid: 68d1c539-6a47-4614-ab59-4b071c9d4b4c
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9c43f75dc17d49fe34094829387673b0f1f1d028
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50201584"
---
# <a name="best-practices-for-assembly-loading"></a>최선의 어셈블리 로드 방법
이 문서에서는 <xref:System.InvalidCastException>, <xref:System.MissingMethodException> 및 다른 오류를 발생시킬 수 있는 형식 ID 문제를 방지하는 방법을 설명합니다. 이 문서에서는 다음 권장 사항을 설명합니다.  
  
-   [로드 컨텍스트의 장점 및 단점 이해](#load_contexts)  
  
-   [부분 어셈블리 이름에 대한 바인딩 방지](#avoid_partial_names)  
  
-   [여러 컨텍스트에 어셈블리 로드 방지](#avoid_loading_into_multiple_contexts)  
  
-   [같은 컨텍스트에 어셈블리의 여러 버전 로드 방지](#avoid_loading_multiple_versions)  
  
-   [기본 로드 컨텍스트로 전환 고려](#switch_to_default)  
  
 첫 번째 권장 사항인 [로드 컨텍스트의 장점 및 단점 이해](#load_contexts)에서는 다른 권장 사항에 대한 배경 정보를 제공합니다. 그 이유는 권장 사항은 모두 로드 컨텍스트의 지식에 의존하기 때문입니다.  
  
<a name="load_contexts"></a>   
## <a name="understand-the-advantages-and-disadvantages-of-load-contexts"></a>로드 컨텍스트의 장점 및 단점 이해  
 응용 프로그램 도메인 내에서 어셈블리는 세 개의 컨텍스트 중 하나로 로드되거나 컨텍스트 없이 로드될 수 있습니다.  
  
-   기본 로드 컨텍스트에는 전역 어셈블리 캐시, 런타임이 호스트된 경우 호스트 어셈블리 저장소(예: SQL Server에서), 응용 프로그램 도메인의 <xref:System.AppDomainSetup.ApplicationBase%2A> 및 <xref:System.AppDomainSetup.PrivateBinPath%2A>를 검색하여 찾은 어셈블리가 포함됩니다. <xref:System.Reflection.Assembly.Load%2A> 메서드의 대부분 오버로드는 어셈블리 이 컨텍스트에 로드합니다.  
  
-   로드 소스 컨텍스트에는 로더를 통해 검색되지 않은 위치에서 로드된 어셈블리가 포함됩니다. 예를 들어 추가 기능은 응용 프로그램 경로 아래에 없는 디렉터리에 설치될 수 있습니다. <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType>, <xref:System.AppDomain.CreateInstanceFrom%2A?displayProperty=nameWithType> 및 <xref:System.AppDomain.ExecuteAssembly%2A?displayProperty=nameWithType>는 경로로 로드되는 메서드의 예제입니다.  
  
-   리플렉션 전용 컨텍스트에는 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A> 및 <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A> 메서드를 사용하여 로드되는 어셈블리가 포함됩니다. 이 컨텍스트의 코드는 실행될 수 없으므로 여기서 설명하지 않습니다. 자세한 내용은 [방법: 리플렉션 전용 컨텍스트에 어셈블리 로드](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)를 참조하세요.  
  
-   리플렉션 내보내기를 사용하여 임시 동적 어셈블리를 생성한 경우 이 어셈블리는 컨텍스트에 포함되지 않습니다. 또한 <xref:System.Reflection.Assembly.LoadFile%2A> 메서드를 사용하여 로드된 대부분 어셈블리는 컨텍스트 없이 로드되고, 바이트 배열에서 로드된 어셈블리는 전역 어셈블리 캐시에 포함되도록 해당 ID(정책이 적용된 후)에 설정된 경우가 아니면 컨텍스트 없이 로드됩니다.  
  
 실행 컨텍스트에는 다음 섹션에서 설명된 장점과 단점이 있습니다.  
  
### <a name="default-load-context"></a>기본 로드 컨텍스트  
 어셈블리가 기본 로드 컨텍스트에 로드되면 해당 종속성은 자동으로 로드됩니다. 기본 로드 컨텍스트 또는 로드 소스 컨텍스트의 어셈블리의 경우 기본 로드 컨텍스트에 로드된 종속성은 자동으로 발견됩니다. 어셈블리 ID로 로드하면 알 수 없는 버전의 어셈블리가 사용되지 않았는지 확인되므로 응용 프로그램의 안정성이 증가합니다([부분 어셈블리 이름에 대한 바인딩 방지](#avoid_partial_names) 섹션 참조).  
  
 기본 로드 컨텍스트 사용에는 다음과 같은 단점이 있습니다.  
  
-   다른 컨텍스트에 로드된 종속성은 사용할 수 없습니다.  
  
-   검색 경로 외부의 위치에서 기본 로드 컨텍스트로 어셈블리를 로드할 수는 없습니다.  
  
### <a name="load-from-context"></a>로드 소스 컨텍스트  
 로드 소스 컨텍스트를 통해 응용 프로그램 경로 아래에 없는 경로에서 어셈블리를 로드할 수 있으므로 검색에 포함되지 않습니다. 경로 정보는 컨텍스트에서 유지 관리되므로 이 컨텍스트를 사용하여 해당 경로에서 종속성을 찾고 로드할 수 있습니다. 또한 이 컨텍스트의 어셈블리는 기본 로드 컨텍스트에 로드되는 종속성을 사용할 수 있습니다.  
  
 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 메서드나 경로로 로드되는 다른 메서드 중 하나를 사용하여 어셈블리를 로드하면 다음과 같은 단점이 있습니다.  
  
-   같은 ID를 가진 어셈블리가 이미 로드되어 있으면 다른 경로가 지정된 경우에도 <xref:System.Reflection.Assembly.LoadFrom%2A>은 로드된 어셈블리를 반환합니다.  
  
-   어셈블리가 <xref:System.Reflection.Assembly.LoadFrom%2A>을 사용하여 로드되고 나중에 기본 로드 컨텍스트의 어셈블리가 표시 이름으로 같은 어셈블리를 로드하려고 하면 로드 시도가 실패합니다. 어셈블리가 deserialize되면 이 문제가 발생할 수 있습니다.  
  
-   어셈블리가 <xref:System.Reflection.Assembly.LoadFrom%2A>을 사용하여 로드되고 검색 경로에 ID가 같지만 위치가 다른 어셈블리가 포함되면 <xref:System.InvalidCastException>, <xref:System.MissingMethodException> 또는 기타 예기치 않은 동작이 발생할 수 있습니다.  
  
-   <xref:System.Reflection.Assembly.LoadFrom%2A>은 지정된 경로에서 <xref:System.Security.Permissions.FileIOPermissionAccess.Read?displayProperty=nameWithType>와 <xref:System.Security.Permissions.FileIOPermissionAccess.PathDiscovery?displayProperty=nameWithType> 또는 <xref:System.Net.WebPermission>을 요구합니다.  
  
-   어셈블리에 대한 네이티브 이미지가 있는 경우 이 이미지가 사용되지 않습니다.  
  
-   어셈블리는 도메인 중립적으로 로드될 수 없습니다.  
  
-   .NET Framework 버전 1.0 및 1.1에서는 정책이 적용되지 않습니다.  
  
### <a name="no-context"></a>컨텍스트 없음  
 리플렉션 내보내기를 사용하여 생성된 임시 어셈블리의 경우 컨텍스트 없이 로드해야 합니다. 같은 ID를 가진 여러 어셈블리를 하나의 응용 프로그램 도메인에 로드하려면 컨텍스트 없이 로드해야 합니다. 검색 비용이 발생하지 않습니다.  
  
 정책이 적용될 때 설정되는 어셈블리의 ID가 전역 어셈블리 캐시의 어셈블리 ID와 일치하는 경우가 아니면 바이트 배열에서 로드된 어셈블리는 컨텍스트 없이 로드됩니다. 이 경우 어셈블리는 전역 어셈블리 캐시에서 로드됩니다.  
  
 컨텍스트 없이 어셈블리를 로드하는 방법에는 다음과 같은 단점이 있습니다.  
  
-   <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 이벤트를 처리하는 경우가 아니면 컨텍스트 없이 로드된 어셈블리에 다른 어셈블리를 바인딩할 수 없습니다.  
  
-   종속성은 자동으로 로드되지 않습니다. 어셈블리를 컨텍스트 없이 미리 로드하거나, 기본 로드 컨텍스트에 미리 로드하거나, <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 이벤트를 처리하여 로드할 수 있습니다.  
  
-   컨텍스트 없이 같은 ID를 가진 여러 어셈블리를 로드하면 같은 ID를 가진 어셈블리를 여러 컨텍스트에 로드하는 경우 발생한 문제와 비슷한 형식 ID 문제가 발생할 수 있습니다. [여러 컨텍스트에 어셈블리 로드 방지](#avoid_loading_into_multiple_contexts)를 참조하세요.  
  
-   어셈블리에 대한 네이티브 이미지가 있는 경우 이 이미지가 사용되지 않습니다.  
  
-   어셈블리는 도메인 중립적으로 로드될 수 없습니다.  
  
-   .NET Framework 버전 1.0 및 1.1에서는 정책이 적용되지 않습니다.  
  
<a name="avoid_partial_names"></a>   
## <a name="avoid-binding-on-partial-assembly-names"></a>부분 어셈블리 이름에 대한 바인딩 방지  
 부분 이름 바인딩은 어셈블리 로드 시 어셈블리 표시 이름(<xref:System.Reflection.Assembly.FullName%2A>)의 일부만 지정할 경우 발생합니다. 예를 들어 버전, 문화권 및 공개 키 토큰을 생략한 어셈블리의 간단한 이름만 사용하여 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드를 호출할 수 있습니다. 또는 <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType> 메서드를 호출할 수 있습니다. 이 메서드는 먼저 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드를 호출하고, 어셈블리를 찾지 못하면 전역 어셈블리 캐시를 검색하고 가장 최근 사용 가능한 버전의 어셈블리를 로드합니다.  
  
 부분 이름 바인딩을 사용하면 다음과 같은 여러 문제가 발생할 수 있습니다.  
  
-   <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType> 메서드는 같은 간단한 이름을 가진 다른 어셈블리를 로드할 수 있습니다. 예를 들어 두 개의 응용 프로그램이 둘 다 간단한 이름 `GraphicsLibrary`를 가진 두 개의 완전히 다른 어셈블리를 전역 어셈블리 캐시에 설치할 수 있습니다.  
  
-   실제로 로드되는 어셈블리가 이전 버전과 호환되지 않을 수 있습니다. 예를 들어 버전을 지정하지 않으면 프로그램이 원래 사용하도록 기록된 버전보다 훨씬 이후 버전이 로드될 수 있습니다. 이후 버전의 변경 내용으로 인해 응용 프로그램에서 오류가 발생할 수 있습니다.  
  
-   실제로 로드되는 어셈블리가 이후 버전과 호환되지 않을 수 있습니다. 예를 들어 최신 버전의 어셈블리를 사용하여 응용 프로그램을 빌드하고 테스트했을 수 있지만 부분 바인딩은 응용 프로그램에서 사용하는 기능이 없는 훨씬 이전 버전을 로드할 수 있습니다.  
  
-   새 응용 프로그램을 설치하면 기존 응용 프로그램이 중단됩니다. 공유 어셈블리의 더 새로운 호환되지 않는 버전을 설치하면 <xref:System.Reflection.Assembly.LoadWithPartialName%2A> 메서드를 사용하는 응용 프로그램이 중단될 수 있습니다.  
  
-   예기치 않은 종속성 로드가 발생할 수 있습니다. 종속성을 공유하는 두 개의 어셈블리를 로드할 경우 부분 바인딩을 사용하여 로드하면 빌드 또는 테스트에 사용되지 않은 구성 요소를 사용하는 하나의 어셈블리가 생성될 수 있습니다.  
  
 이로 인해 발생할 수 있는 문제 때문에 <xref:System.Reflection.Assembly.LoadWithPartialName%2A> 메서드는 obsolete로 표시되었습니다. 대신에 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드를 사용하고 전체 어셈블리 표시 이름을 지정하는 것이 좋습니다. [로드 컨텍스트의 장점 및 단점 이해](#load_contexts) 및 [기본 로드 컨텍스트로 전환 고려](#switch_to_default)를 참조하세요.  
  
 어셈블리를 쉽게 로드할 수 있기 때문에 <xref:System.Reflection.Assembly.LoadWithPartialName%2A> 메서드를 사용하려는 경우 누락된 어셈블리를 나타내는 오류 메시지와 함께 응용 프로그램이 실패하게 하면 알 수 없는 버전의 어셈블리를 자동으로 사용하여 예측할 수 없는 동작 및 보안 허점을 유발하는 것보다 사용자에게 더 나은 환경이 제공될 수 있습니다.  
  
<a name="avoid_loading_into_multiple_contexts"></a>   
## <a name="avoid-loading-an-assembly-into-multiple-contexts"></a>여러 컨텍스트에 어셈블리 로드 방지  
 어셈블리를 여러 컨텍스트에 로드하면 형식 ID 문제가 발생할 수 있습니다. 같은 형식이 같은 어셈블리에서 두 개의 다른 컨텍스트로 로드되는 경우는 같은 이름을 가진 두 개의 다른 형식이 로드된 것과 같습니다. 한 형식을 다른 형식으로 캐스팅하려고 하면 <xref:System.InvalidCastException>이 throw되고 `MyType` 형식을 `MyType` 형식으로 캐스팅할 수 없다는 혼동되는 메시지가 표시됩니다.  
  
 예를 들어 프로그램에서 참조되거나 프로그램이 로드하는 다른 어셈블리에서 참조되는 `Utility` 어셈블리에 `ICommunicate` 인터페이스가 선언된 경우를 살펴봅니다. 이러한 다른 어셈블리에는 프로그램에서 사용할 수 있도록 `ICommunicate` 인터페이스를 구현하는 형식이 포함됩니다.  
  
 이제 프로그램이 실행될 경우 어떤 일이 발생하는지 살펴봅니다. 프로그램에서 참조하는 어셈블리는 기본 로드 컨텍스트로 로드됩니다. <xref:System.Reflection.Assembly.Load%2A> 메서드를 사용하여 ID로 대상 어셈블리를 로드하면 어셈블리 및 종속성이 기본 로드 컨텍스트에 포함됩니다. 프로그램 및 대상 어셈블리는 둘 다 같은 `Utility` 어셈블리를 사용하게 됩니다.  
  
 하지만 <xref:System.Reflection.Assembly.LoadFile%2A> 메서드를 사용하여 파일 경로로 대상 어셈블리를 로드하는 경우를 살펴봅니다. 어셈블리는 컨텍스트 없이 로드되므로 종속성이 자동으로 로드되지 않습니다. 종속성을 제공하기 위한 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 이벤트 처리기가 있을 수 있고 이 처리기가 <xref:System.Reflection.Assembly.LoadFile%2A> 메서드를 사용하여 `Utility` 어셈블리를 컨텍스트 없이 로드할 수 있습니다. 이제 대상 어셈블리에 포함된 형식의 인스턴스를 만들고 인스턴스에 `ICommunicate` 형식의 변수를 지정하려고 하면 <xref:System.InvalidCastException>이 throw됩니다. 그 이유는 런타임은 `Utility` 어셈블리의 두 가지 복사본에 있는 `ICommunicate` 인터페이스를 서로 다른 형식으로 간주하기 때문입니다.  
  
 어셈블리를 여러 컨텍스트에 로드할 수 있는 다양한 다른 시나리오가 있습니다. 가장 좋은 방법은 대상 어셈블리를 응용 프로그램 경로에 재배치하고 <xref:System.Reflection.Assembly.Load%2A> 메서드를 전체 표시 이름과 함께 사용하여 충돌을 피하는 것입니다. 어셈블리는 기본 로드 컨텍스트에 로드되고 두 어셈블리는 모두 같은 `Utility` 어셈블리를 사용합니다.  
  
 대상 어셈블리가 응용 프로그램 경로 외부에서 유지되어야 하는 경우 <xref:System.Reflection.Assembly.LoadFrom%2A> 메서드를 사용하여 어셈블리를 로드 소스 컨텍스트에 로드할 수 있습니다. 대상 어셈블리가 응용 프로그램의 `Utility` 어셈블리에 대한 참조를 사용하여 컴파일된 경우 이 어셈블리는 응용 프로그램이 기본 로드 컨텍스트에 로드된 `Utility` 어셈블리를 사용합니다. 대상 어셈블리에 응용 프로그램 경로 외부에 있는 `Utility` 어셈블리의 복사본에 대한 종속성이 있는 경우에는 문제가 발생할 수 있습니다. 응용 프로그램이 `Utility` 어셈블리를 로드하기 전에 해당 어셈블리가 로드 소스 컨텍스트에 로드되면 응용 프로그램의 로드가 실패합니다.  
  
 [기본 로드 컨텍스트로 전환 고려](#switch_to_default) 섹션에서는 <xref:System.Reflection.Assembly.LoadFile%2A> 및 <xref:System.Reflection.Assembly.LoadFrom%2A>과 같은 파일 경로 로드 대신 사용할 수 있는 방법을 설명합니다.  
  
<a name="avoid_loading_multiple_versions"></a>   
## <a name="avoid-loading-multiple-versions-of-an-assembly-into-the-same-context"></a>같은 컨텍스트에 어셈블리의 여러 버전 로드 방지  
 여러 버전의 어셈블리를 하나의 로드 컨텍스트에 로드하면 형식 ID 문제가 발생할 수 있습니다. 같은 형식이 같은 어셈블리의 두 가지 버전에서 로드되는 경우는 같은 이름을 가진 두 개의 다른 형식이 로드된 것과 같습니다. 한 형식을 다른 형식으로 캐스팅하려고 하면 <xref:System.InvalidCastException>이 throw되고 `MyType` 형식을 `MyType` 형식으로 캐스팅할 수 없다는 혼동되는 메시지가 표시됩니다.  
  
 예를 들어 프로그램은 `Utility` 어셈블리의 한 가지 버전을 직접 로드하거나 나중에 `Utility` 어셈블리의 여러 가지 버전을 로드하는 또 다른 어셈블리를 로드할 수 있습니다. 또는 코딩 오류로 인해 응용 프로그램의 두 가지 다른 코드 경로가 어셈블리의 서로 다른 버전을 로드할 수 있습니다.  
  
 기본 로드 컨텍스트에서 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드를 사용하고 서로 다른 버전 번호를 포함하는 전체 어셈블리 표시 이름을 지정할 경우 이 문제가 발생할 수 있습니다. 컨텍스트 없이 로드된 어셈블리의 경우 <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType> 메서드를 사용하여 서로 다른 경로에서 같은 어셈블리를 로드하면 문제가 발생할 수 있습니다. 런타임은 ID가 같은 경우에도 서로 다른 경로에서 로드된 두 개의 어셈블리를 서로 다른 어셈블리로 간주합니다.  
  
 형식 ID 문제 이외에 어셈블리의 여러 버전이 있으면 어셈블리의 한 버전에서 로드된 형식이 다른 버전의 해당 형식을 필요로 하는 코드에 전달될 경우 <xref:System.MissingMethodException>이 발생할 수 있습니다. 예를 들어 코드에는 이후 버전에 추가된 메서드가 필요할 수 있습니다.  
  
 형식의 동작이 버전 간에 변경된 경우 더 교묘한 오류가 발생할 수 있습니다. 예를 들어 메서드가 예기치 않은 예외를 throw하거나 예기치 않은 값을 반환할 수 있습니다.  
  
 어셈블리의 한 가지 버전만 로드되도록 코드를 주의해서 검토하세요. <xref:System.AppDomain.GetAssemblies%2A?displayProperty=nameWithType> 메서드를 사용하여 특정 시점에 로드되는 어셈블리를 결정할 수 있습니다.  
  
<a name="switch_to_default"></a>   
## <a name="consider-switching-to-the-default-load-context"></a>기본 로드 컨텍스트로 전환 고려  
 응용 프로그램 어셈블리 로드 및 배포 패턴을 살펴봅니다. 바이트 배열에서 로드된 어셈블리를 제거할 수 있나요? 어셈블리를 검색 경로로 이동할 수 있나요? 어셈블리가 전역 어셈블리 캐시 또는 응용 프로그램 도메인의 검색 경로(<xref:System.AppDomainSetup.ApplicationBase%2A> 및 <xref:System.AppDomainSetup.PrivateBinPath%2A>)에 있는 경우 ID로 어셈블리를 로드할 수 있습니다.  
  
 모든 어셈블리를 검색 경로에 포함할 수 없는 경우에는 .NET Framework 추가 기능 모델을 사용하거나 어셈블리를 전역 어셈블리 캐시에 포함하거나 응용 프로그램 도메인을 만드는 것과 같은 대체 방법을 고려하세요.  
  
### <a name="consider-using-the-net-framework-add-in-model"></a>.NET Framework 추가 기능 모델 사용 고려  
 일반적으로 응용 프로그램 기준 위치에 설치되지 않는 추가 기능을 구현하는 데 로드 소스 컨텍스트를 사용할 경우 .NET Framework 추가 기능 모델을 사용하세요. 이 모델은 응용 프로그램 도메인 또는 프로세스 수준에서 격리되므로, 사용자가 응용 프로그램 도메인을 직접 관리할 필요가 없습니다. 추가 기능 모델에 대한 자세한 내용은 [추가 기능 및 확장성](../../../docs/framework/add-ins/index.md)을 참조하세요.  
  
### <a name="consider-using-the-global-assembly-cache"></a>전역 어셈블리 캐시 사용 고려  
 어셈블리를 전역 어셈블리 캐시에 포함하면 기본 로드 컨텍스트의 장점을 잃거나 다른 컨텍스트의 단점을 떠맡지 않고 응용 프로그램 기준 위치 외부에 있는 공유 어셈블리 경로를 활용할 수 있습니다.  
  
### <a name="consider-using-application-domains"></a>응용 프로그램 도메인 사용 고려  
 일부 어셈블리를 응용 프로그램의 검색 경로에 배포할 수 없는 것으로 확인되면 해당 어셈블리에 대한 새 응용 프로그램 도메인을 만드는 것이 좋습니다. <xref:System.AppDomainSetup>을 사용하여 새 응용 프로그램 도메인을 만들고 <xref:System.AppDomainSetup.ApplicationBase%2A?displayProperty=nameWithType> 속성을 사용하여 로드할 어셈블리가 포함된 경로를 지정합니다. 검색할 디렉터리가 여러 개 있는 경우에는 <xref:System.AppDomainSetup.ApplicationBase%2A>를 루트 디렉터리로 설정하고 <xref:System.AppDomainSetup.PrivateBinPath%2A?displayProperty=nameWithType> 속성을 사용하여 검색할 하위 디렉터리를 확인할 수 있습니다. 또는 여러 응용 프로그램 도메인을 만들고 각 응용 프로그램 도메인의 <xref:System.AppDomainSetup.ApplicationBase%2A>를 어셈블리의 적절한 경로로 설정할 수 있습니다.  
  
 이러한 어셈블리를 로드하는 데는 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 메서드를 사용할 수 있습니다. 이제 어셈블리가 검색 경로에 있으므로 어셈블리는 로드 소스 컨텍스트가 아닌 기본 로드 컨텍스트에 로드됩니다. 하지만 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드로 전환하고 전체 어셈블리 표시 이름을 제공하여 올바른 버전이 항상 사용되는지 확인하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType>
- <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType>
- <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType>
- <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType>
- [추가 기능 및 확장성](../../../docs/framework/add-ins/index.md)
