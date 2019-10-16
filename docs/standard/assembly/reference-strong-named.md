---
title: '방법: 강력한 이름의 어셈블리 참조'
ms.date: 08/20/2019
helpviewer_keywords:
- strong-named assemblies, compile-time references
- compile-time assembly referencing
- assemblies [.NET Framework], strong-named
- assembly binding, strong-named
ms.assetid: 4c6a406a-b5eb-44fa-b4ed-4e95bb95a813
author: rpetrusha
ms.author: ronpet
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 324cd42a2781202f19e7e1cb5055d571f0c58cf5
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972614"
---
# <a name="how-to-reference-a-strong-named-assembly"></a>방법: 강력한 이름의 어셈블리 참조
강력한 이름의 어셈블리에서 형식이나 리소스를 참조하는 프로세스는 일반적으로 투명합니다. 컴파일 시간(초기 바인딩) 또는 런타임에 참조를 만들 수 있습니다.  
  
컴파일 시간 참조는 컴파일할 어셈블리가 다른 어셈블리를 명시적으로 참조한다고 컴파일러에 표시할 때 발생합니다. 컴파일 시간 참조를 사용하는 경우 컴파일러가 대상으로 지정된 강력한 이름의 어셈블리의 공개 키를 자동으로 가져오고 컴파일되는 어셈블리의 어셈블리 참조에 배치합니다.
  
> [!NOTE]
> 강력한 이름의 어셈블리는 다른 강력한 이름의 어셈블리에서 형식만 사용할 수 있습니다. 그러지 않으면 강력한 이름의 어셈블리 보안이 손상됩니다.  
  
## <a name="make-a-compile-time-reference-to-a-strong-named-assembly"></a>강력한 이름의 어셈블리에 대한 컴파일 시간 참조 만들기  

명령 프롬프트에서 다음 명령을 입력합니다.  

\<*compiler command*>  **/reference:** \<*assembly name*>  

이 명령에서 *compiler command*는 사용되는 언어의 컴파일러 명령이고, *assembly name*은 참조되는 어셈블리의 강력한 이름입니다. 라이브러리 어셈블리를 만들기 위해 **/t:library** 옵션과 같은 다른 컴파일러 옵션을 사용할 수도 있습니다.  

다음 예제에서는 *myLibAssembly.dll*이라는 강력한 이름의 어셈블리를 참조하는 *myAssembly.dll*이라는 어셈블리를 *myAssembly.cs*라는 코드 모듈에서 만듭니다.  

```cmd
csc /t:library myAssembly.cs /reference:myLibAssembly.dll  
```  

## <a name="make-a-run-time-reference-to-a-strong-named-assembly"></a>강력한 이름의 어셈블리에 대한 런타임 참조 만들기  
  
강력한 이름의 어셈블리에 대한 런타임 참조를 만드는 경우(예: <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 또는 <xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType> 메서드 사용), 참조되는 강력한 이름의 어셈블리의 표시 이름을 사용해야 합니다. 표시 이름의 구문은 다음과 같습니다.  

\<*assembly name*> **,** \<*version number*> **,** \<*culture*> **,** \<*public key token*>  

예:  

```console
myDll, Version=1.1.0.0, Culture=en, PublicKeyToken=03689116d3a4ae33   
```  

이 예제에서 `PublicKeyToken`은 16진수 형식의 공개 키 토큰입니다. 문화권 값이 없는 경우 `Culture=neutral`을 사용합니다.  

다음 코드 예제에서는 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드와 함께 이 정보를 사용하는 방법을 보여 줍니다.  

```cpp
Assembly^ myDll =
    Assembly::Load("myDll, Version=1.0.0.1, Culture=neutral, PublicKeyToken=9b35aa32c18d4fb1");
```

```csharp
Assembly myDll =
    Assembly.Load("myDll, Version=1.0.0.1, Culture=neutral, PublicKeyToken=9b35aa32c18d4fb1");
```

```vb
Dim myDll As Assembly = _
    Assembly.Load("myDll, Version=1.0.0.1, Culture=neutral, PublicKeyToken=9b35aa32c18d4fb1")
```

다음 [강력한 이름(Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md) 명령을 사용하여 특정 어셈블리에 대한 공개 키와 공개 키 토큰의 16진수 형식을 인쇄할 수 있습니다.  

**sn -Tp \<** *assembly* **>**  

공개 키 파일이 있는 경우 다음 명령을 대신 사용할 수 있습니다(명령줄 옵션의 대/소문자 차이 확인).  

**sn -tp \<** ‘공개 키 파일’ **>**   

## <a name="see-also"></a>참고 항목

- [강력한 이름의 어셈블리 만들기 및 사용](create-use-strong-named.md)
