---
title: 데스크톱 응용 프로그램용 위성 어셈블리 만들기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- deploying applications [.NET Framework], resources
- resource files, deploying
- hub-and-spoke resource deployment model
- resource files, packaging
- application resources, packaging
- public keys, obtaining
- satellite assemblies
- assemblies [.NET Framework], signing
- application resources, deploying
- Al.exe
- GAC (global assembly cache), satellite assemblies
- Assembly Linker
- directory locations for satellite assemblies
- global assembly cache, satellite assemblies
- packaging application resources
- compiling satellite assemblies
- re-signing assemblies
ms.assetid: 8d5c6044-2919-41d2-8321-274706b295ac
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 17465b07172788f18a432784653afadda18467fe
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045693"
---
# <a name="creating-satellite-assemblies-for-desktop-apps"></a>데스크톱 응용 프로그램용 위성 어셈블리 만들기

리소스 파일은 지역화된 애플리케이션에서 중요한 역할을 합니다. 애플리케이션을 사용하여 사용자의 언어 및 문화권에서 문자열, 이미지 및 기타 데이터를 표시하고 사용자의 언어 또는 문화권에 대한 리소스를 사용할 수 없는 경우 대체 데이터를 제공할 수 있습니다. .NET Framework에서는 허브 및 스포크 모델을 사용하여 지역화된 리소스를 찾고 검색합니다. 허브는 지역화할 수 없는 실행 코드와 중립 또는 기본 문화권이라고 하는 단일 문화권의 리소스를 포함하는 주 어셈블리입니다. 기본 문화권은 애플리케이션의 대체 문화권으로, 지역화된 리소스를 사용할 수 없는 경우 사용됩니다. <xref:System.Resources.NeutralResourcesLanguageAttribute> 특성을 사용하여 애플리케이션의 기본 문화권의 문화를 지정합니다. 각 스포크는 지역화된 단일 문화권의 리소스를 포함하지만 코드는 포함하지 않는 위성 어셈블리에 연결됩니다. 위성 어셈블리는 주 어셈블리의 일부가 아니므로 애플리케이션의 주 어셈블리를 바꾸지 않고도 특정 문화권에 해당하는 리소스를 손쉽게 업데이트하거나 바꿀 수 있습니다.

> [!NOTE]
> 애플리케이션의 기본 문화권의 리소스를 위성 어셈블리에 저장할 수도 있습니다. 그러려면 <xref:System.Resources.NeutralResourcesLanguageAttribute> 특성에 <xref:System.Resources.UltimateResourceFallbackLocation.Satellite?displayProperty=nameWithType>의 값을 할당합니다.

## <a name="satellite-assembly-name-and-location"></a>위성 어셈블리의 이름 및 위치

허브 및 스포크 모델을 사용하려면 리소스를 쉽게 찾아서 사용할 수 있도록 특정 위치에 두어야 합니다. 리소스 컴파일과 이름 지정을 제대로 하지 않거나 리소스를 정확한 위치에 두지 않으면 공용 언어 런타임에서는 이 리소스를 찾을 수 없으며 대신 기본 문화권의 리소스를 사용합니다. <xref:System.Resources.ResourceManager> 개체로 표현되는 .NET Framework 리소스 관리자는 지역화된 리소스에 자동으로 액세스하는 데 사용됩니다. 리소스 관리자에는 다음 사항이 필요합니다.

- 단일 위성 어셈블리는 특정 문화권에 대한 모든 리소스를 포함해야 합니다. 즉, 여러 .txt 또는 .resx 파일을 단일 이진 .resources 파일로 컴파일해야 합니다.

- 해당 문화권의 리소스를 저장하는 각 지역화된 문화권에 대한 애플리케이션 디렉터리에 있는 별도의 하위 디렉터리가 있어야 합니다. 하위 디렉터리 이름은 문화권 이름과 동일해야 합니다. 또는 위성 어셈블리를 전역 어셈블리 캐시에 저장할 수 있습니다. 이 경우 어셈블리의 강력한 이름의 문화권 정보 구성 요소는 해당 문화권을 나타내야 합니다. 이 항목의 뒷부분에 있는 [위성 어셈블리를 전역 어셈블리 캐시에 설치](#SN)를 참조하세요.

  > [!NOTE]
  > 애플리케이션에 하위 문화권의 리소스가 들어 있는 경우 각 하위 문화권을 애플리케이션 디렉터리 아래 별도의 하위 디렉터리에 둡니다. 주 문화권의 디렉터리 아래 하위 디렉터리에 하위 문화권을 두면 안 됩니다.

- 위성 어셈블리는 애플리케이션과 동일한 이름을 가져야 하고 ".resources.dll"을 파일 이름 확장명으로 사용해야 합니다. 예를 들어, 애플리케이션의 이름이 Example.exe인 경우, 각 위성 어셈블리의 이름은 Example.resources.dll이어야 합니다. 위성 어셈블리 이름이 해당 리소스 파일의 문화권을 나타내지 않는다는 것에 주의합니다. 그러나, 위성 어셈블리는 문화권을 지정하는 디렉터리에 나타납니다.

- 위성 어셈블리의 문화권에 대한 정보는 어셈블리의 메타데이터에 포함되어야 합니다. 문화권 이름을 위성 어셈블리의 메타데이터에 저장하려면 [어셈블리 링커](../tools/al-exe-assembly-linker.md)를 사용하여 리소스를 위성 어셈블리에 포함할 때 `/culture` 옵션을 지정합니다.

다음 그림은 [전역 어셈블리 캐시](../app-domains/gac.md)에 설치하지 않는 애플리케이션에 대한 샘플 디렉터리 구조 및 위치 요구 사항을 보여 줍니다. .txt 및 .resources 확장명을 가진 항목은 최종 애플리케이션과 함께 제공되지 않습니다. 이러한 중간 리소스 파일은 최종 위성 리소스 어셈블리를 만드는 데 사용됩니다. 이 예제에서는 .resx 파일을 .txt 파일로 대체할 수 있습니다. 자세한 내용은 [리소스 패키지 및 배포](packaging-and-deploying-resources-in-desktop-apps.md)를 참조하세요.

다음 이미지는 위성 어셈블리 디렉터리를 보여 줍니다.

![지역화된 문화권 하위 디렉터리가 포함된 위성 어셈블리 디렉터리입니다.](./media/creating-satellite-assemblies-for-desktop-apps/satellite-assembly-directory.gif)

## <a name="compiling-satellite-assemblies"></a>위성 어셈블리 컴파일

[리소스 파일 생성기(Resgen.exe)](../tools/resgen-exe-resource-file-generator.md)를 사용하여 리소스를 포함하는 텍스트 파일 또는 XML(.resx) 파일을 이진 .resources 파일로 컴파일합니다. 그런 다음 [어셈블리 링커(Al.exe)](../tools/al-exe-assembly-linker.md)를 사용하여 .resources 파일을 위성 어셈블리로 컴파일합니다. Al.exe는 지정한 .resources 파일에서 어셈블리를 만듭니다. 위성 어셈블리는 리소스만 포함할 수 있으며, 어떠한 실행 코드도 포함할 수 없습니다.

다음 Al.exe 명령은 독일 리소스 파일 strings.de.resources에서 `Example` 애플리케이션에 대한 위성 어셈블리를 만듭니다.

```console
al -target:lib -embed:strings.de.resources -culture:de -out:Example.resources.dll
```

다음 Al.exe 명령은 파일 strings.de.resources에서 `Example` 애플리케이션에 대한 위성 어셈블리도 만듭니다. **/template** 옵션을 사용하면 위성 어셈블리가 부모 어셈블리(Example.dll)로부터 문화권 관련 정보를 제외한 모든 어셈블리 메타데이터를 상속합니다.

```console
al -target:lib -embed:strings.de.resources -culture:de -out:Example.resources.dll -template:Example.dll
```  
  
 다음 표에서는 이러한 명령에 사용된 Al.exe 옵션을 더 자세히 설명합니다.
  
|옵션|설명|
|------------|-----------------|
|**-target:** lib|위성 어셈블리가 라이브러리(.dll) 파일로 컴파일되도록 지정합니다. 위성 어셈블리가 실행 코드를 포함하지 않고 애플리케이션의 주 어셈블리가 아니므로 위성 어셈블리를 DLL로 저장해야 합니다.|
|**-embed:** strings.de.resources|Al.exe가 어셈블리를 컴파일할 때 포함할 리소스 파일의 이름을 지정합니다. 위성 어셈블리에 여러 개의 .resources 파일을 포함할 수 있지만, 허브 및 스포크 모델을 따르는 경우, 각 문화권에 대해 하나의 위성 어셈블리를 컴파일해야 합니다. 그러나 문자열 및 개체에 대해 별도의 .resources 파일을 만들 수 있습니다.|
|**-culture:** de|컴파일한 리소스의 문화권을 지정합니다. 공용 언어 런타임은 지정된 문화권의 리소스를 검색할 때 이 정보를 사용합니다. 이 옵션을 생략해도 Al.exe는 리소스를 컴파일하지만 런타임에서는 사용자가 리소스를 요청할 때 해당 리소스를 찾을 수 없습니다.|
|**-out:** Example.resources.dll|출력 파일의 이름을 지정합니다. 이 이름은 명명 표준 *baseName*.resources.*extension*을 따라야 합니다. 여기서 *baseName*은 주 어셈블리의 이름이고 *extension*은 유효한 파일 이름 확장명(예: .dll)입니다. 런타임이 출력 파일 이름을 기반으로 위성 어셈블리의 문화권을 결정할 수 없는 경우 지정하기 위해 **/culture** 옵션을 사용해야 합니다.|
|**-template:** Example.dll|위성 어셈블리가 culture 필드를 제외하고 모든 어셈블리 메타데이터를 상속할 어셈블리를 지정합니다. 이 옵션은 [강력한 이름](../../standard/assembly/strong-named.md)을 가진 어셈블리를 지정할 때에만 위성 어셈블리에 영향을 미칩니다.|
  
 Al.exe에서 사용할 수 있는 전체 옵션 목록을 보려면 [어셈블리 링커(Al.exe)](../tools/al-exe-assembly-linker.md)를 참조하세요.
  
## <a name="satellite-assemblies-an-example"></a>위성 어셈블리: 예제  
 다음은 지역화된 인사말이 들어 있는 메시지 상자를 표시하는 간단한 "Hello world" 예제입니다. 이 예제에서는 영어(미국), 프랑스어(프랑스) 및 러시아어(러시아) 문화권에 대한 리소스가 포함되고 해당 대체 문화권은 영어입니다. 예제를 만들려면 다음을 수행합니다.  
  
1. 기본 문화권의 리소스를 포함하는 Greeting.resx 또는 Greeting.txt라는 리소스 파일을 만듭니다. 값이 “Hello world!”인 `HelloString`이라는 단일 문자열을 이 파일에 저장합니다.
  
2. 영어(en)가 애플리케이션의 기본 문화권임을 나타내려면 다음 <xref:System.Resources.NeutralResourcesLanguageAttribute?displayProperty=nameWithType> 특성을 애플리케이션의 AssemblyInfo 파일 또는 애플리케이션의 주 어셈블리로 컴파일할 주 소스 코드 파일에 추가합니다.
  
    [!code-csharp[Conceptual.Resources.Locating#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.locating/cs/assemblyinfo.cs#2)]
    [!code-vb[Conceptual.Resources.Locating#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.locating/vb/assemblyinfo.vb#2)]  
  
3. 추가 문화권(en-US, fr-FR 및 ru-RU)에 대한 지원을 애플리케이션에 다음과 같이 추가할 수 있습니다.  
  
    - "en-US" 또는 영어(미국) 문화권을 지원하려면 Greeting.en-US.resx 또는 Greeting.en-US.txt라는 리소스 파일을 만들어 값이 "Hi world!"인 `HelloString`이라는 단일 문자열에 저장합니다.  
  
    - "fr-FR" 또는 프랑스어(프랑스) 문화권을 지원하려면 Greeting.fr-FR.resx 또는 Greeting.fr-FR.txt라는 리소스 파일을 만들어 값이 "Salut tout le monde!"인 `HelloString`이라는 단일 문자열에 저장합니다.  
  
    - ru-RU 또는 러시아어(러시아) 문화권을 지원하려면 Greeting.ru-RU.resx 또는 Greeting.ru-RU.txt라는 리소스 파일을 만들어 값이 "Всем привет!"인 `HelloString`이라는 단일 문자열에 저장합니다.  
  
4. [Resgen.exe](../tools/resgen-exe-resource-file-generator.md)를 사용하여 각 텍스트 또는 XML 리소스 파일을 이진 .resources 파일로 컴파일합니다. 출력은 .resx 또는 .txt 파일과 동일한 루트 파일 이름을 가지고 있지만 .resources 확장명과는 다른 파일의 집합입니다. Visual Studio를 사용하여 예제를 만들면 컴파일 프로세스는 자동으로 처리됩니다. Visual Studio를 사용하지 않는 경우, .resx 파일을 .resources 파일로 컴파일하는 데 다음 명령을 실행합니다.  
  
    ```console
    resgen Greeting.resx
    resgen Greeting.en-us.resx
    resgen Greeting.fr-FR.resx
    resgen Greeting.ru-RU.resx
    ```

    리소스가 XML 파일 대신 텍스트 파일에 있는 경우 .resx 확장명을 .txt로 바꿉니다.

5. 다음 소스 코드를 기본 문화권에 대한 리소스와 함께 애플리케이션의 주 어셈블리로 컴파일합니다.

    > [!IMPORTANT]
    > Visual Studio 대신 명령줄을 사용하여 예제를 만들 경우 <xref:System.Resources.ResourceManager> 클래스 생성자에 대한 호출을 `ResourceManager rm = new ResourceManager("Greetings", typeof(Example).Assembly);`와 같이 수정해야 합니다.

    [!code-csharp[Conceptual.Resources.Locating#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.locating/cs/program.cs#1)]
    [!code-vb[Conceptual.Resources.Locating#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.locating/vb/module1.vb#1)]

    애플리케이션의 이름이 Example이고 명령줄에서 컴파일하는 경우 C# 컴파일러에 대한 명령은 다음과 같습니다.

    ```console
    csc Example.cs -res:Greeting.resources
    ```

    해당 Visual Basic 컴파일러 명령은 다음과 같습니다.

    ```console
    vbc Example.vb -res:Greeting.resources
    ```

6. 애플리케이션에서 지원되는 각 지역화된 문화권에 대한 주 애플리케이션 디렉터리에서 하위 디렉터리를 만듭니다. en-US, fr-FR 및 ru-RU 하위 디렉터리를 만들어야 합니다. Visual Studio는 컴파일 프로세스의 일부로 이러한 하위 디렉터리를 자동으로 만듭니다.

7. 각 문화권별 .resources 파일을 위성 어셈블리로 포함하고 해당 디렉터리에 저장합니다. 각 .resources 파일에 대해 이 작업을 수행하는 명령은 다음과 같습니다.

    ```console
    al -target:lib -embed:Greeting.culture.resources -culture:culture -out:culture\Example.resources.dll
    ```  
  
     여기서 *culture*는 리소스가 위성 어셈블리에 포함된 문화권의 이름입니다. Visual Studio는 이 프로세스를 자동으로 처리합니다.
  
 그런 다음 예제를 실행할 수 있습니다. 지원되는 문화권 중 하나를 현재 문화권으로 임의로 만들고 지역화된 인사말을 표시합니다.
  
<a name="SN"></a>   

## <a name="installing-satellite-assemblies-in-the-global-assembly-cache"></a>전역 어셈블리 캐시에 위성 어셈블리 설치  
로컬 애플리케이션 하위 디렉터리에 어셈블리를 설치하는 대신, 전역 어셈블리 캐시에 설치할 수 있습니다. 이는 클래스 라이브러리 및 클래스 라이브러리 리소스 어셈블리가 여러 애플리케이션에서 사용되는 경우 특히 유용합니다.
  
전역 어셈블리 캐시에 어셈블리를 설치하려면 강력한 이름이 필요합니다. 강력한 이름의 어셈블리는 유효한 퍼블릭/프라이빗 키 쌍으로 서명됩니다. 바인딩 요청을 만족시키는 데 사용할 어셈블리를 결정하기 위해 런타임에서 사용하는 버전 정보가 포함됩니다. 강력한 이름과 버전 관리에 대한 자세한 내용은 [어셈블리 버전 관리](../../standard/assembly/versioning.md)를 참조하세요. 강력한 이름에 대한 자세한 내용은 [강력한 이름의 어셈블리](../../standard/assembly/strong-named.md)를 참조하세요.
  
애플리케이션을 개발 중이면 최종 퍼블릭/프라이빗 키 쌍에 액세스할 권한이 없을 수 있습니다. 위성 어셈블리를 전역 어셈블리 캐시에 설치하고 예상대로 작동하는지 확인하려면 지연된 서명이라는 방법을 사용할 수 있습니다. 어셈블리 서명을 연기하면 빌드할 때 강력한 이름 시그니처에 사용할 파일 공간이 예약됩니다. 나중에 최종 퍼블릭/프라이빗 키 쌍을 사용할 수 있을 때까지 실제 서명이 연기됩니다. 지연된 서명에 대한 자세한 내용은 [어셈블리 서명 연기](../../standard/assembly/delay-sign.md)를 참조하세요.
  
### <a name="obtaining-the-public-key"></a>공개 키 가져오기  

어셈블리 서명을 연기하려면 공개 키에 대한 액세스 권한이 있어야 합니다. 최종 서명을 수행하는 회사 내 조직으로부터 실제 공개 키를 얻거나 [강력한 이름 도구(Sn.exe)](../tools/sn-exe-strong-name-tool.md)를 사용하여 공개 키를 만들 수 있습니다.
  
다음 Sn.exe 명령으로 테스트 퍼블릭/프라이빗 키 쌍을 만듭니다. **–k** 옵션은 Sn.exe가 새 키 쌍을 만들고 TestKeyPair.snk라는 파일에 저장하도록 지정합니다.
  
```console
sn –k TestKeyPair.snk
```

테스트 키 쌍을 포함하는 파일에서 공개 키를 추출할 수 있습니다. 다음 명령은 TestKeyPair.snk에서 공개 키를 추출하고 PublicKey.snk에 저장합니다.

```console
sn –p TestKeyPair.snk PublicKey.snk
```

### <a name="delay-signing-an-assembly"></a>어셈블리 서명 연기

공개 키를 얻었거나 만든 후에는 [어셈블리 링커(Al.exe)](../tools/al-exe-assembly-linker.md)를 사용하여 어셈블리를 컴파일하고 지연된 서명을 지정합니다.

다음 Al.exe 명령은 strings.ja.resources 파일로부터 StringLibrary 애플리케이션에 대한 강력한 이름의 위성 어셈블리를 만듭니다.

```console
al -target:lib -embed:strings.ja.resources -culture:ja -out:StringLibrary.resources.dll -delay+ -keyfile:PublicKey.snk
```

**-delay+** 옵션은 어셈블리 링커가 어셈블리 서명을 연기하도록 지정합니다. **-keyfile** 옵션은 어셈블리 서명을 연기하는 데 사용할 공개 키를 포함하는 키 파일의 이름을 지정합니다.

### <a name="re-signing-an-assembly"></a>어셈블리 다시 서명

애플리케이션을 배포하기 전에, 실제 키 쌍으로 지연 서명된 위성 어셈블리를 다시 서명해야 합니다. Sn.exe를 사용하여 이를 수행할 수 있습니다.

다음 Sn.exe 명령은 RealKeyPair.snk 파일에 저장된 실제 키 쌍으로 StringLibrary.resources.dll에 서명합니다. **–R** 옵션은 이전에 서명했거나 지연 서명된 어셈블리에 다시 서명하도록 지정합니다.

```console
sn –R StringLibrary.resources.dll RealKeyPair.snk
```

### <a name="installing-a-satellite-assembly-in-the-global-assembly-cache"></a>전역 어셈블리 캐시에 위성 어셈블리 설치

런타임이 리소스 대체 프로세스에서 리소스를 검색할 때, 가장 먼저 [전역 어셈블리 캐시](../app-domains/gac.md)에서 찾습니다. 자세한 내용은 [리소스 패키지 및 배포](packaging-and-deploying-resources-in-desktop-apps.md) 항목의 “리소스 대체 프로세스” 섹션을 참조하세요. 위성 어셈블리를 강력한 이름으로 서명하는 즉시 [전역 어셈블리 캐시 도구(Gacutil.exe)](../tools/gacutil-exe-gac-tool.md)를 사용하여 전역 어셈블리 캐시에 설치할 수 있습니다.

다음 Gacutil.exe 명령은 StringLibrary.resources.dll을 전역 어셈블리 캐시에 설치합니다.

```console
gacutil -i:StringLibrary.resources.dll
```

**/i** 옵션은 Gacutil.exe가 지정된 어셈블리를 전역 어셈블리 캐시에 설치하도록 지정합니다. 위성 어셈블리가 캐시에 설치된 후, 포함된 리소스는 위성 어셈블리를 사용하도록 설계된 모든 애플리케이션에서 사용할 수 있게 됩니다.

### <a name="resources-in-the-global-assembly-cache-an-example"></a>글로벌 어셈블리 캐시의 리소스: 예제

다음 예제에서는 .NET Framework 클래스 라이브러리에서 메서드를 사용하여 지역화된 인사말을 리소스 파일에서 추출하고 반환합니다. 라이브러리 및 리소스를 전역 어셈블리 캐시에 등록합니다. 예제에는 영어(미국), 프랑스어(프랑스), 러시아어(러시아) 및 영미 문화권에 대한 리소스가 포함됩니다. 영어는 기본 문화권으로, 해당 리소스는 주 어셈블리에 저장됩니다. 처음 예제는 라이브러리 및 퍼블릭 키를 가진 위성 어셈블리의 서명을 연기한 다음, 퍼블릭/프라이빗 키 쌍을 사용하여 다시 서명합니다. 예제를 만들려면 다음을 수행합니다.

1. Visual Studio를 사용하지 않는 경우 다음 [강력한 이름 도구(Sn.exe)](../tools/sn-exe-strong-name-tool.md) 명령을 사용하여 ResKey.snk라는 퍼블릭/프라이빗 키 쌍을 만듭니다.

    ```console
    sn –k ResKey.snk
    ```

    Visual Studio를 사용하는 경우 프로젝트 **속성** 대화 상자의 **서명** 탭을 사용하여 키 파일을 생성합니다.

2. 다음 [강력한 이름 도구(Sn.exe)](../tools/sn-exe-strong-name-tool.md) 명령을 사용하여 PublicKey.snk라는 공개 키 파일을 만듭니다.

    ```console
    sn –p ResKey.snk PublicKey.snk
    ```

3. 기본 문화권의 리소스를 포함할 Strings.resx라는 리소스 파일을 만듭니다. "How do you do?"의 값을 가진 `Greeting`이라는 이름의 단일 문자열을 해당 파일에 저장합니다.

4. "en"가 애플리케이션의 기본 문화권임을 나타내려면 다음 <xref:System.Resources.NeutralResourcesLanguageAttribute?displayProperty=nameWithType> 특성을 애플리케이션의 AssemblyInfo 파일 또는 애플리케이션의 주 어셈블리로 컴파일할 주 소스 코드 파일에 추가합니다.

    [!code-csharp[Conceptual.Resources.Satellites#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.satellites/cs/stringlibrary.cs#2)]
    [!code-vb[Conceptual.Resources.Satellites#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.satellites/vb/stringlibrary.vb#2)]

5. 추가 문화권(en-US, fr-FR 및 ru-RU 문화권)에 대한 지원을 애플리케이션에 다음과 같이 추가합니다.

    - "en-US" 또는 영어(미국) 문화권을 지원하려면 Strings.en-US.resx 또는 Strings.en-US.txt라는 리소스 파일을 만들어 값이 "Hello!"인 `Greeting`이라는 단일 문자열에 저장합니다.

    - "fr-FR" 또는 프랑스어(프랑스) 문화권을 지원하려면 Strings.fr-FR.resx 또는 Strings.fr-FR.txt라는 리소스 파일을 만들어 값이 ""Bon jour!"인 `Greeting`이라는 단일 문자열에 저장합니다.

    - "ru-RU" 또는 러시아어(러시아) 문화권을 지원하려면 Strings.ru-RU.resx 또는 Strings.ru-RU.txt라는 리소스 파일을 만들어 값이 "Привет!"인 `Greeting`이라는 단일 문자열에 저장합니다.

6. [Resgen.exe](../tools/resgen-exe-resource-file-generator.md)를 사용하여 각 텍스트 또는 XML 리소스 파일을 이진 .resources 파일로 컴파일합니다. 출력은 .resx 또는 .txt 파일과 동일한 루트 파일 이름을 가지고 있지만 .resources 확장명과는 다른 파일의 집합입니다. Visual Studio를 사용하여 예제를 만들면 컴파일 프로세스는 자동으로 처리됩니다. Visual Studio를 사용하지 않는 경우, .resx 파일을 .resources 파일로 컴파일하는 데 다음 명령을 실행합니다.

    ```console
    resgen filename
    ```

    여기서 *filename*은 선택적 경로, 파일 이름 및 .resx 또는 텍스트 파일의 확장명입니다.

7. StringLibrary.vb 또는 StringLibrary.cs에 대한 다음 소스 코드를 기본 문화권의 리소스와 함께 StringLibrary.dll이라는 지연 서명된 라이브러리 어셈블리로 컴파일합니다.

    > [!IMPORTANT]
    > Visual Studio 대신 명령줄을 사용하여 예제를 만들 경우 <xref:System.Resources.ResourceManager> 클래스 생성자에 대한 호출을 `ResourceManager rm = new ResourceManager("Strings",` `typeof(Example).Assembly);`로 수정해야 합니다.

    [!code-csharp[Conceptual.Resources.Satellites#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.satellites/cs/stringlibrary.cs#1)]
    [!code-vb[Conceptual.Resources.Satellites#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.satellites/vb/stringlibrary.vb#1)]

    C# 컴파일러에 대한 명령은 다음과 같습니다.

    ```console
    csc -t:library -resource:Strings.resources -delaysign+ -keyfile:publickey.snk StringLibrary.cs
    ```

    해당 Visual Basic 컴파일러 명령은 다음과 같습니다.

    ```console
    vbc -t:library -resource:Strings.resources -delaysign+ -keyfile:publickey.snk StringLibrary.vb
    ```

8. 애플리케이션에서 지원되는 각 지역화된 문화권에 대한 주 애플리케이션 디렉터리에서 하위 디렉터리를 만듭니다. en-US, fr-FR 및 ru-RU 하위 디렉터리를 만들어야 합니다. Visual Studio는 컴파일 프로세스의 일부로 이러한 하위 디렉터리를 자동으로 만듭니다. 위성 어셈블리가 모두 같은 파일 이름을 갖기 때문에, 퍼블릭/프라이빗 키 쌍으로 서명될 때까지 각 문화권별 위성 어셈블리를 저장하는 데 하위 디렉터리가 사용됩니다.

9. 각 문화권별 .resources 파일을 지연 서명된 위성 어셈블리로 포함하고 해당 디렉터리에 저장합니다. 각 .resources 파일에 대해 이 작업을 수행하는 명령은 다음과 같습니다.

    ```console
    al -target:lib -embed:Strings.culture.resources -culture:culture -out:culture\StringLibrary.resources.dll -delay+ -keyfile:publickey.snk
    ```

    여기서 *culture*는 문화권의 이름입니다. 이 예제에서 문화권 이름은 en-US, fr-FR 및 ru-RU입니다.

10. 다음과 같이 [강력한 이름 도구(Sn.exe)](../tools/sn-exe-strong-name-tool.md)를 사용하여 StringLibrary.dll에 다시 서명합니다.

    ```console
    sn –R StringLibrary.dll RealKeyPair.snk
    ```

11. 개별 위성 어셈블리에 다시 서명합니다. 이를 위해 각 위성 어셈블리에 대해 [강력한 이름 도구(Sn.exe)](../tools/sn-exe-strong-name-tool.md)를 다음과 같이 사용합니다.

    ```console
    sn –R StringLibrary.resources.dll RealKeyPair.snk
    ```

12. 다음 명령을 사용하여 StringLibrary.dll 및 전역 어셈블리 캐시에 있는 각 위성 어셈블리를 등록합니다.

    ```console
    gacutil -i filename
    ```

    여기서 *filename*은 등록할 파일의 이름입니다.

13. Visual Studio를 사용하는 경우 `Example`이라는 새 **콘솔 애플리케이션** 프로젝트를 만들고, StringLibrary.dll에 참조와 다음 소스 코드를 추가하고 컴파일합니다.

    [!code-csharp[Conceptual.Resources.Satellites#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.satellites/cs/example.cs#3)]
    [!code-vb[Conceptual.Resources.Satellites#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.satellites/vb/example.vb#3)]

    명령줄에서 컴파일하려면 C# 컴파일러에서 다음 명령을 사용합니다.

    ```console
    csc Example.cs -r:StringLibrary.dll
    ```

    Visual Basic 컴파일러의 명령줄은 다음과 같습니다.

    ```console
    vbc Example.vb -r:StringLibrary.dll
    ```

14. Example.exe를 실행합니다.

## <a name="see-also"></a>참고 항목

- [리소스 패키징 및 배포](packaging-and-deploying-resources-in-desktop-apps.md)
- [어셈블리 서명 연기](../../standard/assembly/delay-sign.md)
- [Al.exe(어셈블리 링커)](../tools/al-exe-assembly-linker.md)
- [Sn.exe(강력한 이름 도구)](../tools/sn-exe-strong-name-tool.md)
- [Gacutil.exe(전역 어셈블리 캐시 도구)](../tools/gacutil-exe-gac-tool.md)
- [데스크톱 앱의 리소스](index.md)
