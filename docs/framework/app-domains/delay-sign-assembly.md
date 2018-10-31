---
title: 어셈블리 서명 연기
ms.date: 07/31/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- deferring assembly signing
- signing assemblies
- assemblies [.NET Framework], signing
- strong-named assemblies, delaying assembly signing
- partial assembly signing
ms.assetid: 9d300e17-5bf1-4360-97da-2aa55efd9070
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 87346b28ff98c453949fe31aea4d0ef1880b0095
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50192633"
---
# <a name="delay-signing-an-assembly"></a>어셈블리 서명 연기
조직에 개발자가 일상적으로 액세스할 수 없는 엄격하게 보호된 키 쌍이 있을 수 있습니다. 대부분이 경우 공개 키를 사용할 수 있지만 개인 키에 대한 액세스는 몇몇 개인만으로 제한됩니다. 강력한 이름을 사용하여 어셈블리를 개발할 경우 강력한 이름의 대상 어셈블리를 참조하는 각 어셈블리에는 대상 어셈블리에 강력한 이름을 지정하는 데 사용되는 공개 키의 토큰이 포함됩니다. 이를 위해 개발 프로세스 중에 공개 키를 사용할 수 있어야 합니다.  
  
 빌드 시간에 지연된 서명이나 부분 서명을 사용하여 PE(이식 가능한 실행 파일) 파일에서 강력한 이름 시그니처에 사용할 공간을 예약하지만, 약간 이후 단계까지(일반적으로 어셈블리를 제공하기 바로 전) 실제 서명을 연기할 수 있습니다.  
  
 다음 단계에서는 어셈블리 서명을 연기하는 프로세스를 간략하게 설명합니다.  
  
1.  최종 서명을 수행할 조직에서 키 쌍의 공개 키 부분을 가져옵니다. 일반적으로 이 키는 .snk 파일 형식으로, [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)]에서 제공된 [강력한 이름 도구(Sn.exe)](../../../docs/framework/tools/sn-exe-strong-name-tool.md)를 사용하여 만들 수 있습니다.  
  
2.  <xref:System.Reflection>의 두 가지 사용자 지정 특성을 사용하여 어셈블리에 대한 소스 코드를 주석으로 처리합니다.  
  
    -   <xref:System.Reflection.AssemblyKeyFileAttribute> - 매개 변수로 공개 키가 포함된 파일의 이름을 생성자에 전달합니다.  
  
    -   <xref:System.Reflection.AssemblyDelaySignAttribute> - 매개 변수로 **true**를 생성자에 전달하여 서명 지연에 사용 중임을 나타냅니다. 예:  
  
         [!code-cpp[AssemblyDelaySignAttribute#4](../../../samples/snippets/cpp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cpp/source2.cpp#4)]
         [!code-csharp[AssemblyDelaySignAttribute#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cs/source2.cs#4)]
         [!code-vb[AssemblyDelaySignAttribute#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AssemblyDelaySignAttribute/vb/source2.vb#4)]  
  
3.  컴파일러는 공개 키를 어셈블리 매니페스트에 삽입하고 PE 파일에서 전체 강력한 이름 시그니처에 사용할 공간을 예약합니다. 실제 공개 키는 어셈블리가 빌드되는 동안 저장되어야 합니다. 그래야 이 어셈블리를 참조하는 다른 어셈블리가 자체적인 어셈블리 참조에 저장할 키를 가져올 수 있습니다.  
  
4.  어셈블리에 유효한 강력한 이름 시그니처가 없으므로 해당 시그니처의 확인이 해제되어야 합니다. 강력한 이름 도구와 함께 **–Vr** 옵션을 사용하여 이 작업을 수행할 수 있습니다.  
  
     다음 예제에서는 `myAssembly.dll`이라는 어셈블리에 대한 확인을 해제합니다.  
  
    ```  
    sn –Vr myAssembly.dll  
    ```  
  
     ARM(Advanced RISC Machine) 마이크로프로세서와 같은 강력한 이름 도구를 실행할 수 없는 플랫폼에서 확인을 해제하려면 **–Vk** 옵션을 사용하여 레지스트리 파일을 만듭니다. 확인을 해제하려는 컴퓨터의 레지스트리에 레지스트리 파일을 가져옵니다. 다음 예제에서는 `myAssembly.dll`에 대한 레지스트리 파일을 만듭니다.  
  
    ```  
    sn –Vk myRegFile.reg myAssembly.dll  
    ```  
  
     **–Vr** 또는 **–Vk** 옵션을 사용하여 테스트 키 서명에 대해 .snk 파일을 선택적으로 포함할 수 있습니다.  
  
    > [!WARNING]
    > 강력한 이름을 보안용으로 사용하지 마세요. 강력한 이름은 고유한 ID를 제공할 뿐입니다.
  
    > [!NOTE]
    >  64비트 컴퓨터에서 Visual Studio를 통해 개발하는 동안 서명 연기를 사용하고 **모든 CPU**에 대한 어셈블리를 컴파일할 경우 **-Vr** 옵션을 두 번 적용해야 할 수 있습니다. Visual Studio에서 **모든 CPU**는 **플랫폼 대상** 빌드 속성의 값이고 명령줄에서 컴파일할 경우 기본값입니다. 응용 프로그램을 명령줄 또는 파일 탐색기에서 실행하려면 [Sn.exe(강력한 이름 도구)](../../../docs/framework/tools/sn-exe-strong-name-tool.md)의 64비트 버전을 사용하여 **-Vr** 옵션을 어셈블리에 적용합니다. 디자인 타임에 어셈블리를 Visual Studio에 로드하려면(예: 어셈블리에 응용 프로그램의 다른 어셈블리에서 사용되는 구성 요소가 포함된 경우) 강력한 이름 도구의 32비트 버전을 사용합니다. 그 이유는 JIT(Just-In-Time) 컴파일러가 명령줄에서 실행되는 어셈블리를 64비트 네이티브 코드로 컴파일하고, 디자인 타임 환경에 로드되는 어셈블리를 32비트 네이티브 코드로 컴파일하기 때문입니다.  
  
5.  나중에, 일반적으로 제공하기 바로 전에 강력한 이름 도구와 함께 **–R** 옵션을 사용하여 실제 강력한 이름으로 서명하기 위해 조직의 서명 기관에 어셈블리를 제출합니다.  
  
     다음 예제에서는 `myAssembly.dll` 키 쌍 파일을 사용하여 강력한 이름으로 `sgKey.snk` 어셈블리에 서명할 수 있습니다.  
  
    ```  
    sn -R myAssembly.dll sgKey.snk  
    ```  
  
## <a name="see-also"></a>참고 항목  
- [어셈블리 만들기](../../../docs/framework/app-domains/create-assemblies.md)  
- [방법: 공개/개인 키 쌍 만들기](../../../docs/framework/app-domains/how-to-create-a-public-private-key-pair.md)  
- [Sn.exe(강력한 이름 도구)](../../../docs/framework/tools/sn-exe-strong-name-tool.md)  
- [어셈블리를 사용한 프로그래밍](../../../docs/framework/app-domains/programming-with-assemblies.md)
