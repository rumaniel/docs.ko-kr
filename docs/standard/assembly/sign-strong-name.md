---
title: '방법: 강력한 이름으로 어셈블리 서명'
ms.date: 08/20/2019
helpviewer_keywords:
- strong-named assemblies, signing with strong names
- signing assemblies
- assemblies [.NET Framework], signing
- assemblies [.NET Framework], strong-named
ms.assetid: 2c30799a-a826-46b4-a25d-c584027a6c67
author: rpetrusha
ms.author: ronpet
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 527fd68ef40e152b57a1fc98113094d3b41fbaae
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972554"
---
# <a name="how-to-sign-an-assembly-with-a-strong-name"></a>방법: 강력한 이름으로 어셈블리 서명

> [!NOTE]
> .NET Core가 강력한 이름의 어셈블리를 지원하고 .NET Core 라이브러리의 모든 어셈블리는 서명되어 있지만 대부분의 타사 어셈블리에는 강력한 이름이 필요하지 않습니다. 자세한 내용은 GitHub의 [강력한 이름 서명](https://github.com/dotnet/corefx/blob/master/Documentation/project-docs/strong-name-signing.md)을 참조하세요.

강력한 이름으로 어셈블리에 서명하는 여러 가지 방법이 있습니다.  
  
- Visual Studio에서 프로젝트의 **속성** 대화 상자에서 **서명** 탭을 사용하는 방법. 이는 가장 쉽고 편리하게 강력한 이름으로 어셈블리에 서명하는 방법입니다.  
  
- [어셈블리 링커(Al.exe)](../../framework/tools/al-exe-assembly-linker.md)를 사용하여 .NET Framework 코드 모듈( *.netmodule* 파일)을 키 파일과 연결하는 방법.  
  
- 어셈블리 특성을 사용하여 강력한 이름 정보를 코드에 삽입하는 방법. 사용할 키 파일의 위치에 따라 <xref:System.Reflection.AssemblyKeyFileAttribute> 또는 <xref:System.Reflection.AssemblyKeyNameAttribute> 특성을 사용할 수 있습니다.  
  
- 컴파일러 옵션을 사용하는 방법.  
  
 강력한 이름으로 어셈블리를 서명하려면 암호화 키 쌍이 있어야 합니다. 키 쌍을 만드는 방법에 대한 자세한 내용은 [방법: 퍼블릭/프라이빗 키 쌍 만들기](create-public-private-key-pair.md)를 참조하세요.  
  
## <a name="create-and-sign-an-assembly-with-a-strong-name-by-using-visual-studio"></a>Visual Studio를 사용하여 강력한 이름으로 어셈블리를 만들고 서명  
  
1. **솔루션 탐색기**에서 프로젝트의 바로 가기 메뉴를 열고 **속성**을 선택합니다.  
  
2. **서명** 탭을 선택합니다.  
  
3. **어셈블리 서명** 상자를 선택합니다.  
  
4. **강력한 이름 키 파일 선택** 상자에서 **찾아보기**를 선택한 다음 키 파일로 이동합니다. 새 키 파일을 만들려면 **새로 만들기**를 선택하고 **강력한 이름 키 만들기** 대화 상자에 이름을 입력합니다.  
  
> [!NOTE]
> [어셈블리를 지연 서명](delay-sign.md)하기 위해 공개 키 파일을 선택합니다.  
  
### <a name="create-and-sign-an-assembly-with-a-strong-name-by-using-the-assembly-linker"></a>어셈블리 링커를 사용하여 강력한 이름으로 어셈블리를 만들고 서명  
  
[Visual Studio용 개발자 명령 프롬프트](../../framework/tools/developer-command-prompt-for-vs.md)에서 다음 명령을 입력합니다.  

**al** **/out:** \<*assemblyName*>  *\<moduleName>* **/keyfile:** \<*keyfileName*>  

여기서  

- *assemblyName*은 어셈블리 링커가 내보낼 강력하게 서명된 어셈블리( *.dll* 또는 *.exe* 파일)의 이름입니다.  
  
- *moduleName*은 하나 이상의 형식을 포함하는 .NET Framework 코드 모듈( *.netmodule* 파일)의 이름입니다. C# 또는 Visual Basic에서 `/target:module` 스위치로 코드를 컴파일하여 *.netmodule* 파일을 만들 수 있습니다.
  
- *keyfileName*은 키 쌍을 포함하는 컨테이너 또는 파일의 이름입니다. 어셈블리 링커는 현재 디렉터리를 기준으로 상대 경로를 해석합니다.  

다음 예제에서는 키 쌍 파일 *sgKey.snk*를 사용하여 강력한 이름으로 *MyAssembly.dll* 어셈블리에 서명합니다.  

```console
al /out:MyAssembly.dll MyModule.netmodule /keyfile:sgKey.snk  
```  
  
이 도구에 대한 자세한 내용은 [어셈블리 링커](../../framework/tools/al-exe-assembly-linker.md)를 참조하십시오.  
  
## <a name="sign-an-assembly-with-a-strong-name-by-using-attributes"></a>특성을 사용하여 강력한 이름으로 어셈블리 서명  
  
1. <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=nameWithType> 또는 <xref:System.Reflection.AssemblyKeyNameAttribute> 특성을 소스 코드 모듈에 추가하고, 강력한 이름으로 어셈블리를 서명할 때 사용할 키 쌍이 포함된 컨테이너 또는 파일의 이름을 지정합니다.  
   
2. 소스 코드 파일을 정상적으로 컴파일합니다.  
   
   > [!NOTE]
   > C# 및 Visual Basic 컴파일러에서는 소스 코드에 <xref:System.Reflection.AssemblyKeyFileAttribute> 또는 <xref:System.Reflection.AssemblyKeyNameAttribute> 특성이 나올 때 컴파일러 경고(각각 CS1699 및 BC41008)를 발생시킵니다. 이런 경고는 무시할 수 있습니다.  

다음 예제에서는 어셈블리가 컴파일된 디렉터리에 있는 *keyfile.snk*라는 키 파일과 함께 <xref:System.Reflection.AssemblyKeyFileAttribute> 특성을 사용합니다.  

```cpp
[assembly:AssemblyKeyFileAttribute("keyfile.snk")];
```

```csharp
[assembly:AssemblyKeyFileAttribute("keyfile.snk")]
```

```vb
<Assembly:AssemblyKeyFileAttribute("keyfile.snk")>
```

또한, 소스 파일을 컴파일할 때 어셈블리 서명을 연기할 수 있습니다. 자세한 내용은 [어셈블리 지연 서명](delay-sign.md)을 참조하세요.  

## <a name="sign-an-assembly-with-a-strong-name-by-using-the-compiler"></a>컴파일러를 사용하여 강력한 이름으로 어셈블리 서명  

C# 및 Visual Basic 컴파일러에서 `/keyfile` 또는 `/delaysign` 컴파일러 옵션을 사용하거나 C++에서 `/KEYFILE` 또는 `/DELAYSIGN` 링커 옵션을 사용하여 소스 코드 파일을 컴파일합니다. 옵션 이름 다음에 콜론과 키 파일의 이름을 추가합니다. 명령줄 컴파일러를 사용할 때, 소스 코드 파일이 포함된 디렉터리에 키 파일을 복사할 수 있습니다.  

지연 서명에 대한 자세한 내용은 [어셈블리 지연 서명](delay-sign.md)을 참조하세요.  

다음 예제에서는 C# 컴파일러를 사용하고 키 파일 *sgKey.snk*를 사용하여 강력한 이름으로 *UtilityLibrary.dll* 어셈블리에 서명합니다.  

```cmd
csc /t:library UtilityLibrary.cs /keyfile:sgKey.snk  
```  

## <a name="see-also"></a>참고 항목

- [강력한 이름의 어셈블리 만들기 및 사용](create-use-strong-named.md)
- [방법: 퍼블릭/프라이빗 키 쌍 만들기](create-public-private-key-pair.md)
- [Al.exe(어셈블리 링커)](../../framework/tools/al-exe-assembly-linker.md)
- [어셈블리 지연 서명](delay-sign.md)
- [어셈블리 및 매니페스트 서명 관리](/visualstudio/ide/managing-assembly-and-manifest-signing)
- [서명 페이지, 프로젝트 디자이너](/visualstudio/ide/reference/signing-page-project-designer)
