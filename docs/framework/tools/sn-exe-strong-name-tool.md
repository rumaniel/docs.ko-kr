---
title: Sn.exe(강력한 이름 도구)
ms.date: 03/30/2017
helpviewer_keywords:
- public keys, signing files
- Strong Name tool
- Sn.exe
- assemblies [.NET Framework], signing
- signing files
- strong-named assemblies, signing files
- key pairs for signing files
ms.assetid: c1d2b532-1b8e-4c7a-8ac5-53b801135ec6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 262ee168dabafcdc0b284f1ae5528843975a7e9d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044159"
---
# <a name="snexe-strong-name-tool"></a>Sn.exe(강력한 이름 도구)
강력한 이름 도구(Sn.exe)를 사용하면 [강력한 이름](../../standard/assembly/strong-named.md)으로 어셈블리에 서명할 수 있습니다. Sn.exe를 실행하면 키 관리, 서명 생성 및 서명 확인을 위한 옵션이 제공됩니다.  
  
> [!WARNING]
> 강력한 이름을 보안용으로 사용하지 마세요. 강력한 이름은 고유한 ID를 제공할 뿐입니다.

 강력한 이름 지정 및 강력한 이름의 어셈블리에 대한 자세한 내용은 [강력한 이름의 어셈블리](../../standard/assembly/strong-named.md) 및 [방법: 강력한 이름으로 어셈블리 서명](../../standard/assembly/sign-strong-name.md)을 참조하세요.  
  
 강력한 이름 도구는 Visual Studio와 함께 자동으로 설치됩니다. 이 도구를 시작하려면 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.  

> [!NOTE]
> 64비트 컴퓨터에서는 Visual Studio용 개발자 명령 프롬프트를 사용하여 32비트 Sn.exe 버전을 실행하고 Visual Studio x64 Win64 명령 프롬프트를 사용하여 64비트 버전을 실행합니다. 
  
 명령 프롬프트에 다음을 입력합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
sn [-quiet][option [parameter(s)]]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|옵션|설명|  
|------------|-----------------|  
|**-a** *identityKeyPairFile* *signaturePublicKeyFile*|ID 키를 파일의 서명 키로 마이그레이션하기 위해 <xref:System.Reflection.AssemblySignatureKeyAttribute> 데이터를 생성합니다.|  
|**-ac** *identityPublicKeyFile* *identityKeyPairContainer* *signaturePublicKeyFile*|ID 키를 키 컨테이너의 서명 키로 마이그레이션하기 위해 <xref:System.Reflection.AssemblySignatureKeyAttribute> 데이터를 생성합니다.|  
|**-c** [*csp*]|강력한 이름 서명에 사용할 기본 CSP(암호화 서비스 공급자)를 설정하며, 이 설정은 컴퓨터 전체에 적용됩니다. CSP 이름을 지정하지 않으면 현재 설정이 지워집니다.|  
|**-d** *container*|지정된 키 컨테이너를 강력한 이름 CSP에서 삭제합니다.|  
|**-D**  *assembly1 assembly2*|두 개의 어셈블리가 서명만 다른지 확인합니다. 이 옵션은 다른 키 쌍을 사용하여 어셈블리를 다시 서명한 후의 검사 방법으로 종종 사용됩니다.|  
|**-e**  *assembly outfile*|*assembly*에서 공개 키를 추출하여 *outfile*에 저장합니다.|  
|**-h**|이 도구의 명령 구문 및 옵션을 표시합니다.|  
|**-i** *infile container*|지정된 키 컨테이너에 있는 *infile*에서 키 쌍을 설치합니다. 키 컨테이너는 강력한 이름 CSP에 상주합니다.|  
|**-k** [*keysize*] *outfile*|지정한 크기의 새 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 키를 생성하여 지정된 파일에 씁니다.  퍼블릭 키와 프라이빗 키 모두 이 파일에 작성됩니다.<br /><br /> 키 크기를 지정하지 않으면 Microsoft 고급 암호화 공급자가 설치된 경우 기본적으로 1,024비트 키가 생성되고 그러지 않은 경우 512비트 키가 생성됩니다.<br /><br /> *keysize* 매개 변수는 Microsoft 고급 암호화 공급자가 설치된 경우 8비트씩 증가시킬 수 있는 384비트에서 16,384비트까지의 키 길이를 지원합니다.  Microsoft Base Cryptographic Provider가 설치되어 있는 경우에는 길이가 384 - 512비트(8비트 단위로 증가)인 키를 지원합니다.|  
|**-m** [**y** *&#124;* **n**]|키 컨테이너가 컴퓨터 관련 컨테이너인지 아니면 사용자 관련 컨테이너인지를 지정합니다. *y*를 지정하면 키 컨테이너는 컴퓨터 관련 컨테이너입니다. *n*을 지정하면 키 컨테이너는 사용자 관련 컨테이너입니다.<br /><br /> y나 n을 모두 지정하지 않으면 현재 설정이 표시됩니다.|  
|**-o**  *infile* [*outfile*]|*infile*에서 공개 키를 추출하여 .csv 파일에 저장합니다. 공개 키의 각 바이트는 쉼표로 구분됩니다. 이 형식은 키에 대한 참조를 소스 코드의 초기화된 배열로 하드 코드하는 데 유용합니다. *outfile*을 지정하지 않으면 출력 파일은 클립보드에 넣어집니다. **참고:**  이 옵션은 입력 파일에 공개 키만 있는지는 확인하지 않습니다. `infile`에 프라이빗 키를 포함한 키 쌍이 들어 있으면 프라이빗 키도 추출됩니다.|  
|**-p** *infile outfile* [*hashalg*]|*infile*의 키 쌍에서 공개 키를 추출하며 *outfile*에 저장하며, 이 경우 *hashalg*에서 지정된 RSA 알고리즘을 선택적으로 사용합니다. 이 공개 키는 [어셈블리 링커(Al.exe)](al-exe-assembly-linker.md)의 **/delaysign+** 및 **/keyfile** 옵션을 사용하여 어셈블리 서명을 연기하는 데 사용될 수 있습니다. 어셈블리 서명이 연기되면 컴파일 타임에 퍼블릭 키만 설정되고, 나중에 프라이빗 키가 알려질 때 서명을 추가할 공간이 파일에 예약됩니다.|  
|**-pc**  *container* *outfile* [*hashalg*]|*container*의 키 쌍에서 공개 키를 추출하여 *outfile*에 저장합니다. *hashalg* 옵션을 사용할 경우 RSA 알고리즘은 공개 키를 추출하는 데 사용됩니다.|  
|**-Pb** [**y** *&#124;* **n**]|강력한 이름 건너뛰기 정책을 적용할지 여부를 지정합니다. *y*를 지정하면 완전 신뢰 <xref:System.AppDomain>에 완전 신뢰 어셈블리가 로드될 때 강력한 이름의 유효성이 검사되지 않습니다. *n*을 지정하면 강력한 이름이 올바른지 검사되지만 특정 강력한 이름은 검사되지 않습니다. 완전 신뢰 어셈블리에는 <xref:System.Security.Permissions.StrongNameIdentityPermission>이 적용되지 않으므로 강력한 이름이 일치하는지 여부는 직접 검사해야 합니다.<br /><br /> `y`나 `n`을 모두 지정하지 않으면 현재 설정이 표시됩니다. 기본값은 `y`입니다. **참고:**  64비트 컴퓨터에서는 Sn.exe의 32비트 및 64비트 인스턴스 모두에 이 매개 변수를 설정해야 합니다.|  
|**-q**[**uiet**]|자동 모드를 지정합니다. 즉, 성공 메시지가 표시되지 않도록 합니다.|  
|**-R**[**a**] *assembly* *infile*|*infile*에 있는 키 쌍을 사용하여 이전에 서명했거나 서명을 연기한 어셈블리에 다시 서명합니다.<br /><br /> **-Ra**를 사용하는 경우 어셈블리에 있는 모든 파일에 대해 해시가 다시 계산됩니다.|  
|**-Rc**[**a**] *assembly container*|*container*에 있는 키 쌍을 사용하여 이전에 서명했거나 서명이 연기된 어셈블리에 다시 서명합니다.<br /><br /> **-Rca**를 사용하는 경우 어셈블리에 있는 모든 파일에 대해 해시가 다시 계산됩니다.|  
|**-Rh** *assembly*|어셈블리에 있는 모든 파일에 대해 해시를 다시 계산합니다.|  
|**-t**[**p**] *infile*|*infile*에 저장된 공개 키의 토큰을 표시합니다. *infile*의 내용은 이전에 **-p**를 사용하여 키 쌍 파일로부터 생성된 공개 키여야 합니다.  **-t[p]** 옵션을 사용하여 키 쌍 파일에서 직접 토큰을 추출하지 마세요.<br /><br /> Sn.exe는 해시 함수를 사용하여 공개 키에서 토큰을 계산합니다. 공용 언어 런타임에서는 공간을 절약하기 위해 강력한 이름을 가진 어셈블리에 대한 종속성을 기록할 때 매니페스트의 공개 키 토큰을 다른 어셈블리에 대한 참조의 일부로 저장합니다. **-tp** 옵션을 사용하면 공개 키와 토큰이 모두 표시됩니다. <xref:System.Reflection.AssemblySignatureKeyAttribute> 특성이 어셈블리에 적용된 경우 토큰은 ID 키용이며 해시 알고리즘의 이름 및 ID 키가 표시됩니다.<br /><br /> 이 옵션은 어셈블리 서명을 확인하지 않으며 신뢰 결정을 내리는 데 사용해서는 안 됩니다.  이 옵션은 원시 공개 키 토큰 데이터만 표시합니다.|  
|**-T**[**p**] *assembly*|*assembly*에 대한 공개 키 토큰을 표시합니다. *assembly*는 어셈블리 매니페스트가 들어 있는 파일의 이름이어야 합니다.<br /><br /> Sn.exe는 해시 함수를 사용하여 공개 키에서 토큰을 계산합니다. 런타임에서는 공간을 절약하기 위해 강력한 이름을 가진 어셈블리에 대한 종속성을 기록할 때 매니페스트의 공개 키 토큰을 다른 어셈블리에 대한 참조의 일부로 저장합니다. **-Tp** 옵션을 사용하면 공개 키와 토큰이 모두 표시됩니다. <xref:System.Reflection.AssemblySignatureKeyAttribute> 특성이 어셈블리에 적용된 경우 토큰은 ID 키용이며 해시 알고리즘의 이름 및 ID 키가 표시됩니다.<br /><br /> 이 옵션은 어셈블리 서명을 확인하지 않으며 신뢰 결정을 내리는 데 사용해서는 안 됩니다.  이 옵션은 원시 공개 키 토큰 데이터만 표시합니다.|  
|`-TS` `assembly` `infile`|`assembly`의 키 쌍을 사용하여 서명되거나 부분적으로 서명된 `infile`의 서명을 테스트합니다.|  
|-`TSc` `assembly` `container`|`assembly` 키 컨테이너의 키 쌍을 사용하여 서명되거나 부분적으로 서명된 `container`의 서명을 테스트합니다.|  
|**-v** *assembly*|*assembly*에 있는 강력한 이름을 확인합니다. 여기에서 *assembly*는 어셈블리 매니페스트가 들어 있는 파일의 이름입니다.|  
|**-vf**  *assembly*|*assembly*에서 강력한 이름을 확인합니다. **-v** 옵션과 달리 **-vf** 옵션을 사용하면 **-Vr** 옵션으로 비활성화된 경우에도 확인이 수행됩니다.|  
|**-Vk**  *regfile.reg* *assembly* [*userlist*] [*infile*]|확인을 건너뛸 지정된 어셈블리를 등록하는 데 사용할 수 있는 등록 항목 파일(.reg)을 만듭니다. **-Vr** 옵션에 적용되는 어셈블리 명명 규칙은 **–Vk**에도 적용됩니다. *userlist* 및 *infile* 옵션에 대한 자세한 내용은 **–Vr** 옵션을 참조하세요.|  
|**-Vl**|해당 컴퓨터의 강력한 이름 확인에 대한 현재 설정을 표시합니다.|  
|**-Vr**  *assembly* [*userlist*] [*infile*]|확인을 건너뛸 *assembly*를 등록합니다. 필요에 따라 확인 건너뛰기 적용을 쉼표로 구분된 사용자 이름 목록에 지정할 수 있습니다. *infile*을 지정하면 확인은 활성화된 상태로 유지되지만 *infile*의 공개 키는 확인 작업에 사용됩니다. *assembly*를 *\*, strongname* 형식으로 지정하여 지정된 강력한 이름을 가진 모든 어셈블리를 등록할 수 있습니다. *strongname*으로 공개 키의 토큰 형식을 나타내는 16진수 문자열을 지정합니다. 공개 키 토큰을 표시하려면 **-t** 및 **-T** 옵션을 참조하세요. **주의:**  개발하는 동안에만 이 옵션을 사용합니다. 어셈블리를 확인 생략 목록에 추가하면 보안상 허점이 발생합니다. 악의적인 어셈블리가 확인 건너뛰기 목록에 추가된 어셈블리의 정규화된 어셈블리 이름(어셈블리 이름, 버전, culture 및 공개 키 토큰)을 사용하여 해당 어셈블리의 ID를 모방할 수 있습니다. 이렇게 되면 악의적인 어셈블리도 확인을 건너뛸 수 있습니다.|  
|||  
|**-Vu**  *assembly*|확인을 건너뛸 *assembly*를 등록 취소합니다. **-Vr**에 적용되는 것과 동일한 어셈블리 명명 규칙이 **-Vu**에도 적용됩니다.|  
|**-Vx**|확인을 건너뛸 모든 항목을 제거합니다.|  
|**-?**|이 도구의 명령 구문 및 옵션을 표시합니다.|  
  
> [!NOTE]
> Sn.exe의 모든 옵션은 대/소문자가 구분되므로 표시된 대로 정확히 입력해야만 도구에서 제대로 인식합니다.  
  
## <a name="remarks"></a>설명  
 **-R** 및 **–Rc** 옵션은 서명이 연기된 어셈블리에 유용합니다. 이 시나리오에서는 컴파일 타임에 퍼블릭 키만 설정되고, 나중에 프라이빗 키가 알려질 때 서명이 수행됩니다.  
  
> [!NOTE]
> 레지스트리와 같은 보호되는 리소스에 쓰는 매개 변수(예: –**Vr**)는 SN.exe를 관리자로 실행합니다.  
  
강력한 이름 도구는 퍼블릭/프라이빗 키 쌍이 `AT_SIGNATURE` 알고리즘 식별자를 사용하여 생성된다고 가정합니다. `AT_KEYEXCHANGE` 알고리즘을 사용하여 생성된 퍼블릭/프라이빗 키 쌍이 오류를 생성합니다. 

## <a name="examples"></a>예  
 다음 명령을 사용하여 난수 키 쌍을 새로 만들어 `keyPair.snk`에 저장합니다.  
  
```console  
sn -k keyPair.snk  
```  
  
 다음 명령을 사용하여 `keyPair.snk`에 있는 키를 강력한 이름 CSP의 `MyContainer` 컨테이너에 저장합니다.  
  
```console  
sn -i keyPair.snk MyContainer  
```  
  
 다음 명령은 `keyPair.snk`에서 공개 키를 추출하여 `publicKey.snk`에 저장합니다.  
  
```console  
sn -p keyPair.snk publicKey.snk  
```  
  
 다음 명령은 `publicKey.snk`에 들어 있는 공개 키와 공개 키의 토큰을 표시합니다.  
  
```console  
sn -tp publicKey.snk  
```  
  
 다음 명령을 사용하여 어셈블리 `MyAsm.dll`을 확인합니다.  
  
```console  
sn -v MyAsm.dll  
```  
  
 다음 명령을 사용하여 기본 CSP에서 `MyContainer`를 삭제합니다.  
  
```console  
sn -d MyContainer  
```  
  
## <a name="see-also"></a>참고 항목

- [도구](index.md)
- [Al.exe(어셈블리 링커)](al-exe-assembly-linker.md)
- [강력한 이름의 어셈블리](../../standard/assembly/strong-named.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
