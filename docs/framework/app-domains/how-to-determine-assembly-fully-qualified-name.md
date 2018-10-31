---
title: '방법: 어셈블리의 정규화된 이름 식별'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- names [.NET Framework], fully qualified type names
- names [.NET Framework], assemblies
- assemblies [.NET Framework], names
ms.assetid: 009dae23-e1f6-4a64-9a9a-32e4c34802b0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bb5978859ba25e1595ac3da7a2d7dad8cc2cad85
ms.sourcegitcommit: 9bd8f213b50f0e1a73e03bd1e840c917fbd6d20a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50041104"
---
# <a name="how-to-determine-an-assembly39s-fully-qualified-name"></a>방법: 어셈블리의 정규화된 이름 식별
전역 어셈블리 캐시에서 어셈블리의 정규화된 이름을 찾으려면 전역 어셈블리 캐시 도구([Gacutil.exe](../../../docs/framework/tools/gacutil-exe-gac-tool.md))를 사용합니다. [방법: 전역 어셈블리 캐시의 내용 보기](../../../docs/framework/app-domains/how-to-view-the-contents-of-the-gac.md)를 참조하세요.  
  
 전역 어셈블리 캐시에 없는 어셈블리의 경우, 코드를 사용하여 콘솔이나 변수로 정보를 출력하거나 [Ildasm.exe(IL 디스어셈블러)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)를 사용하여 정규화된 이름이 포함된 어셈블리의 메타데이터를 검사하는 등 다양한 방법으로 정규화된 어셈블리 이름을 가져올 수 있습니다.  
  
-   응용 프로그램에서 어셈블리를 이미 로드한 경우 <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> 속성의 값을 검색하여 정규화된 이름을 가져올 수 있습니다. 어셈블리가 GAC에 있는지 여부에 관계없이 이 접근 방식을 사용할 수 있습니다. 예제에서는 그림을 제공합니다.  
  
-   어셈블리의 파일 시스템 경로를 알고 있는 경우 static(Visual basic에서는 `Shared`) <xref:System.Reflection.AssemblyName.GetAssemblyName%2A?displayProperty=nameWithType> 메서드를 호출하여 정규화된 어셈블리 이름을 가져올 수 있습니다. 다음은 간단한 예제입니다.  
  
     [!code-csharp[System.Reflection.AssemblyName.GetAssemblyName#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.reflection.assemblyname.getassemblyname/cs/getassemblyname1.cs#1)]
     [!code-vb[System.Reflection.AssemblyName.GetAssemblyName#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.reflection.assemblyname.getassemblyname/vb/getassemblyname1.vb#1)]  
  
-   [Ildasm.exe(IL 디스어셈블러)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)를 사용하여 정규화된 이름이 포함된 어셈블리의 메타데이터를 검사할 수 있습니다.  
  
 버전, 문화권 및 어셈블리 이름과 같은 어셈블리 특성 설정에 대한 자세한 내용은 [어셈블리 특성 설정](../../../docs/framework/app-domains/set-assembly-attributes.md)을 참조하세요. 어셈블리에 강력한 이름을 지정하는 방법에 대한 자세한 내용은 [강력한 이름의 어셈블리 만들기 및 사용](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)을 참조하세요.  
  
## <a name="example"></a>예  
 다음 코드 예제에서는 지정된 클래스를 포함하는 어셈블리의 정규화된 이름을 콘솔에 표시하는 방법을 보여 줍니다. 앱에서 이미 로드한 어셈블리의 이름을 검색하므로 어셈블리가 GAC에 있는지 여부는 중요하지 않습니다.  
  
 [!code-cpp[Assembly.Fullname#2](../../../samples/snippets/cpp/VS_Snippets_CLR/Assembly.FullName/CPP/example2.cpp#2)]
 [!code-csharp[Assembly.Fullname#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Assembly.FullName/CS/example2.cs#2)]
 [!code-vb[Assembly.Fullname#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Assembly.FullName/VB/example2.vb#2)]  
  
## <a name="see-also"></a>참고 항목  
- [어셈블리 이름](../../../docs/framework/app-domains/assembly-names.md)  
- [어셈블리 만들기](../../../docs/framework/app-domains/create-assemblies.md)  
- [강력한 이름의 어셈블리 만들기 및 사용](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)  
- [전역 어셈블리 캐시](../../../docs/framework/app-domains/gac.md)  
- [런타임에서 어셈블리를 찾는 방법](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)  
- [어셈블리를 사용한 프로그래밍](../../../docs/framework/app-domains/programming-with-assemblies.md)
