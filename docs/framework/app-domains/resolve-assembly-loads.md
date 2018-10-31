---
title: 어셈블리 로드 해결
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- assemblies [.NET Framework], resolving loads
- application domains, loading assemblies
- resolving assembly loads
- assemblies [.NET Framework], loading
- application domains, resolving assembly loads
ms.assetid: 5099e549-f4fd-49fb-a290-549edd456c6a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bdd610ade931bedc9ee387b65b18efd1909ef58b
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50202213"
---
# <a name="resolving-assembly-loads"></a>어셈블리 로드 해결
.NET Framework에서는 어셈블리 로드를 보다 효율적으로 제어해야 하는 응용 프로그램에 대해 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 이벤트를 제공합니다. 이 이벤트를 처리하면 응용 프로그램이 정상적인 검색 경로 외부에서 로드 컨텍스트에 어셈블리를 로드하고, 여러 어셈블리 버전 중에서 로드할 버전을 선택하고, 동적 어셈블리를 내보내 반환하는 작업 등을 수행할 수 있습니다. 이 항목에서는 <xref:System.AppDomain.AssemblyResolve> 이벤트 처리 지침을 제공합니다.  
  
> [!NOTE]
>  리플렉션 전용 컨텍스트에서 어셈블리 로드를 확인하려면 <xref:System.AppDomain.ReflectionOnlyAssemblyResolve?displayProperty=nameWithType> 이벤트를 대신 사용합니다.  
  
## <a name="how-the-assemblyresolve-event-works"></a>AssemblyResolve 이벤트 작동 방식  
 <xref:System.AppDomain.AssemblyResolve> 이벤트 처리기를 등록하면 런타임에 이름으로 어셈블리에 바인딩하지 못할 때마다 처리기가 호출됩니다. 예를 들어 사용자 코드에서 다음 메서드를 호출하면 <xref:System.AppDomain.AssemblyResolve> 이벤트가 발생할 수 있습니다.  
  
-   첫 번째 인수가 로드할 어셈블리의 표시 이름을 나타내는 문자열(즉, <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> 속성에서 반환되는 문자열)인 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> 메서드 오버로드 또는 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드 오버로드  
  
-   첫 번째 인수가 로드할 어셈블리를 식별하는 <xref:System.Reflection.AssemblyName> 개체인 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> 메서드 오버로드 또는 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드 오버로드  
  
-   <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType> 메서드 오버로드  
  
-   다른 응용 프로그램 도메인의 개체를 인스턴스화하는 <xref:System.AppDomain.CreateInstance%2A?displayProperty=nameWithType> 또는 <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=nameWithType> 메서드 오버로드  
  
### <a name="what-the-event-handler-does"></a>이벤트 처리기의 용도  
 <xref:System.AppDomain.AssemblyResolve> 이벤트 처리기는 <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> 속성을 통해 로드할 어셈블리의 표시 이름을 받습니다. 처리기가 어셈블리 이름을 인식하지 못하는 경우 null(Visual Basic에서는 `Nothing`, Visual C++에서는 `nullptr`)이 반환됩니다.  
  
 처리기가 어셈블리 이름을 인식하면 요청을 충족하는 어셈블리를 로드하고 반환할 수 있습니다. 다음 목록에서는 몇 가지 샘플 시나리오를 설명합니다.  
  
-   처리기가 어셈블리 버전의 위치를 알고 있다면 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 또는 <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType> 메서드를 사용하여 어셈블리를 로드할 수 있으며, 성공할 경우 로드된 어셈블리를 반환할 수 있습니다.  
  
-   처리기가 바이트 배열로 저장된 어셈블리 데이터베이스에 액세스할 수 있는 경우 바이트 배열을 사용하는 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드 오버로드 중 하나를 사용하여 바이트 배열을 로드할 수 있습니다.  
  
-   처리기는 동적 어셈블리를 생성하고 반환할 수 있습니다.  
  
> [!NOTE]
>  처리기는 어셈블리를 로드 소스 컨텍스트에 로드하거나, 로드 컨텍스트에 로드하거나, 컨텍스트 없이 로드해야 합니다. 처리기가 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> 또는 <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=nameWithType> 메서드를 사용하여 어셈블리를 리플렉션 전용 컨텍스트에 로드하는 경우 <xref:System.AppDomain.AssemblyResolve> 이벤트를 발생시킨 로드 시도가 실패합니다.  
  
 적합한 어셈블리를 반환하는 것은 이벤트 처리기의 책임입니다. 처리기는 <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> 속성 값을 <xref:System.Reflection.AssemblyName.%23ctor%28System.String%29> 생성자에 전달하여 요청된 어셈블리의 표시 이름을 구문 분석할 수 있습니다. [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]부터 처리기는 <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> 속성을 사용하여 현재 요청이 다른 어셈블리의 종속성인지 여부를 확인합니다. 이 정보는 종속성을 충족하는 어셈블리를 식별하는 데 도움이 됩니다.  
  
 이벤트 처리기는 요청된 버전과 다른 어셈블리 버전을 반환할 수 있습니다.  
  
 대부분의 경우 처리기에서 반환되는 어셈블리는 처리기가 로드하는 컨텍스트에 관계없이 로드 컨텍스트에 나타납니다. 예를 들어 처리기가 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 메서드를 사용하여 어셈블리를 로드 소스 컨텍스트에 로드하는 경우 처리기에서 반환되는 어셈블리는 로드 컨텍스트에 표시됩니다. 그러나 다음과 같은 경우에는 처리기에서 반환되는 어셈블리가 컨텍스트 없이 나타납니다.  
  
-   즉, 처리기가 컨텍스트 없이 어셈블리를 로드합니다.  
  
-   <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> 속성이 null이 아닌 경우.  
  
-   요청하는 어셈블리(즉, <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> 속성에서 반환되는 어셈블리)가 컨텍스트 없이 로드된 경우.  
  
 컨텍스트에 대한 자세한 내용은 <xref:System.Reflection.Assembly.LoadFrom%28System.String%29?displayProperty=nameWithType> 메서드 오버로드를 참조하세요.  
  
 동일한 어셈블리의 여러 버전을 동일한 응용 프로그램 도메인에 로드할 수 있습니다. 이 방법은 형식 할당 문제를 일으킬 수 있으므로 권장되지 않습니다. [최선의 어셈블리 로드 방법](../../../docs/framework/deployment/best-practices-for-assembly-loading.md)을 참조하세요.  
  
### <a name="what-the-event-handler-should-not-do"></a>이벤트 처리기에서 수행하지 않아야 하는 작업  
 <xref:System.AppDomain.AssemblyResolve> 이벤트 처리의 기본 규칙은 알 수 없는 어셈블리를 반환하지 않아야 한다는 것입니다. 처리기를 작성할 때 이벤트를 발생시킬 수 있는 어셈블리를 알아야 합니다. 처리기는 다른 어셈블리에 대해 null을 반환해야 합니다.  
  
> [!IMPORTANT]
>  [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]부터 위성 어셈블리에 대해 <xref:System.AppDomain.AssemblyResolve> 이벤트가 발생합니다. 이 변경 내용은 처리기가 모든 어셈블리 로드 요청을 확인하려는 경우 이전 버전의 .NET Framework에 대해 작성된 이벤트 처리기에 영향을 줍니다. 알 수 없는 어셈블리를 무시하는 이벤트 처리기는 이러한 변경의 영향을 받지 않습니다. null을 반환하고 일반적인 대체 메커니즘을 따릅니다.  
  
 어셈블리를 로드할 때 이벤트 처리기는 <xref:System.AppDomain.AssemblyResolve> 이벤트가 재귀적으로 발생될 수 있게 하여 스택 오버플로가 발생할 수 있는 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> 또는 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드 오버로드를 사용하면 안 됩니다. 이 항목의 앞부분에 제공된 목록을 참조하세요. 이 문제는 모든 이벤트 처리기가 반환될 때까지 예외가 throw되지 않기 때문에 로드 요청에 대한 예외 처리를 제공하는 경우에도 발생합니다. 따라서 다음 코드는 `MyAssembly`를 찾을 수 없는 경우 스택 오버플로를 발생시킬 수 있습니다.  
  
 [!code-cpp[AssemblyResolveRecursive#1](../../../samples/snippets/cpp/VS_Snippets_CLR/assemblyresolverecursive/cpp/example.cpp#1)]
 [!code-csharp[AssemblyResolveRecursive#1](../../../samples/snippets/csharp/VS_Snippets_CLR/assemblyresolverecursive/cs/example.cs#1)]
 [!code-vb[AssemblyResolveRecursive#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/assemblyresolverecursive/vb/example.vb#1)]  
  
## <a name="see-also"></a>참고 항목  
- [최선의 어셈블리 로드 방법](../../../docs/framework/deployment/best-practices-for-assembly-loading.md)  
- [응용 프로그램 도메인 사용](../../../docs/framework/app-domains/use.md)
