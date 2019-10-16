---
title: -platform (Visual Basic)
ms.date: 03/13/2018
helpviewer_keywords:
- platform compiler option [Visual Basic]
- /platform compiler option [Visual Basic]
- -platform compiler option [Visual Basic]
ms.assetid: f9bc61e6-e854-4ae1-87b9-d6244de23fd1
ms.openlocfilehash: 21526484b8423f9b366da64307bc44f8fb061fe9
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005300"
---
# <a name="-platform-visual-basic"></a>-platform (Visual Basic)
출력 파일을 실행할 수 있는 CLR(공용 언어 런타임) 플랫폼 버전을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-platform:{ x86 | x64 | Itanium | arm | anycpu | anycpu32bitpreferred }  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`x86`|32비트, x86 호환 CLR에 의해 실행되도록 어셈블리를 컴파일합니다.|  
|`x64`|AMD64 또는 EM64T 명령 집합을 지원하는 컴퓨터에서 64비트 CLR에 의해 실행되도록 어셈블리를 컴파일합니다.|  
|`Itanium`|Itanium 프로세서 탑재 컴퓨터에서 64비트 CLR에 의해 실행되도록 어셈블리를 컴파일합니다.|  
|`arm`|ARM(고급 RISC 컴퓨터) 프로세서를 탑재한 컴퓨터에서 실행되도록 어셈블리를 컴파일합니다.|  
|`anycpu`|임의의 플랫폼에서 실행되도록 어셈블리를 컴파일합니다. 애플리케이션은 32비트 버전 Windows에서는 32비트 애플리케이션으로, 64비트 버전 Windows에서는 64비트 애플리케이션으로 실행됩니다. 이 플래그가 기본값입니다.|  
|`anycpu32bitpreferred`|임의의 플랫폼에서 실행되도록 어셈블리를 컴파일합니다. 애플리케이션은 32비트 및 64비트 버전 Windows 둘 다에서 32비트 애플리케이션으로 실행됩니다. 이 플래그는 실행 파일 ()에 대해서만 유효 합니다. EXE)를 사용 하려면 .NET Framework 4.5가 필요 합니다.|  
  
## <a name="remarks"></a>설명  
 출력 파일의 대상 프로세서 유형을 지정하려면 `-platform` 옵션을 사용합니다.  
  
 일반적으로 Visual Basic에서 작성된 .NET Framework 어셈블리는 플랫폼에 관계없이 동일하게 실행됩니다. 그러나 플랫폼별로 동작이 다른 경우도 있습니다. 이러한 경우의 일반적인 예는 다음과 같습니다.  
  
- 포인터 형식과 같이 플랫폼에 따라 크기가 달라지는 멤버를 포함하는 구조체  
  
- 상수 크기를 포함하는 포인터 산술 연산  
  
- 핸들에 대해 `Integer` 대신 <xref:System.IntPtr>를 사용하는 잘못된 플랫폼 호출 또는 COM 선언  
  
- <xref:System.IntPtr>을 `Integer`로 캐스팅  
  
- 일부 플랫폼에만 있는 구성 요소를 통한 플랫폼 호출 또는 COM interop 사용  
  
 **-Platform** 옵션은 코드가 실행 되는 아키텍처에 대 한 가정을 알고 있는 경우 몇 가지 문제를 완화 합니다. 구체적으로는 다음과 같습니다.  
  
- 애플리케이션이 32비트 컴퓨터에서 실행되는데 64비트 플랫폼을 대상으로 지정하는 경우에는 오류 메시지가 훨씬 더 일찍 표시되며, 이 스위치를 사용하지 않아 발생하는 오류보다는 문제 자체에 대한 내용이 중점적으로 표시됩니다.  
  
- 옵션에 대해 `x86` 플래그를 설정한 후 애플리케이션을 64비트 컴퓨터에서 실행하면 애플리케이션이 기본적으로 실행되지 않고 WOW 하위 시스템에서 실행됩니다.  
  
 64비트 Windows 운영 체제:  
  
- `-platform:x86`으로 컴파일된 어셈블리는 WOW64에서 실행되는 32비트 CLR에서 실행됩니다.  
  
- `-platform:anycpu`로 컴파일된 실행 파일은 64비트 CLR에서 실행됩니다.  
  
- `-platform:anycpu`로 컴파일된 DLL은 이 DLL이 로드된 프로세스와 동일한 CLR에서 실행됩니다.  
  
- `-platform:anycpu32bitpreferred`로 컴파일된 실행 파일은 32비트 CLR에서 실행됩니다.  
  
 64 비트 버전의 Windows에서 실행할 응용 프로그램을 개발 하는 방법에 대 한 자세한 내용은 [64 비트 응용 프로그램](../../../framework/64-bit-apps.md)을 참조 하십시오.  
  
### <a name="to-set--platform-in-the-visual-studio-ide"></a>Visual Studio IDE에서 플랫폼을 설정 하려면  
  
1. **솔루션 탐색기**에서 프로젝트를 선택 하 고 **프로젝트** 메뉴를 연 다음 **속성**을 클릭 합니다.  
  
2. **컴파일** 탭에서 **32 비트 선호** 확인란을 선택 하거나 선택 취소 하거나 **대상 CPU** 목록에서 값을 선택 합니다.  
  
     자세한 내용은 [컴파일 페이지, 프로젝트 디자이너 (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)를 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `-platform` 컴파일러 옵션을 사용하는 방법을 보여 줍니다.  
  
```console
vbc -platform:x86 myFile.vb  
```  
  
## <a name="see-also"></a>참조

- [/target (Visual Basic)](target.md)
- [Visual Basic 명령줄 컴파일러](index.md)
- [샘플 컴파일 명령줄](sample-compilation-command-lines.md)
