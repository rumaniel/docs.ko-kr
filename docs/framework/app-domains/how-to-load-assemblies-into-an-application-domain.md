---
title: '방법: 응용 프로그램 도메인에 어셈블리 로드'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- application domains, loading assemblies
- loading assemblies
ms.assetid: 1432aa2d-bd83-4346-bf3b-a1b7920e2aa9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5e91441f593b7533026d5980f8cf39fb5a3d5b71
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50193073"
---
# <a name="how-to-load-assemblies-into-an-application-domain"></a>방법: 응용 프로그램 도메인에 어셈블리 로드
응용 프로그램 도메인에 어셈블리를 로드하는 방법에는 여러 가지가 있습니다. <xref:System.Reflection.Assembly?displayProperty=nameWithType> 클래스의 `static`(Visual Basic에서는 `Shared`) <xref:System.Reflection.Assembly.Load%2A> 메서드를 사용하는 것이 좋습니다. 어셈블리를 로드할 수 있는 다른 방법은 다음과 같습니다.  
  
-   <xref:System.Reflection.Assembly> 클래스의 <xref:System.Reflection.Assembly.LoadFrom%2A> 메서드는 파일 위치가 지정된 경우 어셈블리를 로드합니다. 이 메서드로 어셈블리를 로드하는 경우 다른 로드 컨텍스트가 사용됩니다.  
  
-   <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A> 및 <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A> 메서드는 리플렉션 전용 컨텍스트에 어셈블리를 로드합니다. 이 컨텍스트에 로드된 어셈블리는 검사할 수만 있고 실행할 수 없으므로 다른 플랫폼을 대상으로 하는 어셈블리를 검사할 수 있습니다. [방법: 리플렉션 전용 컨텍스트에 어셈블리 로드](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)를 참조하세요.  
  
> [!NOTE]
>  리플렉션 전용 컨텍스트는 .NET Framework 버전 2.0의 새로운 기능입니다.  
  
-   <xref:System.AppDomain> 클래스의 <xref:System.AppDomain.CreateInstance%2A> 및 <xref:System.AppDomain.CreateInstanceAndUnwrap%2A>과 같은 메서드는 응용 프로그램 도메인에 어셈블리를 로드할 수 있습니다.  
  
-   <xref:System.Type> 클래스의 <xref:System.Type.GetType%2A> 메서드는 어셈블리를 로드할 수 있습니다.  
  
-   <xref:System.AppDomain?displayProperty=nameWithType> 클래스의 <xref:System.AppDomain.Load%2A> 메서드는 어셈블리를 로드할 수 있지만 COM 상호 운용성을 위해 주로 사용됩니다. 호출 시 사용된 응용 프로그램 도메인 이외의 응용 프로그램 도메인에 어셈블리를 로드하는 데 사용하면 안 됩니다.  
  
> [!NOTE]
>  .NET Framework 버전 2.0부터 런타임은 현재 로드된 런타임보다 높은 버전 번호를 가진 .NET Framework 버전으로 컴파일된 어셈블리를 로드하지 않습니다. 이는 버전 번호의 주 버전 및 부 버전 구성 요소 조합에 적용됩니다.  
  
 로드된 어셈블리의 JIT(Just-In-Time) 컴파일된 코드가 응용 프로그램 도메인 간에 공유되는 방식을 지정할 수 있습니다. 자세한 내용은 [응용 프로그램 도메인 및 어셈블리](https://msdn.microsoft.com/library/433b04ae-4ba8-4849-9dbd-79194f240346)를 참조하세요.  
  
## <a name="example"></a>예  
 다음 코드는 "example.exe" 또는 "example.dll"이라는 어셈블리를 로드 현재 응용 프로그램 도메인에 로드하고, 어셈블리에서 `Example` 형식을 가져온 다음 해당 형식에 대한 매개 변수가 없는 `MethodA` 메서드를 가져와서 실행합니다. 로드된 어셈블리에서 정보를 가져오는 방법에 대한 자세한 내용은 [형식 동적 로드 및 사용](../../../docs/framework/reflection-and-codedom/dynamically-loading-and-using-types.md)을 참조하세요.  
  
 [!code-cpp[System.AppDomain.Load#2](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.appdomain.load/cpp/source2.cpp#2)]
 [!code-csharp[System.AppDomain.Load#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.load/cs/source2.cs#2)]
 [!code-vb[System.AppDomain.Load#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.load/vb/source2.vb#2)]  
  
## <a name="see-also"></a>참고 항목  
- <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A>  
- [응용 프로그램 도메인으로 프로그래밍](application-domains.md#programming-with-application-domains)  
- [리플렉션](../../../docs/framework/reflection-and-codedom/reflection.md)  
- [응용 프로그램 도메인 사용](../../../docs/framework/app-domains/use.md)  
- [방법: 리플렉션 전용 컨텍스트에 어셈블리 로드](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)  
- [응용 프로그램 도메인 및 어셈블리](https://msdn.microsoft.com/library/433b04ae-4ba8-4849-9dbd-79194f240346)
