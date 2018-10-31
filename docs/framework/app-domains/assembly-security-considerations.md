---
title: 어셈블리 보안 고려 사항
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], security
- signcodes
- names [.NET Framework], assemblies
- strong-named assemblies, security considerations
- signing assemblies
- assemblies [.NET Framework], signing
- granting permissions, assemblies
- assemblies [.NET Framework], strong-named
- names [.NET Framework], strong names
- permissions [.NET Framework], assemblies
- security [.NET Framework], assemblies
- integrity with assemblies
ms.assetid: 1b5439c1-f3d5-4529-bd69-01814703d067
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8d83da6e995c35de650c496c5792e55b05dd9095
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50088795"
---
# <a name="assembly-security-considerations"></a>어셈블리 보안 고려 사항
<a name="top"></a> 어셈블리를 빌드할 때 어셈블리를 실행하는 데 필요한 권한을 지정할 수 있습니다. 어셈블리에 대한 특정 권한 부여 여부는 증명 정보를 바탕으로 합니다.  
  
 증명 정보를 사용하는 두 가지 방법은 다음과 같습니다.  
  
-   먼저 입력된 증명 정보를 로더에 의해 수집된 증명 정보와 결합하여 정책 결정에 사용할 최종 증명 정보를 만듭니다. 이 의미 체계를 사용하는 메서드로는 **Assembly.Load**, **Assembly.LoadFrom** 및 **Activator.CreateInstance**가 있습니다.  
  
-   또 다른 방법은 입력된 증명 정보를 바꾸지 않고 정책 결정을 위한 최종 증명 정보로 사용하는 것입니다. 이 의미 체계를 사용하는 메서드로는 **Assembly.Load(byte[])** 및 **AppDomain.DefineDynamicAssembly()** 가 있습니다.  
  
 선택적 권한은 어셈블리가 실행될 컴퓨터에 설정한 [보안 정책](../../../docs/framework/misc/code-access-security-basics.md)으로 부여될 수 있습니다. 코드에서 모든 가능한 보안 예외를 처리하게 하려면 다음 중 하나를 수행해야 합니다.  
  
-   코드에 필요한 모든 권한에 대해 권한 요청을 삽입하고 권한이 부여되지 않았을 때 발생하는 로드 시간 오류를 먼저 처리합니다.  
  
-   코드에 필요할 수 있는 권한을 얻기 위한 권한 요청을 사용하지 않고, 대신 권한이 부여되지 않을 경우를 대비하여 보안 예외를 처리할 수 있도록 준비합니다.  
  
    > [!NOTE]
    >  보안은 매우 복잡한 영역이기 때문에 선택할 수 있는 옵션도 다양합니다. 자세한 내용은 [주요 보안 개념](../../../docs/standard/security/key-security-concepts.md)을 참조하세요.  
  
 로드 시, 어셈블리의 증명 정보는 보안 정책에 대한 입력으로 사용됩니다. 보안 정책은 사용자 정책 설정을 비롯하여 엔터프라이즈 및 컴퓨터의 관리자에 의해 설정되며 모든 관리 코드가 실행될 때 부여되는 권한 집합을 결정합니다. 보안 정책은 어셈블리의 게시자(서명 도구로 생성된 서명이 있는 경우), 어셈블리를 다운로드한 웹 사이트 및 영역(Internet Explorer 용어), 어셈블리의 강력한 이름 등에 대해 설정될 수 있습니다. 예를 들어, 컴퓨터 관리자는 특정 웹 사이트에서 다운로드되고 지정된 소프트웨어 회사에서 서명한 모든 코드가 컴퓨터의 데이터베이스에 액세스할 수 있지만 컴퓨터의 디스크에 쓰지는 못하도록 보안 정책을 설정할 수 있습니다.  
  
## <a name="strong-named-assemblies-and-signing-tools"></a>강력한 이름의 어셈블리 및 서명 도구  

 > [!WARNING]
 > 강력한 이름을 보안용으로 사용하지 마세요. 강력한 이름은 고유한 ID를 제공할 뿐입니다.

 서로 다르지만 보완적인 두 가지 방법, 즉 강력한 이름을 사용하거나 [SignTool.exe(서명 도구)](../../../docs/framework/tools/signtool-exe.md)를 사용하여 어셈블리에 서명할 수 있습니다. 강력한 이름을 사용하여 어셈블리에 서명하면 어셈블리 매니페스트를 포함하는 파일에 공개 키 암호화가 추가됩니다. 이 방법을 사용하면 참조를 확인할 때 이름의 고유성이 보장되고 이름 스푸핑을 방지할 수 있으며, 호출자에게 ID가 제공됩니다.  
  
 어떤 신뢰 수준도 강력한 이름과 연결되지 않기 때문에 [SignTool.exe(서명 도구)](../../../docs/framework/tools/signtool-exe.md)가 필요합니다. 두 가지 서명 도구를 사용하려면 게시자는 외부 기관에서 ID를 증명 받은 후 인증서를 얻어야 합니다. 이 인증서는 파일에 포함되며, 관리자는 이 인증서를 사용하여 코드의 신뢰 여부를 판단합니다.  
  
 강력한 이름과 [SignTool.exe(서명 도구)](../../../docs/framework/tools/signtool-exe.md)를 사용하여 만든 디지털 서명을 어셈블리에 모두 제공하거나 둘 중 하나만 사용할 수 있습니다. 두 서명 도구는 한 번에 파일 하나씩만 서명할 수 있는데, 다중 파일 어셈블리의 경우에는 어셈블리 매니페스트를 포함하는 파일에 서명하면 됩니다. 강력한 이름은 어셈블리 매니페스트를 포함하는 파일에 저장되지만, [SignTool.exe(서명 도구)](../../../docs/framework/tools/signtool-exe.md)로 만든 서명은 어셈블리 매니페스트를 포함하는 PE(이식 가능한 실행) 파일의 예약된 슬롯에 저장됩니다. [SignTool.exe(서명 도구)](../../../docs/framework/tools/signtool-exe.md)에서 생성된 서명을 사용하는 신뢰 계층 구조가 이미 있거나 정책에서 키 부분만 사용하고 신뢰 체인을 확인하지 않으면, 강력한 이름의 유무와 상관 없이 [SignTool.exe(서명 도구)](../../../docs/framework/tools/signtool-exe.md)를 사용하여 어셈블리를 서명할 수 있습니다.  
  
> [!NOTE]
>  어셈블리에 강력한 이름과 서명 도구 서명을 모두 사용하는 경우, 강력한 이름을 먼저 지정해야 합니다.  
  
 또한 공용 언어 런타임에서는 해시를 확인합니다. 어셈블리 매니페스트에는 해당 어셈블리를 구성하는 모든 파일의 목록이 들어 있는데, 이 목록에는 매니페스트가 처음 빌드되었을 당시의 각 파일의 해시가 포함됩니다. 각 파일이 로드될 때 파일의 내용은 해시되어 매니페스트에 저장된 해시 값과 비교됩니다. 두 해시가 일치하지 않으면 어셈블리가 로드되지 않습니다.  
  
 강력한 이름 지정과 [SignTool.exe(서명 도구)](../../../docs/framework/tools/signtool-exe.md)를 사용하는 서명은 무결성을 보장하므로 이 두 가지 형식의 어셈블리 증명 정보에 기반하여 기본 코드 액세스 보안 정책을 설정할 수 있습니다. 강력한 이름을 지정하고 [SignTool.exe(서명 도구)](../../../docs/framework/tools/signtool-exe.md)로 서명하는 경우 인증서와 디지털 서명을 통해 무결성을 보장합니다. 언급된 모든 기술, 즉 해시 확인, 강력한 이름 지정, [SignTool.exe(서명 도구)](../../../docs/framework/tools/signtool-exe.md)를 통한 서명 등은 어셈블리가 어떤 방식으로든 변경되지 않도록 하는 데 사용됩니다.  
  
## <a name="see-also"></a>참고 항목  
- [강력한 이름의 어셈블리](../../../docs/framework/app-domains/strong-named-assemblies.md)  
- [공용 언어 런타임의 어셈블리](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)  
- [SignTool.exe(서명 도구)](../../../docs/framework/tools/signtool-exe.md)
