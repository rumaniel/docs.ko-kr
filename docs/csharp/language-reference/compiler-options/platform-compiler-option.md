---
title: -platform(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /platform
helpviewer_keywords:
- platform compiler option [C#]
- -platform compiler option [C#]
- /platform compiler option [C#]
ms.assetid: c290ff5e-47f4-4a85-9bb3-9c2525b0be04
ms.openlocfilehash: 5150e871d75c3c34dab10f10cdac3d8322d7a834
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70849873"
---
# <a name="-platform-c-compiler-options"></a>-platform(C# 컴파일러 옵션)

어셈블리를 실행할 수 있는 CLR(공용 언어 런타임) 버전을 지정합니다.

## <a name="syntax"></a>구문

```console
-platform:string
```

## <a name="parameters"></a>매개 변수

`string` \
anycpu(기본값), anycpu32bitpreferred, ARM, x64, x86 또는 Itanium입니다.

## <a name="remarks"></a>설명

- **anycpu**(기본값)는 어셈블리를 모든 플랫폼에서 실행되도록 컴파일합니다. 애플리케이션은 가능할 때마다 64비트로 실행되고 해당 모드를 사용할 수 있을 때만 32비트로 전환됩니다.

- **anycpu32bitpreferred**는 어셈블리를 모든 플랫폼에서 실행되도록 컴파일합니다. 애플리케이션은 64비트와 32비트 애플리케이션을 모두 지원하는 시스템에서 32비트로 실행됩니다. .NET Framework 4.5를 대상으로 하는 프로젝트에 대해서만 이 옵션을 지정할 수 있습니다.

- **ARM**은 ARM(고급 RISC 컴퓨터) 프로세서가 있는 컴퓨터에서 실행할 어셈블리를 컴파일합니다.

- **ARM64**는 A64 명령 집합을 지원하는 ARM(고급 RISC 머신) 프로세서가 있는 컴퓨터에서 64비트 CLR에 의해 실행되도록 어셈블리를 컴파일합니다.

- **x64**는 AMD64 또는 EM64T 명령 집합을 지원하는 컴퓨터에서 64비트 CLR에 의해 실행되도록 어셈블리를 컴파일합니다.

- **x86**은 32비트, x86 호환 CLR에 의해 실행되도록 어셈블리를 컴파일합니다.

- **Itanium**은 Itanium 프로세서 탑재 컴퓨터에서 64비트 CLR에 의해 실행되도록 어셈블리를 컴파일합니다.

64비트 Windows 운영 체제:

- **-platform:x86**으로 컴파일된 어셈블리는 WOW64에서 실행되는 32비트 CLR에서 실행됩니다.

- **-platform:anycpu**로 컴파일된 DLL은 이 DLL이 로드된 프로세스와 동일한 CLR에서 실행됩니다.

- **-platform:anycpu**로 컴파일된 실행 파일은 64비트 CLR에서 실행됩니다.

- **-platform:anycpu32bitpreferred**로 컴파일된 실행 파일은 32비트 CLR에서 실행됩니다.

**anycpu32bitpreferred** 설정은 실행 파일(.EXE)에 대해서만 유효하고 .NET Framework 4.5를 필요로 합니다.

Windows 64비트 운영 체제에서 실행할 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [64비트 애플리케이션](../../../framework/64-bit-apps.md)을 참조하세요.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면

1. 프로젝트의 **속성** 페이지를 엽니다.

2. **빌드** 속성 페이지를 클릭합니다.

3. .NET Framework 4.5를 대상으로 하는 프로젝트에 대해 **플랫폼 대상** 속성을 수정하고 **32비트 선호** 확인란을 선택하거나 선택 취소합니다.

> [!NOTE]
> `-platform`은 Visual C# Express의 개발 환경에서 사용할 수 없습니다.

이 컴파일러 옵션을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.PlatformTarget%2A>을 참조하세요.

## <a name="example"></a>예

다음 예제에서는 **-platform** 옵션을 사용하여 애플리케이션이 64비트 Windows 운영 체제의 64비트 CLR에서만 실행되도록 지정하는 방법을 보여 줍니다.

```console
csc -platform:anycpu filename.cs
```

## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
