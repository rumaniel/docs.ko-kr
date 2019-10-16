---
title: .NET 어셈블리
ms.date: 08/15/2019
ms.assetid: 149f5ca5-5b34-4746-9542-1ae43b2d0256
helpviewer_keywords:
- dynamic assemblies
- security [.NET Framework], boundaries
- boundaries of assemblies
- assemblies [.NET Framework], about
- assemblies [.NET Framework], boundaries
- reference scope boundaries
- assemblies [.NET Framework]
- version boundaries
- type boundaries
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 903a553b5383620f15cce274c61a440b7bbb1d7d
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70970010"
---
# <a name="assemblies-in-net"></a>.NET 어셈블리

어셈블리는 .NET 기반 애플리케이션에 대한 배포, 버전 제어, 재사용, 활성화 범위 및 보안 권한의 기본 단위를 형성합니다. 어셈블리는 서로 함께 사용되어 논리적 기능 단위를 형성하도록 빌드되는 형식 및 리소스의 컬렉션입니다. 어셈블리는 실행 파일( *.exe*) 또는 동적 연결 라이브러리( *.dll*) 파일의 형태를 가지며 .NET 애플리케이션의 구성 요소입니다. 어셈블리는 형식 구현을 인식하는 데 필요한 정보와 함께 공용 언어 런타임을 제공합니다. 어셈블리를 함께 작동하도록 빌드되고 논리적 기능 단위를 형성하는 리소스 및 형식 컬렉션으로 생각할 수 있습니다.

.NET Core 및 .NET Framework에서, 소스 코드 파일 1개 이상에서 어셈블리를 빌드할 수 있습니다. .NET Framework에서, 어셈블리 모듈을 하나 이상 포함할 수 있습니다. 따라서 대규모 프로젝트를 계획하여 여러 개발자가 작업하는 별도의 소스 코드 파일이나 모듈을 결합하여 단일 어셈블리를 만들 수 있습니다. 모듈에 대한 자세한 내용은 [ 방법: 다중 파일 어셈블리 빌드](../../framework/app-domains/build-multifile-assembly.md)를 참조하세요.

어셈블리에는 다음과 같은 속성이 있습니다.

- 어셈블리는 *.exe* 또는 *.dll* 파일로 구현됩니다.

- .NET Framework를 대상으로 하는 라이브러리의 경우 [전역 어셈블리 캐시(GAC)](../../framework/app-domains/gac.md)에 어셈블리를 넣으면 애플리케이션 간에 어셈블리를 공유할 수 있습니다. GAC에 어셈블리를 포함하려면 먼저 강력한 이름의 어셈블리를 만들어야 합니다. 자세한 내용은 [강력한 이름의 어셈블리](strong-named.md)를 참조하세요.

- 어셈블리는 필요한 경우에만 메모리에 로드됩니다. 사용되지 않는 경우에는 로드되지 않습니다. 즉, 어셈블리는 대규모 프로젝트에서 리소스를 관리하는 효율적인 방법일 수 있습니다.

- 리플렉션을 사용하여 프로그래밍 방식으로 어셈블리에 대한 정보를 얻을 수 있습니다. 자세한 내용은 [리플렉션(C#)](../../csharp/programming-guide/concepts/reflection.md) 또는 [Reflection(Visual Basic)](../../visual-basic/programming-guide/concepts/reflection.md)을 참조하세요.

- .NET Core에서 <xref:System.Reflection.MetadataLoadContext> 클래스를 사용하거나 .NET Core 및 .NET Framework에서 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> 또는 <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=nameWithType> 메서드를 사용하여 검사만을 위해 어셈블리를 로드할 수 있습니다.

## <a name="assemblies-in-the-common-language-runtime"></a>공용 언어 런타임의 어셈블리

어셈블리는 형식 구현을 인식하는 데 필요한 정보와 함께 공용 언어 런타임을 제공합니다. 런타임에 대해, 형식은 어셈블리 컨텍스트 외부에 존재하지 않습니다. 

어셈블리는 다음 정보를 정의합니다.  
  
- 공용 언어 런타임이 실행하는 코드. 각 어셈블리는 진입점을 하나만 가질 수 있습니다(`DllMain`, `WinMain` 또는 `Main`).
  
- 보안 경계. 어셈블리는 권한이 요청되고 허용되는 단위입니다. 어셈블리의 보안 경계에 대한 자세한 내용은 [어셈블리 보안 고려 사항](security-considerations.md)을 참조하세요.  
  
- 형식 경계. 각 형식의 ID에는 해당 형식이 존재하는 어셈블리의 이름이 포함됩니다. 한 어셈블리의 범위에서 로드된 `MyType`이라는 형식은 다른 어셈블리의 범위에서 로드된 `MyType`이라는 형식과 다릅니다. 
  
- 참조 범위 경계. [어셈블리 매니페스트](#assembly-manifest)에는 형식을 확인하고 리소스 요청을 충족하는 데 사용되는 메타데이터가 있습니다. 매니페스트는 어셈블리 외부에 노출할 형식과 리소스를 지정하고, 해당 어셈블리가 종속된 다른 어셈블리를 열거합니다. 이식 가능(PE) 파일의 Microsoft Intermediate Language(MSIL) 코드는 연결된 [어셈블리 매니페스트](#assembly-manifest)가 없으면 실행되지 않습니다.
  
- 버전 경계. 어셈블리는 공용 언어 런타임에서 가장 작은 버전 지정 가능 단위입니다. 동일한 어셈블리의 모든 형식과 리소스는 하나의 단위로 버전이 지정됩니다. [어셈블리 매니페스트](#assembly-manifest)는 종속 어셈블리에 지정한 버전 종속성을 설명합니다. 버전 관리에 대한 자세한 내용은 [어셈블리 버전 관리](versioning.md)를 참조하세요.  
  
- 배포 단위. 애플리케이션이 시작될 때 애플리케이션이 처음으로 호출하는 어셈블리만 있어야 합니다. 지역화 리소스 또는 유틸리티 클래스가 포함된 어셈블리 등의 다른 어셈블리는 요청 시 검색할 수 있습니다. 이렇게 하면 처음 다운로드될 때 앱이 단순해집니다. 어셈블리 배포에 대한 자세한 내용은 [애플리케이션 배포](../../framework/deployment/index.md)를 참조하세요.  
  
- Side-by-Side 실행 단위. 여러 버전의 어셈블리 실행에 대한 자세한 내용은 [어셈블리 및 Side-by-Side 실행](side-by-side-execution.md)을 참조하세요.  

## <a name="create-an-assembly"></a>어셈블리 만들기

어셈블리는 정적 또는 동적이 될 수 있습니다. 정적 어셈블리는 PE(이식 가능한 실행) 파일로 디스크에 저장됩니다. 정적 어셈블리에는 인터페이스와 클래스뿐 아니라 비트맵, JPEG 파일, 기타 리소스 파일 같은 리소스가 포함될 수 있습니다. 메모리에서 직접 실행되며 실행 전에 디스크에 저장되지 않는 동적 어셈블리를 만들 수도 있습니다. 동적 어셈블리는 실행된 후에 디스크에 저장할 수 있습니다.  

여러 가지 방법으로 어셈블리를 만들 수 있습니다. Visual Studio와 같이 *.dll* 또는 *.exe* 파일을 만들 수 있는 개발 도구를 사용할 수 있습니다. Windows SDK의 도구를 사용하여 다른 개발 환경의 모듈이 포함된 어셈블리를 만들 수 있습니다. 또한 <xref:System.Reflection.Emit?displayProperty=nameWithType> 등의 공용 언어 런타임 API를 사용하여 동적 어셈블리를 만들 수도 있습니다. 

Visual Studio에서 또는 .NET Core 명령줄 인터페이스 도구를 사용하여 어셈블리를 빌드하거나 명령줄 컴파일러를 사용하여 .NET Framework 어셈블리를 빌드하여 어셈블리를 컴파일합니다. .NET Core 명령줄 인터페이스 도구를 사용하여 어셈블리를 빌드하는 방법에 대한 자세한 내용은 [.NET Core 명령줄 인터페이스 도구](../../core/tools/index.md)를 참조하세요. 명령줄 컴파일러를 사용하여 어셈블리를 빌드하려면 C#의 경우 [csc.exe로 명령줄 빌드](../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)를, Visual Basic의 경우 [명령줄에서 빌드](../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)를 참조하세요.

> [!NOTE]
> Visual Studio에서 어셈블리를 빌드하려면 **빌드** 메뉴에서 **빌드**를 선택합니다.

## <a name="assembly-manifest"></a>어셈블리 매니페스트

모든 어셈블리에는 *어셈블리 매니페스트* 파일이 있습니다. 목차와 유사하게 어셈블리 매니페스트에는 다음이 포함됩니다.

- 어셈블리의 ID(해당 이름 및 버전).

- 어셈블리를 구성하는 다른 모든 파일을 설명하는 파일 테이블(예: 사용자의 *.exe* 또는 *.dll* 파일이 의존하는 사용자가 만든 다른 모든 어셈블리 또는 비트맵 파일 또는 추가 정보 파일).

- *.dll* 또는 기타 파일 같은 모든 외부 종속성의 목록인 *어셈블리 참조 목록*. 어셈블리 참조는 global 및 private 개체에 대한 참조를 포함합니다. 전역 개체는 다른 모든 애플리케이션에서 사용할 수 있습니다. .NET Core에서 전역 개체는 특정 .NET Core 런타임과 결합됩니다. .NET Framework에서 전역 개체는 전역 어셈블리 캐시(GAC)에 있습니다. *System.IO.dll*은 GAC에 있는 어셈블리의 예입니다. private 개체는 앱이 설치된 디렉터리와 같거나 낮은 디렉터리 수준에 있어야 합니다.

어셈블리는 콘텐츠, 버전 관리 및 종속성에 대한 정보를 포함하므로 이를 사용하는 애플리케이션은 제대로 작동하기 위해 Windows 시스템의 레지스트리 같은 외부 소스를 사용할 필요가 없습니다. 어셈블리는 *.dll* 충돌을 줄이고 더 안정적이고 배포하기 쉬운 애플리케이션을 구현합니다. 많은 경우에 해당 파일을 대상 컴퓨터에 복사하는 것만으로 .NET 기반 애플리케이션을 설치할 수 있습니다. 자세한 내용은 [어셈블리 매니페스트](manifest.md)를 참조하세요.

## <a name="add-a-reference-to-an-assembly"></a>어셈블리에 대한 참조 추가

애플리케이션에서 어셈블리를 사용하려면 어셈블리에 대한 참조를 추가해야 합니다. 어셈블리가 참조되면 해당 코드가 소스 파일에 속해 있는 것처럼 해당 네임스페이스의 액세스 가능한 모든 유형, 속성, 메서드 및 기타 멤버를 애플리케이션에서 사용할 수 있습니다.

> [!NOTE]
> .NET 클래스 라이브러리의 대부분의 어셈블리는 자동으로 참조됩니다. 시스템 어셈블리가 자동으로 참조되지 않으면 .NET Core의 경우 어셈블리를 포함하는 NuGet 패키지에 대한 참조를 추가할 수 있습니다. Visual Studio에서 NuGet 패키지 관리자를 사용하거나 어셈블리의 [\<PackageReference>](../../core/tools/dependencies.md#the-new-packagereference-element) 요소를 *.csproj* 또는 *.vbproj* 프로젝트에 추가합니다. .NET framework에서 Visual Studio의 **참조 추가** 대화 상자를 사용하거나 [C#](../../csharp/language-reference/compiler-options/reference-compiler-option.md)의 `-reference` 명령줄 옵션 또는 [Visual Basic](../../visual-basic/reference/command-line-compiler/reference.md) 컴파일러를 사용하여 어셈블리에 대한 참조를 추가할 수 있습니다.

C#에서는 단일 애플리케이션에서 동일한 어셈블리의 두 버전을 사용할 수 있습니다. 자세한 내용은 [extern alias](../../csharp/language-reference/keywords/extern-alias.md)를 참조하세요.

## <a name="related-content"></a>관련 콘텐츠
  
|제목|설명|  
|-----------|-----------------|  
|[어셈블리 콘텐츠](contents.md)|어셈블리를 구성하는 요소.|  
|[어셈블리 매니페스트](manifest.md)|어셈블리 매니페스트의 데이터와 이 데이터가 어셈블리에 저장되는 방법.|  
|[전역 어셈블리 캐시](../../framework/app-domains/gac.md)|GAC에서 어셈블리를 저장하고 사용하는 방법.|  
|[강력한 이름의 어셈블리](strong-named.md)|강력한 이름의 어셈블리의 특징.|  
|[어셈블리 보안 고려 사항](security-considerations.md)|어셈블리에 보안이 사용되는 방법.|  
|[어셈블리 버전 관리](versioning.md)|.NET Framework 버전 관리 정책의 개요.|  
|[어셈블리 배치](../../framework/app-domains/assembly-placement.md)|어셈블리가 배치되는 위치.|  
|[어셈블리 및 Side-by-Side 실행](side-by-side-execution.md)|여러 버전의 런타임 또는 어셈블리를 동시에 사용합니다.|  
|[어셈블리를 사용한 프로그램](program.md)|어셈블리를 만들고, 서명하고, 특성을 설정하는 방법.|  
|[동적 메서드 및 어셈블리 내보내기](../../../docs/framework/reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)|동적 어셈블리를 만드는 방법.|  
|[런타임에서 어셈블리를 찾는 방법](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)|.NET Framework가 런타임에서 어셈블리 참조를 확인하는 방법.|  

## <a name="reference"></a>참조  
 <xref:System.Reflection.Assembly?displayProperty=nameWithType>

## <a name="see-also"></a>참고 항목

- [.NET 어셈블리 파일 형식](file-format.md)
- [.NET 어셈블리](index.md)
- [Friend 어셈블리](friend.md)
- [방법: 어셈블리 로드 및 언로드](load-unload.md)
- [방법: .NET Core에서 어셈블리 언로드 기능 사용 및 디버그](unloadability.md)
- [방법: 파일이 어셈블리인지 확인](identify.md)
