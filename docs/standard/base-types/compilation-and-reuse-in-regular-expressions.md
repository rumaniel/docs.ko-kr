---
title: 정규식의 컴파일 및 다시 사용
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- parsing text with regular expressions, compilation
- searching with regular expressions, compilation
- .NET Framework regular expressions, engines
- .NET Framework regular expressions, compilation
- regular expressions, compilation
- compilation, regular expressions
- pattern-matching with regular expressions, compilation
- regular expressions, engines
ms.assetid: 182ec76d-5a01-4d73-996c-0b0d14fcea18
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ca2dfcfbb5407be2727343a5b3a5b429af83ae20
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64634593"
---
# <a name="compilation-and-reuse-in-regular-expressions"></a>정규식의 컴파일 및 다시 사용
정규식 엔진이 식을 컴파일하는 방법과 정규식이 캐시되는 방식을 이해하면 정규식을 광범위하게 사용하는 애플리케이션의 성능을 최적화할 수 있습니다. 이 항목에서는 컴파일과 캐시 둘 다에 대해 설명합니다.  
  
## <a name="compiled-regular-expressions"></a>컴파일된 정규식  
 기본적으로 정규식 엔진은 정규식을 내부 명령 시퀀스(Microsoft 중간 언어, 즉 MSIL과 다른 고급 코드)로 컴파일합니다. 엔진은 정규식을 실행할 때 내부 코드를 해석합니다.  
  
 <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType> 옵션으로 <xref:System.Text.RegularExpressions.Regex> 개체를 생성하는 경우 정규식이 고급 정규식 내부 명령 대신 명시적 MSIL 코드로 컴파일됩니다. 이렇게 하면 .NET의 JIT(Just-In-Time) 컴파일러가 성능 향상을 위해 식을 네이티브 기계어 코드로 변환할 수 있습니다.  
  
그러나 생성된 MSIL을 언로드할 수 없습니다. 코드를 언로드하는 유일한 방법은 전체 애플리케이션 도메인을 언로드하는 것(즉, 모든 애플리케이션 코드 언로드)입니다. 실제로 <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType> 옵션으로 정규식을 컴파일하고 나면, 정규식을 만든 <xref:System.Text.RegularExpressions.Regex> 개체가 가비지 수집에 사용하도록 해제된 경우에도 컴파일된 식에 사용된 리소스를 해제하지 않습니다.  
  
 너무 많은 리소스가 사용되지 않도록 <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType> 옵션으로 컴파일하는 정규식 수를 제한해야 합니다. 애플리케이션이 많거나 무제한 개수의 정규식을 사용해야 하는 경우 각 식을 컴파일하지 않고 해석해야 합니다. 그러나 적은 개수의 정규식을 반복해서 사용하는 경우 성능 향상을 위해 <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType>로 컴파일해야 합니다. 한 가지 대안은 미리 컴파일된 정규식을 사용하는 것입니다. <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A> 메서드를 사용하여 모든 식을 재사용 가능한 DLL로 컴파일할 수 있습니다. 이렇게 하면 컴파일된 정규식의 속도에 따른 이점은 계속 활용하면서 런타임 시 컴파일할 필요가 없습니다.  
  
## <a name="the-regular-expressions-cache"></a>정규식 캐시  
 성능 향상을 위해 정규식 엔진은 애플리케이션 수준의 컴파일된 정규식 캐시를 유지 관리합니다. 캐시는 정적 메서드 호출에만 사용되는 정규식 패턴을 저장합니다. 인스턴스 메서드에 제공된 정규식 패턴은 캐시되지 않습니다. 따라서 사용할 때마다 식을 고급 바이트 코드로 다시 구문 분석할 필요가 없습니다.  
  
 캐시된 정규식의 최대 개수는 `static`(Visual Basic의 경우 `Shared`) <xref:System.Text.RegularExpressions.Regex.CacheSize%2A?displayProperty=nameWithType> 속성 값에 의해 결정됩니다. 기본적으로 정규식 엔진은 최대 15개의 컴파일된 정규식을 캐시합니다. 컴파일된 정규식 개수가 캐시 크기를 초과하면 가장 오래 전에 사용한 정규식이 삭제되고 새 정규식이 캐시됩니다.  
  
 애플리케이션은 다음 두 가지 방법 중 하나로 미리 컴파일된 정규식을 활용할 수 있습니다.  
  
- <xref:System.Text.RegularExpressions.Regex> 개체의 정적 메서드를 사용하여 정규식을 정의합니다. 다른 정적 메서드 호출에서 이미 정의된 정규식 패턴을 사용하는 경우 정규식 엔진이 캐시에서 검색합니다. 이미 정의된 정규식 패턴을 사용하지 않는 경우 엔진이 정규식을 컴파일하고 캐시에 추가합니다.  
  
- 해당 정규식 패턴이 필요할 때까지 기존 <xref:System.Text.RegularExpressions.Regex> 개체를 다시 사용합니다.  
  
 개체 인스턴스화 및 정규식 컴파일의 오버헤드 때문에 수많은 <xref:System.Text.RegularExpressions.Regex> 개체를 만들고 금세 삭제할 경우 매우 큰 비용이 듭니다. 다수의 정규식을 사용하는 애플리케이션의 경우 정적 `Regex` 메서드 호출을 사용하고 정규식 캐시의 크기를 늘려 성능을 최적화할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [.NET 정규식](../../../docs/standard/base-types/regular-expressions.md)
