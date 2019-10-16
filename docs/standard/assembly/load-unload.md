---
title: '방법: 어셈블리 로드 및 언로드'
ms.date: 08/19/2019
ms.assetid: 6a4f490f-3576-471f-9533-003737cad4a3
ms.openlocfilehash: 77ea97c2fc324287e9c697d630def98241432c9f
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972674"
---
# <a name="how-to-load-and-unload-assemblies"></a>방법: 어셈블리 로드 및 언로드
프로그램에서 참조하는 어셈블리는 공용 언어 런타임에 의해 자동으로 로드되지만 현재 애플리케이션 도메인에 특정 어셈블리를 동적으로 로드할 수도 있습니다. 자세한 내용은 [방법: 애플리케이션 도메인에 어셈블리 로드](../../framework/app-domains/how-to-load-assemblies-into-an-application-domain.md)를 참조하세요.

.NET Framework에서는 해당 어셈블리가 포함된 애플리케이션 도메인을 모두 언로드하지 않으면 개별 어셈블리를 언로드할 수 없습니다. 어셈블리가 범위를 벗어난 경우에도 실제 어셈블리 파일은 해당 파일을 포함하는 애플리케이션 도메인이 모두 언로드될 때까지 로드된 상태로 유지됩니다. .NET Core에서는 <xref:System.Runtime.Loader.AssemblyLoadContext?displayProperty=nameWithType> 클래스가 어셈블리 언로드를 처리합니다. 자세한 내용은 [.NET Core에서 어셈블리 언로드 기능을 사용하고 디버그하는 방법](unloadability.md)을 참조하세요.

## <a name="load-and-unload-assemblies"></a>어셈블리 로드 및 언로드

어셈블리를 애플리케이션 도메인에 로드하려면 <xref:System.AppDomain> 및 <xref:System.Reflection.Assembly> 클래스에 포함된 여러 로드 메서드 중 하나를 사용하세요. 자세한 내용은 [방법: 애플리케이션 도메인에 어셈블리 로드](../../framework/app-domains/how-to-load-assemblies-into-an-application-domain.md)를 참조하세요. .NET Core는 단일 애플리케이션 도메인만 지원합니다. 

.NET Framework에서 어셈블리를 언로드하려면 해당 어셈블리를 포함하는 모든 애플리케이션 도메인을 언로드해야 합니다. 애플리케이션 도메인을 언로드하려면 <xref:System.AppDomain.Unload%2A?displayProperty=nameWithType> 메서드를 사용하세요. 자세한 내용은 [방법: 애플리케이션 도메인 언로드](../../framework/app-domains/how-to-unload-an-application-domain.md)를 참조하세요.

.NET Framework 애플리케이션에서 일부 어셈블리만 언로드하고 다른 어셈블리는 언로드하지 않으려는 경우 새 애플리케이션 도메인을 만들어 이 도메인 내에서 코드를 실행한 다음 해당 애플리케이션 도메인을 언로드하는 것이 좋습니다. 자세한 내용은 [방법: 애플리케이션 도메인 언로드](../../framework/app-domains/how-to-unload-an-application-domain.md)를 참조하세요.  

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../../csharp/programming-guide/index.md)
- [프로그래밍 개념(Visual Basic)](../../visual-basic/programming-guide/concepts/index.md)
- [.NET 어셈블리](index.md)
- [방법: 애플리케이션 도메인에 어셈블리 로드](../../framework/app-domains/how-to-load-assemblies-into-an-application-domain.md)
