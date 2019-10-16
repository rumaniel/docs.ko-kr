---
title: 애플리케이션 도메인 및 어셈블리를 사용한 프로그래밍
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], programming
- programming assemblies
- application domains, programming
- programming application domains
ms.assetid: 96d3b8e3-bef8-4da0-9a81-9841e23a94e9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 84d674f7ae8e80d7a5e6a40539e3330fcfa9b563
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053111"
---
# <a name="programming-with-application-domains-and-assemblies"></a>애플리케이션 도메인 및 어셈블리를 사용한 프로그래밍

Microsoft Internet Explorer, ASP.NET 및 Windows 셸과 같은 호스트는 프로세스에 공용 언어 런타임을 로드하고, 해당 프로세스에서 [애플리케이션 도메인](application-domains.md)을 만든 다음 .NET Framework 애플리케이션을 실행할 때 해당 애플리케이션 도메인에서 사용자 코드를 로드한 후 실행합니다. 대부분의 경우 런타임 호스트가 알아서 작업을 진행하므로 애플리케이션 도메인 만들기 및 어셈블리 로드에 대해 걱정할 필요가 없습니다.  
  
그러나 공용 언어 런타임을 호스트하는 애플리케이션 만들거나, 프로그래밍 방식으로 언로드하려는 도구 또는 코드를 만들거나, 즉석에서 언로드 및 다시 로드할 수 있는 플러그형 구성 요소를 만드는 경우 자체 애플리케이션 도메인을 만들게 됩니다. 런타임 호스트를 만들지 않더라도 이 섹션을 통해 애플리케이션 도메인으로 작업하는 방법 및 이러한 애플리케이션 도메인에 로드되는 어셈블리에 대한 중요한 정보를 얻을 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  

[애플리케이션 도메인 및 어셈블리 방법 항목](application-domains-and-assemblies-how-to-topics.md)  
애플리케이션 도메인 및 어셈블리를 사용한 프로그래밍에 대한 개념 설명서에 나오는 모든 방법 항목에 대한 링크를 제공합니다.  
  
[애플리케이션 도메인 사용](use.md)  
애플리케이션 도메인 만들기, 구성 및 사용에 대한 예제를 제공합니다.  
  
[어셈블리를 사용한 프로그래밍](../../standard/assembly/program.md)  
어셈블리를 만들고, 서명하고, 특성을 설정하는 방법에 대해 설명합니다.  
  
## <a name="related-sections"></a>관련 단원  

[동적 메서드 및 어셈블리 내보내기](../reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)  
동적 어셈블리를 만드는 방법에 대해 설명합니다.  
  
[.NET 어셈블리](../../standard/assembly/index.md)  
어셈블리에 대해 개념적으로 설명합니다.  
  
[애플리케이션 도메인](application-domains.md)  
애플리케이션 도메인에 대해 개념적으로 설명합니다.  
  
[리플렉션 개요](../reflection-and-codedom/reflection.md)  
**Reflection** 클래스를 사용하여 어셈블리에 대한 정보를 얻는 방법을 설명합니다.
