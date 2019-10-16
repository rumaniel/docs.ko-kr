---
title: 관리되는 실행 프로세스
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- source code language
- code, managed execution process
- runtime, managed execution process
- compiling source code, managed execution process
- managed execution process
- common language runtime, managed execution process
ms.assetid: 476b03dc-2b12-49a7-b067-41caeaa2f533
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d11567b3a5abca6e81ff0358295aa8516ef6443f
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70969025"
---
# <a name="managed-execution-process"></a>관리되는 실행 프로세스
<a name="introduction"></a> 관리되는 실행 프로세스에는 이 항목의 뒷부분에서 설명하는 다음 단계가 포함됩니다.  
  
1. [컴파일러 선택](#choosing_a_compiler).  
  
     공용 언어 런타임에서 제공되는 이점을 얻으려면 런타임을 대상으로 지정하는 언어 컴파일러를 하나 이상 사용해야 합니다.  
  
2. [코드를 MSIL로 컴파일](#compiling_to_msil).  
  
     컴파일을 통해 소스 코드가 MSIL(Microsoft Intermediate Language)로 변환되고 필요한 메타데이터가 생성됩니다.  
  
3. [MSIL을 네이티브 코드로 컴파일](#compiling_msil_to_native_code).  
  
     실행 시간에 JIT(Just-In-Time) 컴파일러는 MSIL을 네이티브 코드로 변환합니다. 이 컴파일 중에 코드는 MSIL 및 메타데이터를 검사하여 코드가 형식 안전 코드로 판별되는지 확인하는 확인 프로세스를 통과해야 합니다.  
  
4. [코드 실행](#running_code).  
  
     공용 언어 런타임은 실행을 가능하게 하는 인프라와 실행 중에 사용할 수 있는 서비스를 제공합니다.  
  
<a name="choosing_a_compiler"></a>   
## <a name="choosing-a-compiler"></a>컴파일러 선택  
 CLR(공용 언어 런타임)에서 제공되는 이점을 얻으려면 런타임을 대상으로 지정하는 Visual Basic, C#, Visual C++, F# 또는 다양한 타사 컴파일러의 하나(예: Eiffel, Perl 또는 COBOL 컴파일러) 등의 언어 컴파일러를 하나 이상 사용해야 합니다.  
  
 CLR은 다국어 실행 환경이므로 런타임은 다양한 데이터 형식과 언어 기능을 지원합니다. 사용하는 언어 컴파일러에 따라 사용할 수 있는 런타임 기능이 결정되고 사용자가 해당 기능을 사용하여 코드를 디자인합니다. 코드에서 사용해야 하는 구문을 설정하는 것은 런타임이 아니라 컴파일러입니다. 다른 언어로 작성된 구성 요소가 사용자의 구성 요소를 완전히 사용할 수 있어야 하면 사용자 구성 요소의 내보낸 형식은 CLS( [Language Independence and Language-Independent Components](../../docs/standard/language-independence-and-language-independent-components.md) )에 포함된 언어 기능만 노출해야 합니다. <xref:System.CLSCompliantAttribute> 특성을 사용하여 코드가 CLS 규격인지 확인할 수 있습니다. 자세한 내용은 [Language Independence and Language-Independent Components](../../docs/standard/language-independence-and-language-independent-components.md)을 참조하십시오.  
  
 [맨 위로 이동](#introduction)  
  
<a name="compiling_to_msil"></a>   
## <a name="compiling-to-msil"></a>MSIL로 컴파일  
 관리 코드를 컴파일하는 경우 컴파일러는 소스 코드를 네이티브 코드로 효율적으로 변환될 수 있는 CPU 독립적인 명령 집합인 MSIL(Microsoft Intermediate Language)로 변환합니다. MSIL에는 개체에 대한 메서드를 로드, 저장, 초기화, 호출하는 명령과 산술 및 논리 연산, 제어 흐름, 직접 메모리 액세스, 예외 처리 및 기타 작업에 대한 명령이 포함됩니다. 코드를 실행하기 전에 보통 [JIT(Just-In-Time) 컴파일러](#compiling_msil_to_native_code)를 통해 MSIL을 CPU 특정 코드로 변환해야 합니다. 공용 언어 런타임은 지원하는 각 컴퓨터 아키텍처에 대해 JIT 컴파일러를 하나 이상 제공하므로 같은 MSIL 집합이 JIT로 컴파일되고 지원되는 모든 아키텍처에서 실행될 수 있습니다.  
  
 컴파일러는 MSIL을 생성할 때 메타데이터도 생성합니다. 메타데이터는 각 형식의 정의, 각 형식 멤버의 서명, 코드에서 참조하는 멤버 및 실행 시간에 런타임이 사용하는 기타 데이터를 포함하여 코드의 형식에 대해 설명합니다. MSIL 및 메타데이터는 일반적으로 실행 가능 콘텐츠에 대해 사용되는 게시된 Microsoft PE 및 COFF(공용 개체 파일 형식)에 기반을 두고 이를 확장하는 PE(이식 가능한 실행) 파일에 포함됩니다. 메타데이터와 MSIL 또는 네이티브 코드를 수용하는 이 파일 형식을 통해 운영 체제에서 공용 언어 런타임 이미지를 인식할 수 있습니다. MSIL과 함께 파일에 메타데이터가 있으면 코드에서 코드 자체를 설명할 수 있습니다. 즉, 형식 라이브러리 또는 IDL(Interface Definition Language)이 필요하지 않습니다. 런타임이 파일에서 실행 중에 필요한 메타데이터를 찾아서 추출합니다.  
  
 [맨 위로 이동](#introduction)  
  
<a name="compiling_msil_to_native_code"></a>   
## <a name="compiling-msil-to-native-code"></a>MSIL을 네이티브 코드로 컴파일  
 MSIL(Microsoft Intermediate Language)을 실행하기 전에 공용 언어 런타임을 기반으로 MSIL을 대상 컴퓨터 아키텍처에 대한 네이티브 코드로 컴파일해야 합니다. .NET Framework는 이 변환을 수행하는 두 가지 방법을 제공합니다.  
  
- .NET Framework JIT(Just-In-Time) 컴파일러.  
  
- .NET Framework [Ngen.exe(네이티브 이미지 생성기)](../../docs/framework/tools/ngen-exe-native-image-generator.md).  
  
### <a name="compilation-by-the-jit-compiler"></a>JIT 컴파일러에서 컴파일  
 JIT 컴파일은 어셈블리의 콘텐츠가 로드 및 실행되는 애플리케이션 실행 시간에 요청 시 MSIL을 네이티브 코드로 변환합니다. 공용 언어 런타임은 지원되는 각 CPU 아키텍처에 대한 JIT 컴파일러를 제공하므로 개발자는 다양한 컴퓨터 아키텍처를 가진 여러 가지 컴퓨터에서 JIT로 컴파일되고 실행될 수 있는 MSIL 어셈블리 집합을 빌드할 수 있습니다. 그러나 관리 코드는 플랫폼 특정 네이티브 API 또는 플랫폼 특정 클래스 라이브러리를 호출할 경우 해당 운영 체제에서만 실행됩니다.  
  
 JIT 컴파일은 일부 코드가 실행 중에 호출되지 않을 가능성을 고려합니다. PE 파일의 모든 MSIL을 네이티브 코드로 변환하는 데 시간과 메모리를 사용하는 대신 실행 중에 필요에 따라 MSIL을 변환하고 해당 프로세스의 컨텍스트에서 이후 호출을 위해 액세스할 수 있도록 결과 네이티브 코드를 메모리에 저장합니다. 로더는 형식이 로드되고 초기화될 때의 형식으로 스텁을 만들고 각 메서드에 연결합니다. 메서드가 처음 호출될 때 스텁은 JIT 컴파일러로 제어를 전달하고 JIT 컴파일러는 해당 메서드에 대한 MSIL을 네이티브 코드로 변환하고 생성된 네이티브 코드를 직접 가리키도록 스텁을 수정합니다. 따라서 JIT로 컴파일된 메서드에 대한 이후 호출은 직접 네이티브 코드로 이동합니다.  
  
### <a name="install-time-code-generation-using-ngenexe"></a>NGen.exe를 사용하여 설치 시간 코드 생성  
 JIT 컴파일러는 어셈블리에 정의된 개별 메서드가 호출될 때 해당 어셈블리의 MSIL을 네이티브 코드로 변환하므로 런타임에 성능이 저하됩니다. 대부분 경우에 저하된 성능은 허용 가능한 정도입니다. 더 중요한 것은 JIT 컴파일러에서 생성된 코드는 컴파일을 트리거한 프로세스에 바인딩된다는 점입니다. 이 코드는 여러 프로세스에서 공유할 수 없습니다. 생성된 코드를 여러 애플리케이션 호출에서 또는 어셈블리 집합을 공유하는 여러 프로세스에서 공유할 수 있도록 공용 언어 런타임은 사전 컴파일 모드를 지원합니다. 이 사전 컴파일 모드에서는 [Ngen.exe(네이티브 이미지 생성기)](../../docs/framework/tools/ngen-exe-native-image-generator.md)를 사용하여 JIT 컴파일러가 변환하는 것처럼 MSIL 어셈블리를 네이티브 코드로 변환합니다. 그러나 Ngen.exe의 작업은 다음 세 가지 방법에서 JIT 컴파일러의 작업과 다릅니다.  
  
- 애플리케이션이 실행되는 동안이 아니라 애플리케이션을 실행하기 전에 MSIL에서 네이티브 코드로의 변환을 수행합니다.  
  
- 한 번에 한 메서드가 아니라 한 번에 전체 어셈블리를 컴파일합니다.  
  
- 생성된 코드를 네이티브 이미지 캐시에서 디스크의 파일로 유지합니다.  
  
### <a name="code-verification"></a>코드 확인  
 코드가 확인을 무시하도록 허용하는 보안 정책을 관리자가 설정한 경우가 아니면 네이티브 코드에 대한 컴파일 중에 MSIL 코드는 확인 프로세스를 통과해야 합니다. 확인 프로세스에서는 MSIL 및 메타데이터를 검사하여 코드가 형식 안전 코드인지를 확인합니다. 즉, 형식 안전 코드는 액세스 권한이 부여된 메모리 위치에만 액세스합니다. 형식 안전성은 개체를 서로 격리하고 우발적이거나 악의적인 손상으로부터 보호하도록 도와줍니다. 또한 형식 안정성은 코드에 대한 보안 제한을 확실히 적용할 수 있도록 합니다.  
  
 런타임은 다음 문이 확인 가능한 형식 안전 코드에 적용된다는 사실에 기반을 둡니다.  
  
- 형식에 대한 참조는 참조되는 형식과 엄격하게 호환됩니다.  
  
- 적절하게 정의된 작업만 개체에서 호출됩니다.  
  
- ID는 단어 그대로 주체를 나타냅니다.  
  
 확인 프로세스 중에 코드가 메모리 위치에 액세스하고 제대로 정의된 형식을 통해서만 메서드를 호출할 수 있는지를 확인하려고 MSIL 코드를 검사합니다. 예를 들어 코드에서는 메모리 위치를 오버런하도록 허용하는 방식으로 개체의 필드에 액세스할 수 없습니다. 또한 잘못된 MSIL로 인해 형식 안정성 규칙을 위반할 수 있기 때문에 확인 프로세스에서는 코드를 검사하여 MSIL이 제대로 생성되었는지를 확인합니다. 확인 프로세스는 제대로 정의된 형식 안전 코드 집합을 전달하고 형식 안전 코드만 전달합니다. 그러나 확인 프로세스의 일부 제한으로 인해 일부 형식 안전 코드는 확인을 통과할 수 없고, 일부 언어는 계획적으로 확인 가능한 형식 안전 코드를 생성하지 않습니다. 보안 정책에 따라 형식 안전 코드가 필요하지만 코드가 확인을 통과하지 못하면 코드가 실행될 때 예외가 throw 됩니다.  
  
 [맨 위로 이동](#introduction)  
  
<a name="running_code"></a>   
## <a name="running-code"></a>코드 실행  
 공용 언어 런타임은 관리되는 실행을 가능하게 하는 인프라와 실행 중에 사용할 수 있는 서비스를 제공합니다. 메서드를 실행하기 전에 프로세서 특정 코드로 컴파일해야 합니다. MSIL이 생성된 각 메서드는 처음 호출될 때 JIT로 컴파일되고 나서 실행됩니다. 다음에 메서드가 실행될 때 기존의 JIT로 컴파일된 네이티브 코드가 실행됩니다. 코드를 JIT로 컴파일하고 나서 실행하는 프로세스는 실행이 완료될 때까지 반복됩니다.  
  
 실행되는 동안 관리 코드는 가비지 수집, 보안, 비관리 코드와의 상호 운용성, 언어 간 디버깅 지원 및 향상된 배포/버전 관리 지원과 같은 서비스를 수신합니다.  
  
 Microsoft [!INCLUDE[winxp](../../includes/winxp-md.md)] 및 [!INCLUDE[windowsver](../../includes/windowsver-md.md)]에서는 운영 체제 로더가 COFF 헤더에서 비트를 검사하여 관리 모듈을 확인합니다. 설정되는 비트는 관리 모듈을 나타냅니다. 로더는 관리 모듈을 감지하면 mscoree.dll을 로드하고 `_CorValidateImage` 및 `_CorImageUnloading` 는 관리 모듈 이미지가 로드 및 언로드될 때 로더에 알립니다. `_CorValidateImage` 는 다음 작업을 수행합니다.  
  
1. 코드가 올바른 관리 코드인지 확인합니다.  
  
2. 이미지의 진입점을 런타임의 진입점으로 변경합니다.  
  
 64비트 Windows에서 `_CorValidateImage` 는 이미지를 PE32에서 PE32+ 형식으로 변환하여 메모리에 있는 이미지를 수정합니다.  
  
 [맨 위로 이동](#introduction)  
  
## <a name="see-also"></a>참고 항목

- [개요](../../docs/framework/get-started/overview.md)
- [언어 독립성 및 언어 독립적 구성 요소](../../docs/standard/language-independence-and-language-independent-components.md)
- [메타데이터 및 자동 기술 구성 요소](../../docs/standard/metadata-and-self-describing-components.md)
- [Ilasm.exe(IL 어셈블러)](../../docs/framework/tools/ilasm-exe-il-assembler.md)
- [보안](../../docs/standard/security/index.md)
- [비관리 코드와의 상호 운용](../../docs/framework/interop/index.md)
- [배포](../../docs/framework/deployment/net-framework-applications.md)
- [.NET 어셈블리](assembly/index.md)
- [애플리케이션 도메인](../../docs/framework/app-domains/application-domains.md)
