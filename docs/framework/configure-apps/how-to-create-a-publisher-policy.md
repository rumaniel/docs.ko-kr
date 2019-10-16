---
title: '방법: 게시자 정책 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- publisher policy assembly
- publisher policy files
- GAC (global assembly cache), publisher policy assembly
- global assembly cache, publisher policy assembly
ms.assetid: 8046bc5d-2fa9-4277-8a5e-6dcc96c281d9
ms.openlocfilehash: 5484dfeb8cf5292fb43393bb39b9878114119d29
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991189"
---
# <a name="how-to-create-a-publisher-policy"></a>방법: 게시자 정책 만들기

어셈블리 공급 업체는 응용 프로그램에서 업그레이드 된 어셈블리와 함께 게시자 정책 파일을 포함 하 여 최신 버전의 어셈블리를 사용 해야 하는 상태를 지정할 수 있습니다. 게시자 정책 파일은 어셈블리 리디렉션과 코드 베이스 설정을 지정 하 고 응용 프로그램 구성 파일과 동일한 형식을 사용 합니다. 게시자 정책 파일은 어셈블리로 컴파일되고 전역 어셈블리 캐시에 배치 됩니다.

게시자 정책을 만드는 데는 다음과 같은 세 가지 단계가 있습니다.

1. 게시자 정책 파일을 만듭니다.

2. 게시자 정책 어셈블리를 만듭니다.

3. 전역 어셈블리 캐시에 게시자 정책 어셈블리를 추가 합니다.

게시자 정책에 대 한 스키마는 [어셈블리 버전 리디렉션](redirect-assembly-versions.md)에 설명 되어 있습니다. 다음 예에서는의 `myAssembly` 한 버전을 다른 버전으로 리디렉션하는 게시자 정책 파일을 보여 줍니다.

```xml
<configuration>
   <runtime>
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
       <dependentAssembly>
         <assemblyIdentity name="myAssembly"
                           publicKeyToken="32ab4ba45e0a69a1"
                           culture="en-us" />
         <!-- Redirecting to version 2.0.0.0 of the assembly. -->
         <bindingRedirect oldVersion="1.0.0.0"
                          newVersion="2.0.0.0"/>
       </dependentAssembly>
      </assemblyBinding>
   </runtime>
</configuration>
```

코드 베이스를 지정 하는 방법에 대 한 자세한 내용은 [어셈블리 위치 지정](specify-assembly-location.md)을 참조 하세요.

## <a name="creating-the-publisher-policy-assembly"></a>게시자 정책 어셈블리 만들기

[어셈블리 링커 (al.exe)](../tools/al-exe-assembly-linker.md) 를 사용 하 여 게시자 정책 어셈블리를 만듭니다.

#### <a name="to-create-a-publisher-policy-assembly"></a>게시자 정책 어셈블리를 만들려면

명령 프롬프트에서 다음 명령을 입력 합니다.

**al /link:** *publisherPolicyFile* **/out:** *publisherPolicyAssemblyFile* **/keyfile:** *keyPairFile* **/platform:** *processorArchitecture*

이 명령에서 다음을 수행 합니다.

- *PublisherPolicyFile* 인수는 게시자 정책 파일의 이름입니다.

- *PublisherPolicyAssemblyFile* 인수는이 명령에서 생성 되는 게시자 정책 어셈블리의 이름입니다. 어셈블리 파일 이름은 다음 형식을 따라야 합니다.

  **policy.** *majorNumber* **.** *minorNumber* **.** *mainAssemblyName* **.dll**

- *KeyPairFile* 인수는 키 쌍을 포함 하는 파일의 이름입니다. 동일한 키 쌍을 사용 하 여 어셈블리 및 게시자 정책 어셈블리에 서명 해야 합니다.

- *ProcessorArchitecture* 인수는 프로세서별 어셈블리에서 대상으로 지정 된 플랫폼을 식별 합니다.

  > [!NOTE]
  > 특정 프로세서 아키텍처를 대상으로 하는 기능은 .NET Framework 2.0부터 사용할 수 있습니다.

특정 프로세서 아키텍처를 대상으로 지정 하는 기능은 .NET Framework 2.0부터 사용할 수 있습니다. 다음 명령은 이라는 `policy.1.0.myAssembly` `pub.config`게시자 정책 파일에서 라는 게시자 정책 어셈블리를 만들어에 강력한 이름을 할당 합니다. 어셈블리는 `sgKey.snk` 파일의 키 쌍을 사용 하 고 어셈블리는 x86 프로세서 아키텍처를 대상으로 지정 합니다.

```
al /link:pub.config /out:policy.1.0.myAssembly.dll /keyfile:sgKey.snk /platform:x86
```

게시자 정책 어셈블리는 적용 되는 어셈블리의 프로세서 아키텍처와 일치 해야 합니다. 따라서 어셈블리의 <xref:System.Reflection.AssemblyName.ProcessorArchitecture%2A> <xref:System.Reflection.ProcessorArchitecture.MSIL>값이 인 경우 해당 어셈블리에 대 한 게시자 정책 어셈블리는를 사용 `/platform:anycpu`하 여 만들어야 합니다. 각 프로세서별 어셈블리에 대해 별도의 게시자 정책 어셈블리를 제공 해야 합니다.

이 규칙의 결과는 어셈블리에 대 한 프로세서 아키텍처를 변경 하기 위해 올바른 프로세서 아키텍처를 사용 하 여 새 게시자 정책 어셈블리를 제공할 수 있도록 버전 번호의 주 또는 부 구성 요소를 변경 해야 한다는 것입니다. 어셈블리에 다른 프로세서 아키텍처가 있으면 이전 게시자 정책 어셈블리에서 어셈블리를 서비스 할 수 없습니다.

다른 결과는 항상 프로세서 아키텍처를 지정 하기 때문에 버전 2.0 링커를 사용 하 여 이전 버전의 .NET Framework을 사용 하 여 컴파일된 어셈블리에 대 한 게시자 정책 어셈블리를 만들 수 없습니다.

## <a name="adding-the-publisher-policy-assembly-to-the-global-assembly-cache"></a>전역 어셈블리 캐시에 게시자 정책 어셈블리 추가

전역 [어셈블리 캐시 도구 (gacutil.exe)](../tools/gacutil-exe-gac-tool.md) 를 사용 하 여 전역 어셈블리 캐시에 게시자 정책 어셈블리를 추가 합니다.

### <a name="to-add-the-publisher-policy-assembly-to-the-global-assembly-cache"></a>전역 어셈블리 캐시에 게시자 정책 어셈블리를 추가 하려면

명령 프롬프트에서 다음 명령을 입력 합니다.

**gacutil /i**  *publisherPolicyAssemblyFile*

다음 명령은 전역 어셈블리 `policy.1.0.myAssembly.dll` 캐시에를 추가 합니다.

```
gacutil /i policy.1.0.myAssembly.dll
```

> [!IMPORTANT]
> 원본 게시자 정책 파일이 어셈블리와 동일한 디렉터리에 있는 경우가 아니면 게시자 정책 어셈블리를 전역 어셈블리 캐시에 추가할 수 없습니다.

## <a name="see-also"></a>참고자료

- [어셈블리를 사용한 프로그래밍](../../standard/assembly/program.md)
- [런타임에서 어셈블리를 찾는 방법](../deployment/how-the-runtime-locates-assemblies.md)
- [구성 파일을 사용 하 여 앱 구성](index.md)
- [런타임 설정 스키마](./file-schema/runtime/index.md)
- [구성 파일 스키마](./file-schema/index.md)
- [어셈블리 버전 리디렉션](redirect-assembly-versions.md)
