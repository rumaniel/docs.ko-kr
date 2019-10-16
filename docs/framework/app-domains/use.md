---
title: 애플리케이션 도메인 사용
ms.date: 03/30/2017
helpviewer_keywords:
- application domains, about
- common language runtime, application domains
- runtime, application domains
ms.assetid: c6d99815-e022-4d2c-9420-1d7ab5b9d504
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 11774620dba03cc980ec3e2e2d3bd1a855dc6295
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053050"
---
# <a name="using-application-domains"></a>애플리케이션 도메인 사용

애플리케이션 도메인은 공용 언어 런타임에 대한 격리 단위를 제공하고 프로세스 내에서 생성되고 실행됩니다. 애플리케이션 도메인은 대개 런타임을 프로세스로 로드하고 애플리케이션 도메인 내에서 사용자 코드를 실행하는 애플리케이션인 런타임 호스트에서 만들어집니다. 런타임 호스트는 프로세스와 기본 애플리케이션 도메인을 만들고 그 내부에서 관리 코드를 실행합니다. 런타임 호스트에는 ASP.NET, Microsoft Internet Explorer 및 Windows 셸이 포함됩니다.  
  
대부분 애플리케이션의 경우 자체적인 애플리케이션 도메인을 만들 필요가 없습니다. 런타임 호스트에서 필요한 애플리케이션 도메인을 만듭니다. 그러나 애플리케이션이 코드를 분리하거나 DLL을 사용하고 언로드해야 할 경우 직접 추가적인 애플리케이션 도메인을 만들고 구성할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  

[방법: 애플리케이션 도메인 만들기](how-to-create-an-application-domain.md)  
애플리케이션 도메인을 프로그래밍 방식으로 만드는 방법을 설명합니다.  
  
[방법: 애플리케이션 도메인 언로드](how-to-unload-an-application-domain.md)  
애플리케이션 도메인을 프로그래밍 방식으로 언로드하는 방법을 설명합니다.  
  
[방법: 애플리케이션 도메인 구성](how-to-configure-an-application-domain.md)  
애플리케이션 도메인을 구성하는 방법을 소개합니다.  
  
[애플리케이션 도메인에서 설치 정보 검색](retrieve-setup-information.md)  
애플리케이션 도메인에서 설정 정보를 검색하는 방법을 설명합니다.  
  
[방법: 애플리케이션 도메인에 어셈블리 로드](how-to-load-assemblies-into-an-application-domain.md)  
어셈블리를 애플리케이션 도메인으로 로드하는 방법을 설명합니다.  
  
[방법: 어셈블리에서 형식 및 멤버 정보 가져오기](../reflection-and-codedom/get-type-member-information.md)  
어셈블리에 대한 정보를 검색하는 방법을 설명합니다.  
  
[어셈블리 섀도 복사](shadow-copy-assemblies.md)  
어셈블리가 사용되는 동안 섀도 복사를 통해 어셈블리 업데이트를 허용하는 방법과 섀도 복사를 구성하는 방법을 설명합니다.  
  
[방법: 첫째 예외 알림 받기](how-to-receive-first-chance-exception-notifications.md)  
공용 언어 런타임이 예외 처리기 검색을 시작하기 전에 예외가 throw되었다는 알림을 받을 수 있는 방법을 설명합니다.  
  
[어셈블리 로드 해결](../../standard/assembly/resolve-loads.md)  
<xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 이벤트를 사용하여 어셈블리 로드 실패를 해결하는 방법에 대한 지침을 제공합니다.  
  
## <a name="reference"></a>참조  

<xref:System.AppDomain>  
애플리케이션 도메인을 나타냅니다. 애플리케이션 도메인을 만들고 제어하기 위한 메서드를 제공합니다.  
  
## <a name="related-sections"></a>관련 단원  
[.NET 어셈블리](../../standard/assembly/index.md)  
어셈블리가 실행하는 함수의 개요를 제공합니다.  
  
[어셈블리를 사용한 프로그래밍](../../standard/assembly/program.md)  
어셈블리를 만들고, 서명하고, 특성을 설정하는 방법에 대해 설명합니다.  
  
[동적 메서드 및 어셈블리 내보내기](../reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)  
동적 어셈블리를 만드는 방법에 대해 설명합니다.  
  
[애플리케이션 도메인](application-domains.md)  
애플리케이션 도메인에 대해 개념적으로 설명합니다.  
  
[리플렉션 개요](../reflection-and-codedom/reflection.md)  
**Reflection** 클래스를 사용하여 어셈블리에 대한 정보를 얻는 방법을 설명합니다.
